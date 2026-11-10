# D1 Inception Report — Validation Meeting — Slide Notes

**Meeting:** Tuesday 3 November 2026 · virtual · proposed 3 hours including a 10-minute break *(adjust to the actual slot)*
**Participants:** Session 3 participants — UNICEF, Ministry of Social Development, Child Helpline, Primero, BITZ
**Source document:** D1 Inception Report v2.7 (30 October 2026), plus the amendments received by Monday 2 November
**Facilitator:** Nelson Adagi (BITZ) · **Note-taker:** *(name before the meeting)*

## How these slides work

The meeting walks through the inception report **section by section, in the report's order**, so that participants validate every part of the draft in the meeting, not only the parts they read.

Each content slide has four parts:
- **On slide:** what the report says, in short form. Show this.
- **Validate:** the questions the facilitator asks. Each section ends with one of three outcomes:
  - ✅ **Validated:** accurate and complete as written.
  - ✏️ **Validated with amendments:** record the agreed wording.
  - ⏸ **Not yet validated:** record the open point, its owner and a date.
- **Gaps to close:** the open items in that section that need an answer, an owner or a date.
- **Record:** what the note-taker writes in the validation tracker (slide 44) and the decision log (slide 45).

Amendments received by Monday are taken **in the section they relate to**, not in a separate block. Section and table numbers refer to report v2.7.

---

# Part 1 — Opening

## Slide 1 — Title

**On slide:**
- D1 Inception Report — Validation Meeting
- OPENCHS – Primero CPIMS+ Integration, Lesotho Child Helpline 116
- Contract 43427866, Amendment 3 · Deliverable D1 (item 50)
- Tuesday 3 November 2026

**Speaker notes:**
Welcome everyone and thank them for the reviews received. Today we validate the draft inception report together, section by section. By the end we want a report that everyone recognises as accurate, plus a clear list of what is still open, with owners and dates.

---

## Slide 2 — Purpose of today

**On slide:**
1. Validate each section of the draft inception report
2. Agree the amendments proposed by participants
3. Take the decisions needed to approve D1 and start development
4. Give every open item an owner and a date

**Speaker notes:**
- **Why we validate in the meeting:** a document that has not been read cannot be approved. Going through it together means everyone has seen and confirmed the content.
- **What we will not do:** we won't rewrite text in the meeting. Agree the substance, and BITZ will update the wording.

---

## Slide 3 — How we will validate

**On slide:**
- **Every section ends with one outcome:** ✅ Validated · ✏️ Validated with amendments · ⏸ Not yet validated (owner and date)
- **Session 3 decisions (D-005 to D-018)** are not reopened unless someone has new information
- **Each section is time-boxed.** If an item can't be closed in its slot, it gets an owner and a date
- **Amendments** received by Monday are taken in the section they concern
- **Decisions** are recorded live and read back at the end

**Speaker notes:**
Confirm who can take decisions for UNICEF, the Ministry and Primero today. Confirm the note-taker. Explain that the validation tracker (slide 44) will be filled in as we go and shared with the minutes.

**Record:** decision-makers present for each organisation.

---

## Slide 4 — Agenda (follows the report)

**On slide:**

| Time | Report section | Slides |
|---|---|---|
| 0:00 | Opening and how we validate | 1–6 |
| 0:10 | 1 Executive summary | 7–10 |
| 0:20 | 2 Background and contract context | 11–13 |
| 0:30 | 3 Inception activities and findings | 14–17 |
| 0:45 | 4 Scope and boundaries | 18–19 |
| 0:55 | 5 Business requirements and workflow | 20–22 |
| 1:10 | 6 Proposed technical approach | 23–24 |
| 1:20 | 7 Data and safeguarding | 25–28 |
| 1:40 | *Break* | |
| 1:50 | 8 Implementation plan and timetable | 29–33 |
| 2:10 | 9 Governance and coordination | 34–35 |
| 2:20 | 10 Testing and acceptance | 36–38 |
| 2:30 | 11 Risks and outstanding decisions | 39–40 |
| 2:40 | 12 Approval and next steps; Annexes | 41–43 |
| 2:50 | Validation tracker, decision log, close | 44–46 |

**Speaker notes:**
If time runs short, protect sections 4, 5, 7 and 8. They hold the decisions that block development. Sections 9–12 can be finished by email if necessary.

---

## Slide 5 — The report at a glance

**On slide:**

| Section | What it covers |
|---|---|
| 1 Executive summary | Agreed requirements, open matters, decisions needed |
| 2 Background and contract | Context, objectives, signed contract items, discrepancies |
| 3 Inception activities | Consultations, how positions changed, limitations, new documents, requirement baseline |
| 4 Scope | What is in, out, extended or proposed; two-way updates |
| 5 Business workflow | Referral lifecycle and business rules |
| 6 Technical approach | Architecture, flow, error handling, environments |
| 7 Data and safeguarding | Data shared, Data Protection Act, controls, matters to confirm |
| 8 Implementation plan | Work plan, key dates, dependencies, proposed timetable |
| 9 Governance | Roles, RACI, approvals, meetings, escalation, change control |
| 10 Testing and acceptance | Test levels, user testing, fault rules, acceptance criteria, training |
| 11 Risks and decisions | Priority risks, decisions before design and before testing |
| 12 Approval and next steps | Approval record, immediate actions |
| Annexes A–K | Detailed requirements, API, mapping, workflow, registers, test scenarios, sources, design |

**Speaker notes:**
Main sections are validated in the meeting. Annexes are detailed reference material; participants confirm them by email (slide 43).

---

## Slide 6 — Amendments received

**On slide:** *(fill in before the meeting)*

| Section | Amendments received | From |
|---|---|---|
| 1 | | |
| 2 | | |
| … | | |
| Total | | |

**Speaker notes:**
Give a quick overview only: how many amendments, from whom, and which sections. Each one is discussed on that section's slide. Thank those who reviewed. Ask anyone who did not send amendments whether they have none, or whether they will raise points during the walk-through.

---

# Part 2 — Section-by-section validation

## Slide 7 — 1.1–1.3 Purpose, basis and agreed requirements *(Section 1)*

**On slide:**
- **Purpose:** this report is D1 (item 50) under contract 43427866, Amendment 3, signed 15 Sep 2026
- **Basis:** Sessions 1–3 minutes, the Session 3 action tracker, Primero's technical response, the annotated checklist, the Primero API, the signed contract, the 2019 SOP and the data-protection documents
- **Agreed requirements:**
  - Manual referral by the agent
  - Service selection, with the Ministry distributing the case
  - Two-way updates
  - Anonymous reporter, but identified child
  - Agreed field set with narrative at referral; case plan excluded
  - Optional ABR ID
  - Direct connection or OpenFN
  - Receipt kept separate from acceptance
  - User testing led by the Ministry
  - Global demonstration system as fallback

**Validate:**
- Is the list of sources complete? Is any document missing that should have informed the report?
- Do the agreed requirements match what was agreed in the sessions?

**Record:** section 1.1–1.3 outcome; any missing source and who provides it.

---

## Slide 8 — 1.4 Matters remaining open *(Section 1)*

**On slide:**
- Referrals during Primero downtime (A-021)
- Lesotho test-system readiness and access (A-015, A-016)
- National referral pathways (A-013); confirmation that the 2019 SOP is current (A-014)
- Data-protection basis: how the Act applies, hosting, processing contracts (A-017, A-022)
- CPIMS+ service list (A-018)
- Credentials for the unattended connection (API-002)
- Return-update mechanism and status values (RT-006, RT-007)
- Minimum information for emergency referrals (WF-004)
- Consent at referral (R-011)

**Validate:**
- Is this the complete list of open matters? Is anything missing?
- **Consent at referral:** the row currently reads "This is a call consent will be recorded by the agent this can be transferred to primero." Agree the correct wording.

**Gaps to close:** each matter is taken in detail later (the slide number is shown on the decision log).

**Record:** outcome; agreed consent wording.

---

## Slide 9 — 1.5–1.7 Approach, readiness and principal risks *(Section 1)*

**On slide:**
- **Approach:** a secure, authenticated connection that queues and retries undelivered referrals, prevents duplicates, logs each exchange, and keeps receipt, acceptance and progress separate
- **Readiness:** requirements are substantially defined. Blocked by no test-system access, no credentials, no field definitions and outstanding country documents
- **Principal risks:**
  - Access delay
  - Scope change (two-way updates)
  - Milestone slippage
  - Consent and lawful basis
  - Service-routing configuration

**Validate:**
- Does the readiness statement reflect the position today? Has anything been received since 30 October?
- Are these the right five principal risks?

**Record:** outcome; any change in readiness since 30 October.

---

## Slide 10 — 1.8–1.9 Decisions required and next steps *(Section 1)*

**On slide:** nine decisions, each taken later in the meeting:

| # | Decision | Taken on slide |
|---|---|---|
| 1 | Two-way updates and attachments: in scope or a variation | 19 |
| 2 | Dates governing milestones and the timetable | 32 |
| 3 | Named approvers | 41 |
| 4 | Consent or other lawful basis, and override authority | 28 |
| 5 | Minimum child-identification data and emergency exceptions | 21 |
| 6 | Direct connection or OpenFN | 23 |
| 7 | Global demonstration system as test evidence | 36 |
| 8 | Hosting, support access from abroad, data controllers | 28 |
| 9 | Which contract end date applies | 12 |

**Validate:** Is anything missing from this list of decisions?

**Speaker notes:** this slide only maps the decisions; don't take them here.

**Record:** section 1 overall outcome.

---

## Slide 11 — 2.1–2.6 Context, objectives and expected results *(Section 2)*

**On slide:**
- **Today:** there is no system link. The helpline sees only "referred" and "closed". Urgent cases are phoned to police or first responders.
- **Target:** referrals go through the Primero API, the Ministry distributes cases, and status and interventions are returned to the helpline. Urgent calls continue.
- **Roles:** OPENCHS (Child Helpline, maintained by BITZ) · CPIMS+ (Ministry; Primero) · integration service (BITZ)
- **Seven inception objectives:**
  - Lifecycle
  - Information set
  - ABR rules
  - Environments and security
  - Reliability
  - User-testing arrangements
  - Plan and registers
- **Expected results:**
  - D1 approved baseline
  - D2 ABR field, referral control and status display
  - D3 connection client
  - D4 testing, training, go-live and handover

**Validate:**
- Is the description of current practice accurate, especially for urgent cases?
- Are the system roles and owners correct?
- Are the intended outcomes (section 2.3) the right ones?

**Record:** outcome.

---

## Slide 12 — 2.7 Contractual scope *(Section 2)*

**On slide:**

| Item | Deliverable in the signed contract | Proposed date |
|---|---|---|
| 50 | Inception, requirements and environment setup (trip 1, Maseru) | Final D1 by 13 Nov 2026 |
| 60 | ABR ID field, validation rules and referral checkbox UI | 20 Nov 2026 |
| 70 | Outbound REST API client: JWT, retry logic, offline queue, idempotency, audit logging | 11 Dec 2026 |
| 80 | Testing, UAT, operator training and go-live (trip 2, Maseru) | Acceptance by 26 Feb 2027 |

- The contract describes each deliverable by title only and **states no due dates**
- Contract validity: Amendment 3 states three end dates (10 Jun, 7 Jul and 10 Jul 2027)
- Support after go-live for the integration is not specified

**Validate:**
- Is this an accurate summary of the signed contract?
- **Decision 9 (UNICEF):** which end date applies?
- How will support after go-live be arranged?

**Record:** outcome; end date or its owner and date; owner for support arrangements.

---

## Slide 13 — 2.8 Contractual discrepancies *(Section 2)*

**On slide:**
- **CD-01:** the contract item is outbound, but Session 3 agreed two-way updates
- **CD-02:** governing contract confirmed (resolved)
- **CD-03:** "referral checkbox" is read as the agent's explicit referral action, not a save trigger
- **CD-04:** D3 needs more than case creation: the referral operation, updates and attachments
- **CD-05:** ABR validation rules are required, but only the number structure has been supplied
- **CD-06:** the brief expected separate documents; this report combines them
- **CD-07:** the 14-week plan ended on 3 Jan 2027; the proposed timetable runs to 26 Feb 2027
- **CD-09:** the user-testing signatory is not named
- **CD-12:** proposed fault thresholds versus UNICEF's right to withhold payment
- **CD-15:** no due dates in the contract
- **CD-16:** three different end dates
- **CD-17:** a late-submission clause, but no due dates to measure it against

**Validate:**
- Are these discrepancies correctly stated? Are there others?
- Is the CD-03 reading of "referral checkbox" accepted?

**Gaps to close:** CD-01 is decided on slide 19, CD-15/17 on slide 32, CD-09 on slide 36, CD-16 on slide 12.

**Record:** outcome; CD-03 accepted or not.

---

## Slide 14 — 3.1–3.2 Approach and consultations *(Section 3)*

**On slide:**
- **Methods:**
  - Document review
  - Three facilitated sessions
  - OPENCHS walkthrough and CPIMS+ demonstration
  - Primero technical response
  - Decision consolidation
  - Action and risk registers
- **Consultations:**
  - 24 Sep inception meeting (no minutes)
  - 2 Oct written questions to Primero
  - 8 Oct Session 1
  - 9 Oct Session 2
  - 14 Oct technical call (no minutes)
  - 26 Oct Session 3
- **Attendee lists:** recorded only as the minutes and the Session 3 attendance export show them

**Validate (attendance):**
- **Session 3:** Tiisetso Mohlabi, Lucy Mosesane, Likeleli Ramolapong and Ramoletane Lekhanya are in the export but not the minutes. Confirm their roles.
- **Session 3:** who are "Daniel" (UNICEF) and Melusi (Ministry IT)? They are in the minutes but not in the export.
- **Session 3:** who was the Child Protection Services representative who spoke for the helpline?
- **Session 1:** did Mary Damposi and Silepo attend? What are their roles?
- **Sessions 1 and 2:** can the minutes now be finalised?

**Record:** confirmed names and roles; who sends corrections to the Session 1 and 2 minutes, and by when.

---

## Slide 15 — 3.3 How positions changed *(Section 3)*

**On slide:**

| Topic | Earlier | Now |
|---|---|---|
| Routing | Helpline refers directly to the district supervisor | Agent selects a service; the Ministry distributes (D-008) |
| Feedback | One-way follow-up | Two-way updates (D-007) |
| Anonymity | Anonymous reports can't be referred | Anonymous reporter allowed; child identified (D-010, D-011) |
| ABR ID | Optional; checks deferred | Optional; NICR format checks (D-005, D-014) |
| Attachments | Deferred | Included (D-012) |
| Narrative | Timing not stated | Required at referral, not first save (D-013) |
| UNICEF | Absent in Sessions 1–2 | Chaired Session 3 |

**Validate:** Is every "now" position correct? Session 3 governs where it updates an earlier position.

**Record:** outcome.

---

## Slide 16 — 3.4–3.5 Limitations and documents received after Session 3 *(Section 3)*

**On slide:**
- **Limitations:**
  - No minutes for 24 Sep and 14 Oct
  - Unified referral form not yet received
  - Annotated checklist has no author or date
  - No OPENCHS code audit performed
- **Received:**
  - 2019 SOP and Form 4 (referral form and return receipt)
  - Session 3 transcript and attendance export
  - Data Protection Act 2011
  - Draft Data Management Policy
- **Still outstanding:**
  - National pathways
  - Earlier Ministry data-protection work
  - Berea use cases
  - Service list

**Validate:**
- **Ministry:** is the 2019 SOP the current edition? Have there been amendments since? (A-014)
- Is Form 4 the "unified national referral form" referred to under A-004? If not, who sends that form?
- Who can supply minutes or notes of the 24 Sep and 14 Oct meetings, if any exist?

**Record:** outcome; SOP status; referral-form owner and date.

---

## Slide 17 — 3.6 Requirements baseline *(Section 3)*

**On slide:**
- **68 requirements:**
  - 26 Confirmed
  - 4 Contractual
  - 7 Proposed
  - 30 Pending Confirmation
  - 1 Dependency
- **Functional requirements (drive D2):** almost all confirmed
- **Most open items:** data mapping, integration and security, which depend on the configured Primero system and country documents
- **Priorities:** BITZ proposals, for confirmation

**Validate:**
- Are participants content that the full matrix (Annex A and Annex J) is reviewed by email (slide 43)?
- Any objection to the proposed priorities?

**Record:** outcome; Annex A/J review owners.

---

## Slide 18 — 4.1 Scope classification *(Section 4)*

**On slide:**
- **Contractual:**
  - Outbound referral client
  - ABR field and checks
  - Referral control and status display
  - Tokens, retry, queuing, duplicate prevention, audit
  - Testing, user testing, training, go-live
- **Confirmed during inception:**
  - Manual trigger
  - Service selection
  - Anonymous reporter
  - Field set and narrative rule
  - NICR ABR format
  - Two acknowledgements
  - API specification as basis
  - Global demonstration fallback
  - Ministry-led user testing
- **Extends the contract wording:**
  - Two-way updates
  - Attachments
  - Referral and follow-up operations beyond case creation
- **Excluded:** transfer of the helpline case plan
- **Proposed exclusions:**
  - Call recordings and large media
  - Advanced Primero lookup administration
  - Generic integration marketplace
  - Major OPENCHS redesign
  - Non-essential analytics
  - Automated deployment pipeline

**Validate:**
- Is anything missing from scope?
- Are the proposed exclusions acceptable? Confirm each one, or remove it from the exclusion list.

**Record:** outcome; each proposed exclusion accepted or rejected.

---

## Slide 19 — 4.2 Two-way integration — **Decision 1** *(Section 4)*

**On slide:**
- **Contract:** item 70 is an *outbound* client
- **Session 3 (D-007):** updates to referred cases flow back to the helpline
- **Implications:**
  - An inbound endpoint or polling
  - An agreed status vocabulary
  - Ordering and conflict handling
  - Reconciliation (Primero webhooks are not retried)
  - Returned-data minimisation
  - Extra tests
- **Options:**
  - (a) Absorbed within D3 and D4
  - (b) Contract amendment or variation
  - (c) Phased
- **Until decided:** BITZ designs for two-way updates but reports that work separately

**Validate and decide:**
- **Decision 1 (UNICEF, with the Ministry):** which option? What acceptance evidence applies?
- The same question applies to attachments (D-012).

**Record:** option chosen, or the decision owner and date.

---

## Slide 20 — 5 Referral lifecycle *(Section 5, Table 5.1)*

**On slide:**
1. The agent records the call and saves the case. The narrative need not be complete yet.
2. The agent decides to refer and selects a CPIMS+ service, optionally escalating to a supervisor first.
3. OPENCHS checks the narrative and child details. An anonymous reporter or a missing ABR ID is allowed.
4. The referral is sent and the system receipt is recorded.
5. The receiving party accepts or rejects it in CPIMS+.
6. The Ministry distributes and assigns the case internally.
7. Follow-up information goes to the linked case; status and interventions come back.
8. Closure, correction, cancellation and re-referral keep the link and history *(rules pending)*.

Urgent cases are still telephoned in parallel.

**Validate:**
- **Child Helpline and Ministry:** is this how referrals will work in practice? Walk through one real (anonymised) example.
- Is anything missing between steps?

**Record:** outcome.

---

## Slide 21 — 5.1 Business rules at referral — **Decision 5** *(Section 5, Table 5.2)*

**On slide:**

| Rule | Status |
|---|---|
| Agent starts the referral; saving never sends it | Confirmed |
| Narrative required at referral | Confirmed |
| Child identifying details required | Confirmed; fields pending |
| Anonymous reporter allowed | Confirmed |
| ABR ID optional, never blocks | Confirmed |
| **Minimum information for emergency referrals** | **Pending** |
| Parallel phone route for urgent cases | Confirmed |
| **Supervisor escalation rules** | **Pending** |

**Validate and decide:**
- **Decision 5 (Ministry and Child Helpline):** what is the minimum child-identification dataset, and what is allowed in an emergency?
- Is supervisor escalation always optional, or are there cases where it must happen?

**Record:** agreed minimum fields, or owner and date; escalation rule.

---

## Slide 22 — 5.2–5.3 Status tracking and pending business rules *(Section 5, Table 5.3)*

**On slide:**
- **Proposed helpline statuses:** Queued, Received, Accepted, Rejected, In progress, Completed, Withdrawn, Needs action
- **The helpline needs to see:** acceptance, service completion and closure, but *not* internal assignment
- **Pending:**
  - Partial referrals
  - Correction, cancellation and re-referral
  - Service list (A-018)
  - Routing configuration
  - Content of return updates

**Validate:**
- Are the proposed statuses the right ones for helpline staff?
- **Primero:** when will the service list be provided? Who receives each service?
- Who defines the rules for correction and cancellation?

**Record:** outcome; service list date; owners for each pending rule.

---

## Slide 23 — 6.1–6.3 Design principles, architecture and transaction flow — **Decision 6** *(Section 6)*

**On slide:**
- **Design principles:**
  - The agent chooses to send; saving never sends
  - No duplicate cases
  - Failed referrals are kept and visible
  - Only agreed information is shared
  - Exchanges are recorded without copying sensitive detail
- **Architecture:** OPENCHS → CPIMS+ (Ministry distributes) → updates return to OPENCHS
- **Connection:** direct, or through OpenFN. X-Road is only for Home Affairs ABR checks.
- **Transaction flow:**
  1. The agent selects the service
  2. OPENCHS checks the required information
  3. The referral is sent securely
  4. The system receipt is recorded
  5. A person accepts or rejects it
  6. Updates return

**Validate and decide:**
- **Decision 6 (Ministry IT, with Primero):** direct connection or OpenFN?
- Do the design principles match what participants expect?

**Record:** decision 6 outcome, or owner and date.

---

## Slide 24 — 6.4–6.7 Error handling, responsibilities, environments and reliability *(Section 6)*

**On slide:**
- **Failed deliveries:** queued and retried automatically; staff see failures and can correct the information
- **Proposed retries:** after 1 minute, 5 minutes, 30 minutes and 2 hours
- **Responsibilities:**
  - BITZ: helpline form, delivery and duplicate prevention
  - Primero and Ministry: services, recipients and permissions
  - Both technical teams: how updates return
  - Named owners: monitoring
- **Environments:**
  - BITZ development system
  - OPENCHS test system
  - Lesotho CPIMS+ test system (preferred)
  - Global demonstration system (fallback)
  - Production

**Validate:**
- Are the proposed retry intervals and the alerting approach acceptable?
- **Primero:** what happens when CPIMS+ is down? (A-021)
- Who monitors failures and responds to incidents once the system is live?

**Record:** outcome; A-021 owner and date; monitoring owner.

---

## Slide 25 — 7.1 and 7.4 Information shared and its sensitivity *(Section 7)*

**On slide:**

| Data | Direction | Sensitivity |
|---|---|---|
| Child identity, location, contact | OPENCHS → CPIMS+ | High; child's information under the Act |
| Narrative, category, perpetrator details | OPENCHS → CPIMS+ | High; sensitive under the Act |
| Reporter contact | OPENCHS → CPIMS+ when given | High; anonymity respected |
| Attachments | OPENCHS → CPIMS+ | High |
| ABR ID | OPENCHS → CPIMS+ when available | High |
| Status and interventions | CPIMS+ → OPENCHS | High |
| Records of exchanges | Both | Medium |
| Helpline case plan | Not transferred | — |

**Validate:**
- Is the information set correct and complete?
- Is the sensitivity classification acceptable to the Ministry?

**Record:** outcome.

---

## Slide 26 — 7.2 Legal and policy position *(Section 7)*

**On slide:**
- **Data Protection Act, 2011 (Act No. 5 of 2012):** the 2011 and 2012 references are the same Act
- **Data Protection Commission:** not yet established
- **Key provisions:**
  - Child and sensitive information (ss. 29, 34, 36)
  - Lawful grounds (s. 15)
  - Minimal information (s. 16)
  - Retention (s. 19)
  - Security (s. 20)
  - Processing contracts (ss. 21–22)
  - Breach notification (s. 23)
  - Notifying the Commission (ss. 25, 53)
  - Transfers outside Lesotho (s. 52)
  - Offences (s. 55)
- **Draft Data Management Policy:**
  - Government data centres
  - Lesotho law for cross-border data
  - Data classification
  - Security documentation
- **Signed contract:** data belongs to UNICEF and government ministries
- **Note:** this is BITZ's planning reading, not a legal opinion

**Validate:**
- **Ministry and UNICEF:** is this the current law? Are there regulations, codes of conduct or child-protection laws that also apply?
- Who in the Ministry will confirm how the Act applies?

**Record:** outcome; named legal or data-protection contact.

---

## Slide 27 — 7.3 Security controls *(Section 7)*

**On slide:**
- **Confirmed or proposed:**
  - Anonymous reporter preserved
  - Only agreed fields sent
  - Limited integration permissions
  - Encrypted transport (TLS 1.2+ proposed)
  - Fictional test data only
  - Case plan excluded
- **Pending:**
  - Lawful basis
  - Consent and override
  - Credentials
  - Log access and retention
  - Retention periods
  - Incident handling and breach notification
  - Attachment rules
  - Return-update channel
  - Processing contracts
  - Hosting and transfers
  - Notifying the Commission

**Validate:** Is the list of controls complete? Is anything missing for the Ministry's security requirements?

**Record:** outcome.

---

## Slide 28 — 7.5 Matters for confirmation — **Decisions 4 and 8** *(Section 7)*

**On slide:**
1. Status of the Act, regulations and related child-protection law
2. Lawful basis for each direction of exchange
3. **Consent capture and override authority (decision 4)**
4. Retention periods
5. Incident notification contacts
6. Approval of fictional test records
7. Named data-protection approver
8. Data controllers and processing contracts
9. **Hosting location and support access from outside Lesotho (decision 8)**
10. How the Commission is notified while it doesn't exist
11. National data classification policy (UNICEF to supply)
- Plus: data-sharing agreements needed before real case data is exchanged

**Validate and decide:**
- Take decisions 4 and 8 if the right people are present. Otherwise assign an owner and date to each of the 11 items.
- **UNICEF:** when will the earlier Ministry data-protection work (rest of A-017) and the classification policy be shared?

**Record:** an owner and date for each item; decisions 4 and 8.

---

# Break (10 minutes)

---

## Slide 29 — 8.1–8.2 Work plan *(Section 8)*

**On slide:** twelve phases, each mapped to a deliverable:
1. Requirements confirmation (D1)
2. Detailed solution design (D1/D3)
3. Environment preparation (D1)
4. OPENCHS development (D2)
5. API integration (D3)
6. Security and functional testing (D3/D4)
7. Integration testing (D4)
8. User testing (D4)
9. Training and knowledge transfer (D4)
10. Deployment preparation (D4)
11. Go-live support (D4)
12. Handover (D4)

**Validate:** Are the phases, owners and completion criteria in Table 8.1 acceptable?

**Record:** outcome.

---

## Slide 30 — 8.3–8.4 Key dates and current status *(Section 8)*

**On slide:**
- 15 Sep 2026: Amendment 3 signed
- 24 Sep: inception meeting
- 8–9 Oct: Sessions 1 and 2
- 26 Oct: Session 3
- 30 Oct: draft circulated
- 2 Nov: amendments due
- 3 Nov: today

**Status at 30 Oct:**

| Deliverable | Status |
|---|---|
| D1 | In review |
| D2 | No build evidence yet |
| D3 | Blocked on access, credentials and field names |
| D4 | Not started |

**Validate:** Are the key dates and the status correct?

**Record:** outcome.

---

## Slide 31 — 8.5–8.6 Dependencies and work that can proceed *(Section 8)*

**On slide:**

| Input needed before development | Position |
|---|---|
| Test-system credentials and base URL | Expected about a week after 9 Oct; due 28 Oct (A-016); not received |
| ABR specification (check-digit, examples) | Number structure only |
| Aligned protection-concern list (Primero) | Not yet supplied |
| Primero field names | After test-system set-up |

- **Can proceed now:**
  - D2 build
  - D3 against a simulation
  - Test design
  - Training outline

**Validate:**
- Is the position of each input correct?
- **Primero:** when will each input be delivered?

**Record:** a date and owner for each input.

---

## Slide 32 — 8.7 Proposed timetable — **Decision 2** *(Section 8)*

**On slide:**

| Date | Milestone |
|---|---|
| Fri 6 Nov | Updated draft circulated |
| **Fri 13 Nov** | **G1: final D1 · G2: test-system access, credentials, field names, service list** |
| Fri 20 Nov | D2 evidence (item 60) |
| Fri 11 Dec | D3 evidence (item 70) — G3 |
| 14–18 Dec | Component tests |
| 21 Dec – 8 Jan | Contingency |
| 11–22 Jan | Integration testing — G4 |
| 25–29 Jan | User testing |
| Fri 5 Feb | User-testing sign-off — G5 |
| 8–12 Feb | Go-live |
| 15–19 Feb | Training in Maseru; handover pack |
| Fri 26 Feb | D4 acceptance (item 80) |

*Show Figure 7 (Gantt chart) alongside: `D1_FIGURE_7_PROPOSED_TIMETABLE.png`*

**Validate and decide:**
- **Decision 2 (UNICEF and governance):** approve this timetable as the baseline for submissions and for the late-submission clause?
- **Primero and UNICEF:** can G2 (13 Nov) be met? If not, what date? Every later date moves with it.
- Are five working days acceptable for UNICEF review?

**Record:** timetable approved (with any changes); committed G2 date and owner.

---

## Slide 33 — 8.8 Decisions to approve the schedule *(Section 8)*

**On slide:**
- Applicable contract end date
- Timetable as the baseline
- Two-way scope and "checkbox" wording
- Timetable replaces the 14-week plan; G2 date
- Access, fields, ABR rules and data-sharing evidence before real data
- User-testing signatory
- Global demonstration system as evidence
- February travel, training languages and support after go-live

**Validate:** Mark each as taken (with the slide number) or still open. Confirm February travel dates and the training languages (English and Sesotho).

**Record:** outcome; trip 2 dates and languages.

---

## Slide 34 — 9.1–9.2 Roles and RACI *(Section 9)*

**On slide:**
- **UNICEF:** contracting party; pathways, checklist, privacy material, X-Road invitation
- **Ministry IT:** host and coordination, SOPs, Berea use cases, helpline cover
- **Ministry child protection:** CPIMS focal person
- **Child Helpline:** workflow users, user testers, focal person
- **Primero:** test system, service list, credentials, field definitions
- **BITZ:** project management, development, integration, report

**Validate:**
- Is each organisation's role correctly described? Does anyone disagree with their RACI entries in Table 9.2?
- Who is the permanent Child Helpline focal person, and who covers during leave (A-024)?

**Record:** outcome; focal person and cover.

---

## Slide 35 — 9.3–9.7 Approvals, meetings, escalation and change control *(Section 9)*

**On slide:**
- **Approvals needed:**
  - Requirements
  - Technical design
  - Data protection
  - User-testing result
  - Contract or schedule change
  - Go-live
- **Proposed meetings:** weekly progress meeting, minutes within 24 hours, monthly report
- **Deliverables:** submitted with reports in the contract's standard format
- **Escalation:** issue owner → BITZ project manager → technical session → UNICEF and Ministry owners
- **Change control:** raise → assess → review → decide in writing → update the documents
- **Change log:**
  - CR-01 two-way updates
  - CR-02 attachments
  - CR-03 schedule rebaseline
  - CR-04 checkbox wording

**Validate and agree:**
- The weekly meeting day, time and attendees
- The escalation path and change procedure
- Confirm the change log

**Record:** weekly slot; escalation contacts; outcome.

---

## Slide 36 — 10.1–10.2 Test levels and user testing — **Decision 7** *(Section 10)*

**On slide:**
- **Test levels:**
  - Individual features
  - Simulation
  - Both systems together
  - Protection of information
  - Existing services (regression)
  - Testing by users
- **User testing:**
  - Led by the Ministry (D-009)
  - Participants: helpline agents, Ministry users, district supervisors, system administrator
  - UNICEF and Primero proposed to join
  - Fictional test data only
  - Scenarios in Annex H
- **Sign-off:** the signatory is not yet named

**Validate and decide:**
- **Decision 7 (UNICEF, with Primero):** is testing on the global demonstration system acceptable evidence, or must January testing use the Lesotho test system?
- **Who signs user testing?** How is Ministry endorsement recorded? (CD-09)
- Do UNICEF and the Primero team join the user-testing group?
- Who approves the fictional test data?

**Record:** decision 7; named signatory; test-data approver.

---

## Slide 37 — 10.3–10.4 Fault rules and acceptance criteria *(Section 10)*

**On slide:**
- **Fault rules:**
  - No open Critical faults
  - No open High faults unless waived in writing
  - Medium faults need a fix plan
  - Low faults are tracked
- **Proposed criteria:**
  - All "Must" scenarios executed
  - Zero duplicate cases
  - No referrals lost in an outage test
  - Every exchange audited
  - No secrets in logs
  - All validation rules pass
  - No High regression faults
- **Pending:** a timeliness target for return updates
- **Contract:** UNICEF may withhold payment where work is unsatisfactory or incomplete

**Validate:** Are the fault rules and thresholds acceptable to UNICEF and the Ministry? (CD-12, UAT-007)

**Record:** outcome; any change to the thresholds.

---

## Slide 38 — 10.5–10.7 Training, handover and D1 readiness *(Section 10)*

**On slide:**
- **Training:**
  - Operators and social workers: ABR field, referral, status, failures
  - IT staff: architecture, configuration, monitoring, troubleshooting
- **Handover:**
  - Technical report
  - Architecture and configuration guide
  - Mapping reference
  - Audit log guide
  - User manuals
  - Administrator guide
- **D1 readiness:** documents prepared; formal acceptance not yet given. Outstanding:
  - Mapping evidence
  - Environment evidence
  - Approvals

**Validate:**
- Is the training audience correct? How many operators and IT staff will attend?
- What does UNICEF need to see to accept D1 (item 50)?

**Record:** outcome; D1 acceptance evidence agreed.

---

## Slide 39 — 11.1–11.3 Risks *(Section 11)*

**On slide:**

| Risk | What reduces it |
|---|---|
| R-001 Access delay | G2 commitment (slide 32) |
| R-002 Country documents | Action dates (slide 42) |
| R-003 Service routing | Service list (slide 22) |
| R-007 Privacy and approvals | Data-protection owners (slide 28) |
| R-009 Milestone slippage | Agreed timetable (slide 32) |
| R-010 Scope change | Decision 1 (slide 19) |
| R-014 Approvers not named | Slide 41 |
| R-017 Hosting and transfers | Decision 8 (slide 28) |

- **Medium:**
  - R-004 outages and duplicates
  - R-006 two-way design
  - R-011 consent
  - R-012 Primero go-live
  - R-013 authentication
  - R-016 test environment

**Validate:**
- Do participants agree with the likelihood and impact ratings?
- Is any risk missing? Does each risk have the right owner?

**Record:** outcome; new risks and owners.

---

## Slide 40 — 11.4–11.5 Decisions before design and before integration testing *(Section 11)*

**On slide:**
- **Before design:**
  - Minimum child dataset
  - Consent approach
  - Credentials and token renewal
  - Sequence design and service routing
  - Duplicate-prevention key
  - Return-update mechanism
  - Direct connection or OpenFN
  - Hosting and data controllers
- **Before integration testing:**
  - Lesotho environment or accepted fallback
  - Behaviour when Primero is down
  - Approved test data
  - Fault and go-live rules

**Validate:** Tick off the items already decided today. Every remaining item gets an owner and a date before 13 Nov (G2).

**Record:** status of each item.

---

## Slide 41 — 12.1 Approval record — **Decision 3** *(Section 12)*

**On slide:** names needed:

| Role | Name |
|---|---|
| Ministry business owner | |
| UNICEF programme / governance owner | |
| OPENCHS technical authority | |
| Primero technical authority | |
| Data protection / security authority | |
| User-testing signatory | |
| Ministry user-testing endorsement | |

**Validate and decide:** **Decision 3 (UNICEF and Ministry):** name each approver today, or confirm them by Fri 6 Nov.

**Record:** names, or the owner and date for confirming them.

---

## Slide 42 — 12.2 Immediate actions *(Section 12)*

**On slide:**

| Action | Owner | Status | New date |
|---|---|---|---|
| A-013 National referral pathways | Rantsala | Overdue | |
| A-015 Test-system checklist | Rantsala / Isaiah | Overdue | |
| A-016 Test-system or global demonstration system access | Isaiah | Pending | |
| A-017 Earlier Ministry data-protection work | Lekhanya | Partly received | |
| A-018 CPIMS+ service list | Isaiah | Pending | |
| A-020 Berea X-Road use cases | Melusi | Overdue | |
| A-021 Handling referrals during outages | Nelson / Peter / Isaiah | Pending | |
| A-022 Data-protection desk research | Nelson | In progress | |
| A-024 Helpline leave cover | Hopolang | Not confirmed | |
| A-014 Confirm 2019 SOP is current | Hopolang / Ministry | Received; confirmation pending | |
| P-03 Confirm UNICEF action owners | UNICEF | To agree | |

**Validate:** each owner confirms the status and gives a new date. The note-taker fills in the last column live.

**Record:** a new date for each action, or "closed" with the evidence.

---

## Slide 43 — Annexes A–K *(validated by email)*

**On slide:**

| Annex | Content | Reviewer | By |
|---|---|---|---|
| A | Detailed requirements matrix | All | |
| B | API operations and authentication | Primero; BITZ | |
| C | Field mapping and data dictionary status | Primero; Ministry | |
| D | Referral workflow, sequence and status vocabulary | Ministry; Child Helpline; Primero | |
| E | Decision register | All | |
| F | Action register | All | |
| G | Detailed risk register | All | |
| H | User-testing scenario matrix | Ministry; Child Helpline | |
| I | Sources and references | BITZ | |
| J | Categorised requirement baseline | All | |
| K | Detailed connection design and security | Primero; Ministry IT | |

**Validate:** agree a reviewer and a date for each annex. Suggest Thu 5 Nov, so that comments can be included in the 6 Nov draft.

**Record:** a reviewer and date for each annex.

---

# Part 3 — Close

## Slide 44 — Validation tracker *(completed live)*

**On slide:**

| Report section | Outcome (✅ / ✏️ / ⏸) | Amendments agreed | Open points (owner, date) |
|---|---|---|---|
| 1 Executive summary | | | |
| 2 Background and contract | | | |
| 3 Inception activities and findings | | | |
| 4 Scope and boundaries | | | |
| 5 Business requirements and workflow | | | |
| 6 Proposed technical approach | | | |
| 7 Data and safeguarding | | | |
| 8 Implementation plan | | | |
| 9 Governance and coordination | | | |
| 10 Testing and acceptance | | | |
| 11 Risks and outstanding decisions | | | |
| 12 Approval and next steps | | | |
| Annexes A–K | By email | | Reviewers and dates (slide 43) |

**Speaker notes:** read the tracker back. Every ⏸ must have an owner and date.

---

## Slide 45 — Decision log *(completed live)*

**On slide:**

| # | Decision | Outcome | Owner | Date |
|---|---|---|---|---|
| 1 | Two-way updates and attachments | | | |
| 2 | Timetable baseline and G2 date | | | |
| 3 | Named approvers | | | |
| 4 | Consent and lawful basis | | | |
| 5 | Minimum child-identification data | | | |
| 6 | Direct connection or OpenFN | | | |
| 7 | Test environment as evidence | | | |
| 8 | Hosting, data controllers, processing contracts | | | |
| 9 | Contract end date | | | |
| — | Consent wording in section 1.4 | | | |
| — | CD-03 checkbox reading | | | |
| — | Proposed scope exclusions | | | |
| — | User-testing signatory | | | |

**Speaker notes:** ask each decision owner to confirm the outcome as recorded.

---

## Slide 46 — Next steps

**On slide:**
- **Within 24 hours:** minutes, validation tracker and decision log circulated
- **Thu 5 Nov:** annex comments due
- **Fri 6 Nov:** updated draft circulated with the agreed amendments; decisions confirmed in writing
- **Fri 13 Nov:** final D1 submitted (G1); test-system access, credentials, field names and service list supplied (G2)
- **Fri 20 Nov:** D2 evidence
- **Weekly progress meeting:** starts *(agreed date)*

**Speaker notes:** thank participants. Remind them that the report can be approved only once the ⏸ items are closed or accepted as conditions with owners and dates.

---

## Facilitator checklist (not a slide)

**Before the meeting:**
- Fill in slide 6 and add each amendment to the section slide it concerns
- Prepare proposed wording for the consent row in section 1.4 (slide 8)
- Confirm that decision-makers from UNICEF, the Ministry and Primero will attend
- Insert `D1_FIGURE_7_PROPOSED_TIMETABLE.png` into slide 32
- Prepare the validation tracker and decision log for live completion

**For the next version of the report (noted during preparation):**
- The 12.2 actions table and the 6.6 environment status are dated 28 October; update them with today's outcomes

**After the meeting:**
- Circulate the minutes, validation tracker and decision log within 24 hours
- Update the report (new version), the action tracker, the completion inventory and the delivery plan

**Parking lot:**

| Item | Raised by | Owner | Date |
|---|---|---|---|
| | | | |
