---
name: coif-opportunity-intelligence
description: Use this skill whenever Claudia asks to analyze a job post, WhatsApp job group export, recruiter message, company, VC fund, venture studio, consulting lead, partnership opportunity, or potential client using COIF. Trigger on phrases such as COIF, COIF-MAX, COIF-J, COIF-C, COIF-P, COIF-V, COIF-WA, "תנתח משרה", "תבדוק אם מתאים לי", "משרות מקובץ וואטסאפ", "תבדוק אתר חברה", "פוטנציאל שיתוף פעולה", or "לקוחות שלהם". The skill produces a structured opportunity intelligence report, not only a job-fit answer.
---

# COIF v1.4 – Claudia Opportunity Intelligence Framework

## Purpose

COIF is an Opportunity Intelligence skill for Claudia Ben-Yaakov.

It analyzes jobs, companies, WhatsApp job posts, recruiter messages, VC funds, venture studios, potential clients, agencies, and partnership opportunities.

The goal is not only to answer:

> Is this job suitable?

The goal is to answer:

> What is the best value-creation path between Claudia and this organization?

Always evaluate the opportunity through these tracks:

1. Employment
2. Consulting
3. Partnership
4. Client Access
5. AI Opportunity
6. Venture Creation
7. Strategic Value
8. Revenue Potential
9. Accessibility / Relationship path

---

## Claudia Baseline Profile

Use this profile as the default evaluation baseline.

### Strong-fit areas

- Open Innovation
- Corporate Innovation
- Venture Creation
- Venture Studio building
- AI Product Strategy
- AI POC
- POC-to-Product
- Product Discovery
- PMF Strategy
- Startup Programs
- Ecosystem Building
- Strategic Partnerships
- Deep-Tech
- Digital Health
- Investment readiness
- Working with founders, corporates, startups, investors, accelerators, and innovation ecosystems
- Translating technology into business opportunities
- Building practical AI workflows and AI-enabled products

### Medium-fit areas

- Product Management
- Program Management
- Digital Transformation
- Go-to-Market strategy
- Business Development
- Innovation project management

### Lower-fit areas

- Performance Marketing
- Pure Sales
- HR
- Internal IT
- Classic PMO
- Operations-only roles
- Generic marketing execution
- HubSpot / campaigns / paid media as the core role
- Junior roles
- Full-time roles with low strategic ownership

### Current preference

Prefer opportunities that can become:

- Independent consulting
- Part-time work
- Fractional role
- Strategic advisory
- Partnership
- Client access channel
- AI product/service opportunity
- Venture creation opportunity

Employment is relevant, but not the only track.

### Claudia Current Opportunity Strategy

Primary goal:

- Build and grow `CBY Impact` as an independent business.

Secondary goal:

- Generate consulting, advisory, AI implementation, innovation, partnership, and client-access opportunities.

Employment goal:

- Prefer part-time, flexible, fractional, contract, or advisory roles that leave room to continue building the business.

Full-time employment is relevant only if one or more of the following are true:

- Exceptional compensation
- Exceptional strategic value
- Strong AI / innovation / product ownership
- Unique senior career opportunity
- Strong access to decision makers, clients, startups, investors, or corporates

Decision principle:

- Do not assume employment is Claudia's primary objective.
- A part-time role, consulting engagement, partnership, or client-access opportunity may rank above a stronger full-time job if it better supports long-term business creation.
- Exceptional full-time opportunities with high compensation, strong AI/innovation ownership, or significant strategic value should still be surfaced prominently in the Employment ranking.

---

## Trigger Rules

Activate COIF when the user provides or asks about:

- A WhatsApp exported ZIP/TXT from job groups
- A pasted job post
- A LinkedIn job link or recruiter message
- A company website
- A VC / venture studio / startup / agency / consulting opportunity
- A question like “האם זה מתאים לי?”
- A question like “מה אני יכולה להציע להם?”
- A question like “תבדוק את האתר”
- A request to rank opportunities

If the user writes one of these commands, follow the matching mode:

- `COIF-MAX`: full report
- `COIF-J`: job-first analysis
- `COIF-C`: consulting-first analysis
- `COIF-P`: partnership-first analysis
- `COIF-V`: venture-first analysis
- `COIF-WA`: WhatsApp job-group import and ranking

If no command is given but the intent matches, use COIF-MAX by default for a single company/post, and COIF-WA for WhatsApp exports.

---

## Required Behavior

### 1. Do not stop at job matching

For every opportunity, ask:

1. Is this a good job for Claudia?
2. Can Claudia work with them as a consultant?
3. Can this company become a partner?
4. Can their customers become Claudia’s customers?
5. Is there an AI product, workflow, agent, or POC Claudia can offer?
6. Is there a venture creation opportunity?
7. Is there a strategic reason to build a relationship even if the job is not ideal?

### 2. Always inspect the company, not only the post

If the user provides a company name or website, analyze the company deeply:

- What they do
- Business model
- Services/products
- Customers
- Target markets
- Stage
- Whether they are an agency, startup, corporate, VC, venture studio, public-sector organization, nonprofit, or service provider
- What hidden opportunity exists beyond the posted role

When current web information is needed, browse the web and cite sources.

### 3. Learn from OZ Global B2B case

Known lesson:

A role can look relevant because it is part-time or flexible, but the company context may change the conclusion.

Example rule:

- If company type = marketing agency and role = digital/performance/campaigns:
  - Employment Fit decreases
  - Consulting Fit may increase if Claudia can offer AI/product/innovation layer
  - Client Access Fit may increase if the agency has relevant B2B/tech clients
  - Partnership Fit may increase if Claudia can become a specialist partner for AI product strategy or AI-enabled client solutions

Always analyze customer portfolio and service portfolio before final scoring.

### 4. Prefer practical recommendations

Avoid generic recommendations. Every report must end with:

- Apply / do not apply
- Contact / do not contact
- Proposed positioning
- Suggested offer
- Specific outreach message
- Next action

### 5. Always create or update the COIF database

Every COIF analysis must produce two outputs:

1. A readable COIF report in the chat.
2. A structured update to the persistent database file: `COIF_Database.xlsx`.

This database update is not optional and should not depend on a separate user request.

Rules:

- If `COIF_Database.xlsx` does not exist in the current working context, create it.
- If `COIF_Database.xlsx` already exists and is available, append or update the relevant rows.
- Do not create a separate new Excel file for every analysis unless the user explicitly asks for a separate export.
- If the existing database is not available in the current session, create a new standalone `COIF_Database.xlsx` and state clearly that it does not yet include prior analyses.
- The full COIF report may remain in the chat or be exported separately only if the user asks.
- The Excel database stores the structured fields extracted from the report, not the full long-form report text.

---

## Input Handling

### A. Single post / pasted message

Extract:

- Company
- Role / opportunity topic
- Date posted
- Location
- Employment type
- Contact name
- Contact role
- Email
- Phone
- LinkedIn
- Website
- Source link
- Full post text

If missing, mark as `Not found` rather than inventing.

Before adding the post to the database, compute a `Post Hash` and check `COIF_Database.xlsx` history for an exact or near match, following the same rules as the WhatsApp workflow (see **Duplicate Detection and History Handling** under the database section). Do not create a duplicate opportunity row for a post that has already been logged.

### B. Company URL

Use the website to identify:

- Company type
- Business model
- Products/services
- Customers
- Team / leadership / contact path
- Possible fit for Claudia
- Possible AI opportunities
- Possible partnership opportunities
- Possible client-mining opportunities

### C. WhatsApp ZIP/TXT export

When the user uploads a WhatsApp export:

1. Extract the ZIP if needed.
2. Locate the chat `.txt` file.
3. Parse messages by date/time/sender when possible.
4. Run a lightweight relevance scan over all parsed messages and keep only candidate posts (see **Relevance-First WhatsApp Processing** below). Filter out the rest before any further analysis.
5. Create a normalized text version and `Post Hash` for each remaining candidate post.
6. Check the uploaded `COIF_Database.xlsx` history for exact duplicate posts and existing opportunities among the candidates before adding anything new.
7. Prioritize posts from the last 14 days unless the user asks otherwise.
8. Keep the full original post text for shortlisted opportunities.
9. Extract contact details:
   - name
   - role
   - email
   - phone
   - link
   - company
10. Rank opportunities using COIF scoring.
11. Produce:
   - Ranking A: Employment opportunities
   - Ranking B: Business development / consulting / partnership leads
   - Ranking C: Combined COIF opportunity value
   - `Claudia Next Actions` clean task list
   - detailed report for top opportunities
   - automatic update to `COIF_Database.xlsx`

### Relevance-First WhatsApp Processing

WhatsApp processing must be relevance-first and token-efficient. Do not analyze, hash, or run duplicate detection on every message in depth — only on candidate posts that may be relevant to Claudia.

A message becomes a candidate post only if it matches the High or Medium priority criteria in **Filtering Rules**, or the strong/medium-fit areas in **Claudia Baseline Profile** — for example a senior or strategic role, an AI/product/innovation/venture/VC/startup/ecosystem/deep-tech/digital-health opportunity, a part-time/fractional/advisory/flexible role, an organization that could become a client, partner, or referral channel for `CBY Impact`, or a lead that justifies a short strategic note even when the role itself is weak.

Filter out without deep analysis: greetings, thanks, admin chatter, and any message matching the Low priority / lower-fit criteria (junior roles, HR-only, internal IT, pure operations, pure sales with no strategic/client-access value, performance marketing or campaign execution without a clear AI/product/client-access angle, education/coordination without strategic ownership) — including repeated irrelevant posts. Mention that they were filtered out and why; do not analyze them in depth.

Post Hash creation and duplicate/history detection (see **Duplicate Detection and History Handling**) run only on candidate posts, after this filter — never on every parsed message.

Report a short processing funnel at the end of every COIF-WA run (see **E. Required processing and duplicate summary** under the database section).

---

## Scoring Model

Score each category from 0 to 10.

### Categories

- Employment Fit
- Consulting Fit
- Partnership Fit
- Client Access Fit
- AI Opportunity Fit
- Venture Creation Fit
- Strategic Value Fit
- Revenue Potential Fit
- Accessibility Fit

### Suggested weighted final score

- Employment Fit: 15%
- Consulting Fit: 20%
- Partnership Fit: 15%
- Client Access Fit: 15%
- AI Opportunity Fit: 10%
- Venture Creation Fit: 10%
- Strategic Value Fit: 10%
- Revenue Potential Fit: 5%

Accessibility Fit is important but should usually be reported separately unless the user asks to include it in the final score.

### Personal Preference Multiplier

After calculating the base score, apply a strategic preference adjustment before final prioritization.

Add points:

- `+2` for part-time roles
- `+2` for fractional roles
- `+2` for consulting opportunities
- `+2` for roles or leads that directly support building `CBY Impact`
- `+1` for strong business development potential
- `+1` for meaningful client-access or channel-partner potential

Subtract points:

- `-2` for full-time roles with low flexibility
- `-2` for roles that are mainly internal IT, operations, HR, or execution-only
- `-3` for roles that would likely require abandoning or freezing `CBY Impact`

Exception:

- Remove or reduce the full-time penalty when compensation, strategic value, seniority, AI/product ownership, or access to important networks is exceptional.

Important:

- The multiplier should affect prioritization and recommendations, not hide the original category scores. Show both the logic and the conclusion when the multiplier changes the ranking.

### Score meanings

- 0–2: Not relevant
- 3–4: Weak fit
- 5–6: Possible but not priority
- 7–8: Strong opportunity
- 9–10: High-priority opportunity

---

## Output Format – COIF-MAX

Use this format for a full report.

# COIF Report – [Company / Opportunity]

## 1. Executive Snapshot

| Category | Score |
|---|---:|
| Employment Fit | X/10 |
| Consulting Fit | X/10 |
| Partnership Fit | X/10 |
| Client Access Fit | X/10 |
| AI Opportunity Fit | X/10 |
| Venture Creation Fit | X/10 |
| Strategic Value Fit | X/10 |
| Revenue Potential Fit | X/10 |
| Accessibility Fit | X/10 |
| Final COIF Score | X/10 |

### Recommendation

Use clear icons:

- ✅ Apply
- ✅ Contact directly
- ✅ Suggest consulting
- ✅ Suggest partnership
- ✅ Mine client access
- ❌ Do not invest time

Then write 3–5 lines explaining the main conclusion.

---

## 2. Contact Intelligence

| Field | Value |
|---|---|
| Company | |
| Contact Full Name | |
| Contact Role | |
| Email | |
| Mobile | |
| LinkedIn | |
| Website | |
| Source Link | |
| Source / Group | |
| Date Posted | |

If the contact is not the decision maker, identify who the likely decision maker is.

---

## 3. Original Post / Source Summary

Include:

- Original post summary
- Key requirements
- Employment type
- Location
- Red flags
- Missing information

When the user asks for the full original post, provide it if it was supplied in the uploaded/pasted source.

---

## 4. Company Intelligence

Analyze:

- What the company does
- Business model
- Company type
- Products/services
- Customers / client portfolio
- Markets
- Stage / size if available
- Strategic direction
- Why this matters for Claudia

---

## 5. Employment Analysis

Answer:

- Is the role actually suitable?
- Which parts match Claudia?
- Which parts do not match?
- Is this senior enough?
- Is this likely full-time / part-time / consulting?
- Estimated chance of getting a call
- Estimated salary range if relevant and possible

Be direct. If it is not a good employment fit, say so.

---

## 6. Consulting Opportunity

Analyze what Claudia can offer as an independent consultant:

- AI product strategy
- AI workflows
- AI POC
- Innovation strategy
- PMF
- Product discovery
- Startup/corporate partnership
- Venture creation
- Ecosystem / investment readiness

State the best entry point.

---

## 7. Partnership Opportunity

Analyze:

- What can be built together
- How the company benefits
- How Claudia benefits
- Whether the company can be a channel partner
- Whether the company can refer clients
- Whether Claudia can become a specialist expert for them

---

## 8. Client Mining

If the company has clients, partners, portfolio companies, or customers:

- Identify relevant clients
- Explain why they matter
- Identify which clients could become Claudia’s leads
- Identify whether the company can introduce Claudia to them

If client names are not public, infer client types but do not invent names.

---

## 9. AI Opportunity Map

Suggest concrete AI opportunities:

- AI agent idea
- AI workflow idea
- AI layer for website/platform
- AI product extension
- AI POC
- AI enablement workshop
- Internal AI productivity system
- Client-facing AI service

Each idea should include:

- Problem solved
- Who would buy/use it
- Why Claudia is credible
- First small pilot

---

## 10. Venture Opportunity

Analyze whether there is potential for:

- New service line
- New product
- SaaS
- Agentic AI product
- Venture studio collaboration
- Startup spinout
- Joint market validation

Score and explain.

---

## 11. Action Plan

### This week

Provide 3–5 concrete next steps:

1. Apply / do not apply
2. Contact person
3. Message angle
4. What to ask in first conversation
5. What asset to send: CV, one-pager, AI service proposal, LinkedIn note, website link, etc.

---

## 12. Draft Outreach Message

Write one short message in the best language for the source.

Default:
- Hebrew for Israeli WhatsApp / local contacts
- English for global recruiters / international companies

Tone:
- Professional
- Direct
- Strategic
- Not too formal
- Not desperate
- Partnership-oriented when relevant

---

## 13. Learning Engine Update

End with:

### What we assumed initially

### What we discovered

### Lesson learned

### New COIF rule

### Should this update Claudia’s opportunity strategy?

If yes, write the update clearly.

---

## WhatsApp Group Ranking Output

When analyzing a WhatsApp export with multiple posts, do not produce only one ranking. Always produce three separate rankings so Claudia can distinguish between job applications and business-building opportunities.

### Ranking A – Employment Opportunities

Best jobs to apply for.

Criteria:

- Role fit
- Seniority
- Compensation potential
- Flexibility / part-time potential
- Strategic ownership
- AI / innovation / product ownership
- Hiring probability

Table format:

| Rank | Company | Role | Date | Contact | Employment Fit | Flexibility | Salary Potential | Call Probability | Recommendation |
|---:|---|---|---|---|---:|---:|---:|---:|---|

### Ranking B – Business Development Leads

Best opportunities for:

- Consulting
- Partnerships
- Client acquisition
- AI projects
- Workshops
- Fractional roles
- Venture creation

Table format:

| Rank | Company / Lead | Opportunity Type | Date | Contact | Consulting | Partnership | Client Access | AI | Revenue Potential | Recommendation |
|---:|---|---|---|---|---:|---:|---:|---:|---:|---|

### Ranking C – Combined COIF Value

Overall opportunity value considering all dimensions and the personal preference multiplier.

Table format:

| Rank | Company | Role / Opportunity | Date | Contact | Employment | Consulting | Partnership | Client Access | AI | Venture | Final COIF | Recommendation |
|---:|---|---|---|---|---:|---:|---:|---:|---:|---:|---:|---|

Then provide detailed COIF reports only for:

- top 3 opportunities overall, or
- the top items in each ranking when they differ, or
- all opportunities the user asks to expand.

Always preserve the full original post text for top-ranked items when available.

### Claudia Next Actions

Every WhatsApp analysis must end with one clean action list.

Maximum 5 actions.

Table format:

| Priority | Action | Why | Deadline |
|---:|---|---|---|

Rules:

- Only actionable items.
- No more than 5.
- Sort by expected ROI and fit with Claudia's current strategy.
- Prefer actions that support part-time, flexible, consulting, partnership, client access, and CBY Impact growth.
- Include exceptional full-time opportunities only when they are worth Claudia's attention.
- Ignore low-priority opportunities unless there is a specific reason to keep them.

---

## Persistent XLSX Database Requirements

Always create or update an Excel workbook named:

`COIF_Database.xlsx`

The workbook must contain these sheets:

### Sheet 1: Opportunities

Columns:

- ID
- Date Added
- Company
- Opportunity Type
- Source Type
- Source Link
- Source Post Hash
- Job Title / Post Topic
- Company Website
- Contact Full Name
- Contact Role
- Email
- Mobile
- LinkedIn
- Location
- Employment Fit
- Consulting Fit
- Partnership Fit
- Client Access Fit
- AI Opportunity Fit
- Venture Creation Fit
- Strategic Value Fit
- Revenue Potential Fit
- Accessibility Fit
- Final COIF Score
- Recommended Action
- Status
- Report File
- Notes

### Sheet 2: Contacts

Columns:

- Contact ID
- Company
- Full Name
- Role
- Email
- Mobile
- LinkedIn
- Relationship Strength
- Decision Maker Score
- Notes

### Sheet 3: Companies

Columns:

- Company ID
- Company
- Website
- Company Type
- Business Model
- Markets
- Customers
- Stage
- Strategic Relevance
- Client Access Potential
- Notes

### Sheet 4: Lessons

Columns:

- Lesson ID
- Date
- Company
- Initial Assumption
- Discovery
- Lesson Learned
- Rule Added
- Impact Area

### Sheet 5: Raw WhatsApp Posts

By default, store only posts that passed the **Relevance-First WhatsApp Processing** filter: relevant candidate posts, exact duplicates of relevant posts (to update Seen Count / Last Seen Date), reposted or changed versions of existing relevant opportunities, and borderline posts worth preserving for review. Do not log every parsed WhatsApp message. Store the full raw archive only if Claudia explicitly asks for it.

Columns:

- Raw ID
- Post Hash
- Date
- First Seen Date
- Last Seen Date
- Seen Count
- Sender
- Source / Group
- Message Text
- Normalized Message Text
- Detected Company
- Detected Role
- Detected Contact
- Detected Email
- Detected Phone
- Detected Links
- Relevance Category
- Duplicate Status
- Related Opportunity ID
- Related Action ID
- COIF Status
- Notes

### Sheet 6: Claudia Next Actions

Columns:

- Action ID
- Date Added
- Priority
- Action
- Why
- Related Company / Opportunity
- Related Opportunity ID
- Related Raw Post Hash
- Contact
- Deadline
- Suggested Message / Angle
- Asset to Send
- Status
- Last Updated
- Notes

Use clear formatting, freeze header rows, and set column widths.

### Database update behavior

For every new COIF analysis:

1. Add or update one row in `Opportunities`.
2. Add or update related people in `Contacts`.
3. Add or update the organization in `Companies`.
4. Add a row in `Lessons` whenever the Learning Engine produces a new rule, discovery, or strategic insight.
5. Add the original message/post in `Raw WhatsApp Posts` when the source is a WhatsApp export or copied post.
6. Add the top actionable next steps to `Claudia Next Actions` whenever an analysis produces tasks.

For WhatsApp exports, only candidate posts that passed the **Relevance-First WhatsApp Processing** filter are eligible for these steps. Irrelevant messages must not create rows in `Opportunities`, `Contacts`, `Companies`, or `Claudia Next Actions`.

Use stable IDs where possible. If no stable ID exists, create a simple internal ID using the date, company name, and source type.

Before performing steps 1–6 above, apply the **Duplicate Detection and History Handling** rules below. Do not add a new Opportunities, Contacts, Companies, or Claudia Next Actions row for something that already exists in the database history.

### Duplicate Detection and History Handling

Before adding any raw WhatsApp post, copied post, job post, opportunity, contact, company, or action to the workbook, check whether it already exists in the uploaded `COIF_Database.xlsx` history.

#### A. Exact post duplicate detection

For every raw WhatsApp post or copied post, create a stable `Post Hash` before analysis.

Use:

`Post Hash = SHA256(normalized full post text)`

Normalize the post text before hashing:

- Trim leading and trailing spaces.
- Convert repeated spaces and tabs to a single space.
- Standardize line breaks.
- Remove WhatsApp export metadata that is not part of the post content when it is safe to do so.
- Keep the actual post content, links, contact details, company name, and role text.
- Do not translate the post before hashing.

Then check `Raw WhatsApp Posts[Post Hash]`.

If the exact `Post Hash` already exists:

- Do not add a new raw post row.
- Do not create a new opportunity row.
- Do not create a new action row.
- Update the existing raw post row:
  - `Seen Count` = previous count + 1
  - `Last Seen Date` = current post date or current run date
  - `Duplicate Status` = `Exact duplicate`
  - `Notes` = add the new source/run context if useful
- If the post is relevant to an existing open action, add a note to the existing action instead of creating a duplicate task.

#### B. Same opportunity but changed or reposted text

If the post text is not exactly identical, but the company, role/topic, contact, link, or email strongly match an existing row:

- Treat it as a possible update, not as a fully new opportunity.
- Add the raw post as a new raw post row with its own `Post Hash`.
- Link it to the existing `Opportunity ID` when confidence is high.
- Update the existing opportunity `Notes` with the new information.
- Update `Status`, `Recommended Action`, or score fields only if the new post materially changes the analysis.
- Do not create a second opportunity unless the role/topic is meaningfully different.

Examples:

- Same company + same role + same email = likely same opportunity.
- Same company + different role = likely separate opportunity.
- Same post with a changed deadline = update existing opportunity and action notes.
- Same consulting lead reposted by another sender = update source history, do not duplicate the opportunity.

#### C. Action plan duplicate handling

Before adding any row to `Claudia Next Actions`, check whether an open action already exists for the same company, opportunity, contact, or `Post Hash`.

If an open action already exists:

- Do not create a duplicate action.
- Update the existing action `Notes` with: `Post appeared again on [date/source/run].`
- Update `Last Updated`.
- Update `Priority` or `Deadline` only if the repeated post creates urgency or new information.
- Keep the original action ID stable.

If the repeated post is no longer actionable, mark the related action as `Review` rather than deleting it.

#### D. Contacts and companies duplicate handling

Before adding contacts or companies:

- Match contacts by email first, then phone, then LinkedIn, then full name + company.
- Match companies by website/domain first, then normalized company name.
- Update existing rows instead of adding duplicates.
- Add repeated appearances, new senders, new context, or changed roles to `Notes`.

#### E. Required processing and duplicate summary

At the end of every COIF-WA run, include one short funnel summary table covering both relevance filtering and duplicate handling:

| Stage | Count |
|---|---:|
| Total WhatsApp messages parsed | X |
| Candidate relevant posts detected | X |
| Irrelevant messages filtered out before analysis | X |
| Exact duplicates skipped/updated | X |
| New raw posts added | X |
| New opportunities added | X |
| Existing opportunities updated | X |
| New actions added | X |
| Existing actions updated as notes | X |

The goal is to show how much was filtered out before any analysis happened, preserve history, and avoid inflating the opportunity list or task list.

The database should support future questions such as:

- Which companies have the highest Partnership Fit?
- Which opportunities are best for consulting?
- Which contacts are likely decision makers?
- Which companies can open access to clients?
- What patterns have we learned after multiple analyses?

---

## Filtering Rules

High priority for Claudia:

- AI Product
- Innovation
- Venture Studio
- Venture Creation
- Startup programs
- Corporate innovation
- Strategic partnerships
- Product strategy
- Digital health
- Deep-tech
- Investment / VC / portfolio support
- Fractional / part-time / consulting
- Roles where her Samsung + accelerator + AI experience is an advantage

Medium priority:

- Product roles
- Business development roles
- Digital transformation roles
- Strategy roles

Low priority unless there is strong partnership/client access:

- Marketing agency execution roles
- Performance marketing
- HR
- Internal IT
- Pure operations
- Education/program coordination without strategic ownership
- Junior roles

---

## Important Reasoning Rules

### Rule: Employment vs Business Building

When evaluating opportunities for Claudia:

- Do not assume employment is the primary objective.
- The primary objective is building `CBY Impact`.
- A part-time role, consulting engagement, partnership, or client-access opportunity may rank above a stronger full-time job if it better supports long-term business creation.
- Exceptional full-time opportunities with high compensation, strong AI/innovation ownership, or significant strategic value should still be surfaced prominently in the Employment ranking.
- Always separate job-fit ranking from business-lead ranking.

### General rules

1. If a role looks flexible but the company is not strategically aligned, do not over-score Employment Fit.
2. If the company has access to many relevant clients, increase Client Access Fit.
3. If the company is a service provider/agency, check whether Claudia can become a specialist partner rather than an employee.
4. If the role is in VC but too junior or low salary, score Employment lower but Strategic Value may remain high.
5. If the company builds products/platforms, look for AI product extensions.
6. If the company works with startups or corporates, look for venture creation and open innovation angles.
7. If the post lacks enough data, say what is missing and give a provisional score.
8. Never invent contacts, salaries, or clients.
9. Use web research for current company information when available.
10. Cite web sources when using external information.

---

## User Activation Examples

The user may activate the skill by writing:

- `COIF-MAX` + post/link
- `COIF-WA` + WhatsApp ZIP
- `תנתח לפי COIF`
- `תבדוק אם המשרה מתאימה לי`
- `תבדוק את החברה ומה אני יכולה להציע להם`
- `תדרג את המשרות בקובץ`
- `תן לי דוח COIF`
- `תייצר אקסל COIF`
- `תעדכן את COIF_Database.xlsx`

When the user uploads a WhatsApp ZIP and asks to analyze jobs, automatically use COIF-WA.

Remember: the database update is mandatory after every COIF analysis, even when the user does not explicitly ask for Excel output.

---

## Final Note

This skill is designed to serve Claudia’s real strategy:

Not only finding a job.

Building a pipeline of:
- jobs,
- consulting leads,
- partnerships,
- clients,
- AI opportunities,
- and venture creation paths.
