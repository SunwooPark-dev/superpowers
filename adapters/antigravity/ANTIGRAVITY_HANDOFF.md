# Antigravity handoff

이 문서는 Antigravity App에서 이 fork를 바로 재사용하기 위한 전달용 문서다.

목표는 간단하다:

- upstream `superpowers`의 핵심 가치(설계 → 계획 → 최소 변경 구현 → 검증)를 유지한다
- Claude 전용 plugin 가정은 제거한다
- Antigravity에서 바로 붙여 넣어 쓸 수 있는 handoff 블록을 제공한다

---

## Quick start

Antigravity에서 다음 순서로 시작한다.

1. 이 저장소를 Antigravity에서 연다.
2. `adapters/antigravity/ANTIGRAVITY_PROMPT.md` 파일을 컨텍스트로 첨부한다.
3. 아래 **handoff block** 을 그대로 붙여 넣는다.
4. 첫 응답에서 아래 형식으로만 답하게 한다.
   - goal
   - assumptions
   - files to inspect first
   - verification plan
   - first action

---

## Handoff block

아래 블록은 **그대로 복붙용**이다.

```md
Read the attached file `adapters/antigravity/ANTIGRAVITY_PROMPT.md` first and follow it as the operating contract for this session.

You are reusing the imported fork of `obra/superpowers` inside Antigravity App.

Important constraints:
- Treat upstream skill files as workflow references, not Claude-only executable instructions.
- Preserve the reusable core value: design before implementation, explicit assumptions, minimal changes, verification before completion.
- Do not rewrite unrelated upstream assets.
- Prefer additive changes under `adapters/` and `docs/migration/` unless a broader change is clearly justified.
- If ambiguity materially changes the output, stop and present interpretation options instead of guessing.

When useful, reuse these upstream workflow references:
- `skills/brainstorming/SKILL.md`
- `skills/writing-plans/SKILL.md`
- `skills/test-driven-development/SKILL.md`
- `skills/systematic-debugging/SKILL.md`
- `skills/verification-before-completion/SKILL.md`

Before doing any implementation work, respond in exactly these sections:
- goal
- assumptions
- files to inspect first
- verification plan
- first action
```

---

## Task handoff template

아래는 실제 작업을 붙일 때 쓰는 템플릿이다.

```md
Current task:
[여기에 실제 작업 요청]

Success criteria:
- [성공 조건 1]
- [성공 조건 2]

Constraints:
- minimize changes
- preserve existing structure
- no unnecessary refactors
- verify before completion
```

---

## Recommended Antigravity behavior

Antigravity 세션은 아래 순서를 따르는 것이 좋다.

1. **Evaluate before acting**
   - 지금 요청이 조사인지, 설계인지, 구현인지 먼저 판별
2. **State assumptions explicitly**
   - 애매한 전제는 명시
3. **Inspect only the most relevant files first**
   - 관련 없는 넓은 탐색 금지
4. **Make the smallest useful change**
   - 첫 수정은 최소 범위
5. **Verify before claiming completion**
   - 관련 명령/테스트/출력 확인

---

## What to reuse from Superpowers

Antigravity에서는 특히 아래 가치가 유효하다.

- 설계 없이 바로 구현하지 않기
- 작은 작업 단위로 쪼개기
- 테스트/검증 우선
- 디버깅 시 추측보다 증거 우선
- 완료 전 검증 강제

---

## What not to assume in Antigravity

다음은 Antigravity에서 그대로 가정하면 안 된다.

- Claude plugin marketplace 설치 흐름
- Claude의 `Skill` / `Task` 같은 동일 이름 도구
- Claude 전용 subagent dispatch 방식
- Claude 테스트 하네스가 바로 실행 가능하다는 전제

즉, Antigravity에서는:

- skill 문서를 **방법론 reference** 로 읽고
- 실제 실행은 Antigravity가 제공하는 방식으로 옮겨야 한다

---

## Done checklist

작업이 끝날 때는 최소한 아래가 보고되어야 한다.

- goal
- assumptions used
- files changed
- verification performed
- unresolved risk or manual follow-up

---

## Suggested use

가장 현실적인 첫 사용 방식은:

- Antigravity에 `ANTIGRAVITY_PROMPT.md` 첨부
- 이 문서의 handoff block 복붙
- 그 뒤 구체 작업 요청 추가

즉, 이 문서는 **Antigravity용 session bootstrap handoff** 다.
