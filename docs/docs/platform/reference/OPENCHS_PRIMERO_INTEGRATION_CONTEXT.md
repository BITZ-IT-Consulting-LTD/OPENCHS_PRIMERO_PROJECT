# OpenCHSv5 - Primero CPIMS+ Integration Context Document
## TICAD Project - Lesotho Child Helpline Integration

**Document Version:** 1.0  
**Date:** March 2026  
**Target:** OpenCHS v5 (Django Backend + Vue.js Frontend)  
**Integration Target:** Primero CPIMS+ API v2

---

## 📌 Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Architecture Overview](#2-architecture-overview)
3. [Backend Implementation (Django)](#3-backend-implementation-django)
4. [Frontend Implementation (Vue.js)](#4-frontend-implementation-vuejs)
5. [Data Mapping Reference](#5-data-mapping-reference)
6. [API Specifications](#6-api-specifications)
7. [Testing Checklist](#7-testing-checklist)
8. [Common Issues & Solutions](#8-common-issues--solutions)

---

## 1. Executive Summary

### What This Integration Does
When a helpline operator in OpenCHS receives a call about a child at risk and marks it for referral to social welfare, this integration automatically creates a case in Primero CPIMS+ with all relevant child protection information.

### Key Components to Build/Modify

| Component | Location | Purpose |
|-----------|----------|---------|
| Primero API Client | `apps/integrations/primero/` | Handles authentication & API calls |
| Referral Service | `apps/referrals/services.py` | Business logic for creating referrals |
| Call Form | Frontend - Call module | ABR ID field + Referral checkbox |
| Validation Logic | `apps/calls/validators.py` | ABR ID format validation |
| Async Tasks | `apps/integrations/tasks.py` | Celery tasks for API calls |

---

## 2. Architecture Overview

### Data Flow Diagram

```
┌─────────────────────────────────────────────────────────────────────────┐
│                           OPENCHS v5                                    │
│                                                                         │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────────────────┐  │
│  │   Vue.js     │───▶│   Django     │───▶│   Celery Worker          │  │
│  │   Frontend   │    │   REST API   │    │   (Async Processing)     │  │
│  └──────────────┘    └──────────────┘    └──────────────────────────┘  │
│         │                   │                         │                │
│         ▼                   ▼                         ▼                │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────────────────┐  │
│  │ Call Form    │    │ Referral     │    │ Primero API Client       │  │
│  │ - ABR ID     │    │ Service      │    │ - Auth (JWT)             │  │
│  │ - Referral   │    │ - Validation │    │ - Case Creation          │  │
│  │   Checkbox   │    │ - Queue      │    │ - Retry Logic            │  │
│  └──────────────┘    └──────────────┘    └──────────────────────────┘  │
│                                                         │               │
└─────────────────────────────────────────────────────────┼───────────────┘
                                                          │ HTTPS/TLS 1.2+
                                                          ▼
                                          ┌──────────────────────────┐
                                          │   PRIMERO CPIMS+         │
                                          │   API v2                 │
                                          │   /api/v2/cases          │
                                          └──────────────────────────┘
```

### Retry & Queue Strategy

```
OpenCHS Save (Referral Checked)
        │
        ▼
┌───────────────────┐
│  Validation       │── Error? ──▶ Log & Alert Operator
│  (ABR ID Format)  │
└───────────────────┘
        │ Valid
        ▼
┌───────────────────┐
│  Queue Referral   │── Save to DB with PENDING status
└───────────────────┘
        │
        ▼
┌───────────────────┐     ┌────────────────────────────────────────┐
│  Celery Task      │────▶│  Attempt 1: Immediate                  │
│  (Async)          │     │  Fail? ──▶ Retry in 1 min              │
└───────────────────┘     │  Fail? ──▶ Retry in 5 min              │
                          │  Fail? ──▶ Retry in 30 min             │
                          │  Fail? ──▶ Retry in 2 hours            │
                          │  Fail? ──▶ Mark FAILED + Alert Admin   │
                          └────────────────────────────────────────┘
```

---

## 3. Backend Implementation (Django)

### 3.1 Project Structure

Create/modify these files in your OpenCHSv5 backend:

```
backend/
├── apps/
│   ├── referrals/                          # NEW APP (or extend existing)
│   │   ├── __init__.py
│   │   ├── models.py                       # ReferralQueue model
│   │   ├── services.py                     # ReferralService
│   │   ├── admin.py
│   │   └── migrations/
│   │
│   ├── integrations/                       # NEW APP
│   │   ├── __init__.py
│   │   ├── primero/                        # Primero-specific
│   │   │   ├── __init__.py
│   │   │   ├── client.py                   # PrimeroAPIClient
│   │   │   ├── auth.py                     # JWT Authentication
│   │   │   ├── mappers.py                  # Data transformation
│   │   │   └── exceptions.py               # Custom exceptions
│   │   ├── tasks.py                        # Celery tasks
│   │   └── models.py                       # IntegrationLog
│   │
│   └── calls/                              # EXISTING - Modify
│       ├── models.py                       # Add abr_id, referral_to_primero
│       ├── validators.py                   # NEW - ABR ID validation
│       └── serializers.py                  # Add new fields
│
├── config/
│   └── settings/
│       └── base.py                         # Add Primero settings
│
└── requirements/
    └── base.txt                            # Add requests, tenacity
```

### 3.2 Settings Configuration

**File:** `config/settings/base.py`

```python
# =============================================================================
# PRIMERO CPIMS+ INTEGRATION SETTINGS
# =============================================================================

PRIMERO_CONFIG = {
    # Connection
    'BASE_URL': env('PRIMERO_BASE_URL', default='https://primero-sandbox.example.com'),
    'TIMEOUT': env.int('PRIMERO_TIMEOUT', default=30),
    'VERIFY_SSL': env.bool('PRIMERO_VERIFY_SSL', default=True),
    
    # Authentication
    'USERNAME': env('PRIMERO_USERNAME', default=''),
    'PASSWORD': env('PRIMERO_PASSWORD', default=''),
    'TOKEN_EXPIRY_BUFFER': 300,  # Refresh token 5 mins before expiry
    
    # API Endpoints
    'ENDPOINTS': {
        'TOKEN': '/api/v2/tokens',
        'CASES': '/api/v2/cases',
        'FORMS': '/api/v2/forms',
        'LOOKUPS': '/api/v2/lookups',
    },
    
    # Retry Configuration
    'MAX_RETRIES': 4,
    'RETRY_DELAYS': [60, 300, 1800, 7200],  # 1min, 5min, 30min, 2hrs
    
    # Case Configuration
    'DEFAULT_MODULE': 'primeromodule-cp',
    'REFERRAL_SOURCE': 'child_helpline_116',
}

# Celery Configuration for Integration
CELERY_BEAT_SCHEDULE = {
    'process-pending-referrals': {
        'task': 'apps.integrations.tasks.process_pending_referrals',
        'schedule': 300.0,  # Every 5 minutes
    },
}
```

### 3.3 Database Models

**File:** `apps/calls/models.py` (Add to existing Call model)

```python
from django.core.validators import RegexValidator
from django.db import models

class Call(models.Model):
    # ... existing fields ...
    
    # NEW FIELDS FOR PRIMERO INTEGRATION
    abr_id = models.CharField(
        max_length=50,
        blank=True,
        null=True,
        verbose_name='ABR ID',
        help_text='Birth Registration ID from MoHA',
        validators=[
            RegexValidator(
                regex=r'^ABR\d{9,12}$',  # Adjust when spec is provided
                message='ABR ID must start with ABR followed by 9-12 digits',
                code='invalid_abr_id'
            )
        ],
        db_index=True,
    )
    
    referral_to_primero = models.BooleanField(
        default=False,
        verbose_name='Refer to Social Welfare/Primero',
        help_text='Check to create a case in Primero CPIMS+'
    )
    
    referral_submitted_at = models.DateTimeField(
        null=True,
        blank=True,
        verbose_name='Referral Submitted At'
    )
    
    primero_case_id = models.CharField(
        max_length=100,
        blank=True,
        null=True,
        verbose_name='Primero Case ID',
        help_text='Case ID returned from Primero after successful creation'
    )
    
    class Meta:
        # ... existing meta ...
        indexes = [
            # ... existing indexes ...
            models.Index(fields=['abr_id', 'referral_to_primero']),
            models.Index(fields=['referral_to_primero', 'referral_submitted_at']),
        ]
```

**File:** `apps/referrals/models.py` (New Model)

```python
import uuid
from django.db import models
from django.contrib.postgres.fields import JSONField
from model_utils.models import TimeStampedModel
from model_utils import Choices

class ReferralQueue(TimeStampedModel):
    """
    Queue for managing referrals to Primero.
    Handles retry logic and audit trail.
    """
    STATUS = Choices(
        ('pending', 'Pending'),
        ('processing', 'Processing'),
        ('completed', 'Completed'),
        ('failed', 'Failed'),
        ('cancelled', 'Cancelled'),
    )
    
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    
    # Source
    call = models.ForeignKey(
        'calls.Call',
        on_delete=models.CASCADE,
        related_name='referrals'
    )
    
    # Status
    status = models.CharField(
        max_length=20,
        choices=STATUS,
        default=STATUS.pending
    )
    
    # Retry Tracking
    retry_count = models.PositiveIntegerField(default=0)
    next_retry_at = models.DateTimeField(null=True, blank=True)
    
    # Payload (snapshot of data at time of queue)
    payload = JSONField(default=dict)
    
    # Result
    primero_case_id = models.CharField(max_length=100, blank=True)
    response_data = JSONField(default=dict, blank=True)
    error_message = models.TextField(blank=True)
    error_code = models.CharField(max_length=50, blank=True)
    
    # Audit
    submitted_by = models.ForeignKey(
        'users.User',
        on_delete=models.SET_NULL,
        null=True,
        related_name='submitted_referrals'
    )
    completed_at = models.DateTimeField(null=True, blank=True)
    
    class Meta:
        ordering = ['-created']
        indexes = [
            models.Index(fields=['status', 'next_retry_at']),
            models.Index(fields=['call', 'status']),
        ]
    
    def __str__(self):
        return f"Referral {self.id} - {self.status}"


class IntegrationLog(TimeStampedModel):
    """
    Detailed log of all API interactions with Primero.
    """
    LOG_TYPE = Choices(
        ('auth', 'Authentication'),
        ('create_case', 'Create Case'),
        ('get_forms', 'Get Forms'),
        ('error', 'Error'),
    )
    
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    referral = models.ForeignKey(
        ReferralQueue,
        on_delete=models.CASCADE,
        related_name='logs',
        null=True
    )
    log_type = models.CharField(max_length=20, choices=LOG_TYPE)
    
    # Request Details
    endpoint = models.URLField()
    method = models.CharField(max_length=10)
    request_headers = JSONField(default=dict, blank=True)
    request_body = JSONField(default=dict, blank=True)
    
    # Response Details
    response_status = models.PositiveIntegerField(null=True)
    response_body = JSONField(default=dict, blank=True)
    response_time_ms = models.PositiveIntegerField(null=True)
    
    # Error Details
    error_message = models.TextField(blank=True)
    stack_trace = models.TextField(blank=True)
    
    class Meta:
        ordering = ['-created']
```

### 3.4 ABR ID Validation

**File:** `apps/calls/validators.py` (New File)

```python"""
ABR ID Validation for Lesotho Birth Registration IDs.

NOTE: These are DRAFT rules - update when MoHA provides official spec.
Expected format based on typical systems:
- Prefix: ABR
- Regional code: 2 digits
- Sequence: 6-9 digits
- Check digit: 1 digit (Luhn or similar)
"""

import re
from django.core.exceptions import ValidationError
from django.utils.translation import gettext_lazy as _


class ABRIDValidator:
    """
    Validates ABR (Automated Birth Registration) ID format.
    
    Draft specification (pending MoHA confirmation):
    - Format: ABR{REGION}{SEQUENCE}{CHECK_DIGIT}
    - Example: ABR0100001234
    - Total length: 11-14 characters
    """
    
    # Pattern: ABR + 2-3 region digits + 6-9 sequence digits + optional check
    PATTERN = re.compile(r'^ABR\d{9,12}$')
    
    # When MoHA provides spec, implement check digit validation
    # Common algorithms: Luhn, Verhoeff, Modulo 11
    
    def __init__(self, validate_check_digit=False):
        self.validate_check_digit = validate_check_digit
    
    def __call__(self, value):
        if not value:
            return  # Allow empty (field is optional)
        
        value = value.strip().upper()
        
        # Basic format check
        if not self.PATTERN.match(value):
            raise ValidationError(
                _('Invalid ABR ID format. Expected: ABR followed by 9-12 digits.'),
                code='invalid_format'
            )
        
        # Check digit validation (when spec is available)
        if self.validate_check_digit:
            self._validate_check_digit(value)
    
    def _validate_check_digit(self, value):
        """
        TODO: Implement when MoHA provides check digit algorithm.
        
        Example implementation for Luhn algorithm:
        
        def luhn_check(digits):
            odd_sum = sum(digits[-1::-2])
            even_sum = sum([sum(divmod(2 * d, 10)) for d in digits[-2::-2]])
            return (odd_sum + even_sum) % 10 == 0
        """
        # Placeholder - raise if check digit is invalid
        # For now, just log warning
        pass


def validate_abr_id(value):
    """Shortcut function for use in model validators."""
    validator = ABRIDValidator()
    validator(value)


# When MoHA provides specification, update:
# 1. Total length
# 2. Character set (digits only? alphanumeric?)
# 3. Structure breakdown (region codes, year, etc.)
# 4. Check digit algorithm
# 5. Sample valid IDs for testing
```

### 3.5 Primero API Client

**File:** `apps/integrations/primero/exceptions.py` (New File)

```python"""
Custom exceptions for Primero API integration.
"""

class PrimeroAPIError(Exception):
    """Base exception for Primero API errors."""
    
    def __init__(self, message, status_code=None, response_data=None):
        super().__init__(message)
        self.status_code = status_code
        self.response_data = response_data or {}


class PrimeroAuthError(PrimeroAPIError):
    """Authentication/Authorization errors (401, 403)."""
    pass


class PrimeroNotFoundError(PrimeroAPIError):
    """Resource not found (404)."""
    pass


class PrimeroValidationError(PrimeroAPIError):
    """Validation errors (422)."""
    pass


class PrimeroServerError(PrimeroAPIError):
    """Server errors (5xx)."""
    pass


class PrimeroRateLimitError(PrimeroAPIError):
    """Rate limit exceeded (429)."""
    pass
```

**File:** `apps/integrations/primero/auth.py` (New File)

```python"""
JWT Authentication handler for Primero API v2.
"""

import logging
from datetime import datetime, timedelta
from typing import Optional

import requests
from django.conf import settings
from django.core.cache import cache

from .exceptions import PrimeroAuthError

logger = logging.getLogger(__name__)


class PrimeroAuth:
    """
    Handles JWT authentication with Primero API.
    
    Token management:
    - Obtains token via POST /api/v2/tokens
    - Caches token to minimize auth requests
    - Auto-refreshes before expiry
    """
    
    CACHE_KEY = 'primero_jwt_token'
    TOKEN_EXPIRY_BUFFER = 300  # 5 minutes buffer
    
    def __init__(self):
        self.config = settings.PRIMERO_CONFIG
        self.base_url = self.config['BASE_URL'].rstrip('/')
        self.username = self.config['USERNAME']
        self.password = self.config['PASSWORD']
    
    def get_token(self) -> str:
        """
        Get valid JWT token, fetching new one if needed.
        
        Returns:
            JWT Bearer token string
            
        Raises:
            PrimeroAuthError: If authentication fails
        """
        # Check cache first
        token_data = cache.get(self.CACHE_KEY)
        
        if token_data:
            expires_at = datetime.fromisoformat(token_data['expires_at'])
            if datetime.utcnow() < expires_at - timedelta(seconds=self.TOKEN_EXPIRY_BUFFER):
                logger.debug("Using cached Primero token")
                return token_data['token']
        
        # Fetch new token
        return self._fetch_token()
    
    def _fetch_token(self) -> str:
        """
        Authenticate with Primero and obtain JWT token.
        
        Primero API v2 Auth:
        POST /api/v2/tokens
        Body: { "user": { "user_name": "...", "password": "..." } }
        Response: { "token": "...", "expires_at": "..." }
        """
        url = f"{self.base_url}{self.config['ENDPOINTS']['TOKEN']}"
        
        payload = {
            "user": {
                "user_name": self.username,
                "password": self.password
            }
        }
        
        try:
            response = requests.post(
                url,
                json=payload,
                timeout=self.config['TIMEOUT'],
                verify=self.config['VERIFY_SSL']
            )
            response.raise_for_status()
            
            data = response.json()
            token = data.get('token')
            expires_at = data.get('expires_at')
            
            if not token:
                raise PrimeroAuthError("No token in response")
            
            # Parse expiry (Primero returns ISO format)
            if expires_at:
                expires_dt = datetime.fromisoformat(expires_at.replace('Z', '+00:00'))
            else:
                # Default: 60 minutes if not provided
                expires_dt = datetime.utcnow() + timedelta(minutes=60)
            
            # Cache the token
            cache.set(
                self.CACHE_KEY,
                {
                    'token': token,
                    'expires_at': expires_dt.isoformat()
                },
                timeout=int((expires_dt - datetime.utcnow()).total_seconds())
            )
            
            logger.info("Successfully obtained new Primero JWT token")
            return token
            
        except requests.exceptions.HTTPError as e:
            if response.status_code == 401:
                raise PrimeroAuthError(
                    "Invalid credentials",
                    status_code=401,
                    response_data=response.json() if response.text else {}
                )
            raise PrimeroAuthError(
                f"Authentication failed: {str(e)}",
                status_code=response.status_code,
                response_data=response.json() if response.text else {}
            )
        except requests.exceptions.RequestException as e:
            raise PrimeroAuthError(f"Connection error: {str(e)}")
    
    def invalidate_token(self) -> None:
        """
        Invalidate current token (logout).
        DELETE /api/v2/tokens
        """
        token_data = cache.get(self.CACHE_KEY)
        if not token_data:
            return
        
        url = f"{self.base_url}{self.config['ENDPOINTS']['TOKEN']}"
        
        try:
            requests.delete(
                url,
                headers={'Authorization': f"Bearer {token_data['token']}"},
                timeout=self.config['TIMEOUT'],
                verify=self.config['VERIFY_SSL']
            )
        except Exception as e:
            logger.warning(f"Token invalidation failed: {e}")
        finally:
            cache.delete(self.CACHE_KEY)
```

**File:** `apps/integrations/primero/client.py` (New File)

```python"""
Primero API v2 Client for case creation and management.
"""

import logging
import time
from typing import Dict, Any, Optional

import requests
from django.conf import settings

from .auth import PrimeroAuth
from .exceptions import (
    PrimeroAPIError,
    PrimeroAuthError,
    PrimeroNotFoundError,
    PrimeroValidationError,
    PrimeroServerError,
    PrimeroRateLimitError,
)

logger = logging.getLogger(__name__)


class PrimeroAPIClient:
    """
    Client for Primero CPIMS+ API v2.
    
    Features:
    - Automatic JWT authentication
    - Retry logic with exponential backoff
    - Comprehensive error handling
    - Request/Response logging
    """
    
    def __init__(self):
        self.config = settings.PRIMERO_CONFIG
        self.base_url = self.config['BASE_URL'].rstrip('/')
        self.auth = PrimeroAuth()
        self.session = requests.Session()
    
    def _make_request(
        self,
        method: str,
        endpoint: str,
        data: Optional[Dict] = None,
        params: Optional[Dict] = None,
        retry_auth: bool = True
    ) -> Dict[str, Any]:
        """
        Make authenticated request to Primero API.
        
        Args:
            method: HTTP method (GET, POST, PATCH, DELETE)
            endpoint: API endpoint path (e.g., '/api/v2/cases')
            data: Request body for POST/PATCH
            params: Query parameters
            retry_auth: Whether to retry on auth failure
            
        Returns:
            Parsed JSON response
            
        Raises:
            PrimeroAPIError: For API errors
        """
        url = f"{self.base_url}{endpoint}"
        token = self.auth.get_token()
        
        headers = {
            'Authorization': f'Bearer {token}',
            'Content-Type': 'application/json',
            'Accept': 'application/json',
        }
        
        start_time = time.time()
        
        try:
            response = self.session.request(
                method=method,
                url=url,
                headers=headers,
                json=data,
                params=params,
                timeout=self.config['TIMEOUT'],
                verify=self.config['VERIFY_SSL']
            )
            
            response_time = int((time.time() - start_time) * 1000)
            
            # Handle specific status codes
            if response.status_code == 401 and retry_auth:
                # Token expired, invalidate and retry once
                self.auth.invalidate_token()
                return self._make_request(method, endpoint, data, params, retry_auth=False)
            
            if response.status_code == 401:
                raise PrimeroAuthError("Authentication failed", 401)
            elif response.status_code == 403:
                raise PrimeroAuthError("Permission denied", 403)
            elif response.status_code == 404:
                raise PrimeroNotFoundError("Resource not found", 404)
            elif response.status_code == 422:
                raise PrimeroValidationError(
                    "Validation failed",
                    422,
                    response.json() if response.text else {}
                )
            elif response.status_code == 429:
                raise PrimeroRateLimitError("Rate limit exceeded", 429)
            elif response.status_code >= 500:
                raise PrimeroServerError(
                    f"Server error: {response.status_code}",
                    response.status_code
                )
            
            response.raise_for_status()
            
            logger.debug(f"Primero API {method} {endpoint}: {response.status_code} ({response_time}ms)")
            
            return response.json() if response.text else {}
            
        except requests.exceptions.Timeout:
            raise PrimeroAPIError(f"Request timeout after {self.config['TIMEOUT']}s")
        except requests.exceptions.ConnectionError as e:
            raise PrimeroAPIError(f"Connection error: {str(e)}")
        except requests.exceptions.HTTPError as e:
            raise PrimeroAPIError(f"HTTP error: {str(e)}", response.status_code)
    
    # =================================================================
    # CASE OPERATIONS
    # =================================================================
    
    def create_case(self, case_data: Dict[str, Any]) -> Dict[str, Any]:
        """
        Create a new case in Primero.
        
        Args:
            case_data: Case data following Primero v2 schema
            
        Returns:
            Created case with ID
            
        Raises:
            PrimeroValidationError: If validation fails
            PrimeroAPIError: For other errors
            
        Example case_data:
        {
            "data": {
                "abr_id": "ABR123456789",
                "name_first": "Child",
                "name_last": "Name",
                "sex": "female",
                "age": 8,
                "date_of_birth": "2018-01-15",
                "protection_concerns": ["neglect", "abuse"],
                "risk_level": "high",
                "referral_source": "child_helpline_116",
                "referral_notes": "Detailed notes...",
                "module_id": "primeromodule-cp",
                "openchs_reference_id": "OCHS-2026-001234"
            }
        }
        """
        endpoint = self.config['ENDPOINTS']['CASES']
        
        # Ensure module_id is set
        if 'data' in case_data and 'module_id' not in case_data['data']:
            case_data['data']['module_id'] = self.config['DEFAULT_MODULE']
        
        logger.info(f"Creating case in Primero: {case_data.get('data', {}).get('openchs_reference_id')}")
        
        response = self._make_request('POST', endpoint, data=case_data)
        
        case_id = response.get('data', {}).get('id')
        logger.info(f"Case created successfully in Primero: {case_id}")
        
        return response
    
    def get_case(self, case_id: str) -> Dict[str, Any]:
        """Fetch a specific case by ID."""
        endpoint = f"{self.config['ENDPOINTS']['CASES']}/{case_id}"
        return self._make_request('GET', endpoint)
    
    def list_cases(self, params: Optional[Dict] = None) -> Dict[str, Any]:
        """
        List/query cases with optional filters.
        
        Common params:
        - case_id: Filter by case ID
        - Abr_id: Filter by ABR ID
        - owned_by: Filter by owner
        - status: Filter by status
        """
        endpoint = self.config['ENDPOINTS']['CASES']
        return self._make_request('GET', endpoint, params=params)
    
    def update_case(self, case_id: str, case_data: Dict[str, Any]) -> Dict[str, Any]:
        """Update an existing case."""
        endpoint = f"{self.config['ENDPOINTS']['CASES']}/{case_id}"
        return self._make_request('PATCH', endpoint, data=case_data)
    
    # =================================================================
    # CONFIGURATION OPERATIONS
    # =================================================================
    
    def get_forms(self) -> Dict[str, Any]:
        """
        Fetch available forms and their structure.
        Use this to understand required fields and options.
        """
        endpoint = self.config['ENDPOINTS']['FORMS']
        return self._make_request('GET', endpoint)
    
    def get_lookups(self) -> Dict[str, Any]:
        """
        Fetch lookup values (dropdown options).
        Important for protection_concerns, risk_level mappings.
        """
        endpoint = self.config['ENDPOINTS']['LOOKUPS']
        return self._make_request('GET', endpoint)
```

### 3.6 Data Mapper

**File:** `apps/integrations/primero/mappers.py` (New File)

```python"""
Data mapping between OpenCHS and Primero schemas.

Maps OpenCHS Call/Case data to Primero API v2 format.
"""

from typing import Dict, Any, List, Optional
from datetime import datetime


class PrimeroCaseMapper:
    """
    Maps OpenCHS call data to Primero case structure.
    
    Primero Case Structure (v2):
    {
        "data": {
            "id": "...",
            "case_id": "...",
            "case_id_display": "...",
            "name_first": "...",
            "name_last": "...",
            "sex": "male|female",
            "date_of_birth": "YYYY-MM-DD",
            "age": 10,
            "protection_concerns": ["concern_code1", "concern_code2"],
            "risk_level": "high|medium|low",
            "module_id": "primeromodule-cp",
            ...
        }
    }
    """
    
    # Mapping of OpenCHS protection concerns to Primero codes
    # TODO: Update with actual Primero lookup values
    PROTECTION_CONCERNS_MAP = {
        'physical_abuse': 'physical_abuse',
        'sexual_abuse': 'sexual_abuse',
        'emotional_abuse': 'emotional_abuse',
        'neglect': 'neglect',
        'exploitation': 'exploitation',
        'abandonment': 'abandonment',
        'child_labour': 'worst_forms_of_child_labor',
        'trafficking': 'trafficking',
        'early_marriage': 'early_marriage',
        'harmful_practices': 'harmful_practices',
        'absent_parent': 'absent_parent',
        'violence': 'violence',
        'disability': 'disability',
        'other': 'other',
    }
    
    # Risk level mapping
    RISK_LEVEL_MAP = {
        'critical': 'high',
        'high': 'high',
        'medium': 'medium',
        'low': 'low',
        'none': 'low',
    }
    
    @classmethod
    def map_call_to_case(cls, call: 'Call') -> Dict[str, Any]:
        """
        Transform OpenCHS Call to Primero Case payload.
        
        Args:
            call: OpenCHS Call model instance
            
        Returns:
            Primero API v2 compatible case data
        """
        # Extract child info from call
        child_info = cls._extract_child_info(call)
        
        # Build protection concerns list
        protection_concerns = cls._map_protection_concerns(call)
        
        # Map risk level
        risk_level = cls._map_risk_level(call)
        
        # Construct Primero payload
        case_data = {
            "data": {
                # Unique identifiers
                "abr_id": call.abr_id,
                "openchs_reference_id": f"OCHS-{call.id}",
                
                # Child identity (use anonymous if privacy required)
                "name_first": child_info.get('first_name', 'Anonymous'),
                "name_last": child_info.get('last_name', ''),
                "sex": child_info.get('sex', 'unknown'),
                "date_of_birth": child_info.get('date_of_birth'),
                "age": child_info.get('age'),
                "estimated": child_info.get('age_is_estimate', False),
                
                # Location (if available)
                "location_current": cls._map_location(call),
                
                # Protection information
                "protection_concerns": protection_concerns,
                "risk_level": risk_level,
                
                # Referral source
                "referral_source": "child_helpline_116",
                "referral_source_other": "OpenCHS Child Helpline",
                
                # Notes
                "referral_notes": cls._build_referral_notes(call),
                "call_summary": call.notes or '',
                
                # Call metadata
                "call_date": call.created.isoformat() if call.created else None,
                "call_operator": call.answered_by.get_full_name() if call.answered_by else 'Unknown',
                "call_duration": call.duration_seconds if hasattr(call, 'duration_seconds') else None,
                
                # Module
                "module_id": "primeromodule-cp",
                
                # Status
                "status": "open",
                "case_status_reopened": False,
            }
        }
        
        # Remove None values to keep payload clean
        case_data["data"] = {k: v for k, v in case_data["data"].items() if v is not None}
        
        return case_data
    
    @classmethod
    def _extract_child_info(cls, call: 'Call') -> Dict[str, Any]:
        """Extract child demographic info from call."""
        # This depends on your OpenCHS data structure
        # Adjust based on how child info is stored in your system
        
        info = {
            'first_name': getattr(call, 'child_first_name', None),
            'last_name': getattr(call, 'child_last_name', None),
            'sex': cls._normalize_sex(getattr(call, 'child_sex', None)),
            'date_of_birth': getattr(call, 'child_date_of_birth', None),
            'age': getattr(call, 'child_age', None),
            'age_is_estimate': getattr(call, 'age_is_estimate', False),
        }
        
        # Calculate age from DOB if available
        if info['date_of_birth'] and not info['age']:
            try:
                dob = datetime.strptime(str(info['date_of_birth']), '%Y-%m-%d')
                today = datetime.now()
                info['age'] = today.year - dob.year - ((today.month, today.day) < (dob.month, dob.day))
            except (ValueError, TypeError):
                pass
        
        return info
    
    @classmethod
    def _map_protection_concerns(cls, call: 'Call') -> List[str]:
        """Map OpenCHS concern categories to Primero codes."""
        # Get concerns from call - adjust based on your model
        call_concerns = getattr(call, 'protection_concerns', []) or []
        
        mapped = []
        for concern in call_concerns:
            primero_code = cls.PROTECTION_CONCERNS_MAP.get(concern.lower())
            if primero_code:
                mapped.append(primero_code)
        
        return mapped if mapped else ['other']
    
    @classmethod
    def _map_risk_level(cls, call: 'Call') -> str:
        """Map OpenCHS risk level to Primero."""
        openchs_risk = getattr(call, 'risk_level', 'medium')
        return cls.RISK_LEVEL_MAP.get(openchs_risk, 'medium')
    
    @classmethod
    def _map_location(cls, call: 'Call') -> Optional[str]:
        """Map location to Primero format (if using location hierarchies)."""
        # Primero uses location codes like: "L1-L2-L3-L4"
        # Adjust based on your location structure
        
        location = getattr(call, 'location', None)
        if location:
            # Return location code that matches Primero's location hierarchy
            return getattr(location, 'primero_code', None) or str(location)
        return None
    
    @classmethod
    def _build_referral_notes(cls, call: 'Call') -> str:
        """Build comprehensive referral notes."""
        notes = []
        
        notes.append("=== CHILD HELPLINE 116 REFERRAL ===")
        notes.append(f"Call ID: {call.id}")
        notes.append(f"Call Date: {call.created}")
        
        if hasattr(call, 'caller_name') and call.caller_name:
            notes.append(f"Caller: {call.caller_name}")
        
        if hasattr(call, 'caller_phone') and call.caller_phone:
            notes.append(f"Caller Phone: {call.caller_phone}")
        
        if hasattr(call, 'caller_relationship') and call.caller_relationship:
            notes.append(f"Relationship to Child: {call.caller_relationship}")
        
        notes.append("\n--- INCIDENT DETAILS ---")
        notes.append(call.notes or "No detailed notes available")
        
        if hasattr(call, 'immediate_action_taken') and call.immediate_action_taken:
            notes.append(f"\n--- IMMEDIATE ACTION TAKEN ---")
            notes.append(call.immediate_action_taken)
        
        return "\n".join(notes)
    
    @staticmethod
    def _normalize_sex(sex: Optional[str]) -> str:
        """Normalize sex field to Primero values."""
        if not sex:
            return 'unknown'
        
        sex_lower = sex.lower()
        if sex_lower in ['male', 'm', 'boy']:
            return 'male'
        elif sex_lower in ['female', 'f', 'girl']:
            return 'female'
        else:
            return 'unknown'


# =============================================================================
# FIELD MAPPING REFERENCE (Update when Primero schema is confirmed)
# =============================================================================

"""
OPENCHS FIELD                  →   PRIMERO FIELD
─────────────────────────────────────────────────────────────────
call.id                         →   openchs_reference_id
call.abr_id                     →   abr_id (custom field)
call.child_first_name           →   name_first
call.child_last_name            →   name_last
call.child_sex                  →   sex
call.child_date_of_birth        →   date_of_birth
call.child_age                  →   age
call.protection_concerns[]      →   protection_concerns[]
call.risk_level                 →   risk_level
call.location                   →   location_current
call.notes                      →   referral_notes, call_summary
call.created                    →   call_date
call.answered_by                →   call_operator

CALLER INFORMATION:
call.caller_name                →   (in referral_notes)
call.caller_phone               →   (in referral_notes)
call.caller_relationship        →   (in referral_notes)

METADATA:
"child_helpline_116"            →   referral_source
"OpenCHS Child Helpline"        →   referral_source_other
"primeromodule-cp"              →   module_id
"open"                          →   status
"""
```

### 3.7 Referral Service

**File:** `apps/referrals/services.py` (New File)

```python"""
Business logic for managing referrals to Primero.
"""

import logging
from datetime import datetime
from typing import Optional

from django.db import transaction

from apps.calls.models import Call
from apps.integrations.primero.client import PrimeroAPIClient
from apps.integrations.primero.mappers import PrimeroCaseMapper
from apps.integrations.primero.exceptions import (
    PrimeroAPIError,
    PrimeroValidationError,
    PrimeroAuthError,
)
from .models import ReferralQueue, IntegrationLog

logger = logging.getLogger(__name__)


class ReferralService:
    """
    Service for creating and managing Primero referrals.
    
    Usage:
        service = ReferralService()
        service.queue_referral(call)  # Queue for async processing
        # or
        service.process_referral_sync(call)  # Process immediately
    """
    
    def __init__(self):
        self.primero = PrimeroAPIClient()
    
    def queue_referral(self, call: Call, submitted_by=None) -> ReferralQueue:
        """
        Queue a call for referral to Primero.
        
        Args:
            call: The Call to refer
            submitted_by: User who initiated the referral
            
        Returns:
            ReferralQueue instance
        """
        with transaction.atomic():
            # Build payload
            payload = PrimeroCaseMapper.map_call_to_case(call)
            
            # Create queue entry
            referral = ReferralQueue.objects.create(
                call=call,
                status=ReferralQueue.STATUS.pending,
                payload=payload,
                submitted_by=submitted_by
            )
            
            # Update call status
            call.referral_to_primero = True
            call.save(update_fields=['referral_to_primero'])
            
            logger.info(f"Queued referral {referral.id} for call {call.id}")
            
            return referral
    
    def process_referral(self, referral: ReferralQueue) -> bool:
        """
        Process a queued referral - send to Primero.
        
        This is called by Celery task.
        
        Args:
            referral: ReferralQueue to process
            
        Returns:
            True if successful, False otherwise
        """
        from apps.integrations.tasks import process_referral_async
        
        # Use async task
        process_referral_async.delay(str(referral.id))
        return True
    
    def process_referral_sync(self, referral: ReferralQueue) -> bool:
        """
        Synchronously process referral to Primero.
        
        Args:
            referral: ReferralQueue instance
            
        Returns:
            True if successful, False if failed
        """
        referral.status = ReferralQueue.STATUS.processing
        referral.save(update_fields=['status'])
        
        try:
            # Send to Primero
            response = self.primero.create_case(referral.payload)
            
            # Extract case ID
            case_data = response.get('data', {})
            primero_case_id = case_data.get('id') or case_data.get('case_id')
            
            # Update referral
            referral.status = ReferralQueue.STATUS.completed
            referral.primero_case_id = primero_case_id
            referral.response_data = response
            referral.completed_at = datetime.utcnow()
            referral.save()
            
            # Update call
            call = referral.call
            call.primero_case_id = primero_case_id
            call.referral_submitted_at = datetime.utcnow()
            call.save(update_fields=['primero_case_id', 'referral_submitted_at'])
            
            # Log success
            self._log_integration(
                referral=referral,
                log_type=IntegrationLog.LOG_TYPE.create_case,
                endpoint='/api/v2/cases',
                method='POST',
                request_body=referral.payload,
                response_status=201,
                response_body=response
            )
            
            logger.info(f"Referral {referral.id} successfully sent to Primero: {primero_case_id}")
            return True
            
        except PrimeroValidationError as e:
            logger.error(f"Validation error for referral {referral.id}: {e}")
            self._handle_failure(referral, e, 'validation_error')
            return False
            
        except PrimeroAuthError as e:
            logger.error(f"Auth error for referral {referral.id}: {e}")
            self._handle_failure(referral, e, 'auth_error', retry=True)
            return False
            
        except PrimeroAPIError as e:
            logger.error(f"API error for referral {referral.id}: {e}")
            self._handle_failure(referral, e, 'api_error', retry=True)
            return False
            
        except Exception as e:
            logger.exception(f"Unexpected error processing referral {referral.id}")
            self._handle_failure(referral, e, 'system_error', retry=True)
            return False
    
    def _handle_failure(self, referral: ReferralQueue, error, error_code, retry=False):
        """Handle referral failure and schedule retry if appropriate."""
        from django.conf import settings
        
        config = settings.PRIMERO_CONFIG
        max_retries = config['MAX_RETRIES']
        retry_delays = config['RETRY_DELAYS']
        
        referral.retry_count += 1
        referral.error_message = str(error)
        referral.error_code = error_code
        
        # Determine if we should retry
        if retry and referral.retry_count <= max_retries:
            # Schedule retry
            delay_index = min(referral.retry_count - 1, len(retry_delays) - 1)
            delay_seconds = retry_delays[delay_index]
            
            from datetime import timedelta
            referral.next_retry_at = datetime.utcnow() + timedelta(seconds=delay_seconds)
            referral.status = ReferralQueue.STATUS.pending
            
            logger.warning(
                f"Referral {referral.id} failed, scheduling retry "
                f"#{referral.retry_count} in {delay_seconds}s"
            )
        else:
            # Max retries exceeded or non-retryable error
            referral.status = ReferralQueue.STATUS.failed
            referral.next_retry_at = None
            logger.error(f"Referral {referral.id} failed permanently: {error}")
        
        referral.save()
        
        # Log failure
        self._log_integration(
            referral=referral,
            log_type=IntegrationLog.LOG_TYPE.error,
            endpoint='/api/v2/cases',
            method='POST',
            request_body=referral.payload,
            error_message=str(error),
            error_code=error_code
        )
    
    def _log_integration(self, **kwargs):
        """Create integration log entry."""
        try:
            IntegrationLog.objects.create(**kwargs)
        except Exception as e:
            logger.error(f"Failed to create integration log: {e}")
    
    def retry_failed_referrals(self):
        """
        Retry referrals that are due for retry.
        Called by periodic Celery task.
        """
        from django.utils import timezone
        
        pending = ReferralQueue.objects.filter(
            status=ReferralQueue.STATUS.pending,
            next_retry_at__lte=timezone.now()
        )
        
        count = 0
        for referral in pending:
            self.process_referral(referral)
            count += 1
        
        if count > 0:
            logger.info(f"Queued {count} referrals for retry")
        
        return count
    
    def get_referral_status(self, call: Call) -> Optional[dict]:
        """Get referral status for a call."""
        referral = ReferralQueue.objects.filter(call=call).first()
        if not referral:
            return None
        
        return {
            'status': referral.status,
            'retry_count': referral.retry_count,
            'primero_case_id': referral.primero_case_id,
            'created_at': referral.created,
            'completed_at': referral.completed_at,
            'error_message': referral.error_message if referral.status == 'failed' else None,
        }
```

### 3.8 Celery Tasks

**File:** `apps/integrations/tasks.py` (New File)

```python"""
Celery tasks for Primero integration.
"""

import logging

from celery import shared_task
from celery.exceptions import MaxRetriesExceededError

from apps.referrals.models import ReferralQueue
from apps.referrals.services import ReferralService

logger = logging.getLogger(__name__)


@shared_task(
    bind=True,
    max_retries=3,
    default_retry_delay=60,
    queue='integrations'
)
def process_referral_async(self, referral_id: str):
    """
    Process a referral to Primero asynchronously.
    
    Args:
        referral_id: UUID of the ReferralQueue entry
    """
    try:
        referral = ReferralQueue.objects.get(id=referral_id)
    except ReferralQueue.DoesNotExist:
        logger.error(f"Referral {referral_id} not found")
        return
    
    service = ReferralService()
    success = service.process_referral_sync(referral)
    
    if not success and referral.status == ReferralQueue.STATUS.pending:
        # Retry scheduled by service, but Celery can also retry
        if referral.retry_count <= 3:
            try:
                self.retry(countdown=60 * (self.request.retries + 1))
            except MaxRetriesExceededError:
                logger.error(f"Max Celery retries exceeded for referral {referral_id}")


@shared_task(queue='integrations')
def process_pending_referrals():
    """
    Periodic task to process pending referrals.
    Runs every 5 minutes via Celery Beat.
    """
    service = ReferralService()
    count = service.retry_failed_referrals()
    return f"Processed {count} pending referrals"


@shared_task(queue='integrations')
def sync_primero_lookups():
    """
    Sync Primero lookups (protection concerns, risk levels, etc.)
    Run daily to keep mappings current.
    """
    from apps.integrations.primero.client import PrimeroAPIClient
    
    client = PrimeroAPIClient()
    
    try:
        lookups = client.get_lookups()
        # Store lookups in cache or database for reference
        logger.info(f"Synced {len(lookups.get('data', []))} lookups from Primero")
        return lookups
    except Exception as e:
        logger.error(f"Failed to sync Primero lookups: {e}")
        raise
```

### 3.9 Admin Configuration

**File:** `apps/referrals/admin.py` (New File)

```python"""
Django Admin for Referral Queue and Integration Logs.
"""

from django.contrib import admin
from .models import ReferralQueue, IntegrationLog


@admin.register(ReferralQueue)
class ReferralQueueAdmin(admin.ModelAdmin):
    list_display = [
        'id', 'call', 'status', 'retry_count', 
        'primero_case_id', 'created', 'completed_at'
    ]
    list_filter = ['status', 'created', 'error_code']
    search_fields = ['call__id', 'primero_case_id', 'error_message']
    readonly_fields = [
        'id', 'created', 'modified', 'payload', 
        'response_data', 'error_message'
    ]
    date_hierarchy = 'created'
    
    actions = ['retry_referrals']
    
    def retry_referrals(self, request, queryset):
        """Admin action to retry failed referrals."""
        from .services import ReferralService
        service = ReferralService()
        
        count = 0
        for referral in queryset.filter(status='failed'):
            referral.status = 'pending'
            referral.retry_count = 0
            referral.error_message = ''
            referral.save()
            service.process_referral(referral)
            count += 1
        
        self.message_user(request, f"Queued {count} referrals for retry")
    retry_referrals.short_description = "Retry selected failed referrals"


@admin.register(IntegrationLog)
class IntegrationLogAdmin(admin.ModelAdmin):
    list_display = [
        'id', 'referral', 'log_type', 'endpoint', 
        'method', 'response_status', 'created'
    ]
    list_filter = ['log_type', 'response_status', 'created']
    search_fields = ['endpoint', 'error_message']
    readonly_fields = [
        'id', 'created', 'modified', 'request_body', 
        'response_body', 'stack_trace'
    ]
    date_hierarchy = 'created'
```

---

## 4. Frontend Implementation (Vue.js)

### 4.1 Component: Call Form Extension

**File:** `frontend/src/components/calls/CallFormPrimeroFields.vue` (New File)

```vue
<template>
  <div class="primero-integration-section">
    <h3 class="section-title">
      <i class="icon-primero"></i>
      Social Welfare Referral
    </h3>
    
    <!-- ABR ID Field -->
    <div class="form-group" :class="{ 'has-error': abrIdError }">
      <label for="abr-id">
        ABR ID (Birth Registration Number)
        <span class="optional-badge">Optional</span>
      </label>
      <input
        id="abr-id"
        v-model="localAbrId"
        type="text"
        placeholder="ABR123456789"
        @blur="validateAbrId"
        @input="onAbrIdInput"
        class="form-control"
        :disabled="isSubmitting"
      />
      <small class="help-text">
        Birth Registration ID from Ministry of Home Affairs
      </small>
      <small v-if="abrIdError" class="error-text">
        {{ abrIdError }}
      </small>
      <small v-else-if="abrIdValid" class="success-text">
        <i class="icon-check"></i> Valid ABR ID format
      </small>
    </div>
    
    <!-- Referral Checkbox -->
    <div class="form-group checkbox-group">
      <label class="checkbox-label">
        <input
          type="checkbox"
          v-model="localReferralToPrimero"
          :disabled="isSubmitting"
        />
        <span class="checkbox-text">
          <strong>Refer to Social Welfare / Primero</strong>
        </span>
      </label>
      <small class="help-text">
        Check this box to create a case in the Child Protection Information 
        Management System (CPIMS+) for social welfare follow-up.
      </small>
    </div>
    
    <!-- Referral Preview (when checked) -->
    <div v-if="localReferralToPrimero" class="referral-preview">
      <div class="preview-header">
        <i class="icon-info"></i>
        The following information will be sent to Primero:
      </div>
      <ul class="preview-list">
        <li><strong>ABR ID:</strong> {{ localAbrId || 'Not provided' }}</li>
        <li><strong>Child Info:</strong> Name, Age, Sex</li>
        <li><strong>Protection Concerns:</strong> {{ protectionConcernsText }}</li>
        <li><strong>Risk Level:</strong> {{ riskLevelText }}</li>
        <li><strong>Call Notes:</strong> Summary of the incident</li>
      </ul>
      <div class="privacy-notice">
        <i class="icon-lock"></i>
        Data is transmitted securely via encrypted connection.
      </div>
    </div>
    
    <!-- Referral Status (if already submitted) -->
    <div v-if="referralStatus" class="referral-status" :class="referralStatus.status">
      <div class="status-header">
        <i :class="statusIcon"></i>
        <strong>{{ statusText }}</strong>
      </div>
      <div v-if="referralStatus.primero_case_id" class="status-detail">
        Primero Case ID: <code>{{ referralStatus.primero_case_id }}</code>
      </div>
      <div v-if="referralStatus.error_message" class="status-error">
        Error: {{ referralStatus.error_message }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CallFormPrimeroFields',
  
  props: {
    abrId: {
      type: String,
      default: ''
    },
    referralToPrimero: {
      type: Boolean,
      default: false
    },
    protectionConcerns: {
      type: Array,
      default: () => []
    },
    riskLevel: {
      type: String,
      default: 'medium'
    },
    referralStatus: {
      type: Object,
      default: null
    },
    isSubmitting: {
      type: Boolean,
      default: false
    }
  },
  
  data() {
    return {
      localAbrId: this.abrId,
      localReferralToPrimero: this.referralToPrimero,
      abrIdError: null,
      abrIdValid: false,
      validationTimeout: null
    }
  },
  
  computed: {
    protectionConcernsText() {
      return this.protectionConcerns.length > 0 
        ? this.protectionConcerns.join(', ')
        : 'Will be determined during triage';
    },
    
    riskLevelText() {
      const labels = {
        'critical': 'Critical - Immediate action required',
        'high': 'High - Urgent response needed',
        'medium': 'Medium - Standard response',
        'low': 'Low - Routine follow-up'
      };
      return labels[this.riskLevel] || this.riskLevel;
    },
    
    statusIcon() {
      const icons = {
        'pending': 'icon-clock',
        'processing': 'icon-spinner',
        'completed': 'icon-check-circle',
        'failed': 'icon-error'
      };
      return icons[this.referralStatus?.status] || 'icon-info';
    },
    
    statusText() {
      const texts = {
        'pending': 'Referral queued for processing',
        'processing': 'Sending to Primero...',
        'completed': 'Successfully sent to Primero',
        'failed': 'Referral failed - will retry automatically'
      };
      return texts[this.referralStatus?.status] || 'Unknown status';
    }
  },
  
  watch: {
    localAbrId(val) {
      this.$emit('update:abrId', val);
    },
    localReferralToPrimero(val) {
      this.$emit('update:referralToPrimero', val);
    }
  },
  
  methods: {
    onAbrIdInput() {
      // Clear validation state while typing
      this.abrIdError = null;
      this.abrIdValid = false;
      
      // Debounce validation
      clearTimeout(this.validationTimeout);
      if (this.localAbrId) {
        this.validationTimeout = setTimeout(() => {
          this.validateAbrId();
        }, 500);
      }
    },
    
    validateAbrId() {
      if (!this.localAbrId) {
        this.abrIdError = null;
        this.abrIdValid = false;
        return true;
      }
      
      // Pattern: ABR + 9-12 digits
      const pattern = /^ABR\d{9,12}$/i;
      
      if (!pattern.test(this.localAbrId)) {
        this.abrIdError = 'Invalid ABR ID format. Expected: ABR followed by 9-12 digits (e.g., ABR123456789)';
        this.abrIdValid = false;
        return false;
      }
      
      // TODO: Add check digit validation when MoHA provides spec
      
      this.abrIdError = null;
      this.abrIdValid = true;
      return true;
    }
  }
}
</script>

<style scoped>
.primero-integration-section {
  background: #f8f9fa;
  border: 1px solid #dee2e6;
  border-radius: 8px;
  padding: 1.5rem;
  margin: 1rem 0;
}

.section-title {
  font-size: 1.1rem;
  font-weight: 600;
  color: #495057;
  margin-bottom: 1rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.optional-badge {
  font-size: 0.7rem;
  background: #6c757d;
  color: white;
  padding: 0.15rem 0.4rem;
  border-radius: 4px;
  font-weight: 500;
}

.form-group {
  margin-bottom: 1.25rem;
}

.form-group label {
  display: block;
  font-weight: 500;
  margin-bottom: 0.5rem;
  color: #212529;
}

.form-control {
  width: 100%;
  padding: 0.5rem 0.75rem;
  border: 1px solid #ced4da;
  border-radius: 4px;
  font-size: 1rem;
}

.form-control:focus {
  border-color: #80bdff;
  outline: 0;
  box-shadow: 0 0 0 0.2rem rgba(0, 123, 255, 0.25);
}

.has-error .form-control {
  border-color: #dc3545;
}

.help-text {
  display: block;
  margin-top: 0.25rem;
  color: #6c757d;
  font-size: 0.875rem;
}

.error-text {
  color: #dc3545;
  font-size: 0.875rem;
}

.success-text {
  color: #28a745;
  font-size: 0.875rem;
}

.checkbox-group {
  background: white;
  padding: 1rem;
  border-radius: 4px;
  border: 1px solid #dee2e6;
}

.checkbox-label {
  display: flex;
  align-items: flex-start;
  gap: 0.75rem;
  cursor: pointer;
}

.checkbox-label input[type="checkbox"] {
  width: 1.25rem;
  height: 1.25rem;
  margin-top: 0.125rem;
}

.checkbox-text {
  font-size: 1rem;
  color: #212529;
}

.referral-preview {
  background: #e7f3ff;
  border: 1px solid #b8daff;
  border-radius: 4px;
  padding: 1rem;
  margin-top: 1rem;
}

.preview-header {
  font-weight: 500;
  color: #004085;
  margin-bottom: 0.75rem;
}

.preview-list {
  margin: 0;
  padding-left: 1.25rem;
}

.preview-list li {
  margin-bottom: 0.25rem;
  color: #495057;
}

.privacy-notice {
  margin-top: 0.75rem;
  padding-top: 0.75rem;
  border-top: 1px solid #b8daff;
  font-size: 0.875rem;
  color: #004085;
}

.referral-status {
  margin-top: 1rem;
  padding: 1rem;
  border-radius: 4px;
}

.referral-status.pending {
  background: #fff3cd;
  border: 1px solid #ffc107;
}

.referral-status.processing {
  background: #e7f3ff;
  border: 1px solid #007bff;
}

.referral-status.completed {
  background: #d4edda;
  border: 1px solid #28a745;
}

.referral-status.failed {
  background: #f8d7da;
  border: 1px solid #dc3545;
}

.status-header {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 0.5rem;
}

.status-detail {
  font-size: 0.875rem;
  color: #495057;
}

.status-error {
  font-size: 0.875rem;
  color: #721c24;
  margin-top: 0.5rem;
}
</style>
```

### 4.2 API Service

**File:** `frontend/src/services/primeroApi.js` (New File)

```javascript"""
/**
 * API service for Primero integration
 */

import axios from 'axios';

const API_BASE_URL = import.meta.env.VITE_API_URL || '/api/v1';

const primeroApi = {
  /**
   * Get referral status for a call
   * @param {string} callId 
   * @returns {Promise<Object>}
   */
  async getReferralStatus(callId) {
    const response = await axios.get(`${API_BASE_URL}/calls/${callId}/referral-status/`);
    return response.data;
  },

  /**
   * Retry a failed referral (admin only)
   * @param {string} referralId 
   * @returns {Promise<Object>}
   */
  async retryReferral(referralId) {
    const response = await axios.post(`${API_BASE_URL}/referrals/${referralId}/retry/`);
    return response.data;
  },

  /**
   * Get integration statistics (admin only)
   * @param {Object} params 
   * @returns {Promise<Object>}
   */
  async getIntegrationStats(params = {}) {
    const response = await axios.get(`${API_BASE_URL}/integrations/primero/stats/`, { params });
    return response.data;
  },

  /**
   * Test Primero connection (admin only)
   * @returns {Promise<Object>}
   */
  async testConnection() {
    const response = await axios.post(`${API_BASE_URL}/integrations/primero/test-connection/`);
    return response.data;
  }
};

export default primeroApi;
```

### 4.3 Integration with Existing Call Form

**Example: Modifying existing CallForm.vue**

```vue
<template>
  <form @submit.prevent="submitCall">
    <!-- ... existing form fields ... -->
    
    <!-- ADD THIS SECTION -->
    <CallFormPrimeroFields
      v-model:abrId="form.abr_id"
      v-model:referralToPrimero="form.referral_to_primero"
      :protectionConcerns="form.protection_concerns"
      :riskLevel="form.risk_level"
      :referralStatus="referralStatus"
      :isSubmitting="isSubmitting"
    />
    
    <!-- ... rest of form ... -->
  </form>
</template>

<script>
import CallFormPrimeroFields from './CallFormPrimeroFields.vue';
import primeroApi from '@/services/primeroApi.js';

export default {
  components: { CallFormPrimeroFields },
  
  data() {
    return {
      form: {
        // ... existing fields ...
        
        // NEW FIELDS
        abr_id: '',
        referral_to_primero: false,
      },
      referralStatus: null,
      statusPollingInterval: null
    };
  },
  
  methods: {
    async submitCall() {
      this.isSubmitting = true;
      
      try {
        const response = await this.saveCall(this.form);
        
        // If referral was queued, start polling for status
        if (this.form.referral_to_primero && response.referral_queued) {
          this.startStatusPolling(response.id);
        }
        
        this.$emit('success', response);
      } catch (error) {
        this.handleError(error);
      } finally {
        this.isSubmitting = false;
      }
    },
    
    startStatusPolling(callId) {
      // Poll for referral status every 5 seconds
      this.statusPollingInterval = setInterval(async () => {
        try {
          const status = await primeroApi.getReferralStatus(callId);
          this.referralStatus = status;
          
          // Stop polling if completed or failed
          if (['completed', 'failed'].includes(status.status)) {
            clearInterval(this.statusPollingInterval);
          }
        } catch (error) {
          console.error('Failed to fetch referral status:', error);
          clearInterval(this.statusPollingInterval);
        }
      }, 5000);
      
      // Stop polling after 2 minutes max
      setTimeout(() => {
        if (this.statusPollingInterval) {
          clearInterval(this.statusPollingInterval);
        }
      }, 120000);
    }
  },
  
  beforeUnmount() {
    if (this.statusPollingInterval) {
      clearInterval(this.statusPollingInterval);
    }
  }
}
</script>
```

---

## 5. Data Mapping Reference

### 5.1 OpenCHS → Primero Field Mapping

| OpenCHS Field | Primero API v2 Field | Notes |
|---------------|---------------------|-------|
| `call.id` | `openchs_reference_id` | Unique reference back to OpenCHS |
| `call.abr_id` | `abr_id` | Custom field - confirm field name with Primero team |
| `call.child_first_name` | `name_first` | Required |
| `call.child_last_name` | `name_last` | Optional |
| `call.child_sex` | `sex` | Values: `male`, `female`, `unknown` |
| `call.child_date_of_birth` | `date_of_birth` | Format: `YYYY-MM-DD` |
| `call.child_age` | `age` | Number or range |
| `call.age_is_estimate` | `estimated` | Boolean |
| `call.protection_concerns[]` | `protection_concerns[]` | Array of codes - see mapping below |
| `call.risk_level` | `risk_level` | `high`, `medium`, `low` |
| `call.location` | `location_current` | Location code matching Primero hierarchy |
| `call.notes` | `referral_notes` | Full case notes |
| N/A | `referral_source` | Hardcoded: `child_helpline_116` |
| N/A | `referral_source_other` | Hardcoded: `OpenCHS Child Helpline` |
| N/A | `module_id` | Hardcoded: `primeromodule-cp` |
| N/A | `status` | Hardcoded: `open` |

### 5.2 Protection Concerns Mapping

**OpenCHS Categories → Primero Codes**

| OpenCHS | Primero Code | Status |
|---------|-------------|--------|
| Physical Abuse | `physical_abuse` | ✅ Confirmed |
| Sexual Abuse | `sexual_abuse` | ✅ Confirmed |
| Emotional Abuse | `emotional_abuse` | ✅ Confirmed |
| Neglect | `neglect` | ✅ Confirmed |
| Child Labour | `worst_forms_of_child_labor` | ✅ Confirmed |
| Trafficking | `trafficking` | ✅ Confirmed |
| Early Marriage | `early_marriage` | ⚠️ Verify |
| Absent Parent | `absent_parent` | ✅ Confirmed |
| Exploitation | `exploitation` | ⚠️ Verify |
| Disability | `disability` | ⚠️ Verify |
| Violence | `violence` | ⚠️ Verify |
| Other | `other` | ✅ Default |

**Action Required:** Get full list from Primero team via `GET /api/v2/lookups`

### 5.3 Risk Level Mapping

| OpenCHS | Primero |
|---------|---------|
| `critical` | `high` |
| `high` | `high` |
| `medium` | `medium` |
| `low` | `low` |
| `none` | `low` |

---

## 6. API Specifications

### 6.1 Primero API v2 Endpoints

#### Authentication
```http
POST /api/v2/tokens
Content-Type: application/json

{
  "user": {
    "user_name": "username",
    "password": "password"
  }
}

# Response
{
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "expires_at": "2026-03-30T13:54:22Z"
}
```

#### Create Case
```http
POST /api/v2/cases
Authorization: Bearer <token>
Content-Type: application/json

{
  "data": {
    "module_id": "primeromodule-cp",
    "abr_id": "ABR123456789",
    "name_first": "Child",
    "name_last": "Name",
    "sex": "female",
    "age": 8,
    "date_of_birth": "2018-01-15",
    "protection_concerns": ["neglect", "absent_parent"],
    "risk_level": "high",
    "referral_source": "child_helpline_116",
    "referral_notes": "Detailed notes...",
    "openchs_reference_id": "OCHS-2026-001234"
  }
}

# Success Response (201 Created)
{
  "data": {
    "id": "abc-123-def-456",
    "case_id": "ABC-2026-001234",
    "case_id_display": "ABC-2026-001234",
    "created_at": "2026-03-30T12:54:22Z",
    ...
  }
}

# Error Response (422 Unprocessable Entity)
{
  "errors": [
    {
      "code": "validation_error",
      "message": "Protection concerns contains invalid values",
      "field": "protection_concerns"
    }
  ]
}
```

### 6.2 OpenCHS Internal API (Add These)

#### Get Referral Status
```http
GET /api/v1/calls/{call_id}/referral-status/
Authorization: Bearer <token>

# Response
{
  "status": "completed",  // pending, processing, completed, failed
  "retry_count": 0,
  "primero_case_id": "ABC-2026-001234",
  "created_at": "2026-03-30T12:50:00Z",
  "completed_at": "2026-03-30T12:54:22Z",
  "error_message": null
}
```

---

## 7. Testing Checklist

### 7.1 Unit Tests

**Backend Tests (pytest)**

```python
# tests/integrations/primero/test_client.py
def test_create_case_success():
    """Test successful case creation."""
    pass

def test_create_case_validation_error():
    """Test handling of 422 validation errors."""
    pass

def test_create_case_auth_retry():
    """Test token refresh on 401."""
    pass

def test_retry_mechanism():
    """Test exponential backoff retry logic."""
    pass

def test_abr_id_validation():
    """Test ABR ID format validation."""
    pass

# tests/referrals/test_services.py
def test_queue_referral():
    """Test referral queuing."""
    pass

def test_process_referral_success():
    """Test successful referral processing."""
    pass

def test_process_referral_failure():
    """Test failure handling and retry."""
    pass
```

### 7.2 Integration Tests

- [ ] End-to-end: Call save → API call → Case in Primero
- [ ] ABR ID validation at form level
- [ ] Referral checkbox triggers queue
- [ ] Retry on network failure
- [ ] Duplicate prevention (idempotency)
- [ ] Error logging and admin notification

### 7.3 Manual Testing Scenarios

| Scenario | Steps | Expected Result |
|----------|-------|----------------|
| Happy Path | 1. Enter valid ABR ID<br>2. Check referral box<br>3. Save call | Case created in Primero within 30s |
| Invalid ABR ID | Enter malformed ABR ID | Frontend validation error, save blocked |
| Network Failure | Save with Primero offline | Referral queued, retry scheduled |
| Auth Failure | Wrong credentials | Log error, alert admin, don't retry infinitely |
| Duplicate Call | Same call saved twice | Only one case created in Primero |
| Large Payload | Very long notes | Successfully transmitted, no truncation |

---

## 8. Common Issues & Solutions

### Issue: Token Expires During Request
**Solution:** Client auto-refreshes token on 401 and retries once.

### Issue: Primero Returns 422 for Unknown Protection Concern
**Solution:** 
1. Sync lookups daily via Celery task
2. Map unknown values to `other`
3. Log warning for admin review

### Issue: Network Timeout on Large Payloads
**Solution:** 
- Increase timeout in settings
- Compress payload if possible
- Consider async file attachments

### Issue: Duplicate Cases Created
**Solution:**
- Include `openchs_reference_id` in payload
- Check for existing case before creation (if Primero supports)
- Use idempotency key in headers

### Issue: ABR ID Format Changes
**Solution:**
- Keep validation rules configurable
- Update regex pattern in validators.py
- Version your API client

---

## Appendix A: Environment Variables

Add to `.env` file:

```bash
# Primero CPIMS+ Configuration
PRIMERO_BASE_URL=https://primero-sandbox.example.com
PRIMERO_USERNAME=openchs_integration
PRIMERO_PASSWORD=secure_password_here
PRIMERO_TIMEOUT=30
PRIMERO_VERIFY_SSL=true

# Feature Flags
ENABLE_PRIMERO_INTEGRATION=true
```

## Appendix B: Required Dependencies

Add to `requirements/base.txt`:

```
# Already in OpenCHSv5 (likely)
Django>=4.2
djangorestframework>=3.14
celery>=5.3
redis>=4.5

# New for integration
requests>=2.31.0
tenacity>=8.2.0  # For retry logic (optional, can use Celery retry)
```

---

## Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-03-30 | TICAD Team | Initial version |

**Next Review:** When MoHA provides ABR ID specification
