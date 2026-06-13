# Decisions Log — Daily Brief

Append a new entry at the end of every working session. Do not edit past entries.

---

## 2026-06-12

- **Project kicked off** — Deliverable defined: 7am Telegram message with next actions + blockers per active project, pulling from Notion Action Items DB.
- **Telegram-only for v1** — Notion dashboard deferred. Push delivery is faster to build and higher utility. Notion view is Phase 2.
- **Notion Action Items DB as data source** — Not OPEN_LOOPS.md Markdown files. Dynamic Notion query handles new projects automatically without workflow changes.
- **7am CT delivery time** — Early enough to have the brief ready before starting the day.

## 2026-06-13 — Build Session

- **n8n workflow built and live** — Workflow ID wJQbhYfr2Bb7FFEw. Schedule: 0 13 * * * UTC (7am CT). Active and verified end-to-end.
- **HTTP Request node used instead of n8n Notion node** — n8n native Notion node uses OAuth (n8n - elast.io integration) which was not resolving DBs correctly. Direct HTTP Request with integration token is the reliable pattern, consistent with Inbox Triage.
- **Notion collection IDs ≠ Notion API database IDs** — MCP collection IDs (eb5f9099..., c475717e...) do not work with direct Notion API calls. Real IDs: Action Items = 2eef09b2-ee02-4f4d-9814-ac0eda0448d3, Projects = 3fca6a5b-1330-475b-880d-97e6935a37e8.
- **Two-node Notion query approach** — Query Action Items (filtered Ready + Blocked) + Fetch Projects (all, for name/URL lookup). Code node cross-references using page IDs from relation field.
- **Brief scope: High priority Ready + all Blocked only** — Normal Ready items excluded. Brief answers "what's urgent today" not "what are all my tasks".
- **Telegram HTML parse mode** — Switched from Markdown to HTML. Required to render bold project name as a tappable hyperlink simultaneously. Markdown mode does not support both on same element.
- **Action item naming convention locked** — Names stay clean and concise throughout the lifecycle. Status and Blocker fields carry state. No encoding blocked/completed state into item names.
- **Notion write dedup incident** — Action Items DB was seeded twice across two sessions (Jun 12 and Jun 13), creating duplicates. Root cause: no read-before-write check. Fix: dedup rule added to AI_SESSION_PROTOCOL.md. Duplicates cleaned manually.
- **Notion Daily Brief dashboard deferred to next session** — Next action for this project. Scope: more detailed Notion view with calendar items, Google Tasks, upcoming events, social posts scheduled.
