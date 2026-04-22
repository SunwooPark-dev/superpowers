# Superpowers adapter for Codex App

Use this file as a lightweight Codex-first operating contract when reusing the
imported Superpowers repository inside Codex App or Codex CLI.

## Purpose

Preserve the reusable core of Superpowers — design before implementation,
minimum-change execution, explicit verification, and disciplined workflow
selection — while removing assumptions that require Claude-only commands or
plugin behavior.

## Core operating rules

1. **Think before acting.** Review the task, current repo state, and the most
   relevant files before changing anything.
2. **Minimum viable implementation first.** Prefer the smallest change that
   proves the intended behavior.
3. **Only modify what is necessary.** Keep the diff narrow and additive.
4. **No unnecessary refactors.** Do not restructure unrelated code while
   delivering the requested outcome.
5. **Ask when uncertainty materially affects correctness.** If multiple
   interpretations would lead to different behavior, pause and resolve it.
6. **Verification before completion.** Run the strongest available checks that
   are relevant to the change and read the results before claiming success.

## How to reuse the imported Superpowers assets

- Start with `skills/brainstorming/SKILL.md` when the task is not yet
  decision-complete.
- Use `skills/writing-plans/SKILL.md` to turn an approved design into clear,
  verifiable task slices.
- Use `skills/test-driven-development/SKILL.md` for feature and bugfix work.
- Use `skills/systematic-debugging/SKILL.md` for failures and regressions.
- Use `skills/verification-before-completion/SKILL.md` before closing work.

## Codex-specific replacements

- Treat Claude-style tool names in skill docs as conceptual references.
- Prefer Codex-native workflow support documented in:
  - `docs/README.codex.md`
  - `skills/using-superpowers/references/codex-tools.md`
- When a skill expects subagents, use Codex multi-agent features only if they
  are available; otherwise keep execution single-session and preserve the same
  task boundaries.
- Use native planning/tracking facilities instead of Claude-only task helpers.

## Recommended Codex workflow

1. Review the request and identify the relevant Superpowers skill(s).
2. Read the corresponding skill document(s) before implementation.
3. Implement the smallest useful change.
4. Verify with targeted checks first, then broader checks if needed.
5. Summarize:
   - files changed
   - what was verified
   - remaining risks or manual follow-up

## Verification checklist

Before completion, confirm:

- The change is the minimum viable implementation.
- Only necessary files were modified.
- No unnecessary refactors were introduced.
- The strongest relevant verification available was run.
- Any remaining uncertainty or risk is called out explicitly.
