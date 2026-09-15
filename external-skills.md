# 외부 스킬 카탈로그

직접 만들지 않았지만 자주 쓰는 외부 스킬 목록이다. **2026-09-15 기준으로 원본 저장소와 대조했다.** 스킬 본문은 이 저장소에 복사하지 않고 **원본 저장소에서 설치**한다. 원본이 업데이트되면 `npx skills update`로 따라간다.

> 스킬은 에이전트의 전체 권한으로 실행된다. 처음 설치하는 스킬은 SKILL.md를 먼저 읽어 보고 설치한다.
>
> 원본 저장소에서 스킬 이름이 바뀌거나 삭제될 수 있다. 설치가 `No matching skills found`로 실패하면 `npx skills add <저장소> --list`로 현재 이름을 확인하고 이 문서를 고친다.

## AI가 이 문서를 쓰는 방법

1. 사용자의 요청에 맞는 스킬을 아래 표의 "언제 쓰나" 열에서 찾는다.
2. `~/.claude/skills/<스킬>/SKILL.md` 또는 프로젝트 `.claude/skills/<스킬>/SKILL.md`가 있는지 확인한다.
3. 없으면 사용자에게 설치할지 한 번 묻고, 승인하면 해당 절의 설치 명령을 실행한다. 설치한 뒤에는 SKILL.md를 읽고 이어서 진행한다.

## 설치 명령 형식

```bash
# 한 개 설치 (전역, Claude Code, 확인 프롬프트 생략)
npx skills add <저장소> --skill <스킬> -g -a claude-code -y

# 저장소에 어떤 스킬이 있는지 보기
npx skills add <저장소> --list
```

---

## 1. addyosmani/agent-skills

개발 전 과정(명세 → 계획 → 구현 → 테스트 → 리뷰 → 배포)을 단계별로 나눈 엔지니어링 스킬 모음.
원본: https://github.com/addyosmani/agent-skills

```bash
# 방법 A. Claude Code 플러그인으로 전체 설치 (/build /plan /review /ship /spec /test 명령 포함)
/plugin marketplace add addyosmani/agent-skills
/plugin install agent-skills@addy-agent-skills

# 방법 B. 필요한 스킬만
npx skills add addyosmani/agent-skills --skill <스킬> -g -a claude-code -y
```

| 스킬 | 언제 쓰나 |
|---|---|
| `using-agent-skills` | 이 묶음의 스킬 중 무엇을 언제 쓸지 안내가 필요할 때 |
| `idea-refine` | 막연한 아이디어를 발산·수렴하며 다듬을 때 |
| `spec-driven-development` | 새 기능·프로젝트를 코딩 전에 명세부터 잡을 때 |
| `planning-and-task-breakdown` | 명세를 순서가 있는 작은 작업 단위로 쪼갤 때 |
| `api-and-interface-design` | REST/GraphQL API, 모듈 경계, 타입 계약을 설계할 때 |
| `incremental-implementation` | 여러 파일에 걸친 변경을 작게 나눠 구현할 때 |
| `test-driven-development` | 로직 구현·버그 수정을 테스트로 증명하며 진행할 때 |
| `source-driven-development` | 공식 문서를 근거로 프레임워크 코드를 작성할 때 |
| `frontend-ui-engineering` | 실서비스 수준의 UI 컴포넌트·레이아웃을 만들 때 |
| `browser-testing-with-devtools` | Chrome DevTools MCP로 DOM·콘솔·네트워크를 실제 브라우저에서 확인할 때 |
| `debugging-and-error-recovery` | 테스트 실패·빌드 깨짐 등 원인을 체계적으로 찾을 때 |
| `code-review-and-quality` | 머지 전 정확성·가독성·구조·보안·성능 5축 리뷰 |
| `code-simplification` | 동작은 그대로 두고 코드를 읽기 쉽게 정리할 때 |
| `performance-optimization` | 성능 요구사항이 있거나 Core Web Vitals·로딩 시간을 개선할 때 |
| `security-and-hardening` | 사용자 입력·인증·외부 연동을 다루는 코드를 보강할 때 |
| `git-workflow-and-versioning` | 브랜치·커밋·충돌 해결 방식을 정리할 때 |
| `ci-cd-and-automation` | 빌드·배포 파이프라인과 품질 게이트를 구성할 때 |
| `documentation-and-adrs` | 아키텍처 결정(ADR)과 공개 API 변경을 문서로 남길 때 |
| `deprecation-and-migration` | 오래된 시스템·API를 걷어내거나 이관할 때 |
| `context-engineering` | 세션 시작, 출력 품질 저하 시 규칙 파일·컨텍스트를 정비할 때 |
| `shipping-and-launch` | 프로덕션 배포 전 체크리스트·모니터링·롤백 계획을 세울 때 |

## 2. mattpocock/skills

인터뷰형 설계 검토, 명세·티켓 흐름, TDD 등 실무 흐름 중심 스킬.
원본: https://github.com/mattpocock/skills (2026-09-04 커밋 `3cca18b` 기준으로 확인)

```bash
# 방법 A. Claude Code 공식 마켓플레이스 플러그인 (원본 README 권장 · 스킬 25개 묶음 · 자동 업데이트)
claude plugins install mattpocock-skills        # 세션 안에서는 /plugin install mattpocock-skills

# 방법 B. 필요한 스킬만 파일로 복사 (수정 가능 · npx skills update로 갱신)
npx skills add mattpocock/skills --skill <스킬> -g -a claude-code -y
```

A와 B를 둘 다 쓰면 같은 스킬이 두 번 설치된다. 하나만 고른다. 어느 쪽이든 설치 후 저장소마다 `/setup-matt-pocock-skills`를 한 번 실행한다.

| 스킬 | 언제 쓰나 |
|---|---|
| `grill-me` | 계획·설계를 질문 하나씩 끝까지 파고들어 검증받고 싶을 때 |
| `grill-with-docs` | 위와 같되 CONTEXT.md·ADR 같은 기존 문서와 대조하며 문서도 갱신할 때 |
| `prototype` | 설계를 확정하기 전에 버리는 프로토타입(터미널 앱 또는 UI 시안 여러 개)을 만들 때 |
| `to-spec` | 지금까지의 대화를 명세로 정리해 이슈 트래커에 올릴 때 |
| `to-tickets` | 계획·명세를 선후 관계가 표시된 티켓 단위로 쪼개 트래커에 올릴 때 |
| `triage` | 이슈·외부 PR을 분류·검증하고 에이전트가 바로 작업할 수 있는 요약으로 정리할 때 |
| `tdd` | red-green-refactor 루프로 기능 구현·버그 수정 |
| `diagnosing-bugs` | 재현 → 축소 → 가설 → 계측 → 수정 → 회귀 테스트 순으로 어려운 버그·성능 저하를 잡을 때 |
| `improve-codebase-architecture` | 모듈 구조 개선 기회를 찾아 HTML 보고서로 보고, 고른 항목을 인터뷰로 파고들 때 |
| `handoff` | 현재 대화를 다른 에이전트가 이어받을 수 있게 인계 문서로 압축할 때 |
| `writing-for-agents` | 스킬·AGENTS.md·CLAUDE.md처럼 에이전트가 읽는 문서를 쓰거나 고칠 때 |
| `setup-matt-pocock-skills` | 위 엔지니어링 스킬을 처음 쓰기 전에 이슈 트래커·라벨·문서 위치를 설정할 때 |

플러그인(방법 A)에는 위 표 외에 `ask-matt`(어떤 스킬을 쓸지 안내), `code-review`, `research`, `domain-modeling`, `codebase-design`, `wayfinder`, `implement`, `resolving-merge-conflicts`, `wizard`, `grilling`, `teach`, `to-questionnaire`, `wait-what`이 함께 들어 있다.

**원본에서 바뀐 이름** — 예전에 설치한 사본에는 옛 이름이 남아 있을 수 있다.

| 옛 이름 | 현재 | 변경 커밋 |
|---|---|---|
| `diagnose` | `diagnosing-bugs` | 2026-06-12 `221ffca` |
| `to-prd` | `to-spec` | 2026-07-08 `386d4ff` |
| `to-issues` | `to-tickets` | 2026-07-08 `386d4ff` |
| `write-a-skill` | `writing-for-agents` | 2026-06-17 `bc4cf90`(→ writing-great-skills), 2026-07-31 `1fc6573` |
| `zoom-out` | 삭제 (대체 없음) | 2026-06-17 `e112a6b` |
| `caveman` | 삭제 (대체 없음) | 2026-06-12 `7d3ada9` |

## 3. google/agents-cli

Google ADK(Agent Development Kit)로 에이전트를 만들고 배포하는 스킬 묶음.
원본: https://github.com/google/agents-cli

```bash
npx skills add google/agents-cli --skill <스킬> -g -a claude-code -y
```

| 스킬 | 언제 쓰나 |
|---|---|
| `google-agents-cli-workflow` | ADK 에이전트 개발 전체 흐름의 진입점 (항상 먼저) |
| `google-agents-cli-scaffold` | 새 ADK 프로젝트 생성, CI/CD·배포 구성 추가 |
| `google-agents-cli-adk-code` | 에이전트·도구·콜백·상태 관리 코드 작성 |
| `google-agents-cli-eval` | 평가 데이터셋 작성, LLM-as-judge 평가 실행·실패 분석 |
| `google-agents-cli-deploy` | Agent Runtime·Cloud Run·GKE 배포, 시크릿, 롤백 |
| `google-agents-cli-publish` | Gemini Enterprise / Agent Registry에 에이전트 등록 |
| `google-agents-cli-observability` | Cloud Trace·로깅·BigQuery 분석 등 운영 모니터링 |

## 4. Vercel

원본: https://github.com/vercel-labs/skills , https://github.com/vercel-labs/agent-skills

```bash
npx skills add vercel-labs/skills --skill find-skills -g -a claude-code -y
npx skills add vercel-labs/agent-skills --skill <스킬> -g -a claude-code -y
```

| 스킬 | 저장소 | 언제 쓰나 |
|---|---|---|
| `find-skills` | vercel-labs/skills | "이런 걸 해주는 스킬 있어?"처럼 설치할 스킬을 찾을 때 |
| `vercel-react-best-practices` | vercel-labs/agent-skills | React·Next.js 코드를 성능·패턴 기준으로 작성·리뷰할 때 |
| `web-design-guidelines` | vercel-labs/agent-skills | UI 코드의 접근성·UX 가이드라인 준수 여부를 점검할 때 |

## 5. Anthropic

원본: https://github.com/anthropics/skills

```bash
npx skills add anthropics/skills --skill frontend-design -g -a claude-code -y
```

| 스킬 | 언제 쓰나 |
|---|---|
| `frontend-design` | 흔한 AI 느낌이 아닌, 완성도 높은 웹 페이지·컴포넌트를 디자인할 때 |

## 6. multica-ai/andrej-karpathy-skills

원본: https://github.com/multica-ai/andrej-karpathy-skills (구 forrestchang/andrej-karpathy-skills)

```bash
/plugin marketplace add https://github.com/multica-ai/andrej-karpathy-skills.git
/plugin install andrej-karpathy-skills@karpathy-skills
```

| 스킬 | 언제 쓰나 |
|---|---|
| `karpathy-guidelines` | 과한 추상화를 피하고 단순·명확한 코드를 쓰도록 코딩 원칙을 적용할 때 |
