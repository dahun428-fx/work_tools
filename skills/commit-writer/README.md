# commit-writer

스테이징된 변경분(`git diff --staged`)을 읽고, **짧고 일관된 한 줄 커밋 메시지**를 만들어 커밋하는 [Claude Code](https://claude.com/claude-code) 스킬입니다.

## ✨ 메시지 형식

```
<영어 동사>: <한글 요약 ~30자>
```

```
Add: 로그인 입력값 검증 추가
Fix: 빈 장바구니 결제 오류 수정
Update: 회원가입 안내문구 변경
Remove: 안 쓰는 유틸 함수 삭제
```

- 앞머리는 변경 성격을 나타내는 **영어 동사**(Add/Fix/Update/Remove/Refactor/Docs/Test/Style/Chore)
- 요약은 **한글**, 약 30자 내외, 의미 중심 (파일명 나열 X)

## 📦 설치

```bash
npx skills add dahun428-fx/work_tools --skill commit-writer -g -a claude-code -y
```

npx를 쓸 수 없으면 이 폴더를 `~/.claude/skills/commit-writer`(개인 전역) 또는 `<프로젝트>/.claude/skills/commit-writer`(프로젝트 공유)에 복사합니다.

## 🚀 사용법

스테이징한 뒤 자연어로 요청하면 됩니다.

```bash
git add <변경한 파일>
```
```
"커밋해줘"      /  "이거 커밋 메시지 써줘"  /  /commit-writer
```

- 스테이징된 변경만 대상으로 커밋합니다. (임의로 `git add .` 하지 않음)
- 스테이징된 게 없으면 작업 내용을 보여주고 무엇을 스테이징할지 먼저 확인합니다.
- 무관한 변경이 섞여 있으면 나눠 커밋을 제안합니다.

자세한 동작 원칙은 [`SKILL.md`](./SKILL.md) 참고.
