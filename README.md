# COIF – Claudia Opportunity Intelligence Framework

COIF is Claudia Ben-Yaakov's personal opportunity intelligence framework.

It is designed to analyze:

- Job opportunities
- WhatsApp job posts
- Recruiter messages
- Companies
- Consulting leads
- Partnership opportunities
- VC / venture studio opportunities
- Potential clients
- AI product and workflow opportunities

COIF is not only a job-fit tool.

Its main purpose is to help Claudia decide:

> What is the best value-creation path between Claudia and this opportunity?

---

## Current Strategic Context

Claudia is currently building **CBY Impact** as an independent business.

Therefore, COIF prioritizes:

1. Part-time / flexible roles
2. Consulting opportunities
3. Fractional roles
4. Strategic advisory work
5. Partnership and client-access opportunities
6. AI product / AI workflow projects
7. Venture creation opportunities

Full-time employment is relevant only when the role is exceptional in:

- Compensation
- Strategic value
- AI / Innovation ownership
- Seniority
- Long-term career leverage

---

## Core Outputs

Every COIF analysis should produce:

1. Employment Ranking
2. Business Development Ranking
3. Combined COIF Ranking
4. Claudia Next Actions
5. Structured database update

---

## Main Files

- `skill.md` – Main ChatGPT Skill instructions
- `claudia_profile.md` – Claudia's profile, goals, preferences and fit areas
- `SCORING_MODEL.md` – COIF scoring logic
- `LEARNING_ENGINE.md` – Lessons learned and rule updates
- `lessons.md` – Running operational notes and discoveries
- `CHANGELOG.md` – Version history
- `CHANGE_REQUESTS.md` – Future improvements
- `ROADMAP.md` – Development roadmap

---

## Database

Generated Excel files such as `COIF_Database.xlsx` and `COIF_Action_Plan_*.xlsx` are working data.

They should usually not be committed to Git.

Recommended `.gitignore`:

```gitignore
*.xlsx
```

---

## Recommended Git Workflow

After updating the Skill or documentation:

```bash
git status
git add skill.md README.md SCORING_MODEL.md claudia_profile.md lessons.md CHANGELOG.md LEARNING_ENGINE.md CHANGE_REQUESTS.md ROADMAP.md
git commit -m "Update COIF documentation and strategy files"
git push
```

---

## Current Version

Current working version: **v1.4**

Main v1.4 updates:

- Relevance-first WhatsApp processing: filter before hashing/dedup/scoring, not after
- Candidate-only default storage for Raw WhatsApp Posts (full archive only on request)
- Single merged processing/duplicate funnel summary at the end of every COIF-WA run

Previous v1.3 updates:

- Post Hash duplicate/history detection for WhatsApp and pasted posts
- Seen Count / First Seen / Last Seen tracking for reposted opportunities

Previous v1.2 updates:

- CBY Impact strategy layer
- Preference for part-time / consulting / fractional work
- Three separate rankings
- Claudia Next Actions
- Employment vs Business Building rule
