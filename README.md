# action-first

**Claude Code가 답을 묻어버리지 않게 만드는 스킬.** 다음 행동부터 말하고, 단계는 번호를 매기고, "도움이 되었으면 좋겠습니다!"는 안 붙임.

Claude Code 전용입니다. 다른 하네스는 지원하지 않습니다.

## 설치

```bash
claude plugin marketplace add aciddust/action-first
claude plugin install action-first@action-first
```

## 사용

| 하고 싶은 것 | 방법 |
|---|---|
| 이번 세션에 켜기 | `/action-first` |
| 끄기 | `stop action-first` (또는 `normal mode`) |
| 항상 켜두기 | 아래 always-on 참고 |

스킬에는 `disable-model-invocation: true`가 걸려 있습니다. 직접 호출하기 전까지는 아무것도 적용되지 않습니다.

## always-on

매번 `/action-first`를 치기 귀찮으면 플래그 파일 하나만 만들면 됩니다.

```bash
touch ~/.claude/.action-first-always
```

이후 모든 세션 시작(`startup` / `resume` / `clear` / `compact`) 시점에 규칙 전문이 자동으로 주입됩니다.

끄려면 지우면 됩니다.

```bash
rm ~/.claude/.action-first-always
```

`CLAUDE_CONFIG_DIR`을 따로 쓰고 있다면 `~/.claude` 대신 그 경로에 만드세요.

## 규칙 10개

1. **다음 행동부터 시작** — 첫 줄은 바로 실행할 수 있는 것. 맥락도 계획도 아님
2. **여러 단계면 번호 매기기** — 한 단계에 한 동작
3. **끝은 구체적인 다음 행동 하나** — 2분 안에 할 수 있는 것으로
4. **곁가지 억제** — 두 번째 이슈는 첫 번째를 끝내고 따로 질문
5. **매 턴 상태 복기** — "5단계 중 3단계 완료"를 독자가 기억하게 두지 않음
6. **시간 추정은 구체적으로** — "좀 걸립니다" 대신 "테스트가 이미 있으면 15분"
7. **끝난 일은 눈에 보이게** — 이제 뭐가 되는지 구체적으로
8. **에러는 담담하게** — "앗 문제가 있네요" 금지. 원인과 해결책만
9. **긴 목록은 묶고 순위 매기기** — 그룹당 5개 목표. 표현 방식만 제한하고 분석은 제한하지 않음
10. **서론·요약·맺음 인사 없음** — "좋은 질문이에요", "도움이 되었으면"

규칙을 깨야 하는 경우(설명 요청, 파괴적 작업 확인, 디버깅 교착, 진짜 모호함 등)는 [`skills/action-first/SKILL.md`](skills/action-first/SKILL.md)에 정리되어 있습니다.

## 구조

```
.claude-plugin/     플러그인 · 마켓플레이스 메타데이터
skills/action-first/SKILL.md    규칙 전문
hooks/              always-on SessionStart 훅
```

## 크레딧

[ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd)에서 아이디어와 초기 규칙셋을 가져왔습니다. 원저작자에게 감사드립니다.

이 저장소는 Claude Code 한 곳만 지원하도록 범위를 좁히고 독자적인 방향으로 발전시키기 위해 분리되었습니다.

## 라이선스

MIT. [LICENSE](LICENSE) 참고 — 원저작권 표기를 포함하고 있습니다.
