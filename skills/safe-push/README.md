# safe-push

변경사항을 지정한 브랜치로 **검증 단계를 거쳐** 푸시하는 오케스트레이터 [Claude Code](https://claude.com/claude-code) 스킬입니다. 단순 `git push`가 아니라, 시크릿 유출·미검증 코드가 원격에 올라가는 걸 구조적으로 막습니다.

## ✨ 파이프라인

```
0. 브랜치 준비   — 없으면 생성, 있으면 전환
1. 시크릿 스캔   — secret-scan     발견 시 ❌ 중단
2. 테스트        — test-writer     실패/취약점 시 ❌ 중단
3. 커밋          — commit-writer   메시지 생성 + 커밋
4. 푸시          — 대상 브랜치로 push (신규면 -u)
```

각 단계는 **게이트**입니다. 앞 단계가 실패하면 다음으로 넘어가지 않고 멈춥니다.

## 📦 설치

`secret-scan`, `test-writer`, `commit-writer`가 함께 설치돼 있어야 파이프라인이 완전하게 동작합니다. 빠진 스킬이 있으면 실행 시 설치할지 묻고, 승인하면 자동으로 설치합니다.

```bash
# 권장: 네 개를 함께 설치
npx skills add dahun428-fx/work_tools --skill safe-push --skill secret-scan --skill test-writer --skill commit-writer -g -a claude-code -y
```

## 🚀 사용법

```
"feature/login 브랜치로 푸시해줘"
"변경사항 release/0.3 브랜치에 올려줘"
"이거 푸시해줘"        (대상 브랜치를 물어봅니다)
```

- 대상 브랜치가 없으면 현재 변경을 가진 채 새로 만듭니다(`git switch -c`).
- 시크릿 발견·테스트 실패 시 멈추고 이유를 보고합니다.
- 보호 브랜치 거부 등으로 푸시가 막히면 원인을 보여주고, 임의로 force-push 하지 않습니다.

자세한 동작은 [`SKILL.md`](./SKILL.md) 참고.
