# D 김건우: stash/pop 실습 기록

## 1. 참여자 및 기록 범위
- 담당 팀원·요청자: 김건우 (`papawolf42`)
- 이번 실행·기록 작성: 사용자의 요청으로 Codex가 별도 복제본에서 Git 명령을 직접 실행함.
- 재실습 시작 시각: 2026-09-29T20:16:29+09:00 (KST)
- 재실습 브랜치: `feature/gunwoo-stash-evidence-fix`
- 출발 커밋: `f25c75c7e9137451ee5d3291b01c20e2d19b3997`
- 보완 PR: [#33](https://github.com/beatles12/codyssey-b2-2-gitflow/pull/33)
- 보완 이슈: [#32](https://github.com/beatles12/codyssey-b2-2-gitflow/issues/32)
- 기존 실습: [이슈 #15](https://github.com/beatles12/codyssey-b2-2-gitflow/issues/15), [PR #18](https://github.com/beatles12/codyssey-b2-2-gitflow/pull/18)

기존 문서에는 보관 전 diff, stash 목록, 복원 후 diff의 실제 출력이 빠져 있었다. 아래는 **이번에 새로 실행하여 수집한 기록**이다. 과거 실행 출력의 복원이나 김건우가 직접 입력한 기록으로 주장하지 않는다.

## 2. 상황과 재현 조건
`src/practice/gunwoo-recovery.txt`를 수정하던 중 main을 확인해야 하는 상황을 재현했다. 작업 도중인 내용을 커밋하지 않고 stash에 보관하고, main을 확인한 뒤 원래 브랜치로 돌아와 pop으로 복원했다.

별도 복제본에서 수정 파일과 기존 stash가 없는 것을 확인하고 시작했다. 파일에 아래 한 줄을 UTF-8로 추가했다. 기존 두 줄은 유지했다.

```text
stash 재실습: 미완성 작업을 보관한 뒤 브랜치 복귀 시 복원한다.
```

## 3. 실제 명령과 출력
다음은 실행 순서대로 수집한 stdout/stderr이다. 모든 명령의 종료 코드는 0이다. `(출력 없음)`은 빈 출력을 설명하기 위한 표기이다. 로그에서 `origin/main`을 추적한다고 나오는 것은 실습 브랜치를 그 지점에서 만들었기 때문이며, main에 push했다는 뜻이 아니다.

### 1. `git status --porcelain`

```text
(출력 없음)
```

### 2. `git stash list`

```text
(출력 없음)
```

### 3. `git checkout -b feature/gunwoo-stash-evidence-fix origin/main`

```text
Switched to a new branch 'feature/gunwoo-stash-evidence-fix'
branch 'feature/gunwoo-stash-evidence-fix' set up to track 'origin/main'.
```

### 4. `git rev-parse HEAD`

```text
f25c75c7e9137451ee5d3291b01c20e2d19b3997
```

### 5. `git diff -- src/practice/gunwoo-recovery.txt`

```text
diff --git a/src/practice/gunwoo-recovery.txt b/src/practice/gunwoo-recovery.txt
index bb2fc6a..3ea155a 100644
--- a/src/practice/gunwoo-recovery.txt
+++ b/src/practice/gunwoo-recovery.txt
@@ -1,2 +1,3 @@
 stash 복구 비교용 기준 내용
 작업 중이던 미완성 추가 라인
+stash 재실습: 미완성 작업을 보관한 뒤 브랜치 복귀 시 복원한다.
```

### 6. `git stash push -m stash-rerun-before-branch-switch -- src/practice/gunwoo-recovery.txt`

```text
Saved working directory and index state On feature/gunwoo-stash-evidence-fix: stash-rerun-before-branch-switch
```

### 7. `git stash list`

```text
stash@{0}: On feature/gunwoo-stash-evidence-fix: stash-rerun-before-branch-switch
```

### 8. `git rev-parse stash@{0}`

```text
b36412b029fa68eaa0319dcd7f81b6c3e14c9538
```

### 9. `git status --porcelain`

```text
(출력 없음)
```

### 10. `git checkout main`

```text
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
```

### 11. `git status --short --branch`

```text
## main...origin/main
```

### 12. `git checkout feature/gunwoo-stash-evidence-fix`

```text
Switched to branch 'feature/gunwoo-stash-evidence-fix'
Your branch is up to date with 'origin/main'.
```

### 13. `git stash pop`

```text
On branch feature/gunwoo-stash-evidence-fix
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   src/practice/gunwoo-recovery.txt

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (b36412b029fa68eaa0319dcd7f81b6c3e14c9538)
```

### 14. `git diff -- src/practice/gunwoo-recovery.txt`

```text
diff --git a/src/practice/gunwoo-recovery.txt b/src/practice/gunwoo-recovery.txt
index bb2fc6a..3ea155a 100644
--- a/src/practice/gunwoo-recovery.txt
+++ b/src/practice/gunwoo-recovery.txt
@@ -1,2 +1,3 @@
 stash 복구 비교용 기준 내용
 작업 중이던 미완성 추가 라인
+stash 재실습: 미완성 작업을 보관한 뒤 브랜치 복귀 시 복원한다.
```

### 15. `git stash list`

```text
(출력 없음)
```

### 16. `git diff --check`

```text
(출력 없음)
```

## 4. 전후 비교 검증
- stash 직후 파일 바이트가 실습 전 기준 파일과 같은지 확인: 통과.
- main으로 이동한 뒤 파일 바이트가 기준 파일과 같은지 확인: 통과.
- 보관 전과 pop 후 `git diff` 전체 문자열 비교: 같음.
- 보관 전 파일 SHA-256: `28f42c487485130ee3b658dfbfa4fdfe443f0c8a4e96f07fbee6c270065c32a3`
- 복원 후 파일 SHA-256: `28f42c487485130ee3b658dfbfa4fdfe443f0c8a4e96f07fbee6c270065c32a3`
- 위 비교는 실행 스크립트가 파일 바이트와 diff를 읽어 직접 검사한 결과다. Git 명령의 출력으로 꾸민 문장이 아니다.
- pop 후 `git stash list`: 출력 없음. 이번 보관 항목이 제거됨.
- `git diff --check`: 출력 없음, 종료 코드 0.
- 실제 stash 객체: `b36412b029fa68eaa0319dcd7f81b6c3e14c9538`. pop 후 제거된 로컬 stash이며, GitHub에서 조회 가능한 커밋 링크로 취급하지 않는다.

## 5. 결과와 선택 이유
미완성 변경 한 줄이 main 작업 공간에서는 사라지고, 원래 브랜치에서 pop한 뒤 정확히 복원됐다. 복원된 한 줄은 이번 보완 PR의 `src/practice/gunwoo-recovery.txt` 변경에 포함한다.

쉬운 설명: **stash는 잠시 넣어 두는 서랍, pop은 꺼내서 작업으로 돌려놓는 동작**이다. 이번에는 커밋을 취소하려는 상황이 아니라 미완성 작업을 잠시 치워야 해서 stash를 선택했다. `reset`이나 `revert`는 필요하지 않았다.

## 6. 주의점
- stash는 로컬에 보관되므로 일반 push만으로 팀원에게 전달되지 않는다. 따라서 실제 출력을 문서로 남긴다.
- pop 중 충돌이 나면 자동으로 완료됐다고 간주하지 말고 상태와 파일을 확인한다.
- 이번에는 추적 중인 파일 하나만 지정했다. 새 파일까지 보관하려면 별도로 `-u` 사용 여부를 판단한다.
- 다른 사용자의 stash나 진행 중인 변경을 건드리지 않도록 별도 복제본을 사용했다.
- 이 기록은 도구 실행 증빙이다. 학습자가 stash의 이유와 동작을 직접 설명할 수 있는지는 별도로 확인해야 한다.
