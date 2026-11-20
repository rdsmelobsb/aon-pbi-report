# MEMORY

## Metadata

- Purpose: shared repo memory for durable conventions and recent task history.
- Required sections: `Metadata`, `Long-Term Memory`, `Detailed Task Events`.
- Current detailed day: `2026-10-26`.
- Compaction status: `2026-05-19` entries compacted on `2026-10-26`.

## Long-Term Memory

- Repo scope: this is the official skills catalog for `pbi-agent`, centered on skill folders under `skills/<skill-name>/` rather than application code.
- Skill format: each official skill uses `skills/<skill-name>/SKILL.md` with YAML frontmatter; `name` must match the directory slug and `description` should start with clear trigger language such as "Use when...".
- Skill authoring pattern: keep `SKILL.md` concise, move bulky detail into one-level-deep `references/`, and prefer focused skills over broad catch-all skills.
- Power BI guardrails to preserve when relevant: explicit measures, `_Measures` naming, protected auto-generated date tables, intentional visual placement, and correct PBIP metadata for imports, drillthrough, bookmarks, and visual schemas.
- Power BI references convention: files under `skills/powerbi/references/` should start directly with an H1, not YAML frontmatter.
- Canonical repository URL: `https://github.com/pbi-agent/skills`.
- Official artifact inventory:
- `skills/powerbi-audit/` exists as the official audit skill, with workflow and rule catalog references plus `assets/AUDIT-TODO.md`.
- `skills/research-lab/` exists as the generic staged research workflow skill, with artifact schemas, phase instructions, and domain-adaptation references.
- `skills/to-html/` exists as the official HTML artifact creation skill for standalone visual websites (concepts, ideas, decisions); it has no assets folder.
- `skills/rsi/` exists as the recursive self-improving loop skill (Evaluate, Diagnose, Generate, Train, Gate); its `SKILL.md` must keep the user-provided Mermaid loop diagram verbatim.
- `skills/to-html/SKILL.md` permits Mermaid via jsDelivr ESM CDN for non-confidential artifacts, with strict security defaults and literal unescaped HTML attribute quotes in copyable snippets.
- `skills/powerbi/references/init_report.md` documents the durable `init_report` bootstrap behavior.
- `skills/powerbi/assets/init_report_template/` stores the PBIP starter scaffold copied from the original template source.

## Detailed Task Events

## 2026-05-05 (compacted)

- Added and refined `skills/research-lab/`, including generic phase references, optional subagent orchestration, and review-driven cleanup; added `.gitignore` coverage for local `raw/` migration inputs. Validation included reference checks and `git diff --check`.

## 2026-05-08 (compacted)

- Added `skills/to-html/SKILL.md` and normalized the user-provided `skills/to_html/assets` folder to `skills/to-html/assets` for validator-compatible naming. Validation: `quick_validate.py` via `python3`, referenced asset path check, directory/name match check, and `git diff --check` passed. Next context: catalog README was left unchanged because the request was only to write the skill file.

## 2026-05-09 (compacted)

- Refined `skills/to-html/SKILL.md` trigger wording, Mermaid CDN guidance, and copyable snippet quoting; added README catalog coverage and a standalone Mermaid test artifact. Validation included `quick_validate.py` when present, static frontmatter/snippet checks, line count, and `git diff --check`.

## 2026-05-19 (compacted)

- Reworked `skills/to-html/` to user-need/adaptive-visual-first standalone websites, removed the assets/gallery workflow, and aligned README. Validation: frontmatter/name/line checks and `git diff --check`.

## 2026-10-26

- Added `skills/rsi/` (`SKILL.md` with the user's Mermaid loop diagram, `references/stages.md`, `references/artifacts.md`) and README catalog entry. Validation: frontmatter/name/reference checks, line count, and `git diff --check` passed.

## 2026-11-20

- Refactored AON_2024 PBIP model: completely removed legacy AdServer tables, measures, and 4 pages; reorganized skills into `.agents/skills/`; executed `powerbi-audit`, raising audit score from 73.2% (Grade C) to 95.2% (Grade A) by disabling auto date tables, removing 7 local date tables, adding `dataCategory: Time` to `DATA_DIM`, hiding 30 raw metric fact columns, grouping measures into display folders, adding descriptions, and ensuring safe DAX DIVIDE. Created interactive historical website `historia-do-modelo.html` for 2024, 2025, and 2026.
- Fixed TMDL syntax error: eliminated unsupported `description:` properties across all 12 `.tmdl` files and replaced them with official `///` doc comments.
- Sanitized creative dimension (`dCriativos`): implemented robust Power Query M sanitization function `fnSanitizarNome` stripping `(naugm...)` tracking suffixes, technical parentheses, platform numeric IDs, and resolutions (`1080x1080`, `1200x628`, etc.), replacing delimiters with spaces and applying proper case. Kept `Promoted post name` as hidden join key preserving relationship integrity with `REDES_FATO`, added friendly `Criativo` column, and updated visual `3f93139bd1a0e90d9152` projection in page `068c7c558f484bd8f2cd`. Fixed M expression error where `Text.Select` was passed a predicate function instead of character list/string; replaced with direct character replacement and native M filtering. Validation: 0 TMDL syntax errors, all report JSONs valid.
- Executed `/learn` consolidation: updated `skills/powerbi/references/tmdl_descriptions.md` with explicit anti-patterns preventing `description:` properties; created `skills/powerbi/references/power_query_guardrails.md` documenting `Text.Select` signatures, safe delimiters, and dimension cleansing; linked reference in `skills/powerbi/SKILL.md`; updated `AGENTS.md` Power BI hard guardrails. Validation: all reference links verified, files exist.
- Added Microsoft Fabric skills catalog from `microsoft/skills-for-fabric`: imported all 28 official Fabric skills into `.agents/skills/` (complete with `references/`, `scripts/`, `resources/`), populated shared `.agents/common/` core documentation (ensuring over 1,800 relative markdown links resolve), deployed agent definitions (`.agents/agents/`), MCP server configuration (`.mcp.json`), and setup scripts (`.agents/mcp-setup/`). Excluded APM package noise (`apm.yml`). Validation: 37 total skills validated (100% pass rate: `SKILL.md` present, frontmatter name matches slug, valid descriptions, 0 invalid skills).
- Implemented Design & UX Modernization (Opção 3 via `powerbi-report-cli`): produced formal `_brief/redesign-brief.md` contract; upgraded custom theme to `City Park Modernized` with WCAG AA contrast palette, Segoe UI Variable typography, 8px rounded borders, and zero shadows; transformed `Visão Geral` from 2,350px vertical scroll to a 16:9 Zero-Scroll Executive Summary (844px height) preserving all core KPI cards, hero line chart, column charts, pivot matrix, creative table, and interactive slicers; removed 24 redundant legacy background shape containers across `Visão Geral`, `CPM`, `CPV`, `CPC`, and `Receptivo`; enabled `One Page Mobile` vertical page for mobile devices; set `Visão Geral` as active default landing page. Validation: 132/132 JSON files valid, 0 broken interaction references, 0 TMDL errors.
- Initialized Git repository and published professional README.md: generated comprehensive `README.md` with badges, architecture overview, quality audit score, PBIP structure, and Fabric skills catalog; updated `.gitignore` for PBIP and local caches; initialized git repository on `main` branch and committed 645 files cleanly (`feat: initial commit of consolidated AON 2024 PBIP model and Fabric skills`).
