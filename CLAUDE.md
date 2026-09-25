# Session Memory

This repo is used to persist working memory across Claude Code sessions.

- At the **start** of every session, read `STATE.md` before doing anything else — it has the current status, what's in progress, and what's next.
- At the **end** of every session (or after any meaningful chunk of work), update `STATE.md`:
  - Move finished items to "Recently done"
  - Update "In progress" / "Next up"
  - Note any decisions or context worth remembering
- Keep `STATE.md` short and current — prune stale detail rather than letting it grow forever. It's a working memory, not an archive.
