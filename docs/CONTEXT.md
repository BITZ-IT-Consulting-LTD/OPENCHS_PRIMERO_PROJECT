# OpenCHSv5 — Complete Reverse-Engineered Context

> **Purpose:** This document contains the full technical specification of the OpenCHSv5 Omnichannel Helpline Case Management System. An AI agent with this context should be able to rebuild the entire platform from scratch.
> **Version:** 1.0
> **Date:** 2026-04-30

---

## 1. Executive Summary

OpenCHSv5 is a **full-stack Case Management System (CMS)** designed for **child helplines and crisis call centers**. It enables caseworkers to receive calls via a built-in WebRTC softphone, create and manage cases, track contacts, run AI-powered analysis on call recordings, manage referrals to external agencies, and integrate with government child protection systems (Primero CPIMS+).

For sensitive helpline cases, the target product model is **survivor-based case management**. The system must preserve survivor safety, confidentiality, dignity and self-determination, non-discrimination, safe contact preferences, informed consent, minimum necessary sharing, survivor-led support plans, and human review around sensitive AI and workflow decisions. The implementation truth source for this practice model is `context/21_SURVIVOR_BASED_CASE_MANAGEMENT_CONTEXT.md`.

### Core Value Proposition
- **Real-time call handling** with Asterisk PBX integration and WebSocket notifications
- **AI-augmented case management** (transcription, translation, NER, summarization, classification, risk assessment)
- **Workflow engine** with visual builder and safeguarding compliance
- **Referral management** including automated external system integration
- **Survivor-based case management controls** for safe intake, service and sharing decisions, safety plans, support plans, follow-up, and closure review
- **Quality Assurance** with both manual and AI-driven evaluations
- **Role-Based Access Control** for Agents, Supervisors, Admins, QA Officers, and Partners

---

## 2. Technology Stack

### Backend
| Layer | Technology | Version |
|-------|-----------|---------|
| Framework | Django | 4.2 |
| API | Django REST Framework | 3.14 |
| Auth | djangorestframework-simplejwt | 5.3.1 |
| Real-time | Django Channels + Daphne | 4.0 / 4.0 |
| Cache/Broker | Redis + channels-redis | 7 / 4.1 |
| Tasks | Celery | 5.3.6 |
| Database | PostgreSQL | 15 |
| Storage | MinIO (S3-compatible) | latest |
| Telephony | Asterisk | 20 LTS |
| AMI Client | panoramisk | 1.4 |
| Docs | drf-spectacular | 0.27.1 |
| CORS | django-cors-headers | 4.3.1 |
| Other | python-dotenv, requests, Pillow, Faker, cryptography | — |

### Frontend
| Layer | Technology | Version |
|-------|-----------|---------|
| Framework | Vue.js | 3.4.15 |
| Build Tool | Vite | 5.0.11 |
| Router | vue-router | 4.2.5 |
| State | Pinia | 2.1.7 |
| i18n | vue-i18n | 9.14.5 |
| Telephony | jssip | 3.10.1 |
| HTTP | axios | 1.6.7 |
| Rich Text | tiptap | starter-kit + vue-3 |
| Workflow UI | @vue-flow/* | core + background + controls + minimap |
| Icons | @heroicons/vue | — |
| Testing | jest + @vue/test-utils | 29.7.0 / 2.4.6 |

### Infrastructure
- **Containerization:** Docker + Docker Compose
- **Web Server:** Nginx (production frontend)
- **ASGI Server:** Daphne
- **WSGI Server:** Django runserver (dev) / Gunicorn (prod, recommended)

---

## 3. System Architecture

```
┌─────────────────────────────────────────────────────────────────────────┐
│                              USER BROWSER                               │
│                    (WebRTC Softphone + Vue.js SPA)                      │
└───────────────────────────────┬─────────────────────────────────────────┘
                                │ HTTPS / WSS
┌───────────────────────────────┴─────────────────────────────────────────┐
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────────────────┐  │
│  │   Frontend   │◄──►│   Django     │◄──►│   Celery Worker          │  │
│  │  (Vue+Vite)  │    │   REST API   │    │   (Async Tasks)          │  │
│  └──────────────┘    └──────┬───────┘    └──────────────────────────┘  │
│                             │                                          │
│  ┌──────────────┐    ┌─────┴──────┐    ┌──────────────────────────┐  │
│  │  Asterisk    │◄──►│  AMI Svc   │    │   AI Microservice        │  │
│  │  (SIP/PBX)   │    │(panoramisk)│    │  (Transcription/NER/etc) │  │
│  └──────────────┘    └────────────┘    └──────────────────────────┘  │
│                             │                                          │
│              ┌──────────────┼──────────────┐                         │
│              ▼              ▼              ▼                         │
│         ┌────────┐    ┌─────────┐    ┌─────────┐                    │
│         │PostgreSQL│   │  Redis  │    │  MinIO  │                    │
│         │  (15)   │    │(Cache/  │    │(Object  │                    │
│         │         │    │ Broker) │    │ Storage)│                    │
│         └─────────┘    └─────────┘    └─────────┘                    │
└─────────────────────────────────────────────────────────────────────────┘
                                │
                                ▼ HTTPS/TLS 1.2+
                     ┌──────────────────────┐
                     │   PRIMERO CPIMS+     │
                     │   API v2             │
                     └──────────────────────┘
```

---

## 4. Backend Architecture (Django)

### 4.1 Project Structure
```
backend/
├── core/
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   ├── wsgi.py
│   └── celery.py
├── apps/
│   ├── accounts/
│   ├── calls/
│   ├── cases/
│   ├── contacts/
│   ├── messaging/
│   ├── notifications/
│   ├── masterdata/
│   ├── referrals/
│   ├── qa/
│   ├── workflow/
│   ├── reports/
│   ├── ai/
│   ├── config/
│   ├── webhooks/
│   └── integrations/
│       └── primero/
├── manage.py
├── entrypoint.sh
├── requirements.txt
└── Dockerfile
```

### 4.2 Core Settings (`core/settings.py`)

**Installed Apps:**
```python
INSTALLED_APPS = [
    'daphne',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'rest_framework',
    'rest_framework_simplejwt',
    'corsheaders',
    'drf_spectacular',
    'channels',
    # Local apps
    'apps.accounts',
    'apps.calls',
    'apps.messaging',
    'apps.cases',
    'apps.referrals',
    'apps.qa',
    'apps.workflow',
    'apps.reports',
    'apps.ai',
    'apps.notifications',
    'apps.masterdata',
    'apps.contacts',
    'apps.webhooks',
    'apps.config',
    'apps.integrations',
]
```

**Key Settings:**
- `AUTH_USER_MODEL = 'accounts.User'`
- `REST_FRAMEWORK`: JWT auth, `IsAuthenticated` default, PageNumberPagination (page_size=10), DjangoFilterBackend, drf-spectacular AutoSchema
- `SIMPLE_JWT`: access_token_lifetime=1h, refresh_token_lifetime=7d, rotate_refresh_tokens=True, blacklist_after_rotation=True, update_last_login=True
- `CHANNEL_LAYERS`: RedisChannelLayer via `channels_redis`, host from `REDIS_HOST` env (default `redis`)
- `CELERY_BROKER_URL` / `CELERY_RESULT_BACKEND`: redis://redis:6379
- `CELERY_TASK_ALWAYS_EAGER = True` (dev convenience)
- `MEDIA_URL = '/media/'`, `MEDIA_ROOT = BASE_DIR / 'media'`
- `ASTERISK_AMI_HOST`, `ASTERISK_AMI_PORT=5038`, `ASTERISK_AMI_USERNAME`, `ASTERISK_AMI_SECRET`
- `PRIMERO_CONFIG`: dict with BASE_URL, TIMEOUT, VERIFY_SSL, USERNAME, PASSWORD, TOKEN_EXPIRY_BUFFER, ENDPOINTS (TOKEN, CASES, FORMS, LOOKUPS), MAX_RETRIES=4, RETRY_DELAYS=[60,300,1800,7200], DEFAULT_MODULE='primeromodule-cp', REFERRAL_SOURCE='child_helpline_116'
- `CORS_ALLOWED_ORIGINS`: localhost:3000, :5173, :8080, :8000 and their 127.0.0.1 / 0.0.0.0 / https variants
- `CSRF_TRUSTED_ORIGINS`: similar list
- Database: PostgreSQL via env vars `POSTGRES_DB`, `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_HOST`, `POSTGRES_PORT`

### 4.3 URL Routing (`core/urls.py`)

All API routes under `/api/v1/`:
- `auth/login/` → LoginView
- `auth/logout/` → LogoutView
- `auth/me/` → UserView
- `auth/token/refresh/` → TokenRefreshView
- `accounts/users/` → UserListCreateView / UserRetrieveUpdateDestroyView
- `accounts/roles/` → RoleListCreateView / RoleRetrieveUpdateDestroyView
- `accounts/permissions/` → PermissionListView
- `cases/` → include(apps.cases.urls)
- `calls/` → include(apps.calls.urls)
- `messaging/` → include(apps.messaging.urls)
- `referrals/` → include(apps.referrals.urls)
- `qa/` → include(apps.qa.urls)
- `workflow/` → include(apps.workflow.urls)
- `reports/` → include(apps.reports.urls)
- `ai/` → include(apps.ai.urls)
- `notifications/` → include(apps.notifications.urls)
- `masterdata/` → include(apps.masterdata.urls)
- `contacts/` → include(apps.contacts.urls)
- `webhooks/` → include(apps.webhooks.urls)
- `admin/` → include(apps.config.urls)
- `api/schema/` → SpectacularAPIView
- `api/docs/swagger/` → SpectacularSwaggerView
- `api/docs/redoc/` → SpectacularRedocView

### 4.4 ASGI Configuration (`core/asgi.py`)

```python
ProtocolTypeRouter({
    "http": get_asgi_application(),
    "websocket": TokenAuthMiddleware(
        URLRouter(
            apps.notifications.routing.websocket_urlpatterns +
            apps.messaging.routing.websocket_urlpatterns
        )
    ),
})
```

`TokenAuthMiddleware` (in `apps.accounts.middleware`) extracts JWT from query string `token` parameter for WebSocket authentication.

### 4.5 Celery Configuration (`core/celery.py`)

```python
app = Celery('openchsv5')
app.config_from_object('django.conf:settings', namespace='CELERY')
app.autodiscover_tasks()
```

### 4.6 Authentication & Permissions

**User Model** (`apps.accounts.models`):
```python
class Role(models.Model):
    name = models.CharField(max_length=100, unique=True)
    description = models.TextField(blank=True, null=True)
    permissions = models.ManyToManyField(Permission, blank=True)

class User(AbstractUser):
    roles = models.ManyToManyField(Role, related_name='users')
    reporting_to = models.ForeignKey('self', on_delete=models.SET_NULL, null=True, blank=True, related_name='subordinates')
```

**Custom Permission Class** (`apps.accounts.permissions`):
`HasRolePermission` — checks if user has any of the required roles from view's `required_roles` attribute.

**Middleware** (`apps.accounts.middleware.TokenAuthMiddleware`):
Authenticates WebSocket connections by parsing `token` from query string and validating JWT.

---

## 5. Database Schema (Complete Model Reference)

### 5.1 accounts

**Role**
- `name`: CharField(100, unique)
- `description`: TextField(blank, null)
- `permissions`: ManyToManyField(Permission, blank)

**User** (extends AbstractUser)
- `roles`: ManyToManyField(Role)
- `reporting_to`: ForeignKey(User, SET_NULL, related_name='subordinates')

### 5.2 cases

**Case**
- `created_by`: FK(User, PROTECT, related_name='created_cases')
- `assigned_to`: FK(User, SET_NULL, null, blank, related_name='assigned_cases')
- `category`: CharField(100)
- `status`: CharField(50, choices=STATUS_CHOICES, default='RECEIVED')
  - STATUS_CHOICES: RECEIVED, AGENT_HANDLING, ESCALATED_SUPERVISOR, ASSIGNED_CASE_MANAGER, ASSIGNED_CASE_WORKER, REFERRED_EXTERNAL, RESOLVED, CLOSED
- `narrative`: TextField(blank, null)
- `dynamic_fields`: JSONField(default=dict)
- `linked_calls`: ManyToManyField(Call, blank, related_name='linked_to_cases')
- `risk_level`: CharField(50, blank)
- `emergency`: BooleanField(default=False)
- `closure_reason`: CharField(255, blank)
- `closed_date`: DateField(null, blank)
- `plan`: JSONField(null, blank)
- `intake_date`: DateField(null, blank)
- `intake_time`: TimeField(null, blank)
- `channel`: CharField(50, blank)
- `intake_agent`: CharField(100, blank)
- `survivor_satisfaction`: IntegerField(null, blank)
- `anonymization_consent`: BooleanField(default=False)
- `call_recording`: FileField(upload_to='call_recordings/%Y/%m/', null, blank)
- `ai_transcript`: TextField(blank)
- `ai_translated_text`: TextField(blank)
- `ai_summary`: TextField(blank)
- `ai_extracted_entities`: JSONField(default=dict, blank)
- `ai_classification`: JSONField(default=dict, blank)
- `ai_processing_status`: CharField(50, choices=[not_started,in_progress,completed,failed,partial], default='not_started')
- `ai_last_processed`: DateTimeField(null, blank)
- `ai_confidence_score`: FloatField(null, blank)
- `detected_language`: CharField(10, blank)
- `translation_target`: CharField(10, blank)
- `ai_risk_level`: CharField(50, blank)
- `ai_suggested_next_step`: TextField(blank)
- `ai_rationale`: TextField(blank)
- `ai_assessment_json`: JSONField(default=dict, blank)
- `created_at`: DateTimeField(auto_now_add)
- `updated_at`: DateTimeField(auto_now)
- Methods: `trigger_ai_pipeline(pipeline_id, user=None)`, `get_ai_processing_history()`

**CaseActivity**
- `case`: FK(Case, CASCADE, related_name='activities')
- `user`: FK(User, SET_NULL, null)
- `action`: CharField(100)
- `detail`: TextField(blank, null)
- `created_at`: DateTimeField(auto_now_add)

**CaseNote**
- `case`: FK(Case, CASCADE, related_name='notes')
- `author`: FK(User, CASCADE, related_name='authored_notes')
- `content`: TextField
- `mentions`: ManyToManyField(User, related_name='mentioned_in_notes', blank)
- `is_assignment`: BooleanField(default=False)
- `assigned_to_user`: FK(User, SET_NULL, null, blank, related_name='assigned_via_notes')
- `created_at`: DateTimeField(auto_now_add)
- `updated_at`: DateTimeField(auto_now)

**CaseTransition**
- `case`: FK(Case, CASCADE, related_name='transitions')
- `from_state`: CharField(50)
- `to_state`: CharField(50)
- `actor`: FK(User, PROTECT)
- `reason`: TextField
- `context_data`: JSONField(default=dict, blank)
- `created_at`: DateTimeField(auto_now_add)

### 5.3 calls

**TelephonyEnvironment**
- `name`: CharField(100)
- `slug`: SlugField(unique)
- `is_active`: BooleanField(default=True)
- `description`: TextField(blank, null)

**TelephonyAuditLog**
- `user`: FK(User, SET_NULL, null)
- `timestamp`: DateTimeField(auto_now_add)
- `action`: CharField(10, choices=[CREATE,UPDATE,DELETE,RELOAD])
- `affected_model`: CharField(100)
- `affected_id`: CharField(100, blank)
- `diff`: JSONField(null, blank)
- `outcome`: CharField(20, default='success')

**Call**
- `caller_id`: CharField(100)
- `agent`: FK(User, SET_NULL, null, blank)
- `start_time`: DateTimeField(auto_now_add)
- `end_time`: DateTimeField(null, blank)
- `duration`: IntegerField(null, blank) — seconds
- `disposition`: CharField(100, blank)
- `recording_url`: URLField(blank)
- `direction`: CharField(20, choices=[inbound,outbound], default='inbound')
- `notes`: TextField(blank)
- `case`: FK(Case, SET_NULL, null, blank, related_name='calls')
- `child_first_name`: CharField(100, blank)
- `child_last_name`: CharField(100, blank)
- `child_sex`: CharField(20, blank)
- `child_age`: IntegerField(null, blank)
- `age_is_estimate`: BooleanField(default=False)
- `protection_concerns`: JSONField(default=list, blank)
- `risk_level`: CharField(50, default='medium')
- `abr_id`: CharField(50, blank, null, db_index=True)
- `referral_to_primero`: BooleanField(default=False)
- `referral_submitted_at`: DateTimeField(null, blank)
- `primero_case_id`: CharField(100, blank, null)

**SIPExtension**
- `extension_number`: CharField(20, unique)
- `secret`: CharField(128)
- `user`: OneToOneField(User, SET_NULL, null, blank, related_name='sip_extension')
- `sip_server`: CharField(100, blank, null)
- `ws_port`: IntegerField(default=8088)
- `webrtc_enabled`: BooleanField(default=True)
- `dtls_verify`: CharField(20, default='fingerprint')
- `ice_support`: BooleanField(default=True)
- `is_active`: BooleanField(default=True)
- `created_at`: DateTimeField(auto_now_add)

**PJSIPTransport**
- `name`: CharField(100, unique, default='transport-ws')
- `protocol`: CharField(10, choices=[udp,tcp,ws,wss], default='ws')
- `bind_address`: CharField(100, default='0.0.0.0:8088')
- `external_signaling_address`: CharField(100, blank, null)
- `external_signaling_port`: IntegerField(blank, null)
- `allow_reload`: BooleanField(default=True)
- `is_active`: BooleanField(default=True)

**TelephonySetting**
- `key`: CharField(100, unique)
- `label`: CharField(100, blank, null)
- `value`: TextField(blank, null)
- `description`: TextField(blank, null)
- `category`: CharField(50, default='general')
- `key_type`: CharField(20, choices=[string,integer,boolean,select,password], default='string')
- `options`: JSONField(blank, null)
- `is_secret`: BooleanField(default=False)
- `is_system`: BooleanField(default=False)
- `updated_at`: DateTimeField(auto_now)

**SIPTrunk**
- `name`: CharField(100, unique)
- `host`: CharField(255)
- `port`: IntegerField(default=5060)
- `auth_type`: CharField(20, choices=[userpass,ip], default='userpass')
- `username`: CharField(100, blank, null)
- `password`: CharField(100, blank, null)
- `context`: CharField(100, default='from-trunk')
- `outbound_proxy`: CharField(255, blank, null)
- `is_active`: BooleanField(default=True)
- `created_at`: DateTimeField(auto_now_add)

**CallQueue**
- `name`: CharField(100, unique)
- `strategy`: CharField(50, choices=[ringall,leastrecent,fewestcalls,random,rrmemory,linear,wrandom], default='ringall')
- `timeout`: IntegerField(default=15)
- `music_on_hold`: CharField(100, default='default')
- `announce`: CharField(100, blank, null)
- `context`: CharField(100, blank, null)
- `is_active`: BooleanField(default=True)

**QueueMember**
- `queue`: FK(CallQueue, CASCADE, related_name='static_members')
- `extension`: FK(SIPExtension, CASCADE)
- `penalty`: IntegerField(default=0)
- `wrapup_time`: IntegerField(default=0)
- Meta: unique_together=(queue, extension)

**AudioPrompt**
- `name`: CharField(100, unique)
- `description`: TextField(blank, null)
- `file`: FileField(upload_to='prompts/')
- `format`: CharField(10, default='wav')
- `created_at`: DateTimeField(auto_now_add)

**Certificate**
- `name`: CharField(100)
- `cert_file`: FileField(upload_to='certs/')
- `key_file`: FileField(upload_to='certs/', blank, null)
- `is_active`: BooleanField(default=True)
- `created_at`: DateTimeField(auto_now_add)

**IVRMenu**
- `name`: CharField(100, unique)
- `description`: TextField(blank, null)
- `prompt`: FK(AudioPrompt, SET_NULL, null, blank)
- `timeout`: IntegerField(default=10)
- `invalid_retries`: IntegerField(default=3)
- `is_active`: BooleanField(default=True)

**IVROption**
- `menu`: FK(IVRMenu, CASCADE, related_name='options')
- `digit`: CharField(1)
- `action`: CharField(20, choices=[extension,queue,ivr,hangup,voicemail])
- `action_value`: CharField(100)

**CallFlow**
- `name`: CharField(100, unique)
- `description`: TextField(blank, null)
- `is_active`: BooleanField(default=True)
- `created_at`: DateTimeField(auto_now_add)

**CallFlowNode**
- `flow`: FK(CallFlow, CASCADE, related_name='nodes')
- `node_type`: CharField(20, choices=[ivr,queue,dial,playback,hangup])
- `data`: JSONField
- `position_x`: FloatField(default=0)
- `position_y`: FloatField(default=0)

**CallFlowEdge**
- `from_node`: FK(CallFlowNode, CASCADE, related_name='outgoing_edges')
- `to_node`: FK(CallFlowNode, CASCADE, related_name='incoming_edges')
- `condition`: CharField(50)

**ConfigRevision**
- `revision_id`: CharField(50, unique)
- `description`: TextField(blank, null)
- `config_data`: JSONField
- `created_at`: DateTimeField(auto_now_add)
- `is_active`: BooleanField(default=False)
- `created_by`: FK(User, SET_NULL, null)

### 5.4 contacts

**Contact**
- `full_name`: CharField(255)
- `gender`: FK(MasterItem, SET_NULL, null, blank, related_name='contacts_gender')
- `date_of_birth`: DateField(null, blank)
- `age_group`: FK(MasterItem, SET_NULL, null, blank, related_name='contacts_age_group')
- `nationality`: FK(MasterItem, SET_NULL, null, blank, related_name='contacts_nationality')
- `id_type`: FK(MasterItem, SET_NULL, null, blank, related_name='contacts_id_type')
- `id_number`: CharField(100, blank, null)
- `phone_number`: CharField(30, blank, null)
- `email`: EmailField(blank, null)
- `created_at`: DateTimeField(auto_now_add)
- `created_by`: FK(User, SET_NULL, null, related_name='created_contacts')

**CaseParty**
- `case`: FK(Case, CASCADE, related_name='case_parties')
- `contact`: FK(Contact, CASCADE, related_name='case_roles')
- `role`: CharField(50, choices=[reporter,client,perpetrator,guardian,witness])
- `location`: FK(MasterItem, SET_NULL, null, blank, related_name='caseparty_location')
- `marital_status`: FK(MasterItem, SET_NULL, null, blank, related_name='caseparty_marital_status')
- `employment_status`: FK(MasterItem, SET_NULL, null, blank, related_name='caseparty_employment_status')
- `health_status`: FK(MasterItem, SET_NULL, null, blank, related_name='caseparty_health_status')
- `hiv_status`: FK(MasterItem, SET_NULL, null, blank, related_name='caseparty_hiv_status')
- `language`: FK(MasterItem, SET_NULL, null, blank, related_name='caseparty_language')
- `refugee_status`: FK(MasterItem, SET_NULL, null, blank, related_name='caseparty_refugee_status')
- `is_disabled`: BooleanField(default=False)
- `nearest_landmark`: CharField(255, blank)
- `relationship`: FK(MasterItem, SET_NULL, null, blank, related_name='caseparty_relationship')
- `tribe`: FK(MasterItem, SET_NULL, null, blank, related_name='caseparty_tribe')
- `comment`: TextField(blank, null)
- `is_primary`: BooleanField(default=False)
- `created_at`: DateTimeField(auto_now_add)
- Meta: unique_together=(case, contact, role)

### 5.5 messaging

**Tag**
- `name`: CharField(50, unique)

**Message**
- `channel`: CharField(20, choices=[call,sms,whatsapp,telegram,chat,email,walk-in])
- `sender`: CharField(50)
- `recipient`: CharField(50)
- `message_body`: TextField
- `timestamp`: DateTimeField(auto_now_add)
- `direction`: CharField(20, choices=[inbound,outbound])
- `case`: FK(Case, SET_NULL, null, blank, related_name='linked_messages')
- `tags`: ManyToManyField(Tag, blank)
- `ai_category`: CharField(100, null, blank)
- `status`: CharField(20, choices=[delivered,failed,pending], default='pending')
- `external_id`: CharField(100, null, blank)

### 5.6 notifications

**Notification**
- `recipient`: FK(User, CASCADE, related_name='notifications')
- `title`: CharField(255)
- `message`: TextField
- `type`: CharField(20, choices=[case,message,assignment,mention,system,referral], default='system')
- `category`: CharField(20, choices=[info,success,warning,error], default='info')
- `priority`: CharField(20, choices=[low,medium,high,urgent], default='medium')
- `action_url`: CharField(500, blank, null)
- `action_text`: CharField(100, blank, null)
- `metadata`: JSONField(default=dict, blank)
- `read`: BooleanField(default=False)
- `read_at`: DateTimeField(null, blank)
- `archived`: BooleanField(default=False)
- `created_at`: DateTimeField(auto_now_add)
- `updated_at`: DateTimeField(auto_now)
- Methods: `mark_as_read()`, `create_notification()`

### 5.7 masterdata

**MasterCategory**
- `name`: CharField(100, unique)
- `description`: TextField(blank, null)
- `is_active`: BooleanField(default=True)
- `parent`: FK('self', CASCADE, null, blank, related_name='children')

**MasterItem**
- `category`: FK(MasterCategory, CASCADE, related_name='items')
- `code`: CharField(50, blank, null)
- `label`: CharField(255)
- `order`: PositiveIntegerField(default=0)
- `is_active`: BooleanField(default=True)
- `metadata`: JSONField(blank, null)
- `parent`: FK('self', CASCADE, null, blank, related_name='children')

### 5.8 referrals

**ReferralAgency**
- `name`: CharField(255)
- `code`: SlugField(unique)
- `description`: TextField(blank)
- `mode`: CharField(20, choices=[platform,external])
- `contact_person`: CharField(255, blank)
- `contact_email`: EmailField(blank, null)
- `contact_phone`: CharField(20, blank, null)
- `notification_method`: CharField(20, choices=[none,email,whatsapp,both], default='email')
- `webhook_url`: URLField(blank, null)
- `api_key`: CharField(255, blank, null)
- `users`: ManyToManyField(User, related_name='agency_memberships', blank)
- `is_active`: BooleanField(default=True)
- `is_approved`: BooleanField(default=False)
- `handles_high_risk`: BooleanField(default=False)
- `created_at`: DateTimeField(auto_now_add)

**Referral**
- `case`: FK(Case, CASCADE, related_name='case_referrals')
- `initiator`: FK(User, PROTECT, related_name='initiated_referrals')
- `agency`: FK(ReferralAgency, PROTECT, related_name='received_referrals', null)
- `legacy_agency_name`: CharField(255, blank)
- `type`: CharField(100)
- `priority`: CharField(20, default='Normal')
- `consent_obtained`: BooleanField(default=False)
- `consent_details`: TextField(blank, null)
- `legal_basis`: CharField(255, blank)
- `status`: CharField(20, choices=[draft,pending,dispatched,acknowledged,accepted,rejected,completed,failed], default='draft')
- `status_notes`: TextField(blank, null)
- `shared_data`: JSONField(default=dict)
- `outcome`: TextField(blank, null)
- `follow_up_date`: DateField(null, blank)
- `created_at`: DateTimeField(auto_now_add)
- `updated_at`: DateTimeField(auto_now)

**ReferralActivity**
- `referral`: FK(Referral, CASCADE, related_name='activities')
- `user`: FK(User, SET_NULL, null)
- `action`: CharField(100)
- `notes`: TextField(blank, null)
- `created_at`: DateTimeField(auto_now_add)

**ReferralWorkflowConfig** (Singleton)
- `require_consent`: BooleanField(default=True)
- `auto_dispatch`: BooleanField(default=True)
- `require_legal_basis`: BooleanField(default=True)
- `follow_up_days`: IntegerField(default=7)
- `enforce_mandatory_outcome`: BooleanField(default=True)
- `supervisor_review_high_risk`: BooleanField(default=True)
- `updated_at`: DateTimeField(auto_now)
- Methods: `save()` forces pk=1, `get_config()`

**ReferralQueue**
- `id`: UUIDField(primary_key, default=uuid4)
- `call`: FK(Call, CASCADE, related_name='referrals')
- `status`: CharField(20, choices=[pending,processing,completed,failed,cancelled], default='pending')
- `retry_count`: PositiveIntegerField(default=0)
- `next_retry_at`: DateTimeField(null, blank)
- `payload`: JSONField(default=dict)
- `primero_case_id`: CharField(100, blank)
- `response_data`: JSONField(default=dict, blank)
- `error_message`: TextField(blank)
- `error_code`: CharField(50, blank)
- `submitted_by`: FK(User, SET_NULL, null, related_name='submitted_referrals')
- `completed_at`: DateTimeField(null, blank)
- `created_at`: DateTimeField(auto_now_add)
- `updated_at`: DateTimeField(auto_now)

**IntegrationLog**
- `id`: UUIDField(primary_key, default=uuid4)
- `referral`: FK(ReferralQueue, CASCADE, related_name='logs', null)
- `log_type`: CharField(20, choices=[auth,create_case,get_forms,error])
- `endpoint`: URLField
- `method`: CharField(10)
- `request_headers`: JSONField(default=dict, blank)
- `request_body`: JSONField(default=dict, blank)
- `response_status`: PositiveIntegerField(null)
- `response_body`: JSONField(default=dict, blank)
- `response_time_ms`: PositiveIntegerField(null)
- `error_message`: TextField(blank)
- `stack_trace`: TextField(blank)
- `created_at`: DateTimeField(auto_now_add)

### 5.9 qa

**QAScore**
- `agent`: FK(User, CASCADE, related_name='qa_scores')
- `case`: FK(Case, CASCADE, related_name='qa_scores')
- `criteria`: JSONField(default=dict)
- `score`: IntegerField
- `comments`: TextField(blank)
- `created_at`: DateTimeField(auto_now_add)

**AIQAEvaluation**
- `case`: FK(Case, CASCADE, related_name='ai_qa_evaluations')
- `evaluator_agent`: CharField(100)
- `overall_score`: FloatField(null, blank)
- `compliance_score`: FloatField(null, blank)
- `empathy_score`: FloatField(null, blank)
- `criteria_results`: JSONField(default=dict)
- `improvement_suggestions`: JSONField(default=list)
- `full_qa_json`: JSONField(default=dict)
- `created_at`: DateTimeField(auto_now_add)
- `reviewed_by`: FK(User, SET_NULL, null, blank)
- `is_disputed`: BooleanField(default=False)

### 5.10 workflow

**Workflow**
- `id`: UUIDField(primary_key, default=uuid4)
- `name`: CharField(255)
- `description`: TextField(blank, null)
- `status`: CharField(20, choices=[draft,active,archived], default='draft')
- `risk_level`: CharField(20, choices=[low,medium,high,critical], default='low')
- `created_at`: DateTimeField(auto_now_add)
- `updated_at`: DateTimeField(auto_now)
- `created_by`: FK(User, SET_NULL, null)

**WorkflowTrigger**
- `id`: UUIDField(primary_key, default=uuid4)
- `name`: CharField(255)
- `workflow`: FK(Workflow, CASCADE, related_name='triggers')
- `trigger_type`: CharField(50, choices=[call_started,call_ended,message_received,case_created,case_updated,case_event,referral_created,referral_updated,referral_outcome_received,ai_risk_high,task_overdue,scheduled_daily,sla_breached,manual_trigger])
- `trigger_config`: JSONField(default=dict)
- `is_active`: BooleanField(default=True)
- `created_at`: DateTimeField(auto_now_add)

**WorkflowVersion**
- `workflow`: FK(Workflow, CASCADE, related_name='versions')
- `version`: PositiveIntegerField
- `definition`: JSONField(default=dict)
- `is_active`: BooleanField(default=False)
- `created_at`: DateTimeField(auto_now_add)
- `created_by`: FK(User, SET_NULL, null)
- Meta: unique_together=(workflow, version)
- Methods: `validate_safeguards()`, `sync_triggers()`, `save()` auto-deactivates other versions

**WorkflowExecution**
- `id`: UUIDField(primary_key, default=uuid4)
- `workflow_version`: FK(WorkflowVersion, PROTECT, related_name='executions')
- `trigger`: FK(WorkflowTrigger, SET_NULL, null, blank)
- `case`: FK(Case, CASCADE, related_name='workflow_executions', null, blank)
- `trigger_event`: CharField(100)
- `context_data`: JSONField(default=dict)
- `current_node_id`: CharField(100, null, blank)
- `status`: CharField(20, choices=[pending,running,waiting,completed,failed,terminated], default='pending')
- `started_at`: DateTimeField(auto_now_add)
- `finished_at`: DateTimeField(null, blank)
- `error_message`: TextField(blank, null)

**ExecutionLog**
- `execution`: FK(WorkflowExecution, CASCADE, related_name='logs')
- `step_id`: CharField(100)
- `action_type`: CharField(100)
- `input_data`: JSONField(default=dict, blank)
- `output_data`: JSONField(default=dict, blank)
- `audit_context`: JSONField(default=dict, blank)
- `timestamp`: DateTimeField(auto_now_add)
- `success`: BooleanField(default=True)
- `error`: TextField(blank, null)

**Task, TaskExecution, TaskExecutionLog, TaskTemplate** (imported from `task_models.py`)

### 5.11 ai (LLM Layer)

**AIProvider**
- `name`: CharField(100)
- `provider_type`: CharField(20, choices=[openai,anthropic,gemini,deepseek,ollama,mistral,openrouter,antigravity,custom])
- `api_key`: CharField(255, blank, null)
- `base_url`: CharField(255, blank, null)
- `is_active`: BooleanField(default=True)
- `created_at`: DateTimeField(auto_now_add)

**AIModel**
- `model_id`: CharField(100, unique)
- `provider`: FK(AIProvider, CASCADE, related_name='models')
- `model_name`: CharField(100)
- `capabilities`: JSONField(default=dict)
- `context_window`: PositiveIntegerField(default=128000)
- `max_tokens`: PositiveIntegerField(default=4096)
- `recommended_use`: CharField(50, choices=[triage,extraction,translation,summarization,generic])
- `cost_per_1k_input`: DecimalField(10,6, default=0)
- `cost_per_1k_output`: DecimalField(10,6, default=0)
- `status`: CharField(20, choices=[active,deprecated,testing], default='active')
- `successor_model`: FK('self', SET_NULL, null, blank)
- `created_at`: DateTimeField(auto_now_add)

**AIPrompt**
- `prompt_id`: CharField(100, unique)
- `name`: CharField(255)
- `purpose`: CharField(100)
- `input_variables`: JSONField(default=list)
- `output_schema`: JSONField(default=dict)
- `status`: CharField(20, choices=[draft,active,archived], default='active')
- `compatible_models`: ManyToManyField(AIModel, blank)
- `created_at`: DateTimeField(auto_now_add)
- `updated_at`: DateTimeField(auto_now)

**AIPromptVersion**
- `prompt`: FK(AIPrompt, CASCADE, related_name='versions')
- `version_number`: PositiveIntegerField
- `system_role`: TextField(blank)
- `task_instruction`: TextField(blank)
- `constraints_safety`: TextField(blank)
- `user_template`: TextField(blank)
- `examples`: JSONField(default=list, blank)
- `guidance`: TextField(blank)
- `is_active`: BooleanField(default=False)
- `is_locked`: BooleanField(default=False)
- `created_at`: DateTimeField(auto_now_add)
- Meta: unique_together=(prompt, version_number)

**PromptVariable**
- `key`: CharField(100, unique)
- `description`: CharField(255)
- `source_path`: CharField(255)

**AIAgent**
- `name`: CharField(100)
- `agent_id`: SlugField(100, unique, default='default-agent')
- `role`: CharField(20, choices=[triage,summarizer,translator,extractor,qa])
- `model`: FK(AIModel, PROTECT, null, blank)
- `prompt_version`: FK(AIPromptVersion, PROTECT, null, blank)
- `temperature`: FloatField(default=0.0)
- `sba_enabled`: BooleanField(default=True)
- `guardrails`: JSONField(default=list, blank)
- `is_active`: BooleanField(default=True)
- `authorized_by`: FK(User, SET_NULL, null, blank, related_name='authorized_agents')
- `updated_at`: DateTimeField(auto_now)
- Methods: `update_killswitch_status()`, `get_performance_metrics(days=30)`

**AIAgentDocument**
- `agent`: FK(AIAgent, CASCADE, related_name='documents')
- `file`: FileField(upload_to='ai_documents/')
- `filename`: CharField(255)
- `description`: TextField(blank)
- `uploaded_at`: DateTimeField(auto_now_add)

**AIJob**
- `agent`: FK(AIAgent, SET_NULL, null, blank)
- `model_snapshot`: CharField(100, blank)
- `prompt_version_snapshot`: IntegerField(null)
- `input_type`: CharField(50)
- `source`: TextField
- `output`: JSONField(default=dict)
- `latency_ms`: PositiveIntegerField(null)
- `token_usage`: JSONField(default=dict, blank)
- `status`: CharField(20, choices=[pending,processing,completed,failed], default='pending')
- `created_at`: DateTimeField(auto_now_add)
- `updated_at`: DateTimeField(auto_now)

**SBAGlobalConfig** (Singleton)
- `enforcement_enabled`: BooleanField(default=True)
- `min_confidence_threshold`: FloatField(default=0.85)
- `updated_at`: DateTimeField(auto_now)
- Methods: `save()` forces pk=1, `get_solo()`

**RiskTaxonomy**
- `version`: PositiveIntegerField(unique)
- `is_active`: BooleanField(default=False)
- `created_at`: DateTimeField(auto_now_add)
- `description`: TextField(blank)
- `save()` auto-deactivates other versions

**RiskLevel**
- `taxonomy`: FK(RiskTaxonomy, CASCADE, related_name='levels')
- `name`: CharField(50)
- `color`: CharField(7)
- `requires_escalation`: BooleanField(default=True)
- `order`: PositiveIntegerField(default=0)
- `description`: TextField(blank)
- Meta: ordering=['order']

**EscalationRule**
- `risk_level`: FK(RiskLevel, CASCADE, related_name='escalation_rules')
- `target_role`: CharField(50)
- `sla_hours`: PositiveIntegerField(default=24)
- `notification_channel`: CharField(20, default='email')
- `is_active`: BooleanField(default=True)

**AssessmentLog**
- `case`: FK(Case, SET_NULL, null, blank)
- `job`: FK(AIJob, CASCADE)
- `risk_level`: FK(RiskLevel, SET_NULL, null, blank)
- `suggested_disposition`: TextField(blank)
- `recommended_next_state`: CharField(100, blank)
- `rationale_summary`: TextField(blank)
- `confidence_score`: FloatField
- `is_safe`: BooleanField
- `flagged_for_review`: BooleanField(default=False)
- `reviewed_by`: FK(User, SET_NULL, null, blank)
- `is_helpful`: BooleanField(null)
- `decision_application`: CharField(20, choices=[accepted,partially,overridden], blank)
- `override_reason`: CharField(20, choices=[inaccurate,bias,safety,procedural,other], blank)
- `human_comments`: TextField(blank)
- `created_at`: DateTimeField(auto_now_add)

**AIAction**
- `name`: CharField(200)
- `code`: SlugField(100, unique)
- `description`: TextField(blank)
- `method`: CharField(10, choices=[GET,POST], default='POST')
- `endpoint_url`: CharField(500)
- `provider`: FK(AIProvider, SET_NULL, null, blank)
- `content_type`: CharField(100, choices=[application/json,multipart/form-data], default='application/json')
- `timeout_seconds`: IntegerField(default=60)
- `is_active`: BooleanField(default=True)
- `input_mapping`: JSONField(default=dict)
- `output_mapping`: JSONField(default=dict)
- `created_at`: DateTimeField(auto_now_add)
- `updated_at`: DateTimeField(auto_now)

**AIActionExecutionLog**
- `action`: FK(AIAction, CASCADE, related_name='execution_logs')
- `case`: FK(Case, CASCADE, related_name='ai_action_logs')
- `triggered_by`: FK(User, SET_NULL, null, blank)
- `trigger_type`: CharField(50, choices=[manual,workflow], default='manual')
- `status`: CharField(20, choices=[pending,running,success,failed], default='pending')
- `execution_time_ms`: IntegerField(null, blank)
- `request_payload`: JSONField(null, blank)
- `response_payload`: JSONField(null, blank)
- `error_message`: TextField(blank)
- `timestamp`: DateTimeField(auto_now_add)

**AIPredictionFeedback**
- `case`: FK(Case, CASCADE, related_name='ai_prediction_feedback', null, blank)
- `user`: FK(User, SET_NULL, null, blank)
- `model_id`: CharField(100)
- `component_type`: CharField(25, choices=[transcript,translation,summarization,classification,entities,general])
- `rating`: IntegerField
- `comment`: TextField(blank)
- `metadata`: JSONField(default=dict, blank)
- `created_at`: DateTimeField(auto_now_add)

### 5.12 ai_service_models (External AI Pipeline)

**AIServiceConfig**
- `service_type`: CharField(50, choices=[transcription,translation,entity_extraction,classification,summarization,audio_analysis])
- `name`: CharField(200)
- `endpoint_url`: URLField
- `api_key`: CharField(500, blank)
- `timeout_seconds`: IntegerField(default=300)
- `supported_languages`: JSONField(default=list)
- `input_format`: CharField(50, default='application/json')
- `output_format`: CharField(50, default='application/json')
- `service_params`: JSONField(default=dict)
- `default_field_mappings`: JSONField(default=dict)
- `is_active`: BooleanField(default=True)
- `last_health_check`: DateTimeField(null, blank)
- `health_status`: CharField(20, default='unknown')
- Meta: unique_together=[(service_type, name)]

**AIServiceJob**
- `job_id`: UUIDField(default=uuid4, unique)
- `service_config`: FK(AIServiceConfig, PROTECT, related_name='jobs')
- `case`: FK(Case, CASCADE, related_name='ai_service_jobs')
- `triggered_by`: FK(User, SET_NULL, null, blank)
- `trigger_type`: CharField(50, choices=[auto_pipeline,manual_upload,workflow_step,case_update], default='manual_upload')
- `input_data`: JSONField
- `output_data`: JSONField(null, blank)
- `field_mappings`: JSONField(default=dict)
- `auto_populated`: BooleanField(default=False)
- `populated_fields`: JSONField(default=list)
- `status`: CharField(20, choices=[pending,processing,completed,failed,populated], default='pending')
- `error_message`: TextField(blank)
- `started_at`: DateTimeField(null, blank)
- `completed_at`: DateTimeField(null, blank)
- `processing_time_ms`: IntegerField(null, blank)
- Methods: `populate_case_fields()`, `_get_nested_value()`

**AIPipelineConfig**
- `name`: CharField(200)
- `description`: TextField(blank)
- `steps`: JSONField(default=list)
- `auto_trigger_on_call_end`: BooleanField(default=False)
- `auto_trigger_on_case_create`: BooleanField(default=False)
- `stop_on_error`: BooleanField(default=True)
- `retry_failed_steps`: BooleanField(default=False)
- `max_retries`: IntegerField(default=3)
- `is_active`: BooleanField(default=True)
- `created_at`: DateTimeField(auto_now_add)
- `updated_at`: DateTimeField(auto_now)

### 5.13 reports

**DashboardService** (`reports/dashboard_service.py`) — computes metrics for dashboard widgets.

### 5.14 config

**Organization** (`apps.config.models`)
- `name`, `logo`, `address`, `phone`, `email`, `settings` (JSONField)

**SourceChannel**
- `name`, `channel_type` (call, sms, whatsapp, telegram, email, walk-in, chat), `is_active`, `config` (JSONField)

### 5.15 webhooks

Simple webhook receiver endpoints.

---

## 6. Backend API Endpoints (by App)

### accounts
- `POST /api/v1/auth/login/` — JWT login (returns access + refresh)
- `POST /api/v1/auth/logout/` — JWT logout (blacklist refresh)
- `GET /api/v1/auth/me/` — current user profile with roles
- `POST /api/v1/auth/token/refresh/` — refresh access token
- `GET/POST /api/v1/accounts/users/` — user CRUD
- `GET/PUT/PATCH/DELETE /api/v1/accounts/users/<id>/` — user detail
- `GET/POST /api/v1/accounts/roles/` — role CRUD
- `GET/PUT/PATCH/DELETE /api/v1/accounts/roles/<id>/` — role detail
- `GET /api/v1/accounts/permissions/` — list all Django permissions

### cases
- `GET/POST /api/v1/cases/` — list/create cases
- `POST /api/v1/cases/create-complete/` — atomic case creation with nested parties, messages, referrals
- `GET/PUT/PATCH/DELETE /api/v1/cases/<id>/` — case detail
- `PATCH /api/v1/cases/<id>/close/` — close case (Supervisor/Admin only)
- `GET/POST /api/v1/cases/notes/` — case notes

### calls
- `GET/POST /api/v1/calls/` — call CRUD
- `GET/PUT/PATCH/DELETE /api/v1/calls/<id>/` — call detail
- `POST /api/v1/calls/answer/` — answer call via AMI
- `POST /api/v1/calls/hangup/` — hangup call via AMI
- `POST /api/v1/calls/transfer/` — transfer call
- `POST /api/v1/calls/queue/join/` — join queue
- `POST /api/v1/calls/queue/leave/` — leave queue
- `GET /api/v1/calls/queue/stats/` — real-time queue stats
- `POST /api/v1/calls/apply-config/` — sync DB → Asterisk configs + reload
- `GET/POST /api/v1/calls/extensions/` — SIP extension CRUD
- `GET/POST /api/v1/calls/settings/` — telephony settings CRUD
- `GET/POST /api/v1/calls/trunks/` — SIP trunk CRUD
- `GET/POST /api/v1/calls/queues/` — call queue CRUD
- `GET/POST /api/v1/calls/queue-members/` — queue member CRUD
- `GET/POST /api/v1/calls/ivrs/` — IVR menu CRUD
- `GET/POST /api/v1/calls/prompts/` — audio prompt CRUD
- `GET/POST /api/v1/calls/transports/` — PJSIP transport CRUD
- `GET/POST /api/v1/calls/call-flows/` — call flow CRUD
- `GET/POST /api/v1/calls/revisions/` — config revision CRUD
- `GET/POST /api/v1/calls/certificates/` — certificate CRUD

### contacts
- `GET/POST /api/v1/contacts/` — contact CRUD
- `GET/PUT/PATCH/DELETE /api/v1/contacts/<id>/` — contact detail
- `GET/POST /api/v1/contacts/case-parties/` — case party CRUD
- `GET/PUT/PATCH/DELETE /api/v1/contacts/case-parties/<id>/` — case party detail

### messaging
- `GET/POST /api/v1/messaging/` — message CRUD
- `GET/PUT/PATCH/DELETE /api/v1/messaging/<id>/` — message detail

### notifications
- `GET /api/v1/notifications/` — list my notifications
- `POST /api/v1/notifications/<id>/mark-read/` — mark as read
- `POST /api/v1/notifications/mark-all-read/` — mark all read
- `GET /api/v1/notifications/unread-count/` — unread count
- `GET /api/v1/notifications/recent/` — last 10 notifications
- `POST /api/v1/notifications/<id>/archive/` — archive
- `DELETE /api/v1/notifications/clear-all/` — delete all

### masterdata
- `GET/POST /api/v1/masterdata/categories/` — category CRUD
- `GET/PUT/PATCH/DELETE /api/v1/masterdata/categories/<id>/` — category detail
- `GET/POST /api/v1/masterdata/items/` — item CRUD
- `GET/PUT/PATCH/DELETE /api/v1/masterdata/items/<id>/` — item detail
- `POST /api/v1/masterdata/sync/` — sync master data
- `POST /api/v1/masterdata/export/` — export
- `POST /api/v1/masterdata/import/` — import

### referrals
- `GET/POST /api/v1/referrals/` — referral CRUD
- `GET/PUT/PATCH/DELETE /api/v1/referrals/<id>/` — referral detail

### qa
- `GET/POST /api/v1/qa/scores/` — manual QA score CRUD
- `GET/POST /api/v1/qa/ai-evaluations/` — AI QA evaluation CRUD

### workflow
- `GET/POST /api/v1/workflow/definitions/` — workflow CRUD
- `GET/PUT/PATCH/DELETE /api/v1/workflow/definitions/<id>/` — workflow detail
- `GET/POST /api/v1/workflow/triggers/` — trigger CRUD
- `GET/POST /api/v1/workflow/executions/` — execution CRUD
- `POST /api/v1/workflow/executions/<id>/simulate/` — simulate workflow
- `POST /api/v1/workflow/executions/<id>/approve/` — approve execution

### reports
- `GET /api/v1/reports/pivot/` — pivot report
- `GET /api/v1/reports/dashboard-data/` — dashboard metrics

### ai
- `POST /api/v1/ai/generate/` — direct LLM generation
- `GET/POST /api/v1/ai/jobs/` — AI job CRUD + create
- `GET /api/v1/ai/jobs/<id>/` — job status/result
- `POST /api/v1/ai/workflow/transcribe/` — manual transcription
- `POST /api/v1/ai/workflow/translate/` — manual translation
- `POST /api/v1/ai/workflow/extract_entities/` — NER
- `POST /api/v1/ai/workflow/classify/` — classification
- `POST /api/v1/ai/workflow/summarize/` — summarization
- `POST /api/v1/ai/pipelines/<id>/execute/` — execute pipeline
- `POST /api/v1/ai/cases/<case_pk>/ai/trigger-pipeline/` — trigger for case
- `POST /api/v1/ai/cases/<case_pk>/save_insight/` — save manual insight
- `POST /api/v1/ai/actions/<id>/execute/` — execute AI action
- `GET/POST /api/v1/ai/sba/config/` — SBA config
- `GET/POST /api/v1/ai/taxonomy/` — risk taxonomy
- `GET/POST /api/v1/ai/risk-levels/` — risk levels
- `GET/POST /api/v1/ai/providers/` — AI provider registry
- `GET/POST /api/v1/ai/models/` — AI model registry
- `GET/POST /api/v1/ai/prompts/` — prompt registry
- `GET/POST /api/v1/ai/agents/` — agent registry
- `GET/POST /api/v1/ai/documents/` — agent documents
- `GET/POST /api/v1/ai/assessments/` — assessment logs
- `GET/POST /api/v1/ai/actions/` — AI actions registry
- `GET/POST /api/v1/ai/service-configs/` — AI service configs
- `POST /api/v1/ai/call-audio-analysis/` — direct audio analysis (frontend calls external AI)

### config (admin)
- `GET/POST /api/v1/admin/source-channels/` — source channel CRUD
- `GET/PUT /api/v1/admin/organization/` — organization settings

---

## 7. Key Backend Services & Logic

### 7.1 Asterisk Config Service (`apps.calls.services.AsteriskConfigService`)
Generates `.conf` files from DB models into `dockerized-asterisk/config/generated/`:
- `sync_extensions()` → `pjsip_wizard_custom.conf`
- `sync_transports()` → `pjsip_transports.conf`
- `sync_trunks()` → `pjsip_trunks.conf`
- `sync_queues()` → `queues_custom.conf`
- `sync_dialplan()` → `extensions_custom.conf`
- `sync_global_settings()` → `pjsip_common.conf`, `voicemail.conf`
- `create_snapshot()` / `restore_snapshot()` — config versioning
- `apply_config()` — hot-reloads Asterisk via AMI

Signals (`apps.calls.signals`) auto-sync config on every save/delete of telephony models.

### 7.2 AMI Service (`apps.calls.ami_service.AsteriskAMIService`)
Uses `panoramisk` (async AMI library):

**Event Listeners:**
- `Newchannel` → broadcasts `incoming_call` to WebSocket
- `Newstate` → tracks call state changes
- `Hangup` → broadcasts `call_ended`
- `QueueCallerJoin/Leave` → queue status updates
- `QueueMemberAdded/Removed` → agent queue membership

**Control Actions:**
- `answer_call(channel)` — Redirect to 'answered' context
- `hangup_call(channel)` — AMI Hangup
- `transfer_call(channel, extension)` — AMI Redirect
- `add_queue_member(queue, interface)` / `remove_queue_member()`
- `get_queue_summary()` — parses real-time queue stats
- `reload_asterisk(module)` — hot reload

**Management command:** `python manage.py run_ami_listener`

### 7.3 Notification Signals (`apps.notifications.signals`)
Auto-notifications triggered by:
1. **Case post_save**: new assignment → notify assignee; reassignment → notify old+new; status change → notify assignee; risk escalation → high priority warning
2. **Message post_save**: new inbound → notify assigned agent, or broadcast to first 5 agents if unassigned
3. **Notification post_save**: auto-pushes to WebSocket group `user_<recipient_id>`

### 7.4 LLM Service (`apps.ai.services.LLMService`)
- `generate(agent, context)` — unified orchestrator
- Supports OpenAI, OpenRouter, Mistral, Gemini, Ollama, Antigravity
- Dynamic model routing via `AIRouter`
- Multi-layer prompt assembly: system_role → guidance → task → constraints → guardrails → few-shot → output_schema
- Automatic `AssessmentLog` creation on structured outputs
- Retry with exponential backoff on 429

### 7.5 AI Pipeline Executor (`apps.ai.pipeline_executor.AIPipelineExecutor`)
- Executes multi-step pipelines defined in `AIPipelineConfig`
- Sequential step execution with error handling
- Automatic field mapping from AI outputs to Case model fields
- Triggered by case creation, call end, or manual trigger

### 7.6 Primero Integration (`apps.integrations.primero`)
- `PrimeroAuth` — JWT token management with caching
- `PrimeroAPIClient` — full v2 API client with retry logic
- `PrimeroCaseMapper` — maps OpenCHS Call → Primero Case payload
- Celery task `process_referral_async` for async case creation
- Retry delays: 1min, 5min, 30min, 2hrs

---

## 8. Frontend Architecture (Vue 3)

### 8.1 Project Structure
```
frontend/src/
├── main.js
├── App.vue
├── axios.js
├── i18n.js
├── router/
│   └── index.js
├── api/
│   ├── authApi.js
│   ├── casesApi.js
│   ├── callsApi.js
│   ├── contactsApi.js
│   ├── messagingApi.js
│   ├── qaApi.js
│   ├── referralsApi.js
│   ├── reportsApi.js
│   ├── workflowApi.js
│   ├── aiApi.js
│   ├── notificationsApi.js
│   ├── masterdataApi.js
│   ├── configApi.js
│   ├── rolesApi.js
│   ├── usersApi.js
│   ├── permissionsApi.js
│   └── caseCreationApi.js
├── stores/
│   ├── authStore.js
│   ├── callStore.js
│   ├── caseStore.js
│   ├── casesStore.js
│   ├── configStore.js
│   ├── contactsStore.js
│   ├── dashboardStore.js
│   ├── inboxStore.js
│   ├── masterdataStore.js
│   ├── notificationStore.js
│   ├── qaStore.js
│   ├── referralStore.js
│   ├── referralsStore.js
│   ├── settingsStore.js
│   ├── telephonyStore.js
│   ├── aiStore.js
│   └── workflowStore.js
├── views/
│   ├── LoginView.vue
│   ├── DashboardView.vue
│   ├── CasesView.vue
│   ├── CallsView.vue
│   ├── ContactsView.vue
│   ├── InboxView.vue
│   ├── QAView.vue
│   ├── ReferralsView.vue
│   ├── ReportsView.vue
│   ├── MessagingView.vue
│   ├── AIView.vue
│   └── admin/
│       ├── AdminView.vue
│       ├── AdminUsersView.vue
│       ├── RolesView.vue
│       ├── TelephonySettingsView.vue
│       ├── SettingsView.vue
│       ├── MasterDataList.vue
│       ├── SourceChannelsView.vue
│       ├── OrganizationView.vue
│       ├── ExtensionsView.vue
│       ├── ReferralSettingsView.vue
│       ├── AIConfigView.vue
│       ├── AIModelRegistry.vue
│       ├── AIServiceConfig.vue
│       ├── AIPromptRegistry.vue
│       ├── AIAgentBuilder.vue
│       ├── SBASettings.vue
│       ├── AIActionsRegistry.vue
│       ├── AIMonitoringView.vue
│       ├── AssessmentList.vue
│       ├── WorkflowList.vue
│       ├── WorkflowBuilder.vue
│       ├── WorkflowEditor.vue
│       ├── TaskLibrary.vue
│       ├── WorkflowMonitoring.vue
│       └── WorkflowReviewView.vue
├── components/
│   ├── layout/
│   │   ├── AppShell.vue
│   │   ├── Sidebar.vue
│   │   ├── Topbar.vue
│   │   └── ToastNotification.vue
│   ├── common/
│   │   ├── Button.vue
│   │   ├── DataTable.vue
│   │   ├── Input.vue
│   │   ├── Modal.vue
│   │   ├── RichTextEditor.vue
│   │   └── VoiceRecorder.vue
│   ├── dashboard/
│   │   ├── MetricCard.vue
│   │   └── QuickAction.vue
│   ├── cases/
│   │   ├── CaseClosureForm.vue
│   │   ├── CaseNotes.vue
│   │   └── FollowupForm.vue
│   ├── calls/
│   │   ├── CallFormPrimeroFields.vue
│   │   ├── CallList.vue
│   │   └── CallPanel.vue
│   ├── contacts/
│   │   ├── CasePartySection.vue
│   │   ├── ContactForm.vue
│   │   └── ContactList.vue
│   ├── inbox/
│   │   ├── AIAssistantPanel.vue
│   │   ├── CaseCreationModal.vue
│   │   ├── ChannelSelector.vue
│   │   └── ChatMessage.vue
│   ├── messaging/
│   │   ├── AIAssistantPanel.vue
│   │   ├── CallDetail.vue
│   │   ├── MessageComposer.vue
│   │   └── MessageTagger.vue
│   ├── notifications/
│   │   └── NotificationBell.vue
│   ├── qa/
│   │   ├── QAReviewDetail.vue
│   │   └── QAReviewForm.vue
│   ├── referrals/
│   │   ├── ReferralForm.vue
│   │   └── ReferralModal.vue
│   ├── telephony/
│   │   ├── CallControls.vue
│   │   ├── CallPopup.vue
│   │   ├── DialPad.vue
│   │   ├── SIPStatus.vue
│   │   └── Softphone.vue
│   ├── workflow/
│   │   └── (workflow-specific components)
│   ├── admin/
│   │   ├── DynamicFormBuilder.vue
│   │   ├── MasterDataManager.vue
│   │   ├── RoleManager.vue
│   │   ├── UserManager.vue
│   │   └── ...
│   ├── ai/
│   │   ├── AIActionsRegistry.vue
│   │   ├── AIAgentBuilder.vue
│   │   ├── AIModelRegistry.vue
│   │   ├── AIPromptRegistry.vue
│   │   └── ...
│   └── reports/
│       └── PivotReportView.vue
├── composables/
│   ├── useApi.js
│   ├── useAuth.js
│   ├── useCallHandler.js
│   ├── useForm.js
│   ├── useNotification.js
│   └── useWebSocket.js
├── services/
│   ├── ringtoneService.js
│   └── sipService.js
├── locales/
│   ├── en.json
│   ├── sw.json
│   ├── fr.json
│   └── so.json
└── assets/
    └── css/
        ├── reset.css
        ├── variables.css
        ├── main.css
        └── cases-view.css
```

### 8.2 Router (`router/index.js`)

Uses `createWebHistory`. Routes wrapped in `AppShell` layout except `/login`.

**Public Routes:**
- `/login` → LoginView (hideLayout: true)

**Main Routes (requiresAuth):**
- `/` → DashboardView (roles: Admin, Supervisor, Agent, QA Officer, Partner)
- `/contacts` → ContactsView (Admin, Supervisor)
- `/cases` → CasesView (Admin, Supervisor, Agent, QA Officer)
- `/cases/new` → CaseForm (Admin, Supervisor, Agent)
- `/cases/:id` → CaseForm (Admin, Supervisor, Agent, QA Officer)
- `/qa` → QAView (Admin, Supervisor, QA Officer)
- `/inbox` → InboxView (Admin, Supervisor, Agent)
- `/referrals` → ReferralsView (Admin, Supervisor, Agent)
- `/reports` → ReportsView (Admin, Supervisor)
- `/calls` → CallsView (lazy) (Admin, Supervisor, Agent)
- `/messaging` → MessagingView (lazy) (Admin, Supervisor, Agent)
- `/ai-services` → AIView (lazy) (Admin, Supervisor)

**Admin Routes (`/admin`):**
- `/admin/users` → AdminUsersView (Admin)
- `/admin/roles` → RolesView (Admin)
- `/admin/telephony-settings` → TelephonySettingsView (Admin)
- `/admin/settings` → SettingsView (Admin)
- `/admin/settings/masterdata` → MasterDataList (Admin)
- `/admin/settings/source-channels` → SourceChannelsView (Admin)
- `/admin/settings/organization` → OrganizationView (Admin)
- `/admin/extensions` → ExtensionsView (Admin)
- `/admin/referral-settings` → ReferralSettingsView (Admin)
- `/admin/ai-configuration` → AIConfigView (Admin, Supervisor)
- `/admin/ai-configuration/registry` → AIModelRegistry (Admin, Supervisor)
- `/admin/ai-configuration/services` → AIServiceConfig (Admin, Supervisor)
- `/admin/ai-configuration/prompts` → AIPromptRegistry (Admin, Supervisor)
- `/admin/ai-configuration/agents` → AIAgentBuilder (Admin, Supervisor)
- `/admin/ai-configuration/sba` → SBASettings (Admin, Supervisor)
- `/admin/ai-configuration/actions` → AIActionsRegistry (Admin, Supervisor)
- `/admin/ai-monitoring` → AIMonitoringView (Admin, Supervisor, QA Officer)
- `/admin/ai-monitoring/sba` → AssessmentList (Admin, Supervisor, QA Officer)
- `/admin/workflows` → WorkflowList (Admin, Supervisor)
- `/admin/workflows/:id` → WorkflowBuilder (Admin, Supervisor)
- `/admin/workflows/tasks` → TaskLibrary (Admin)
- `/admin/workflows/monitoring` → WorkflowMonitoring (Admin, Supervisor)
- `/admin/workflows/review` → WorkflowReviewView (Admin, Supervisor)

**Router Guards:**
- `DISABLE_GUARD` flag for development
- Sets `document.title` from route meta
- Redirects authenticated users away from `/login` to Dashboard
- Redirects unauthenticated users to Login
- Role check: if user lacks required role, redirect to Login with `error=insufficient_permissions`

### 8.3 Axios Configuration (`axios.js`)
- Base URL from `VITE_API_BASE_URL` or `http://127.0.0.1:8000/api/v1`
- **Request interceptor**: attaches `Authorization: Bearer <accessToken>` to all requests except login/refresh
- **Response interceptor**:
  - Handles 401 with automatic token refresh
  - Queues concurrent requests during refresh
  - On refresh failure → calls `clearAuth()` and redirects to login
  - Error normalization for consistent frontend handling

### 8.4 Pinia Stores Summary

| Store | Type | Key Responsibilities |
|-------|------|---------------------|
| `authStore` | Options API | JWT login/logout/refresh, user profile, SIP config init, role checks (`isAdmin`, `hasRole`) |
| `callStore` | Composition API | SIP/WebRTC call handling, incoming call popup, WebSocket for Asterisk notifications, mute/hold, queue mgmt |
| `caseStore` | Options API | Case creation wizard, draft auto-save to localStorage (24h expiry), case parties, field updates |
| `casesStore` | Options API | Case list CRUD (fetch, create, update, delete) |
| `configStore` | Options API | Organization settings, source channels, logo URL resolution |
| `contactsStore` | Options API | Contact list with pagination, case party CRUD |
| `dashboardStore` | Options API | Dashboard metrics, live operations, AI insights, QA stats, recent activity |
| `inboxStore` | Composition API | Messages and calls list, send messages, tagging |
| `masterdataStore` | Options API | Master data categories/items CRUD |
| `notificationStore` | Options API | Notifications list, unread count, mark read/delete, WebSocket connection |
| `qaStore` | Options API | QA reviews (manual scores) and AI evaluations CRUD |
| `referralStore` | Options API | Agencies and referrals list, initiate referral, update status |
| `referralsStore` | Options API | Case-specific referrals |
| `settingsStore` | Options API | Master data sync, options lookup by category name |
| `telephonyStore` | Options API | Full Asterisk PBX config management — settings, trunks, queues, IVRs, extensions, transports, call flows, certificates, apply config |
| `aiStore` | Options API | AI agents, audio analysis with polling, task cancellation, narrative triage, text refinement, insight mapping |
| `workflowStore` | Options API | Workflow definitions, triggers, executions, approvals |

### 8.5 Key Composables

| Composable | Purpose |
|------------|---------|
| `useApi` | Generic async API wrapper returning `{ data, error, loading, execute }` |
| `useAuth` | Thin wrapper around authStore |
| `useCallHandler` | WebRTC call handling — start/end, mute/hold, MediaRecorder, sends audio to AI on hangup |
| `useForm` | Reactive form/errors, `validateField`, `validateAll`, `resetForm` |
| `useNotification` | Global toast queue with auto-dismiss |
| `useWebSocket` | Reusable WebSocket with JWT auth, auto-reconnect (3 attempts) |

### 8.6 i18n
- Languages: English (`en`), Swahili (`sw`), French (`fr`), Somali (`so`)
- Files in `src/locales/`

---

## 9. Telephony Architecture

### 9.1 Asterisk Configuration (dockerized-asterisk/)
- **Asterisk 20 LTS** compiled from source on Debian Bullseye
- **Ports**: SIP 5060 (TCP/UDP), RTP 10000-10100 (UDP), ARI/HTTP 8088 (TCP), AMI 5038 (TCP)
- **Config files**: `asterisk.conf`, `modules.conf`, `manager.conf` (AMI), `ari.conf`, `http.conf`, `stasis.conf`, `pjsip.conf`, `extensions.conf`, `queues.conf`, `voicemail.conf`, `features.conf`, `rtp.conf`, `indications.conf`, `logger.conf`
- Generated configs in `config/generated/` produced by `AsteriskConfigService`

### 9.2 Call Flow
```
Caller → Asterisk (SIP Trunk)
    ↓
Asterisk emits Newchannel event via AMI (port 5038)
    ↓
AsteriskAMIService.on_newchannel() → channel_layer.group_send('agents', ...)
    ↓
NotificationConsumer pushes 'incoming_call' via WebSocket
    ↓
Vue Frontend: CallPopup appears with caller info
    ↓
Agent clicks Answer → POST /api/calls/answer/
    ↓
Django → ami_service.answer_call() → AMI Redirect → Asterisk connects
```

### 9.3 Call Recording & AI
```
Call in progress → MixMonitor records to Asterisk filesystem
    ↓
Hangup event → AMI service copies recording → MinIO/S3
    ↓
POST /api/calls/ → Create Call record with recording_url
    ↓
Case linked → trigger_ai_pipeline()
    ↓
AIPipelineExecutor: Transcribe → Translate → NER → Classify → Summarize
    ↓
Auto-populate Case fields (ai_transcript, ai_summary, etc.)
```

---

## 10. AI Architecture (Dual Layer)

### 10.1 External AI Service Layer (ML Models)
| Service | Input | Output | Typical Model |
|---------|-------|--------|---------------|
| Transcription | Audio (.wav) | Text + timestamps | Whisper ASR |
| Translation | Text | Translated text + source lang | Helsinki-NLP |
| NER | Text | Entities (PERSON, LOCATION, DATE) | DistilBERT |
| Classification | Text | Categories + confidence | Custom classifier |
| Summarization | Text | Summary | Flan-T5 |
| Audio Analysis | Audio | Complete pipeline output | Orchestrated |

Orchestrated by `AIPipelineExecutor` via `AIServiceConfig` / `AIServiceJob`.

### 10.2 LLM Reasoning Layer (Agents)
| Agent Role | Purpose |
|------------|---------|
| Triage | Risk assessment, urgency scoring |
| Summarizer | Case narrative summarization |
| Translator | Language translation |
| Extractor | Structured data extraction |
| QA | Agent performance evaluation |

Orchestrated by `LLMService.generate(agent, context)` with dynamic routing via `AIRouter`.

### 10.3 Safety-by-Architecture (SBA)
- `SBAGlobalConfig`: min_confidence_threshold=0.85, enforcement_enabled=True
- `AIAgent`: requires `authorized_by` supervisor to activate
- `AIAgent.update_killswitch_status()`: auto-deactivate if error_rate > 25% over 20+ executions
- `AssessmentLog`: immutable AI suggestions, human override tracking with mandatory rationale
- `WorkflowVersion.validate_safeguards()`: high-risk workflows MUST have approval node; case closure workflows MUST have human approval

---

## 11. Deployment & DevOps

### 11.1 Docker Compose Services
| Service | Image | Ports | Purpose |
|---------|-------|-------|---------|
| db | postgres:15 | 5433:5432 | Primary database |
| redis | redis:7 | 6379:6379 | Cache, broker, Channels backplane |
| minio | minio/minio | 9000, 9001 | Object storage (S3-compatible) |
| backend | Build ./backend | 8000 | Django API + Channels |
| frontend | Build ./frontend (Dockerfile.dev) | 5173, 8080 | Vue dev server |
| asterisk | Build ./dockerized-asterisk | 5060, 8088, 5038, 10000-10100 | PBX |

### 11.2 Environment Variables
**Root `.env` (Docker Compose):**
- `SERVICES`
- `POSTGRES_DB`, `POSTGRES_USER`, `POSTGRES_PASSWORD`
- `MINIO_ROOT_USER`, `MINIO_ROOT_PASSWORD`

**Backend `.env`:**
- `SECRET_KEY`, `DEBUG`
- `POSTGRES_DB`, `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_HOST`, `POSTGRES_PORT`
- `REDIS_HOST`, `REDIS_PORT`
- `MINIO_ROOT_USER`, `MINIO_ROOT_PASSWORD`
- `ASTERISK_AMI_HOST`, `ASTERISK_AMI_PORT`, `ASTERISK_AMI_USERNAME`, `ASTERISK_AMI_SECRET`
- `PRIMERO_BASE_URL`, `PRIMERO_USERNAME`, `PRIMERO_PASSWORD`, `PRIMERO_TIMEOUT`, `PRIMERO_VERIFY_SSL`

**Frontend `.env`:**
- `VITE_API_BASE_URL=http://127.0.0.1:8000/api/v1`

### 11.3 Build & Entrypoint
- **Backend Dockerfile**: python:3.9-slim, installs nano/netcat, entrypoint.sh waits for Postgres, runs migrations, seeds DB, starts server
- **Frontend Dockerfile (prod)**: multi-stage node:18-alpine build → nginx:stable-alpine serve
- **Frontend Dockerfile.dev**: node:18-alpine, npm run dev
- **Asterisk Dockerfile**: compiles Asterisk 20 from source

### 11.4 Gaps
- No CI/CD pipelines configured (no `.github/`, GitLab CI, etc.)
- No production docker-compose.prod.yml (only conceptual in docs)
- No Kubernetes manifests
- Secrets in plaintext `.env` files

---

## 12. Data Flows

### 12.1 Incoming Call Flow
```
Caller dials → Asterisk receives SIP
    ↓
Asterisk emits Newchannel via AMI
    ↓
AsteriskAMIService receives event → channel_layer.group_send
    ↓
NotificationConsumer → WebSocket → user_<agent_id> group
    ↓
Vue Frontend: CallPopup with caller_id
    ↓
Agent clicks Answer → POST /api/calls/answer/
    ↓
Django → AMI Redirect → call connected
```

### 12.2 Case Creation Flow
```
Agent clicks 'Create Case' from call popup
    ↓
Vue pre-fills case form with caller info
    ↓
Agent fills details + case parties
    ↓
POST /api/v1/cases/create-complete/
    ↓
CaseCreationSerializer (atomic transaction):
   - Create Contact (if new)
   - Create CaseParties with roles
   - Link Calls
   - Create Messages
   - Create Referrals
    ↓
201 Created → redirect to Case detail
```

### 12.3 AI Processing Flow
```
Call ends → Hangup event
    ↓
Recording uploaded to MinIO
    ↓
Call record created → post_save signal
    ↓
Trigger AIPipelineExecutor
    ↓
Step 1: AIServiceClient.transcribe_audio → ai_transcript
Step 2: AIServiceClient.translate_text → ai_translated_text
Step 3: AIServiceClient.extract_entities → ai_extracted_entities
Step 4: AIServiceClient.classify_case → ai_classification
Step 5: AIServiceClient.summarize_text → ai_summary
    ↓
Auto-populate Case fields via field_mappings
    ↓
If ai_risk_high → WorkflowTrigger → notify supervisor
```

### 12.4 Primero Referral Flow
```
Agent checks 'Refer to Primero' in call form + enters ABR ID
    ↓
Call saved → validation (ABR ID format: ABR + 9-12 digits)
    ↓
ReferralQueue created with status=PENDING
    ↓
Celery task process_referral_async:
   - Attempt 1: immediate POST to Primero /api/v2/cases
   - Fail → retry in 1min, 5min, 30min, 2hrs
   - Max 4 retries → mark FAILED + alert admin
    ↓
On success: Primero case ID stored, status=COMPLETED
```

---

## 13. File Storage Conventions

| Upload Type | Path | Model Field |
|-------------|------|-------------|
| Call recordings | `call_recordings/%Y/%m/` | `Case.call_recording` |
| Audio prompts | `prompts/` | `AudioPrompt.file` |
| Certificates | `certs/` | `Certificate.cert_file`, `.key_file` |
| AI documents | `ai_documents/` | `AIAgentDocument.file` |
| Organization logo | `organization/` | `Organization.logo` |

All served via MinIO/S3-compatible API. Media files served by Django in dev (`static()` in urls), Nginx in prod.

---

## 14. Seed Data

The project includes seed scripts in `backend/scripts/`:
- `seed_all.py` — orchestrates all seeding
- `seed_users.py` — creates demo users (admin, supervisor, agent, qa)
- `seed_master_data.py` — populates MasterCategories and MasterItems
- `seed_cases.py`, `seed_calls.py`, `seed_contacts.py` — demo data
- `seed_agencies.py` — referral agencies
- `seed_organization.py` — organization record
- `seed_source_channels.py` — messaging channels
- `seed_ai_models.py` — AI providers and models
- `seed_prompts.py` — default prompts
- `seed_workflows.py` — default workflows
- `simulate_whatsapp.py` — simulate inbound WhatsApp messages

`entrypoint.sh` runs `seed_everything.py` (idempotent) on container start.

---

## 15. Testing

### Backend
- Django test runner (`python manage.py test`)
- Tests located in each app's `tests.py`

### Frontend
- Jest 29.7.0 + @vue/test-utils 2.4.6 + @vue/vue3-jest 29.2.6
- Config: `jest.config.js`
- Babel config: `babel.config.js`

---

## 16. Security Considerations

- JWT authentication with short-lived access tokens (1h) and rotating refresh tokens (7d)
- CORS configured for local development origins
- Role-based access control on all API endpoints and frontend routes
- CSRF protection enabled
- Clickjacking protection (X-Frame-Options)
- Asterisk AMI uses authenticated connection
- Primero integration uses JWT + SSL verification
- AI Safety-by-Architecture: dual-control authorization, kill switches, immutable audit logs, mandatory override rationale
- Workflow safeguarding: high-risk workflows require human-in-the-loop approval
- Referral consent tracking: `consent_obtained` and `legal_basis` fields mandatory

---

## 17. Integration Points

| External System | Integration Type | Purpose |
|-----------------|------------------|---------|
| **Primero CPIMS+** | REST API v2 | Child protection case referral |
| **Asterisk PBX** | AMI + ARI | Telephony control and events |
| **AI Microservice** | REST API | Transcription, NER, classification, summarization |
| **MinIO/S3** | S3-compatible API | File storage for recordings, documents |
| **WhatsApp/Telegram/SMS** | Webhooks/Messaging API | Omnichannel messaging (extensible) |

---

## 18. Notable Design Patterns

1. **App-based modularity** — Each domain is a self-contained Django app
2. **DB-driven telephony config** — Asterisk configs generated from Django models with versioning
3. **Signal-driven notifications** — `post_save` signals auto-trigger WebSocket pushes
4. **Dual AI architecture** — Separate ML pipeline service + LLM reasoning agents
5. **Case-linked AI jobs** — Every AI operation is auditable and traceable to a case
6. **Auto-population via field mappings** — AI results flow directly into case fields without manual copy-paste
7. **Composition API + Options API mix** in Pinia stores based on complexity
8. **Draft auto-save** for case creation with 24-hour localStorage expiry
9. **Singleton pattern** for global configs (ReferralWorkflowConfig, SBAGlobalConfig)
10. **Retry with exponential backoff** for external integrations (Primero, AI services)

---

*End of CONTEXT.md*
