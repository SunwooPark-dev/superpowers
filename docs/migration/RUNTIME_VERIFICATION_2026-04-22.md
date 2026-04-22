# Runtime verification — 2026-04-22

Repository: `SunwooPark-dev/superpowers`
Branch: `sunwoo/multi-target-adapters`

## Goal

생성한 3개 adapter가 실제 런타임 진입점으로 최소한 유효한지 확인한다.

대상:

- Codex
- Antigravity
- Gemini

---

## Codex verification

### Method

- clean-room workspace 생성
- local `AGENTS.md`로 `adapters/codex/AGENTS.md` 배치
- `codex exec` 로 실제 응답 확인

### Result

- 성공
- Codex가 local `AGENTS.md`를 읽고 운영 규칙을 한국어 bullet로 요약함
- adapter의 핵심 규칙(사전 검토, 최소 구현, 필요한 변경만, 불필요한 리팩터링 금지, 검증 후 완료)이 실제 응답에 반영됨

### Evidence

- `C:\superpowers_runtime_verify_20260422\codex-local-agents.txt`

---

## Gemini verification

### Method

- clean-room workspace 생성
- local `GEMINI.md`로 `adapters/gemini/GEMINI_PROMPT.md` 배치
- `gemini -p` 비대화형 실행으로 실제 응답 확인
- 추가로 extension validate 실행

### Result

- 성공
- Gemini가 workspace guidance를 읽고 운영 규칙을 한국어 bullet로 요약함
- `gemini extensions validate` 도 통과

### Evidence

- `C:\superpowers_runtime_verify_20260422\gemini-last.txt`

---

## Antigravity verification

### Method

- adapter prompt가 있는 clean-room workspace 생성
- `antigravity chat` 로 새 세션 launch 시도
- `antigravity --status` 로 새 window/session 증가 여부 확인

### Result

- 부분 성공
- Antigravity App 설치/실행 가능
- adapter prompt 첨부를 포함한 새 chat session launch 확인
- 다만 CLI가 GUI 중심이라 모델 최종 응답 텍스트를 stdout/file로 자동 회수하는 검증은 불가

### Evidence

- `antigravity --help`
- `antigravity --status`
- session launch 후 window count 증가 확인

### Boundary

- Antigravity는 현재 구조상 **session launch까지는 자동 검증 가능**
- 하지만 **모델 응답 본문 자동 회수는 수동 eyeball check 필요**

---

## Overall status

- Codex: verified
- Gemini: verified
- Antigravity: launch verified, response capture manual

## Practical conclusion

이 fork와 adapter 구조는:

- Codex에서 바로 사용할 수 있고
- Gemini terminal workflow에서도 바로 사용할 수 있으며
- Antigravity에서는 handoff/prompt 기반 bootstrap으로 사용할 수 있다

Antigravity는 다음 단계로:

- `adapters/antigravity/ANTIGRAVITY_PROMPT.md`
- `adapters/antigravity/ANTIGRAVITY_HANDOFF.md`

를 함께 사용하면 된다.
