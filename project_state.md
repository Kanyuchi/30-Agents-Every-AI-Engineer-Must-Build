# Project State

_Last updated: 2026-07-15_

## Working

- Full companion codebase for all 16 chapters (30 agents) is present and committed.
- Notebooks are pre-executed across five provider variants and browse on GitHub.
- Recent history shows provider notebooks re-run against **live** APIs (OpenAI,
  Anthropic, Google) — MockLLM replaced with real provider calls in 37 notebooks
  and all 68 provider notebooks re-run with live keys.
- Errata section + corrected figures (1.3, 1.5, 1.14) added.
- The book PDF is stored locally at `book/` and git-ignored (~84 MB, copyrighted).

## Incomplete / not done

- Shaun has not yet worked through the chapters himself (just acquired the book).
- No chapter run/verified locally on this machine yet.
- Living documentation (`CLAUDE.md`, `session_log.md`, `whats_next.md`,
  `project_state.md`) bootstrapped 2026-07-15 — this is their first version.

## Locked-in decisions

- The commercial PDF stays **out of git** (`book/*.pdf` in `.gitignore`) — kept
  local only, for copyright + size reasons.
- `.gitignore` was repaired from a corrupted state (had a stray heredoc command
  written into it instead of executed).
- Repo is a personal copy under `Kanyuchi/…`; upstream is Packt's official repo.
