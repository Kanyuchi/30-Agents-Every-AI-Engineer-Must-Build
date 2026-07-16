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
- **Local run environment ready:** each `chapterNN/` has an isolated `.venv` (Python
  3.12) + a Jupyter kernel "30 Agents chapterNN (Claude)". A single git-ignored root
  `.env` holds the Claude key (`LLM_PROVIDER=anthropic`); dotenv's upward search means
  every chapter reads it. All 17 kernels verified importing ipykernel + anthropic.

## Incomplete / not done

- Shaun has not yet worked through the chapters himself (just acquired the book).
- No chapter notebook has been fully executed live on this machine yet (envs ready; ch05 next).
- **Known gotcha:** ch10/14/16 have a self-contradictory requirements set (base pins
  langchain-core 0.2.x, claude file pins langchain-anthropic>=0.3.0 which needs 0.3.x).
  Worked around by installing `langchain-anthropic>=0.1.15,<0.2` in those three envs.
- **Known gotcha:** the book pins `claude-sonnet-4-20250514` (retired 2026-06-15, now 404s).
  Migrated repo-wide to `claude-sonnet-5` (2026-07-16). Note: Sonnet 5 / Opus 4.7+ / Fable 5
  reject a `temperature` param — code that sets `temperature` must omit it for those models.
- Living documentation (`CLAUDE.md`, `session_log.md`, `whats_next.md`,
  `project_state.md`) bootstrapped 2026-07-15 — this is their first version.

## Locked-in decisions

- The commercial PDF stays **out of git** (`book/*.pdf` in `.gitignore`) — kept
  local only, for copyright + size reasons.
- `.gitignore` was repaired from a corrupted state (had a stray heredoc command
  written into it instead of executed).
- Repo is a personal copy under `Kanyuchi/…`; upstream is Packt's official repo.
