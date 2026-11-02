# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

Demonstrations of LLM inference algorithms taken from research papers (e.g. decoding, sampling, and serving techniques), implemented as runnable Jupyter notebooks. The sibling repo `../llm-inference-notes` holds the user's written notes on the same papers; this repo is the code companion.

The repo is at the scaffold stage: the uv project (`pyproject.toml`, `uv.lock`) and the Zotero MCP config (`.mcp.json`) exist, but there are no notebooks or shared package yet. Update this file as the real structure appears.

## Tooling

- **Dependencies: `uv`.** Use `uv add <pkg>` / `uv add --dev <pkg>` and `uv sync`, not `pip`. Run things with `uv run ...`. Commit `pyproject.toml` and `uv.lock`.
- **Demo code: Jupyter notebooks.** Each algorithm or paper gets a notebook. Keep notebooks runnable top to bottom, and put code reused across notebooks in a small importable package rather than copy-pasting it.
- **Papers: Zotero via MCP**, same setup as `../llm-inference-notes`:
  - The `zotero` server is [zotero-mcp](https://github.com/54yyyu/zotero-mcp), configured in `.mcp.json` as `uvx --from 'zotero-mcp-server[semantic,pdf]' zotero-mcp serve` with `ZOTERO_LOCAL=true`, and exposed as `mcp__zotero__*` tools. `.mcp.json` is copied from the notes repo; each machine enables the server via `enabledMcpjsonServers` in the git-ignored `.claude/settings.local.json`.
  - It uses the Zotero local API, so the Zotero desktop app must be running with "Allow other applications on this computer to communicate with Zotero" enabled.
  - Use `zotero_semantic_search` for topic discovery and `zotero_search_items` for short author/title/year lookups. The semantic index is not auto-updated; refresh it with `zotero_update_search_database` after the user adds papers.
  - Treat Zotero as read-only unless the user asks otherwise.
- When implementing an algorithm from a paper, read the paper through Zotero first and cite it (citekey or title) in the notebook's intro cell. The matching note, if any, is in `../llm-inference-notes/notes/papers/<citekey>.md`.

## Commands

- `uv sync`: create `.venv` and install everything, including the dev group (JupyterLab, ipykernel, nbstripout, ruff).
- `uv run jupyter lab`: launch notebooks.
- `uv run ruff check .` / `uv run ruff format .`: lint and format.
- `uv run nbstripout --install`: one-time per clone, strips notebook outputs on commit (writes to `.git/config`).

No tests are defined yet, and nothing else is installed. Add ML dependencies (torch, transformers, etc.) with `uv add` as the first notebook needs them, and record how to run notebooks headlessly here once that matters.
