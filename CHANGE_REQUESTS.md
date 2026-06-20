# COIF Change Requests

Use this file to capture future improvements before implementing them.

---

## Open Requests

### CR-001

Status: Planned

Description:

Create Claudia Next Actions worksheet automatically in every COIF database update.

---

### CR-002

Status: Planned

Description:

Add salary estimation engine.

---

### CR-003

Status: Planned

Description:

Add recruiter scoring model.

---

### CR-004

Status: Planned

Description:

Add venture studio identification model.

---

### CR-005

Status: Planned

Description:

Add consulting proposal generator.

---

## Completed Requests

### CR-000

Status: Completed

Description:

Add persistent COIF database.

---

### CR-006

Status: Completed (v1.3)

Description:

Add duplicate/history detection (Post Hash) so reposted WhatsApp jobs and copied posts don't inflate the Opportunities and Claudia Next Actions sheets. Tracks Seen Count, First/Last Seen Date, and links reposted-but-changed posts to the existing opportunity instead of creating a new one.

---

### CR-007

Status: Completed (v1.4)

Description:

Make WhatsApp processing relevance-first and token-efficient: filter messages for relevance before hashing/duplicate detection or scoring, restrict database writes to relevant candidate posts, default Raw WhatsApp Posts to candidate-only storage, and report a single processing/duplicate funnel at the end of each run.
