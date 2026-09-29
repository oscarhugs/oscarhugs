# Current State

_Last updated: 2026-09-29_

## In progress

- Setting up VS Code + Cline (free, open-source coding agent) as a backup tool for when Claude Code / Codex hit their usage limits. Cline will connect to OpenRouter's free-tier (`:free`) models — $0 cost, no card needed, rate-limited (~20 req/min, ~200/day) instead of hard-capped by time window.

## Next up

- On the local machine: download VS Code, install to `D:\Programs\Microsoft VS Code` (custom install location), install the Cline extension from the VS Code Marketplace.
- Sign up free at openrouter.ai, generate an API key (no card required).
- In Cline settings: choose OpenRouter as provider, paste key, pick a current `:free` model (check https://openrouter.ai/collections/free-models — best free model rotates).
- Tell Cline once to read `STATE.md` in whichever project folder it's opened in, so it picks up the same memory convention as Claude Code.
- Reminder: this machine has only ~7.9GB RAM (i5-8265U) — don't run Chrome scraping + Claude Code + VS Code/Cline all at once, it'll be tight. One heavy tool at a time.

## Recently done

- 2026-09-24/25 — Created `CLAUDE.md` + `STATE.md` in `oscarhugs` for cross-session memory; established the pattern (read STATE.md at session start, update at session end).
- 2026-09-25 — Walked through turning `D:\Projects\Peregrine` and `D:\Projects\Peregrine\Zoominfo Scraper` into separate git repos (installed Git for Windows, set PowerShell execution policy, set git identity). Excluded sensitive/generated data before committing: `browser-profile/` (Chrome automation profile), scraped lead CSVs, screenshots, `ocr_cache/`, and `Website Scrapes/` (client/deal data — looked like confidential M&A material).
- 2026-09-25 — Pushed three new repos to GitHub: `oscarhugs/peregrine`, `oscarhugs/zoominfo-scraper`, `oscarhugs/screenshot-to-code` (the last one is the open-source screenshot-to-code project, kept separate since it's a distinct nested project, not merged into Peregrine).
- 2026-09-25 — Added matching `CLAUDE.md` + `STATE.md` to `peregrine` and `zoominfo-scraper`. Installed Claude Code CLI locally (`npm install -g @anthropic-ai/claude-code`, had to allow-scripts and fix PowerShell execution policy).
- 2026-09-25 — Added `start-work.bat` / `finish-work.bat` helper scripts to `peregrine` and `zoominfo-scraper` (pull+launch / commit+push), then superseded them with plain-language trigger words in `CLAUDE.md` ("start" → pull + read STATE.md + summarize; "finish the day" → update STATE.md + commit + push) so it works identically in any session, local or cloud, no scripts needed.
- 2026-09-25 — Diagnosed why a fresh session showed "no memory" despite other tabs having done real work: STATE.md only updates when a session explicitly saves/pushes — separate open tabs don't auto-sync. Fix: run "finish the day" in each tab sequentially (not simultaneously, to avoid STATE.md push conflicts).
- 2026-09-29 — User pushed back on paying for Anthropic API as a fix for hitting Claude Pro's usage limits (also hit Codex's 5-hour window) — correctly, since API billing is metered and could cost more than the $20/mo plan. Researched real free/cheap alternatives: Cline (free, open-source, BYOK, 30+ providers) + OpenRouter free-tier models (`:free` models, $0, no card, rate-limited not capped) is the genuine free fallback path. Chinese model coding subscriptions (DeepSeek/Kimi/GLM) are NOT free at the API level — DeepSeek is API-only paid, Kimi's plan paused signups, GLM's got pricier. Their free access is via chat websites only, not agentic coding.
- 2026-09-29 — Checked local machine specs: ~7.9GB RAM, Intel i5-8265U (8th gen, 4c/8t). VS Code will run fine alone but multitasking with Chrome scraping + Claude Code simultaneously will be tight.

## Notes / decisions

- No external memory tooling (MCP memory server, Graphiti, etc.) needed for this use case — plain CLAUDE.md + STATE.md, read/updated automatically each session, is sufficient.
- Memory setup deliberately kept per-repo (not global `~/.claude/CLAUDE.md`) so it works identically across local machine and cloud sessions — a global file only exists on one machine.
- User is cost-conscious ($20/mo Pro plan only, will not pay for metered API) — future tooling suggestions should default to free/open-source options first, not push paid upgrades.
