# Session Log

## 2026-07-15 — Single root .env for keys + fill template gaps
- Consolidated to ONE git-ignored `.env` at the repo root holding all provider keys — removed the 17 per-chapter `.env` placeholders (they would shadow the root file in `find_dotenv`'s upward search).
- Verified: `load_dotenv()` is called from `.py` files inside the repo (`utils.py`, `supporting/llm_provider.py`), so `find_dotenv` walks up and resolves the root `.env`. Smoke-tested from `chapter07` — root `.env` resolved, `LLM_PROVIDER=auto` read. ✓
- Added missing `.env.template` files for `chapter02` and `chapter14` (three-provider standard + `LLM_PROVIDER=auto`).
- `.gitignore` line 2 (`.env`) covers the root file — keys never get committed.

## 2026-07-15 — Position book PDF + bootstrap living docs
- Moved loose root `9781806109012.pdf` into `book/30-Agents-Every-AI-Engineer-Must-Build_9781806109012.pdf`.
- Added `book/*.pdf` to `.gitignore` so the ~84 MB copyrighted PDF stays local, not committed.
- Repaired `.gitignore`: it contained a literal `cat >> .gitignore << 'EOF' … EOF` heredoc (the command had been written into the file instead of executed). Rewrote as clean ignore patterns.
- Added `book/README.md` documenting what lives in `book/` and why it's ignored.
- Committed + pushed as `8060ca7` (chore).
- Bootstrapped the four living-doc files (`CLAUDE.md`, `project_state.md`, `session_log.md`, `whats_next.md`) — none existed before this session.
