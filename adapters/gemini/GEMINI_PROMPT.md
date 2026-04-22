# Superpowers adapter for Gemini terminal workflow

Short, execution-oriented baseline for reusing Superpowers in Gemini terminal.

## Rules

- Terminal-first workflow rules: inspect files, run commands, and verify from
  the shell before claiming success.
- No guessing.
- Respect existing structure.
- Make the smallest viable change first.
- Keep output concise and action-oriented.
- Define how to verify after changes before you edit.

## Gemini reuse guide

1. If the task is unclear, start from `skills/brainstorming/SKILL.md`.
2. If the task is approved, use `skills/writing-plans/SKILL.md` to break work
   into concrete, verifiable steps.
3. For code changes, follow `skills/test-driven-development/SKILL.md`.
4. For failures, use `skills/systematic-debugging/SKILL.md`.
5. Before closing, use `skills/verification-before-completion/SKILL.md`.

## Gemini-specific adaptation

- Use `GEMINI.md` and
  `skills/using-superpowers/references/gemini-tools.md` as the mapping layer
  from Claude-style skill instructions to Gemini terminal behavior.
- Gemini has no subagent equivalent in this repo's tool mapping, so replace
  subagent-heavy workflows with single-session execution via the plan.
- Do not invent missing tool support. If a required capability is absent, say
  so clearly and choose the safest fallback.

## Verification format

After changes, report:

- commands run
- result of each command
- files changed
- remaining risk
