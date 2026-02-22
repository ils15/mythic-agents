# 🔄 Active Context

> **Priority file** — agents read this first when starting any task.  
> Keep it current. A stale active context is worse than none.

---

## Current Focus

<!-- One sentence: what is being worked on right now? -->
_Ex: "Implementing JWT authentication with refresh tokens in the FastAPI backend."_

**Status:** <!-- In planning | In implementation | In review | Complete -->

---

## Most Recent Decision

<!-- The last significant architectural or design decision relevant to current work. -->
_Ex: "Decided to store refresh tokens in httpOnly cookies with a 7-day TTL to protect against XSS."_

**Date:** <!-- YYYY-MM-DD -->

---

## Active Blockers

<!-- Anything preventing progress. If none, write "None." -->
- None

---

## Next Steps

<!-- The next 2–3 concrete steps after current focus. -->
1. _Ex: Review auth endpoints with @temis_
2. _Ex: Update frontend login flow_

---

## References

<!-- Links to related files or decision notes. -->
- [00-overview.md](00-overview.md) — Project scope
- [01-architecture.md](01-architecture.md) — System design
- [_notes/](_notes/_index.md) — Architectural decision records
- [_tasks/](_tasks/_index.md) — Task history

---

> **For agents:** This file reflects the current sprint/feature state.  
> `@mnemosyne` is responsible for keeping it updated after each delivery.  
> When closing a feature, move context to `_notes/` and reset this file.
