# COIF Change Log

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
