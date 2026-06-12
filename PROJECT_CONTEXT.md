# Project Context: Daily Brief

> **For any AI assistant:** Read this file before beginning work. This is the full context for this project.

**Last Updated:** 2026-06-12
**Repo:** BigBladda/hubb-os-daily-brief
**Area:** 🔵 Personal
**Tags:** Development
**Parent Program:** Hubb OS
**Status:** Active
**Started:** 2026-06-12
**Target:** 2026-06-26

---

## What This Is

Daily Brief is a 7am Telegram message delivering the current next actions and blockers for every active project, pulled live from Notion. It replaces the need to open any tool to know what to work on.

---

## Deliverable

n8n workflow running on schedule at 7am daily, sending a formatted Telegram message to HubbOSBot with next actions (Priority: High and Ready status) and blockers per active project. Data source: Notion Action Items DB.

---

## Approach

| Layer | Tool | Job |
|---|---|---|
| Data | Notion Action Items DB | Source of next actions and blockers |
| Automation | n8n on Elestio | Scheduled 7am workflow |
| Delivery | Telegram (HubbOSBot) | Push notification to Hubb |

**Build sequence:**
1. Notion Action Items DB built and populated (prerequisite — not this project)
2. n8n workflow: query Notion for Ready + Blocked items grouped by Project
3. Format Telegram message
4. Schedule at 7am CT daily
5. Test and verify

---

## Key Constraints

- Data must come from Notion — no Markdown parsing
- Telegram is the only delivery channel (no email, no Notion page rebuild required for v1)
- Message must be scannable in under 60 seconds
- No redesign required when new projects are added — must pull dynamically

---

## Decisions Summary

See DECISIONS.md for full log. Locked decisions:

- Telegram at 7am as primary delivery — push, not pull
- Notion Action Items DB as data source — not OPEN_LOOPS.md
- v1 is Telegram only — Notion dashboard is Phase 2

---

## Open Loops Summary

See OPEN_LOOPS.md for full list. Top priorities right now:

1. Notion Action Items DB must be built before this project can build
2. Design n8n workflow structure
3. Design Telegram message format
