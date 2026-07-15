# Session Log

## 2026-07-15 — Create per-chapter .env files + fill template gaps
- Created a git-ignored `.env` in all 17 chapter dirs by copying each `.env.template` (placeholders ready to paste keys into).
- Added missing `.env.template` files for `chapter02` and `chapter14` (three-provider standard: OpenAI/Anthropic/Google + `LLM_PROVIDER=auto`), then generated their `.env`.
- Verified no `.env` is tracked by git (`.gitignore` line 2 covers `.env`). Only the two new templates are committed.

## 2026-07-15 — Position book PDF + bootstrap living docs
- Moved loose root `9781806109012.pdf` into `book/30-Agents-Every-AI-Engineer-Must-Build_9781806109012.pdf`.
- Added `book/*.pdf` to `.gitignore` so the ~84 MB copyrighted PDF stays local, not committed.
- Repaired `.gitignore`: it contained a literal `cat >> .gitignore << 'EOF' … EOF` heredoc (the command had been written into the file instead of executed). Rewrote as clean ignore patterns.
- Added `book/README.md` documenting what lives in `book/` and why it's ignored.
- Committed + pushed as `8060ca7` (chore).
- Bootstrapped the four living-doc files (`CLAUDE.md`, `project_state.md`, `session_log.md`, `whats_next.md`) — none existed before this session.
