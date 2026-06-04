# Progressive Investment Research

Progressive Investment Research is an agent skill for maintaining a long-running research dossier.

It is not a report generator. Its core job is to keep one recoverable research model current: what we believe now, what evidence supports it, what is still uncertain, what would change the view, and which files are the canonical source of truth.

## What This Skill Does

- Builds a lightweight Markdown dossier for a research topic.
- Keeps `current-synthesis.md` as the human recovery entry point.
- Uses `model-map.md`, `modules/`, `models/`, `open-questions.md`, and `update-log.md` to separate conclusions, evidence, calculations, and state.
- Treats numbers, assumptions, formulas, source quality, and permission boundaries as first-class research objects.
- Supports investment, industry, company, technology, and thematic research where the question evolves over time.

## Public Version Dependency Model

The public version is designed to work without private or local-only tools.

Core functionality only requires:

- An agent runtime that can read and write files.
- Python 3.10+ for the optional helper scripts in `scripts/`.

Optional accelerators:

- Web search or browser tools for public-source discovery.
- URL extraction tools for known web pages.
- PDF, Office, or spreadsheet parsers for user-provided files.
- Local tools such as AnySearch, web-access, markitdown, pdf/docx/xlsx/pptx skills, or RSS pipelines.

When an optional accelerator is missing, use the agent runtime's available search, browser, URL fetch, or file-reading capability. The fallback rule is simple: capture the source, mark its quality and permission status, and do not promote snippets or secondary material directly into the model.

## Install

Copy this directory into your agent's skill/plugin directory, or point the runtime at this folder if it supports local skill loading.

For Codex-style skill loading, the folder contains:

- `SKILL.md`
- `.codex-plugin/plugin.json`
- `references/`
- `templates/`
- `scripts/`

For Claude-style loading, the folder also contains:

- `.claude-plugin/plugin.json`
- `agents/`

## Quick Start

Create a new dossier:

```powershell
python scripts/scaffold_dossier.py "./my-topic" --title "My Topic"
```

Validate the dossier:

```powershell
python scripts/validate_dossier.py "./my-topic" --strict
```

Print a simple dossier index:

```powershell
python scripts/regenerate_index.py "./my-topic" --stdout
```

## Dossier Shape

Minimum active surface:

- `context.md`: entry protocol, scope, and continuation notes.
- `current-synthesis.md`: current model and recovery entry point.
- `model-map.md`: research boundary, axes, modules, and open questions.
- `open-questions.md`: active / monitor / watchlist state index.
- `update-log.md`: model changes over time.
- `modules/`: evidence modules, concept modules, registries, and audits.

On demand:

- `models/`: calculation models and formula-backed reasoning.
- `companies/`: company watchlist cards.
- `data/`: canonical rows or CSVs used by models.
- `archive/`: non-default reading surface.

## Example Fixture

`fixtures/ai-industry-chain-mini/` is a small public fixture rebuilt from the structure of a real AI industry-chain research dossier. It is intentionally sanitized:

- It demonstrates the current contract.
- It uses public-style and illustrative content.
- It is not investment advice.
- It is not a full research database.

## Tests

Run the lightweight contract tests:

```powershell
python tests/test_contract.py
```

The tests use only Python's standard library.

## Release Boundary

Keep these in the public repository:

- `SKILL.md`
- `.codex-plugin/`
- `.claude-plugin/`
- `agents/`
- `references/`
- `scripts/`
- `templates/`
- `fixtures/`
- `evals/`
- `tests/`
- `README.md`
- `LICENSE`

Do not commit local dossiers, private materials, cache directories, generated reports, `.env` files, or bytecode caches.

## License

MIT. See `LICENSE`.
