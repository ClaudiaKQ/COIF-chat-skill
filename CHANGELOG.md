# COIF Change Log

## v1.4 - 2026-06-20

### Added

* Relevance-First WhatsApp Processing rule: lightweight relevance scan and filter run before hashing, duplicate detection, or scoring
* Required processing funnel in the COIF-WA end-of-run summary (messages parsed → candidates → filtered out → duplicates → opportunities/actions)
* Default candidate-only storage policy for the Raw WhatsApp Posts sheet, with an explicit opt-in for a full raw archive

### Updated

* WhatsApp parsing workflow (Section C) re-sequenced so relevance filtering happens before Post Hash creation and duplicate detection, not after
* Database update behavior restricted so irrelevant WhatsApp messages cannot create Opportunities, Contacts, Companies, or Claudia Next Actions rows
* Merged the v1.3 duplicate summary and the new processing funnel into a single end-of-run table to avoid two overlapping reports

### Lessons Learned

* Hashing and duplicate-checking every parsed message before filtering for relevance wastes effort on chatter that should never reach scoring or the database.
* A second summary table reporting nearly the same numbers as an existing one is a maintenance risk; better to extend the existing table than add a parallel one.

---

## v1.3 - 2026-06-20

### Added

* Post Hash duplicate detection (SHA256 of normalized text) for WhatsApp and pasted posts
* History tracking fields in Raw WhatsApp Posts (Seen Count, First/Last Seen Date, Duplicate Status, Related Opportunity ID, Related Action ID)
* Related Opportunity ID / Related Raw Post Hash / Last Updated fields in Claudia Next Actions
* Source Post Hash field in Opportunities
* Required duplicate/history summary at the end of every COIF-WA run

### Updated

* WhatsApp parsing workflow to hash and check for duplicates before scoring
* Single post / pasted message workflow to check history before creating a new opportunity row
* Persistent database update behavior to apply duplicate detection before writing new rows

### Lessons Learned

* WhatsApp job groups repeatedly repost the same opportunity; without hash-based duplicate detection the database and action list grow unbounded over time.
* Exact duplicates and "same opportunity, reposted with changes" are different cases and need different handling: the first should only update a seen-count, the second should update the existing opportunity rather than create a new one.

---

## v1.2 - 2026-06-14

### Added

* CBY Impact strategy layer
* Employment Ranking
* Business Development Ranking
* Combined COIF Ranking
* Claudia Next Actions section
* Employment vs Business Building rule
* Part-time and consulting preference logic

### Updated

* Opportunity scoring model
* WhatsApp opportunity ranking process
* Recommendation workflow

### Lessons Learned

* Job fit and business opportunity fit are different analyses.
* A company can be a poor employment fit but an excellent consulting or partnership opportunity.
* Claudia's primary goal is building CBY Impact while selectively pursuing employment opportunities.

---

## v1.1 - 2026-06-14

### Added

* Persistent COIF database requirement
* Opportunity tracking model
* Contact intelligence model
* Company intelligence model

---

## v1.0 - Initial Release

### Added

* COIF framework
* WhatsApp job analysis
* Company analysis
* Job opportunity scoring
* Consulting opportunity scoring
* Venture opportunity scoring
