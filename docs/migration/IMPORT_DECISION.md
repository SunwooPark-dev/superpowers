# Import Decision — obra/superpowers

Date: 2026-04-21
Source repository: `https://github.com/obra/superpowers`
Owning account: `https://github.com/SunwooPark-dev`

## Import decision

- **Overall verdict:** `partial_migration_needed`
- **Recommended import strategy:** `fork + clone`

## Why the repo was imported

This repository is worth importing because its core value is mostly reusable
workflow and documentation rather than Claude-only executable code. The
strongest reusable assets are the skills library (`skills/**`), harness
guidance (`docs/**`, `agents/**`), and cross-harness adaptation notes for
Codex and Gemini.

The repo is not `directly_usable` for all requested targets because:

- some assets are explicitly Claude-specific
- some workflows assume Claude-style tool names or subagent behavior
- Antigravity App support is not present upstream and needs a starter adapter

## Core value classification

- **Primary core value:** mixed, but weighted toward **workflow +
  documentation**
- **Code value:** secondary (plugin manifests, scripts, hook glue, test harness)

## What reusable value was preserved

The import preserves:

- design-before-implementation discipline
- explicit planning before execution
- test-driven development guidance
- systematic debugging guidance
- verification-before-completion expectations
- multi-harness documentation already present for Codex and Gemini

## Claude-specific elements removed or replaced

These were preserved in the fork for reference, but are not required for the
new multi-target baseline:

- `CLAUDE.md`
- `.claude-plugin/**`
- Claude-centric command assumptions inside some skill docs
- `tests/claude-code/**`
- Claude-oriented slash-command content in `commands/**`

Replacements used for this import:

- **Codex App** → `adapters/codex/AGENTS.md`
- **Antigravity App** → `adapters/antigravity/ANTIGRAVITY_PROMPT.md`
- **Gemini terminal workflow** → `adapters/gemini/GEMINI_PROMPT.md`

## Compatibility review summary

### Codex App

**Status:** compatible with light adaptation

Why:
- repo already includes `.codex/INSTALL.md`
- repo already includes `docs/README.codex.md`
- repo already includes `skills/using-superpowers/references/codex-tools.md`
- upstream design docs show active Codex compatibility work

Codex-friendly assets:
- `skills/**`
- `docs/README.codex.md`
- `.codex/INSTALL.md`
- `agents/**`
- `docs/superpowers/**`

Codex-specific caveats:
- some skills still speak in Claude tool names and need tool-mapping discipline
- subagent-heavy workflows depend on Codex multi-agent availability

### Antigravity App

**Status:** not supported upstream, but reusable via manual adapter

Why:
- no Antigravity-specific manifest, docs, or install path exists upstream
- the core methodology still transfers because it is mostly workflow text

Antigravity-reusable assets:
- `skills/brainstorming/SKILL.md`
- `skills/writing-plans/SKILL.md`
- `skills/test-driven-development/SKILL.md`
- `skills/systematic-debugging/SKILL.md`
- `skills/verification-before-completion/SKILL.md`

Antigravity-only additions:
- `adapters/antigravity/ANTIGRAVITY_PROMPT.md`

### Gemini terminal workflow

**Status:** compatible with light adaptation

Why:
- repo already includes `GEMINI.md`
- repo already includes `gemini-extension.json`
- repo already includes Gemini tool mapping guidance

Gemini-friendly assets:
- `GEMINI.md`
- `gemini-extension.json`
- `skills/using-superpowers/references/gemini-tools.md`
- most workflow skills that do not require subagents

Gemini-specific caveats:
- subagent-driven workflows need fallback to single-session execution

## What is shared across all 3 targets

- planning before implementation
- minimum-change bias
- TDD-oriented execution
- systematic debugging
- explicit verification before completion
- skill documents as reusable workflow references

## What is target-specific

### Only valid in one environment

- `.claude-plugin/**` → Claude-specific
- `.cursor-plugin/**` → Cursor-specific
- `.opencode/**` → OpenCode-specific
- `commands/**` → primarily Claude-style command UX
- `GEMINI.md`, `gemini-extension.json` → Gemini-specific
- `.codex/INSTALL.md`, `docs/README.codex.md` → Codex-specific

### Assets to preserve unchanged

- `skills/**`
- `agents/**`
- `docs/README.codex.md`
- `.codex/INSTALL.md`
- `GEMINI.md`
- `gemini-extension.json`
- `docs/superpowers/**`

### Assets to adapt

- adapter instructions for Codex App
- adapter prompt for Antigravity App
- adapter prompt for Gemini terminal workflow
- import notes describing cross-target reuse boundaries

### Assets to exclude from baseline reuse

Excluded from the starter workflow, but left intact in the fork:

- upstream PR workflow expectations
- Claude-only test harnesses
- Claude marketplace metadata as a required installation path

## Migration plan

Because the verdict is `partial_migration_needed`, the import proceeds with a
minimal additive adapter strategy.

### Core reusable assets

- `skills/**`
- `agents/**`
- `docs/superpowers/**`
- `docs/README.codex.md`
- `.codex/INSTALL.md`
- `GEMINI.md`
- `gemini-extension.json`

### Assets to preserve unchanged

- upstream workflow docs and skill content
- install docs already present for Codex and Gemini
- repository history and remote relationship to upstream

### Assets to adapt

- new adapter files under `adapters/`
- migration decision doc under `docs/migration/`

### Assets to exclude

- upstream-only contribution flow as a requirement for local use
- Claude-only commands/tests as mandatory execution dependencies

### Target-specific replacements

- Claude `Skill`/`Task` assumptions → Codex native skill discovery and tool
  mapping, or Gemini terminal mapping, or Antigravity prompt discipline
- Claude-only install path → target-local adapter entrypoints
- subagent-only flow → single-session fallback where the target lacks subagent
  support

### Minimal additive adapter strategy

1. Keep upstream structure intact.
2. Add only `adapters/**` and `docs/migration/**`.
3. Avoid rewriting upstream skills on first import.
4. Reuse upstream docs by reference rather than duplicating them.

### Verification checklist before commit

- fork exists under `SunwooPark-dev`
- clone exists locally
- `origin` points to the fork
- `upstream` points to `obra/superpowers`
- working branch is isolated from `main`
- required adapter files exist
- required phrases are present in each adapter
- `git diff --check` is clean

## How to use the repo in each target

### Codex App

1. Start from `adapters/codex/AGENTS.md`
2. Use `docs/README.codex.md` and `.codex/INSTALL.md` for native setup
3. Read the relevant `skills/**` document before implementation
4. Apply Codex tool mapping from
   `skills/using-superpowers/references/codex-tools.md`

### Antigravity App

1. Start from `adapters/antigravity/ANTIGRAVITY_PROMPT.md`
2. Treat `skills/**` as workflow reference documents
3. Replace missing Claude-specific mechanics with Antigravity-native behavior
4. Keep execution additive and verification-driven

### Gemini terminal workflow

1. Start from `adapters/gemini/GEMINI_PROMPT.md`
2. Reuse `GEMINI.md` and `gemini-extension.json` as Gemini-native context
3. Apply Gemini tool mapping from
   `skills/using-superpowers/references/gemini-tools.md`
4. Use single-session plan execution when a skill expects subagents
