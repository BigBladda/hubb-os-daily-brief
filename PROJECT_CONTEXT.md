# Project Context: Daily Brief

> **For any AI assistant:** Read this file before beginning work. This is the full context for this project.

**Last Updated:** 2026-06-13
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

n8n workflow (ID: wJQbhYfr2Bb7FFEw) running on schedule at 7am CT daily, sending a formatted Telegram message to HubbOSBot. Shows High priority Ready items (⚡) and all Blocked items (🚫) grouped by project. Project headers are tappable links to Notion. Data source: Notion Action Items DB.

---

## Approach

| Layer | Tool | Job |
|---|---|---|
| Data | Notion Action Items DB (ID: 2eef09b2-ee02-4f4d-9814-ac0eda0448d3) | Source of next actions and blockers |
| Data | Notion Projects DB (ID: 3fca6a5b-1330-475b-880d-97e6935a37e8) | Project name + URL lookup |
| Automation | n8n on Elestio (workflow: wJQbhYfr2Bb7FFEw) | Scheduled 7am workflow |
| Delivery | Telegram (HubbOSBot, chat ID: 8687216711) | Push notification to Hubb |

**Workflow structure:**
- Schedule Trigger (0 13 * * * UTC = 7am CT)
- HTTP Request → Notion Action Items DB (filter: Ready + Blocked)
- HTTP Request → Notion Projects DB (all, for name/URL lookup)
- Code node: filter High priority + Blocked, group by project, format HTML message
- Telegram: send with HTML parse mode

**Key technical notes:**
- Notion API requires real DB IDs (not MCP collection IDs)
- HTTP Request node used (not n8n Notion node) — consistent with Inbox Triage pattern
- n8n - elast.io integration must be connected to each Notion DB via Connections
- Telegram parse_mode: HTML (not Markdown) — required for bold + hyperlink on same element

---

## Key Constraints

- Data must come from Notion — no Markdown parsing
- Telegram is the only delivery channel for v1
- Message must be scannable in under 60 seconds
- No redesign required when new projects are added — pulls dynamically

---

## Decisions Summary

See DECISIONS.md for full log. Locked decisions:

- Telegram at 7am as primary delivery — push, not pull
- Notion Action Items DB as data source — not OPEN_LOOPS.md
- Brief shows High priority Ready + all Blocked only — Normal Ready items excluded (noise)
- Project headers are tappable HTML links to Notion project record
- v1 is Telegram only — Notion dashboard is Phase 2

---

## Open Loops Summary

See OPEN_LOOPS.md for full list. Top priority:

1. Design Notion Daily Brief dashboard — more detailed view with calendar, Google Tasks, events, social
