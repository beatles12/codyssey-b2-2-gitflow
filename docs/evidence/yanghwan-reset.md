# B 장양환: reset --soft 실습 기록

## 1. 참여자 및 작업 정보
- 수행자: 장양환
- 대상 브랜치: `feature/yanghwan-reset-practice`
- 실습 도구: `git reset --soft HEAD~1`

## 2. 상황 및 재현 조건
- 로컬 실습 파일을 커밋했으나 커밋을 취소하고 staged 상태를 유지한 채 재작업하고자 함.
- 아직 원격에 푸시하기 전이므로 로컬 히스토리만 안전하게 한 단계 롤백함.

## 3. 실행 명령 및 상태 변화
- 취소 대상 커밋 SHA: `ecdac5a`
- 실행 명령: `git reset --soft HEAD~1`
- 리셋 후 HEAD 위치: `b6a572a`
- 리셋 후 `git status --short`:
  ```text
  A  src/practice/yanghwan-recovery.txt
  ```
- 확인: 파일이 Staged Area에 온전히 보존되어 녹색 'A' 상태로 확인됨.
- 재커밋 SHA: `5bb0b18`
- 재커밋 명령: `git commit -m "feat: Record soft reset practice and preserve staged changes"`

## 4. 선택 이유 및 주의점
- `--mixed`나 `--hard`와 달리 `--soft`는 작업 파일 및 스테이징 상태를 전혀 손실하지 않고 HEAD 위치만 한 단계 뒤로 이동시킴.
- 로컬 전용 커밋에서만 사용해야 하며, 이미 원격에 공유된 커밋에는 적용하지 않음.