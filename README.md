# work_tools

실무에서 쓰려고 만든 [Claude Code](https://claude.com/claude-code) 스킬 모음.

## 설치

```bash
# 원하는 스킬 하나 (전역 설치)
npx skills add dahun428-fx/work_tools --skill <스킬> -g -a claude-code -y

# 이 저장소의 스킬 전부
npx skills add dahun428-fx/work_tools --skill '*' -g -a claude-code -y

# 목록만 보기
npx skills add dahun428-fx/work_tools --list
```

스킬은 에이전트의 전체 권한으로 실행되므로 설치 전에 SKILL.md를 한 번 읽어 보길 권한다.

`npx`를 쓸 수 없으면 `skills/<스킬>` 폴더를 `~/.claude/skills/` 또는 프로젝트의 `.claude/skills/`에 복사한다.

## 스킬 목록

### 기획 문서

| 스킬 | 하는 일 | 의존 스킬 |
|---|---|---|
| [`product-spec`](skills/product-spec) | 기획서·PRD·정책 문서를 작성·검토한다. 본문은 비개발자 기준 일상어로, 기술 사실은 접히는 개발 상세 블록으로 분리한다 | 없음 |
| [`spec-tone`](skills/spec-tone) | 기획서·보고서의 AI스러운 문체(과한 비유, 근거보다 센 단정, 자기 해설)를 실무 담당자 어투로 고친다 | 없음 |
| [`grill-plan`](skills/grill-plan) | 붙여넣은 기획서를 질문 하나씩 검증하는 인터뷰를 진행하고, 확정된 결정을 계획 문서로 정리한다 | `grill-me` (선택, 외부) |

### 개발 흐름

| 스킬 | 하는 일 | 의존 스킬 |
|---|---|---|
| [`commit-writer`](skills/commit-writer) | 스테이징된 변경을 읽고 `영어 동사: 한글 요약` 한 줄 커밋을 만든다 | 없음 |
| [`secret-scan`](skills/secret-scan) | 변경분에서 하드코딩된 API 키·토큰·비밀번호를 찾아 마스킹해 보고한다 | 없음 |
| [`test-writer`](skills/test-writer) | 변경 코드와 영향 범위에 테스트를 작성·실행하고, 보안 케이스도 함께 점검한다 | 없음 |
| [`safe-push`](skills/safe-push) | 시크릿 스캔 → 테스트 → 커밋 → 푸시를 단계별 게이트로 실행한다 | `secret-scan`, `test-writer`, `commit-writer` (필수) |
| [`troubleshooting-harness`](skills/troubleshooting-harness) | 장애 제보를 재현 조건·확인 명령·해결 절차를 갖춘 트러블슈팅 문서로 만들어 `docs/troubleshooting/`에 저장한다 | `spec-driven-development` (선택, 외부) |

## 의존 스킬 자동 설치

의존 스킬이 있는 스킬은 SKILL.md에 `의존 스킬` 표가 있다. 표에는 설치 명령과 원본 URL이 들어 있다. AI는 실행 전에 의존 스킬이 설치됐는지 확인하고, 없으면 사용자 승인을 받은 뒤 표의 명령으로 설치하고 이어서 진행한다.

```markdown
## 의존 스킬

| 스킬 | 구분 | 없을 때 설치 명령 | 출처 |
|---|---|---|---|
| `secret-scan` | 필수 | `npx skills add dahun428-fx/work_tools --skill secret-scan -g -a claude-code -y` | https://github.com/dahun428-fx/work_tools/tree/main/skills/secret-scan |
```

새 스킬을 추가할 때 다른 스킬을 호출한다면 같은 형식의 표를 넣는다.

## 외부 스킬

직접 만들지 않았지만 함께 쓰는 외부 스킬은 [`external-skills.md`](external-skills.md)에 언제 쓰는지와 설치 명령을 정리했다.
