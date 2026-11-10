# OpenCHS–Primero CPIMS+ Integration

**Subsequent evidence note added 26 October 2026:** The session record below is historical. See [D1 v0.4](../../01_inception/DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO.md) and [Isaiah’s response](../../06_correspondence/ISAIAH_RESPONSE_SOURCE_2026-10-26.md) for later API, environment and ownership evidence. Session 2 revises direct-routing assumptions; this note does not rewrite what was discussed in Session 1.
## Meeting Session 1 — Draft Report

**Project:** Lesotho Child Helpline 116 / OpenCHS integration with Primero CPIMS+  
**Meeting:** First meeting, Session 1  
**Date:** To be confirmed  
**Location / platform:** To be confirmed  
**Report status:** Draft for review and correction  

> This report records the notes captured during Session 1. Items marked **Pending**, **To confirm**, or **Proposed** must not be treated as final requirements until the responsible stakeholders approve them.

## 1. Meeting purpose

The session introduced the Child Helpline and discussed the proposed referral workflow between OpenCHS and Primero CPIMS+, including referral initiation, ABR ID information, mandatory data, automatic referrals, closed-loop feedback, sandbox readiness, routing, and UAT participation.

The project remains aligned to the overall **14-week implementation baseline**, with the first two weeks treated as elapsed and twelve weeks remaining. The detailed schedule and implementation dependencies still require confirmation against the meeting decisions.

## 2. Participants and attendance

The following participants were recorded:

| Name | Designation | Department |
|---|---|---|
| Hopolang Mosena | PC Support Technician | IT |
| Masebatane Lebuso | Social Worker | CHL |
| Mamokoli Sekantsi | Social Worker | CHL |
| Tampose Mapetja | CHL Supervisor | CHL |
| Mamotlatsi Phakisi | Social Worker | Child Protection Services |
| Mokete Mothae | Social Worker | CHL |
| Lerato Ramochele | Auxilliary Social Worker | Maseru District |
| Mapaballo Thaha | Social Worker | Maseru District |
| Likeleli Ramolapong | Research Analyst | IT |
| Hape Nkakole | Social Development Officer (Social Worker Supervisor) | Maseru District |
| Tiisetso Mohlabi | Programs Office | MGYSD |
| Nelson Adagi | Project Manager | BITZ |
| Peter Rogendo | Developer | BITZ |
| Marlon Amunga | Developer | BITZ |
| Isiah Ososti | Primero | UNICEF |

The UNICEF Country Representative was not represented in the meeting. The requirement for their participation or approval must be confirmed.

The supplied participant list has been added. The name of the Child Helpline focal person responsible for the project/integration activities remains to be confirmed.

## 3. Presentations and materials

- Peter presented an overview of the Child Helpline and demonstrated the case form to help the team understand its structure and use.
- A checklist has been provided to the UNICEF Lesotho team.
- Isiah indicated that the UNICEF Lesotho team needs to complete the checklist before the Primero sandbox can be set up. This was identified as a potential project delay.
- The checklist covers sandbox/demo setup, API requirements, and required technical documentation.
- The demo/sandbox environment is expected to be set up within one week, subject to the required access, credentials, API information, and documentation being provided.

## 4. Key discussion points and agreed direction

### 4.1 Referral workflow and SOP

- The referral process will support referrals from the Child Helpline to CPIMS+/MGYSD and other approved stakeholders.
- Tiisetso will share the hard-copy referral workflow/process.
- Ostosti will share the referral form so that the team can determine the required information, workflow, and system fields.
- The team will develop or update the SOP to include the relevant stakeholders and role-holders, not only the initial referral recipient.
- The exact person or role authorised to trigger or approve a referral remains to be confirmed.

### 4.2 Emergency response and data minimisation

- The Child Helpline operates in an emergency-response context.
- Child Helpline operators should not be required to capture every detail from the reporting person before making an urgent referral.
- The referral form should distinguish between:
  - minimum information needed for immediate referral; and
  - additional information that may be collected later by the social-work or case-management team.
- The integration should support incomplete or partial referrals while recording missing information for follow-up.

### 4.3 Mandatory information and perpetrator details

- The supervisor indicated that perpetrator information is important and should be considered a mandatory or priority field.
- The exact perpetrator fields, requiredness, handling of unknown information, and safeguarding considerations remain to be defined.

### 4.4 ABR ID

- ABR ID was discussed as a unique identifier, potentially linked to the birth registration number.
- A referral may need to be submitted with the ABR ID blank when the identifier is unavailable.
- MGYSD facilitates cases where the ABR ID is missing.
- Meh Hopolang will identify the organisation responsible for issuing ABR IDs, possibly Home Affairs, and confirm the validation process.
- The ABR ID issuing authority, official definition, format, validation rules, and whether it is mandatory or conditionally required remain pending.

### 4.5 Automatic referral trigger

- It was agreed in principle that the agent should trigger the referral rather than relying on a separate manual referral action.
- The referral should be triggered when an approved category or rule is selected.
- The term “agent” must be clarified: it may refer to the Child Helpline case-handling agent, an automated system agent, or both.
- The triggering categories, validation rules, exceptions, user notification, and any approval requirement remain to be documented.

### 4.6 Closed-loop referrals and feedback

- Participants agreed that the referral process should support a closed loop.
- CPIMS+/MGYSD should provide feedback or status updates to the Child Helpline after referral.
- The feedback should show what happened to the referred case, subject to appropriate privacy and access controls.
- The team must define the feedback statuses, update mechanism, responsible owner, and whether updates are one-way or synchronised between systems.

### 4.7 Referral routing and ownership

- CPIMS+ stakeholders must agree who will receive referrals.
- The Ministry will take ownership of received referrals and may manually distribute them to the appropriate teams or stakeholders.
- District supervisors should receive cases relating to their respective districts.
- The Child Helpline should be able to refer cases to different approved stakeholders, rather than only to one recipient.
- The final routing model may combine automatic category-based routing with manual Ministry distribution.

## 5. UAT participation and approach

The following participants or groups were identified for UAT:

- OpenCHS/development team.
- Child Helpline agents.
- Ministry-side system administrator.
- Ministry/CPIMS+ users and representatives.
- Relevant district supervisors.
- Other Ministry users who receive, distribute, investigate, or close referrals.

UAT should be led or primarily performed by Ministry users because the Ministry will receive, manage, distribute, and provide feedback on referrals. The Child Helpline and technical teams should participate to verify referral initiation, system behaviour, integration evidence, and user access.

UAT should include at least:

- automatic referral triggered by an approved category;
- referral with an available ABR ID;
- referral where the ABR ID is missing;
- minimum-information emergency referral;
- perpetrator information handling;
- routing to the Ministry and district-specific handling;
- manual distribution by Ministry users;
- feedback/status update to the Child Helpline;
- incomplete or rejected referral handling; and
- audit and access-control verification.

## 6. Decisions and agreements recorded

| ID | Decision/agreement | Status |
|---|---|---|
| D-001 | The project should support referrals from the Child Helpline to CPIMS+/MGYSD and other approved stakeholders. | Agreed in principle |
| D-002 | The SOP should cover the broader referral ecosystem and relevant role-holders. | Agreed in principle |
| D-003 | Child Helpline emergency referrals should not require every detail to be captured before referral. | Agreed direction |
| D-004 | Perpetrator information is important and must be assessed as a mandatory/priority field. | Pending field definition |
| D-005 | ABR ID may be blank where unavailable, subject to the approved Ministry process. | Pending formal rule |
| D-006 | The agent/category rule should trigger the referral instead of a separate manual referral action. | Agreed in principle; terminology and rules pending |
| D-007 | The referral workflow should support closed-loop feedback. | Agreed in principle |
| D-008 | The Ministry will receive and may manually distribute referrals. | Agreed direction; routing details pending |
| D-009 | UAT should include Ministry users, Child Helpline agents, technical teams, and relevant district supervisors. | Agreed direction |

## 7. Action register

| ID | Action | Owner | Due/status |
|---|---|---|---|
| A-001 | Provide the complete list of participants in the room. | Meh Hopolang | Completed — participant list added |
| A-002 | Provide the name of the Child Helpline focal person responsible for the project/integration. | Meh Hopolang | Pending |
| A-003 | Share the hard-copy referral workflow/process. | Tiisetso | Pending |
| A-004 | Share the referral form for review. | Ostosti | Pending |
| A-005 | Review the referral form and identify minimum, mandatory, optional, and follow-up fields. | Project team | Pending form receipt |
| A-006 | Develop/update the SOP to cover Child Helpline, Ministry, CPIMS+, social teams, district supervisors, and other approved stakeholders. | Project team | Pending workflow confirmation |
| A-007 | Identify the organisation that issues ABR IDs and confirm the validation process. | Meh Hopolang | Pending |
| A-008 | Confirm ABR ID format, ownership, mandatory/optional rule, and missing-ID process. | MGYSD / relevant authority | Pending |
| A-009 | Agree the CPIMS+ recipients and referral-routing rules. | Ministry/CPIMS+ stakeholders | Pending |
| A-010 | Define the closed-loop feedback statuses and update mechanism. | Ministry/CPIMS+ and Child Helpline teams | Pending |
| A-011 | Set up the demo/sandbox environment and provide API/documentation access. | UNICEF Lesotho / technical teams | Expected within one week |
| A-012 | Confirm UAT participants, test data, scenarios, and sign-off authority. | Ministry, Child Helpline, and technical teams | Pending |
| A-013 | Confirm whether UNICEF Country Representative participation or approval is required. | UNICEF/project governance | Pending |

## 8. Open questions and risks

1. Who is the final authorised Child Helpline role or system agent that triggers a referral?
2. Which categories automatically trigger referrals?
3. Is a supervisor approval required in any referral scenario?
4. Which fields are mandatory for an emergency referral?
5. How should missing or unknown perpetrator information be recorded safely?
6. Who issues and validates the ABR ID?
7. What happens when an ABR ID is unavailable or later becomes available?
8. Who receives each referral category in CPIMS+/MGYSD?
9. How are district-specific referrals routed?
10. What feedback/statuses will CPIMS+ send back to the Child Helpline?
11. Is feedback sent automatically, manually, or through a combined process?
12. What API documentation, credentials, sample payloads, and sandbox access will be available within the one-week setup period?
13. Who has authority to approve UAT and the eventual go-live decision?

## 9. Proposed next steps

1. Confirm the Child Helpline focal-person name, referral form, and hard-copy workflow.
2. Confirm the ABR ID issuing authority and missing-ID process.
3. Agree the minimum emergency referral dataset and the additional investigation dataset.
4. Confirm referral categories, automatic triggers, recipient routing, and Ministry distribution responsibilities.
5. Draft the end-to-end SOP and circulate it for Child Helpline, Ministry, CPIMS+, and UNICEF review.
6. Confirm sandbox/API/documentation readiness within one week.
7. Prepare Ministry-led UAT scenarios, including closed-loop feedback and district routing.
8. Update the 14-week implementation plan with the confirmed decisions, owners, dependencies, and remaining twelve-week schedule.

## 10. Validation

This is a draft report prepared from live meeting notes. Participants should correct names, roles, terminology, decisions, and action ownership before the report is approved as the official Session 1 record.

**Prepared by:** ____________________  
**Reviewed by:** ____________________  
**Approved by:** ____________________  
**Approval date:** ____________________

