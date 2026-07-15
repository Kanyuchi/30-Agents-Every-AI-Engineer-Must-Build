# CLAUDE.md — Project Instructions

## What this project is

Companion code repository for the book **30 Agents Every AI Engineer Must Build**
by Imran Ahmad, PhD (Packt Publishing, 2026 — ISBN 9781806109012). This is
Shaun's own fork/copy (`Kanyuchi/30-Agents-Every-AI-Engineer-Must-Build`),
used to read through and work the book's 30 agent architectures.

The book PDF itself lives in `book/` and is git-ignored — see `book/README.md`.

## Original Goal

Work through the book end-to-end: run each chapter's agent notebooks, understand
the 30 architectural patterns, and adapt the ones relevant to Shaun's own projects.

## Stack

| Layer | Choice |
|---|---|
| Language | Python 3.10+ |
| Format | Jupyter notebooks (one or more per chapter) |
| LLM providers | OpenAI, Anthropic (Claude), Google (Gemini), local Ollama, plus a no-key MockLLM |
| Provider abstraction | `supporting/llm_provider.py` |
| Deps | per-chapter `requirements.txt` + `requirements-<provider>.txt` |

## Layout

- `chapter01/` … `chapter16/` — one directory per chapter; each holds notebook(s),
  a README, per-provider requirements, and (for many) a `USECASE.md`.
- `supporting/` — shared helpers: `llm_provider.py`, env setup/verify scripts.
- `Errata/` + `ERRATA.md` — figure corrections for the printed book.
- `book/` — local (git-ignored) copy of the commercial PDF.
- `LLM_COMPARISON_SUMMARY.md` — head-to-head provider results across chapters.

## Key patterns

- Every chapter ships **five pre-executed notebook variants** (suffixes
  `__RUN_NO_KEY_SIMULATION`, `__RUN_OPENAI_GPT4o`, `__RUN_CLAUDE_Sonnet4`,
  `__RUN_GEMINI_Flash25`, `__RUN_LOCAL_OLLAMA_DeepSeek_V2_16B`). All produce
  equivalent pedagogical output with identical cell structure.
- API keys live in a per-chapter `.env` (copied from `.env.template`); set ONE of
  `OPENAI_API_KEY` / `ANTHROPIC_API_KEY` / `GOOGLE_API_KEY`. Never commit `.env`.
- Notebooks are committed pre-executed so they browse on GitHub without running.

## Working conventions

- Follow the global living-documentation + git-commit rules in `~/.claude/CLAUDE.md`.
- When building/adapting agents, default to the latest Claude models via the
  `claude-api` skill rather than answering LLM questions from memory.
