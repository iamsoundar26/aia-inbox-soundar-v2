# AI Accountant · Inbox (Soundar) — Neo workspace, version 2

> **Status: ideation-stage concept, version 2.** Branched from `v1.0-locked` on 7 Oct 2026.
> v1 (the light-theme Neo side panel) is untouched and still reachable with Ctrl J / the floating side tab.

## What v2 adds

A dedicated **Neo workspace** at `/neo/` — an AI accounting workspace rather than a chat box:

| Area | Route | What it shows |
|---|---|---|
| Home | `neo/#/` | Greeting, large "Ask Neo anything" composer (attach, agent picker, "Explain why" toggle), six suggested actions, "Your work" stats, "Needs your attention" list, agent cards |
| Chat | `neo/#/chat/<id>` | Three columns: history · conversation · Work panel. Scripted Neo responses produce structured result cards (Ready / Needs review / Blocked), AI suggestion with confidence and "Why this suggestion?", bulk approve with confirmation, audit trail |
| Needs attention | `neo/#/attention` | Exceptions grouped by problem (4 × missing cost centre with "Apply to all"), duplicate / GSTIN / unusual-amount cases with evidence and explicit actions |
| Agents | `neo/#/agents`, `#/agents/<id>` | Agent cards, agent detail (capabilities, data sources, trust model, recent runs, current run), permissions page (Read → Suggest → Execute → Approve), automation page (trigger + workflow), create-agent form in plain language |
| Work / Runs | `neo/#/runs`, `#/runs/<id>` | Running / Needs attention / Completed tabs, progress bars, run detail with activity timeline |
| Knowledge | `neo/#/knowledge` | Company, Accounting, Data and Historical context with connection status |
| Settings | `neo/#/settings` | Explanation and approval preferences |

Entry points from the exported app: a **Neo · NEW** item in the module navigation and the top-nav **Ask Neo** pill (both open `/neo/`).

## Files added or changed in v2

- `neo/index.html`, `neo/neo.css`, `neo/neo.js` — the workspace. Plain HTML/CSS/JS, hash router, no build step. Sample data and scripted Neo responses live at the top of `neo.js`.
- `neo-simple.js` — appended block that injects the module-nav link and redirects the Ask Neo pill.
- All pages: asset version bumped to `?v=5`.

The workspace uses relative paths (`../_next/…`, `../images/logo.png`, `../inbox/`) so it works under any base path without running `set-base-path.py`.

## Run locally

    cd ..                                  # the folder that contains aia-inbox-soundar-v2
    python3 -m http.server 8000
    # open http://localhost:8000/aia-inbox-soundar-v2/inbox/   (app, with Neo in the nav)
    # open http://localhost:8000/aia-inbox-soundar-v2/neo/     (workspace directly)

The build is currently homed at `/aia-inbox-soundar-v2` (see `.basepath`). Use `python3 set-base-path.py <prefix>` to re-home it.

## Prototype interactions that work

Suggested action → chat → structured result · Review exceptions → grouped workspace · Approve 27 invoices → confirmation modal → audit trail updates · Agent card → detail → Run agent → live progress → results · "Why?" on any suggestion · Create agent (name suggested from the description) · Runs tabs and run detail · Chat history: open, rename, pin, archive, delete · Attach files (chips) · Ctrl J focuses the composer · Mobile: Work panel becomes a bottom sheet.

## Known gaps

- Neo's answers are scripted by keyword (review / duplicate / reconcile / GST / AP / month-end / expenses); anything else gets the "needs attention" summary.
- Permissions are display-only; "Edit permissions" shows a note.
- Attached files are listed, not processed. Thumbs feedback only shows a toast.
- State resets on reload (no persistence).
