# Session Log

## 2026-07-16 — Migrate dead model `claude-sonnet-4-20250514` → `claude-sonnet-5`
- The book pinned `claude-sonnet-4-20250514`, which retired 2026-06-15 and now 404s — every `__RUN_CLAUDE_Sonnet4` notebook was silently falling back to MockLLM instead of calling Claude (observed in ch05 output: "Anthropic API error, falling back to MockLLM: 404").
- Swapped the retired ID → `claude-sonnet-5` across 64 files (notebooks + `supporting/llm_provider.py` + LLM_COMPARISON docs). Chosen over Opus to stay in the Sonnet tier the notebooks were built for and keep per-run cost sane across 17 chapters.
- `supporting/llm_provider.py`: added `_anthropic_rejects_sampling()` guard — Sonnet 5 / Opus 4.7+ / Fable 5 reject a non-default `temperature` with a 400, so the LangChain and direct-SDK Anthropic paths now omit `temperature` for those models (verified: `temperature=0` → 400 on sonnet-5).
- Smoke-tested live: the notebook's exact call shape (`claude-sonnet-5`, `max_tokens=1024`, no sampling params) returns `stop_reason=end_turn` with a clean answer — no truncation from default adaptive thinking, no 400.
- Book variant notebooks stay named `__RUN_CLAUDE_Sonnet4` (filename unchanged); only the model string inside changed.

## 2026-07-16 — Per-chapter venvs + Jupyter kernels for all 17 chapters
- Built an isolated `chapterNN/.venv` (Python 3.12, via uv) for every chapter and registered a Jupyter kernel `30agents-chapterNN` / display "30 Agents chapterNN (Claude)". Chapters pin mutually-incompatible langchain/langgraph/numpy versions, so one shared env was impossible — per-chapter isolation chosen.
- Python 3.12 (not 3.13) picked because old pins (`numpy==1.26.4`, `langchain==0.2.16`) have no 3.13 wheels. uv's shared cache dedupes torch across the heavy chapters (06/08/10/13; ch11's torch is commented out → actually light).
- **Book requirements bug:** ch10/14/16 pin `langchain-core==0.2.38` (0.2.x) in requirements.txt but `langchain-anthropic>=0.3.0` (needs core >=0.3) in requirements-claude.txt — unsatisfiable. Remediated by installing `langchain-anthropic>=0.1.15,<0.2` (compatible with 0.2.x core) instead.
- ch11's requirements.txt omits jupyter/ipykernel — added them so its kernel works.
- ch06 system binaries (tesseract, poppler) already present via brew.
- Removed the earlier root `.venv`; kernels are per-chapter now. `.venv/` git-ignored. Verified all 17 kernels import ipykernel + anthropic.

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
