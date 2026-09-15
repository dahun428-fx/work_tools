# secret-scan

코드 변경분에서 **하드코딩된 비밀**(API 키·토큰·비밀번호·개인키·DB 접속정보)을 탐지해, 커밋/푸시 전에 유출을 막는 [Claude Code](https://claude.com/claude-code) 스킬입니다.

## ✨ 무엇을 하나

- 변경분의 **추가 라인**에서 자격증명을 탐지 (AWS/GCP 키, GitHub·Slack·Stripe 토큰, 개인키 블록, `password=...` 류 할당, 자격증명 포함 접속 URI 등)
- **오탐 제거** — `process.env.X`, `your_api_key` 같은 환경변수 참조·플레이스홀더는 통과
- 발견 값은 **마스킹**해서 위치·유형·위험도·개선점 보고
- 이미 푸시된 시크릿은 **폐기·재발급(rotate)** 권고

## 📦 설치

```bash
npx skills add dahun428-fx/work_tools --skill secret-scan -g -a claude-code -y
```

npx를 쓸 수 없으면 이 폴더를 `~/.claude/skills/secret-scan`(개인 전역) 또는 `<프로젝트>/.claude/skills/secret-scan`(프로젝트 공유)에 복사합니다.

## 🚀 사용법

```
"시크릿 스캔해줘"  /  "키 박힌 거 없나 봐줘"  /  /secret-scan
```

- 기본은 스테이징/작업 변경분을 점검합니다. 파일·디렉토리를 지정할 수도 있습니다.
- 발견 시 커밋/푸시를 멈추도록 권고합니다. `safe-push` 파이프라인의 1단계로도 호출됩니다.

자세한 동작은 [`SKILL.md`](./SKILL.md) 참고.
