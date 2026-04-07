# Data Classification Policy Template

A comprehensive data classification framework for organizations that need to categorize, label, and protect information based on sensitivity. This template includes four classification levels (Public, Internal, Confidential, Restricted), detailed handling procedures for each level, labeling standards, a CUI (Controlled Unclassified Information) marking guide, and role definitions for data ownership.

Designed for compliance with NIST SP 800-171, CMMC, HIPAA, SOC 2, PCI DSS, ISO 27001, and GDPR requirements.

## Table of Contents

- [How to Use This Template](#how-to-use-this-template)
- [Classification Levels](#classification-levels)
- [Classification Decision Tree](#classification-decision-tree)
- [Handling Requirements by Level](#handling-requirements-by-level)
- [Labeling and Marking Standards](#labeling-and-marking-standards)
- [CUI Marking Guide](#cui-marking-guide)
- [Roles and Responsibilities](#roles-and-responsibilities)
- [Data Lifecycle Management](#data-lifecycle-management)
- [Compliance Mapping](#compliance-mapping)
- [Implementation Checklist](#implementation-checklist)

---

## How to Use This Template

1. **Review and customize** the classification levels for your organization (most organizations can use these four levels as-is)
2. **Replace all `[PLACEHOLDER]` values** with your organization's specifics
3. **Adapt handling requirements** to match your actual tools and processes
4. **Train all employees** on the classification framework before rollout
5. **Assign data owners** to existing data repositories
6. **Begin classifying** starting with your highest-risk data
7. **Review annually** and update as regulations or business needs change

---

## Classification Levels

### Level 1: Public

**Definition:** Information explicitly approved for public release that poses no risk to the organization if disclosed.

**Examples:**
- Published marketing materials and press releases
- Public website content
- Published job postings
- Open-source code released under approved licenses
- Annual reports (after publication)

**Impact of Unauthorized Disclosure:** None. This information is intended for public consumption.

### Level 2: Internal

**Definition:** Information intended for general use within the organization. Not sensitive, but not intended for public distribution.

**Examples:**
- Internal policies and procedures (non-security)
- Organization charts
- Internal newsletters and announcements
- Non-sensitive meeting notes
- General training materials
- Internal phone directories

**Impact of Unauthorized Disclosure:** Minimal. May cause minor embarrassment or inconvenience but no material harm to the organization.

### Level 3: Confidential

**Definition:** Sensitive information that could cause material harm to the organization, its employees, customers, or partners if disclosed to unauthorized parties.

**Examples:**
- Personally Identifiable Information (PII): names, SSNs, addresses, dates of birth
- Protected Health Information (PHI) under HIPAA
- Customer lists and pricing
- Financial records and projections
- Employee performance reviews and compensation data
- Contracts and legal agreements
- Security policies and architecture documents
- Intellectual property not yet filed or published
- Audit and assessment results

**Impact of Unauthorized Disclosure:** Significant. May result in regulatory penalties, legal liability, competitive disadvantage, or reputational damage.

### Level 4: Restricted

**Definition:** The most sensitive information whose disclosure could cause severe harm to the organization, national security, or individuals.

**Examples:**
- Controlled Unclassified Information (CUI) and Covered Defense Information (CDI)
- Encryption keys and root certificates
- Authentication credentials and secrets
- Trade secrets and proprietary algorithms
- Merger and acquisition data (pre-announcement)
- Active legal hold materials
- Incident investigation details (during active investigation)
- Board-level strategic plans
- SCIF or classified spillage materials

**Impact of Unauthorized Disclosure:** Severe. May result in major regulatory action, criminal liability, loss of government contracts, significant financial loss, or harm to national security.

---

## Classification Decision Tree

Use this flowchart to classify data:

```
Is the information approved for public release?
  YES -> PUBLIC
  NO  -> Continue

Is the information regulated by law (PII, PHI, CUI, PCI)?
  YES -> Is it CUI, trade secrets, or encryption keys?
    YES -> RESTRICTED
    NO  -> CONFIDENTIAL
  NO  -> Continue

Could disclosure cause material harm to the organization?
  YES -> CONFIDENTIAL
  NO  -> INTERNAL
```

**When in doubt, classify UP.** It is always safer to over-classify than to under-classify. Data can be reclassified downward after review by the data owner.

---

## Handling Requirements by Level

### Storage

| Requirement | Public | Internal | Confidential | Restricted |
|-------------|--------|----------|-------------|------------|
| Approved storage locations | Any | Company-managed systems | Encrypted company systems only | Encrypted, access-controlled systems with audit logging |
| Personal devices | Allowed | With company MDM | Only in managed containers | Prohibited |
| Cloud storage | Any cloud | Company-approved cloud only | Encrypted cloud with DLP | Approved cloud with FIPS 140-2 encryption; geographic restrictions may apply |
| Removable media | Allowed | Allowed | Encrypted only | Prohibited without CISO approval |
| Paper storage | Any | Office environment | Locked cabinet | Locked safe/cabinet; access log required |

### Transmission

| Requirement | Public | Internal | Confidential | Restricted |
|-------------|--------|----------|-------------|------------|
| Email | Unrestricted | Company email | Encrypted email or secure file transfer | End-to-end encrypted; no standard email |
| File sharing | Any method | Company file share | Encrypted link with expiration and authentication | Approved encrypted channel only |
| Verbal | Unrestricted | Normal business setting | Private setting; no speakerphone in public | Private setting; need-to-know verified |
| Fax | Allowed | Allowed | Pre-confirmed recipient | Prohibited |
| Physical mail | Standard mail | Standard mail | Sealed, no external markings of contents | Tracked courier with signature required |

### Access Control

| Requirement | Public | Internal | Confidential | Restricted |
|-------------|--------|----------|-------------|------------|
| Who may access | Anyone | All employees | Need-to-know basis with manager approval | Named individuals only with data owner approval |
| Authentication | None required | Standard login | Standard login + access request | MFA required; privileged access management |
| Access review | Not required | Annual | Quarterly | Monthly |
| Third-party access | Unrestricted | NDA required | NDA + data processing agreement | CISO approval + NDA + DPA + security assessment |

### Disposal

| Requirement | Public | Internal | Confidential | Restricted |
|-------------|--------|----------|-------------|------------|
| Digital | Delete | Secure delete | Crypto-erase or 3-pass overwrite | Crypto-erase + verification; physical destruction for hardware |
| Paper | Normal recycling | Cross-cut shred | Cross-cut shred | Cross-cut shred with certificate of destruction |
| Media (USB, disk) | Normal disposal | Secure erase | Degauss or destroy | Physical destruction with certificate |

---

## Labeling and Marking Standards

### Digital Documents

All documents classified Internal or above must be labeled:

**Header/Footer format:**
```
[CLASSIFICATION] - [ORGANIZATION NAME] - [Date]
```

**Examples:**
- `INTERNAL - Acme Corp - 2026-04-07`
- `CONFIDENTIAL - Acme Corp - 2026-04-07`
- `RESTRICTED - Acme Corp - 2026-04-07`

### Email

- **Subject line:** Prefix with classification for Confidential and Restricted
  - `[CONFIDENTIAL] Q4 Financial Report`
  - `[RESTRICTED] Encryption Key Rotation Schedule`
- **Body:** Include classification banner at the top of the email body
- **Attachments:** Apply document labeling to all attachments

### File Naming

Append classification to the filename:
- `project-plan_INTERNAL.docx`
- `customer-database-export_CONFIDENTIAL.csv`
- `encryption-keys_RESTRICTED.txt`

### Physical Documents

- **Cover page:** Large classification label (minimum 14pt bold)
- **Header:** Classification on every page
- **Binder/folder:** Classification label on spine and front cover
- **Envelope/package:** `CONFIDENTIAL` or `RESTRICTED` stamp on inner envelope; outer envelope has no classification markings

---

## CUI Marking Guide

For organizations handling Controlled Unclassified Information under DFARS/CMMC:

### Banner Marking

Every page containing CUI must include:
```
CUI // SP-[Category]
```

Common CUI categories for defense contractors:
- `CUI // SP-CTI` (Controlled Technical Information)
- `CUI // SP-EXPT` (Export Controlled)
- `CUI // SP-PROPIN` (Proprietary Business Information)
- `CUI // SP-PRVCY` (Privacy)

### Portion Marking (Optional but Recommended)

Mark individual paragraphs or sections:
- `(CUI)` before CUI paragraphs
- `(U)` before uncontrolled paragraphs

### CUI Designation Indicator

Bottom of first page:
```
CUI Category: [Category from CUI Registry]
Distribution/Dissemination: [Authorized distribution statement]
POC: [Name and contact for CUI questions]
```

### Email CUI Marking

```
Subject: CUI // [Subject line]
Body: 
CUI
[Email content]

CUI Category: [Category]
Distribution: Authorized personnel only
```

---

## Roles and Responsibilities

| Role | Responsibilities |
|------|-----------------|
| **Data Owner** (Business Unit Leader) | Assign classification level; approve access; review classification annually; approve reclassification |
| **Data Custodian** (IT/Security) | Implement technical controls; manage storage and backups; enforce access controls; maintain audit logs |
| **Data User** (All Employees) | Handle data per classification; report mishandling; request access through proper channels; apply labels |
| **CISO / Security Team** | Define policy; conduct training; audit compliance; investigate incidents; approve exceptions |
| **Legal / Compliance** | Advise on regulatory requirements; review classification for regulated data types; manage legal holds |

---

## Data Lifecycle Management

### Stage 1: Creation/Collection
- Classify at the point of creation or collection
- Apply labeling immediately
- Record in data inventory if Confidential or Restricted

### Stage 2: Storage
- Store in approved locations per handling requirements
- Encrypt per classification level
- Back up per organizational backup policy

### Stage 3: Usage
- Access only with proper authorization
- Handle per classification requirements
- Do not reclassify without data owner approval

### Stage 4: Sharing
- Verify recipient authorization
- Use approved transmission methods
- Track sharing of Confidential and Restricted data

### Stage 5: Archival
- Retain per retention schedule and regulatory requirements
- Maintain classification during archival
- Ensure archived data remains accessible if needed

### Stage 6: Disposal
- Follow disposal procedures for the classification level
- Document destruction of Confidential and Restricted data
- Obtain certificates of destruction where required

---

## Compliance Mapping

| Requirement | Framework | How This Policy Addresses It |
|-------------|-----------|----------------------------|
| Data categorization | NIST 800-171 3.8.1 | Four-level classification framework |
| Media marking | NIST 800-171 3.8.4 | Labeling standards section |
| Media transport protection | NIST 800-171 3.8.5 | Transmission handling requirements |
| Media sanitization | NIST 800-171 3.8.3 | Disposal requirements by level |
| CUI protection | CMMC MP domain | CUI marking guide + Restricted handling |
| Asset inventory | CIS Control 1, 2 | Data lifecycle management |
| Data protection | SOC 2 CC6.5 | Handling requirements matrix |
| PHI safeguards | HIPAA 164.312 | Confidential/Restricted handling |
| Cardholder data | PCI DSS 3.x, 9.x | Confidential handling + disposal |

---

## Implementation Checklist

- [ ] Executive sponsor has approved the policy
- [ ] Legal has reviewed the policy
- [ ] Data classification levels are finalized
- [ ] Handling procedures match actual organizational capabilities
- [ ] Data owners are assigned for major data repositories
- [ ] Initial data inventory is complete (at least for Confidential and Restricted)
- [ ] Labeling tools and templates are available to all employees
- [ ] Training materials are developed
- [ ] All employees have completed data classification training
- [ ] Technical controls are implemented (DLP, encryption, access controls)
- [ ] Audit procedures are defined
- [ ] Policy is published and accessible to all employees
- [ ] First quarterly review is scheduled

---

## About

Created and maintained by [Petronella Technology Group](https://petronellatech.com) - a cybersecurity and managed IT services firm based in Raleigh, NC. With 23+ years of experience and zero client breaches, we help businesses secure their infrastructure and achieve compliance.

- **Website:** [petronellatech.com](https://petronellatech.com)
- **Phone:** 919-348-4912
- **Free Assessment:** [Book a consultation](https://book.petronella.ai/blake)

## License

MIT License - See [LICENSE](LICENSE) for details.
