# 충돌 3: 파일 삭제와 내용 수정

## 1. 참여자 및 재현 조건
- 삭제: 조은익 / 수정 및 해결: 김건우
- 대상 파일: `src/practice/sync-timing.md`
- 공통 기준 SHA: fd69265bc0dc394c5b6de84c8a38dbc5b66ded0e
- 병합 직전 김건우 HEAD: ec5e025eaf9353289ccccd3fce29c589eb9b63fd
- 병합 직전 origin/main: f721723200224b5f3fd5b35ce2dad3e2417fa1e7
- 삭제 PR: https://github.com/beatles12/codyssey-b2-2-gitflow/pull/21
- 수정·해결 PR: (https://github.com/beatles12/codyssey-b2-2-gitflow/pull/22)

## 2. 상황 및 재현 절차
1. 같은 공통 기준에서 두 브랜치를 만들었다.
2. 조은익이 `git rm src/practice/sync-timing.md`로 삭제하고 PR을 먼저 병합했다.
3. 김건우는 삭제 전 기준의 같은 파일에 확인 항목을 추가하고 커밋했다.
4. 김건우 브랜치에서 `git fetch origin`, `git merge origin/main`을 실행했다.

## 3. 실제 충돌 출력
### git merge origin/main
```text
PS C:\Users\alsgu\Dev\Codyssey\codyssey-b2-2-gitflow> git merge origin/main
CONFLICT (modify/delete): src/practice/sync-timing.md deleted in origin/main and modified in HEAD.  Version HEAD of src/practice/sync-timing.md left in tree.
```
### 해결 전 git status --short
```text
PS C:\Users\alsgu\Dev\Codyssey\codyssey-b2-2-gitflow> git status --short
UD src/practice/sync-timing.md
```
- 문장 충돌 마커 유무: 없음. 수정한 파일이 남아 있어도 삭제 여부는 미해결 상태였음.

## 4. 판단과 해결 결과
- 삭제하려던 이유: 짧은 실습 문서여서 삭제하려 함.
- 유지할 필요성: PR 병합 전에 계속 쓸 수 있으니 파일을 남기는게 좋아보임.
- 합의한 결정: 파일을 유지하고 확인 항목을 보존한다.
- 해결 명령: `git add src/practice/sync-timing.md`
- 미해결 파일 확인: `git diff --name-only --diff-filter=U`에 출력 없음.
### git add 후 git status
```text
PS C:\Users\alsgu\Dev\Codyssey\codyssey-b2-2-gitflow> git status
On branch feature/gunwoo-keep-guide
Your branch is up to date with 'origin/feature/gunwoo-keep-guide'.

All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)
```

## 5. 배운 점과 주의점
- 삭제/수정 충돌은 문장 충돌 마커가 없어도 발생한다.
- 삭제 이유와 수정 내용의 필요성을 확인하고 파일을 유지할지 결정해야 한다.
- `git add`로 해결을 표시한 뒤에도 머지 커밋을 만들어야 병합이 끝난다.