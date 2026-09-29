# C 조은익: revert 실습 기록

## 1. 참여자 및 작업 정보
- 수행자: 조은익
- 대상 브랜치: `feature/eunik-revert-practice`
- 실습 도구: `git revert`

## 2. 상황 및 재현 조건
- 원격 저장소에 이미 푸시된 공유 커밋을 취소해야 하는 상황을 가정하여 실습 파일 생성 후 원격 푸시 완료.
- 1차 푸시 대상 커밋 SHA: `8a3deb9`
- 1차 푸시 실행: `git push -u origin feature/eunik-revert-practice` (원격 브랜치에 공유 확인)

## 3. 실행 명령 및 전후 결과
- 취소 명령: `git revert --no-commit HEAD`
- 역커밋 생성 명령: `git commit -m "revert: Revert faulty feature to preserve public commit history"`
- 역커밋 SHA: `f1cf34a`
- 역커밋 2차 푸시: `git push origin feature/eunik-revert-practice` (원격 반영 완료)
- 결과: 이전 커밋 이력을 삭제(reset)하지 않고 취소하는 새로운 역커밋을 추가하여 파일 상태를 안전하게 원복함.

### git log -2 결과 확인 (실행 증빙)
```text
$ git log -2 --oneline
f1cf34a (HEAD -> feature/eunik-revert-practice, origin/feature/eunik-revert-practice) revert: Revert faulty feature to preserve public commit history
8a3deb9 feat: Add faulty feature to be reverted
```

## 4. 선택 이유 및 주의점
- 원격에 이미 푸시된 커밋을 reset으로 되돌리고 force push하면 다른 동료들의 로컬 이력이 깨지는 치명적인 문제가 발생함.
- 협업 중 공유된 커밋 취소에는 항상 revert를 사용하여 이력을 투명하게 보존해야 함.