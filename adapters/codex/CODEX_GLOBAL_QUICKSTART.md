# Codex global quickstart

이 문서는 `superpowers` fork를 **Codex 전역에서 어떻게 쓰는지** 아주 짧게 정리한 문서다.

현재 기준:

- 전역 skill discovery 연결 완료
- source of truth는 local fork
- 기존 `~/.codex/AGENTS.md` 는 건드리지 않음

---

## Current global setup

Codex는 현재 아래 junction을 통해 이 fork의 skills를 전역에서 읽는다.

```text
C:\Users\sunwo\.agents\skills\superpowers
=> C:\Users\sunwo\workspace\superpowers\skills
```

즉, `workspace/superpowers` 쪽 `skills/**` 변경은 Codex 전역 skill discovery에 반영된다.

---

## What was intentionally left alone

다음은 **의도적으로 유지**했다.

- `C:\Users\sunwo\.codex\config.toml`
- `C:\Users\sunwo\.codex\AGENTS.md`

이유:

- 기존 oh-my-codex 전역 환경을 깨지 않기 위해서다
- 이번 셋업은 **전역 AGENTS 덮어쓰기 없이 skill discovery만 추가**하는 방식이다

---

## How to start using it

가장 간단한 사용법:

1. Codex 새 세션을 연다
2. 필요한 skill 이름을 직접 말한다
3. 또는 task를 주면 `using-superpowers` discovery가 relevant skill을 찾게 한다

예:

```text
use brainstorming for this feature
```

```text
use test-driven-development for this bugfix
```

```text
use systematic-debugging for this failing test
```

---

## Most useful skills to start with

처음에는 아래부터 쓰는 게 좋다.

- `using-superpowers`
- `brainstorming`
- `writing-plans`
- `test-driven-development`
- `systematic-debugging`
- `verification-before-completion`

---

## How to verify the global setup

새 Codex 세션에서 아래처럼 물어보면 된다.

```text
If a discovered skill named using-superpowers is available in this session, reply FOUND. Otherwise reply MISSING.
```

또는 실전적으로는:

```text
use brainstorming before implementing this feature
```

라고 했을 때 relevant skill 흐름을 타면 정상이다.

---

## Expected behavior

전역 셋업이 정상이라면 Codex는 다음 성향을 따르기 쉬워진다.

- 먼저 설계/계획 여부를 판단
- 바로 코딩하지 않기
- 최소 변경 우선
- TDD / debugging / verification 문서를 workflow reference로 사용
- 완료 전에 실제 검증 수행

---

## Update path

이 전역 셋업의 실제 source는:

```text
C:\Users\sunwo\workspace\superpowers\skills
```

따라서 업데이트는 보통 이 fork에서 진행하면 된다.

---

## Safety note

전역 skill discovery가 연결되어 있어도:

- user instruction이 항상 우선이고
- project-local `AGENTS.md` / `GEMINI.md` / other local guidance가 더 구체적이면 그쪽이 우선한다

즉, 전역 셋업은 **기본 workflow layer** 이고, 프로젝트 문서가 더 구체적이면 그 문서를 따른다.
