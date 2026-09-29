# D 김건우: stash/pop 실습 기록

## 1. 참여자 및 작업 정보
- 수행자: 김건우
- 대상 브랜치: `feature/gunwoo-stash-practice`
- 실습 도구: `git stash push` 및 `git stash pop`

## 2. 상황 및 재현 조건
- `src/practice/gunwoo-recovery.txt` 파일 작업 중 긴급하게 `main` 브랜치 상태를 확인해야 하는 상황 발생.
- 미완성 작업을 커밋하지 않고 안전하게 보관 후 복귀하고자 함.

## 3. 실행 절차 및 검증
1. 작업 변경점 확인 (보관 전 git diff 출력):
```text
(Step 5-7 3번에서 확인한 git diff 터미널 출력을 붙여넣으세요)
```
2. `git stash push -m "브랜치 전환 전 임시 보관" src/practice/gunwoo-recovery.txt` 실행
- `git stash list` 확인 출력:
```text
(Step 5-7 5번에서 확인한 git stash list 터미널 출력을 붙여넣으세요)
```
3. `git checkout main`으로 전환하여 메인 브랜치 확인 (`git status`: 깨끗함)
4. `git checkout feature/gunwoo-stash-practice`로 원래 작업 브랜치 복귀
5. `git stash pop` 실행하여 보관 내용 복원
- 복원 후 diff 일치 확인:
```text
(Step 5-7 8번에서 확인한 git diff 터미널 출력을 붙여넣으세요)
```
6. 복원 커밋: `git commit -am "feat: Restore stashed work after branch switching"`

## 4. 선택 이유 및 주의점
- 커밋할 수 없는 불완전한 상태의 코드를 안전하게 격리 보관할 수 있음.
- pop 시 충돌이 날 수 있으므로 보관 전후 파일 상태를 명확히 인지해야 함.