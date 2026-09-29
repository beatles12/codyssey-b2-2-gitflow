# 보너스: 개인 브랜치 rebase 기록

## 상황과 범위
- 수행자: 김상교
- 브랜치: feature/sangkyo-rebase-bonus
- 범위: 최초 push 전, 이 브랜치에서 만든 커밋 3개
- 정리 명령: git rebase -i HEAD~3
- 선택: 첫 커밋 reword, 두 번째 squash, 세 번째 pick

## 정리 전
```text
7c62fec docs: Draft rebase practice
27b2411 docs: Add rebase safety rule
82cc811 (HEAD -> feature/sangkyo-rebase-bonus, backup/sangkyo-bonus-before) docs: Add content comparison check
```

## 정리 후
```text
5cfb318 docs: Explain rebase purpose and safety
04b1a83 (HEAD -> feature/sangkyo-rebase-bonus) docs: Add content comparison check
```

## 내용 보존 확인
- 비교 명령: git diff --exit-code backup/sangkyo-bonus-before HEAD
- 실제 출력과 종료 코드: 출력 없음 (전 후 파일 동일) / 종료 코드 0
- 정리 전/후 개수: 전 3개, 후 2개
- 비교 시점: 이 증빙 문서를 추가하기 전

## 선택 이유와 주의점
- 목적과 안전 수칙은 한 작업으로 묶고, 검증 설명은 별도 커밋으로 유지했다.
- 개인 브랜치에서 최초 push 전에 수행했다.
- main 및 동료의 공유 이력을 재작성하지 않았다.
- 커밋 번호는 달라져도 최종 파일 내용은 같아야 한다.