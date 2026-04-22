# Gemini AG handoff

이 문서는 Gemini terminal workflow를 **AG가 대신 셋업하거나 검증할 때**
바로 전달할 수 있는 handoff 문서다.

핵심 목적:

- import한 `superpowers` fork를 Gemini에서 안전하게 재사용하게 만든다
- upstream의 핵심 가치(설계 → 계획 → 최소 변경 구현 → 검증)를 유지한다
- Gemini CLI 기준으로 실제 설치/링크/검증 순서를 짧게 전달한다

---

## Quick start

AG에게 아래 순서로 요청하면 된다.

1. 이 fork repo를 연다.
2. `adapters/gemini/GEMINI_PROMPT.md` 를 먼저 읽게 한다.
3. `GEMINI.md` 와 `gemini-extension.json` 을 확인하게 한다.
4. 필요하면 로컬 path 기반으로 Gemini extension을 link 하게 한다.
5. 실제 Gemini CLI로 최소 검증을 수행하게 한다.

---

## Handoff block

아래 블록은 **그대로 복붙용**이다.

```md
Read `adapters/gemini/GEMINI_PROMPT.md` first and use it as the operating contract for this Gemini setup task.

You are setting up Gemini terminal workflow reuse for the imported fork of `obra/superpowers`.

Important constraints:
- Preserve the reusable core value: design before implementation, minimum-change execution, explicit verification.
- Treat upstream skill files as workflow references, not Claude-only executable commands.
- Respect existing repository structure.
- Do not guess; if a capability is missing, say so clearly.
- Prefer additive setup and verification over rewriting upstream files.

Please inspect these files first:
- `adapters/gemini/GEMINI_PROMPT.md`
- `GEMINI.md`
- `gemini-extension.json`
- `docs/migration/IMPORT_DECISION.md`
- `docs/migration/RUNTIME_VERIFICATION_2026-04-22.md`

Then do the following:
1. determine whether Gemini should use this repo via local extension link or plain workflow reuse
2. if local extension link is appropriate, run the safest Gemini command to link or validate it
3. verify the result with actual Gemini CLI commands
4. report only in these sections:
   - setup status
   - assumptions
   - commands run
   - verification result
   - remaining risk
```

---

## Recommended setup path

Gemini에서는 일반적으로 아래 순서가 가장 안전하다.

### Option A — local link

fork를 로컬에서 계속 다듬으면서 쓸 경우:

```bash
gemini extensions link C:\Users\sunwo\workspace\superpowers
gemini extensions list
gemini extensions validate C:\Users\sunwo\workspace\superpowers
```

### Option B — plain workflow reuse only

extension link 없이 prompt / workflow reference로만 쓸 경우:

- `GEMINI.md`
- `adapters/gemini/GEMINI_PROMPT.md`
- relevant `skills/**`

를 읽고 단일 세션 workflow로 사용한다.

---

## What AG should preserve

AG는 아래 가치를 깨지 말아야 한다.

- terminal-first execution
- no guessing
- minimum viable change first
- respect existing structure
- verification before completion

---

## What AG should not assume

다음은 그대로 가정하면 안 된다.

- Claude의 `Task` / `Skill` / `TodoWrite`가 Gemini에 그대로 있다는 가정
- Gemini가 subagent-driven-development를 그대로 지원한다는 가정
- upstream Claude test harness가 Gemini에서도 동일하게 동작한다는 가정

Gemini에서는:

- `GEMINI.md` 와
- `skills/using-superpowers/references/gemini-tools.md`

를 기준으로 tool mapping을 적용해야 한다.

---

## Done checklist

AG는 마지막에 최소한 아래를 보고해야 한다.

- setup status
- assumptions
- commands run
- verification result
- remaining risk

---

## Suggested first verification prompt

AG가 셋업 직후 실제 확인할 때는 예를 들어 아래처럼 검증하면 된다.

```md
What operating rules are active in this workspace? Answer as exactly five Korean bullet points.
```

이 질문에 아래 성격이 반영되면 baseline은 정상이다.

- terminal-first
- no guessing
- respect existing structure
- minimal viable change
- verify after changes
