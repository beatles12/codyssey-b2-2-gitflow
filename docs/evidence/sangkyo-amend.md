# A 김상교: amend 실습 기록

## 1. 참여자 및 작업 정보
- 수행자: 김상교
- 대상 브랜치: `feature/sangkyo-amend-practice`
- 실습 도구: `git commit --amend`

## 2. 상황 및 재현 조건
- 로컬에서 최신 커밋을 생성했으나 커밋 메시지에 오타(`Rekord ... typoo`)가 포함됨.
- 아직 원격에 푸시하기 전이므로 안전하게 로컬 최신 커밋 메시지를 교체하고자 함.

## 3. 실행 명령 및 전후 결과
- 수정 전 커밋 SHA: `38eaa9998342e3787dd2281f522179d0bfad7bbd`
- 실행 명령: `git commit --amend -m "feat: Record amend practice with corrected commit message"`
- 수정 후 커밋 SHA: `24444d3b2555316734453af0d29779ff1591fd4c`
- 결과: 커밋 내용(트리 스냅샷)은 온전히 유지되고, 커밋 해시가 갱신되며 메시지가 교체됨.

### git log -1 fuller 출력 (실행 증빙)
```text
AuthorDate: Tue Sep 29 15:42:48 2026 +0900
Commit:     beatles12 <happy1200000@gmail.com>
CommitDate: Tue Sep 29 15:47:08 2026 +0900

    feat: Record amend practice with corrected commit message

LG gram@GX56K MINGW64 /d/00_코디세이/codyssey_main/codyssey-b2-2-gitflow (feature/sangkyo-amend-practice)
```

## 4. 선택 이유 및 주의점
- 이미 원격에 푸시된 공유 커밋에는 amend를 사용해서는 안 됩니다 (강제 푸시 force push로 인해 동료들의 로컬 이력이 손상될 위험).
- 만약 이미 푸시된 커밋의 메시지에만 오타가 발생했다면, 파일의 실제 변경 내용을 취소해 버리는 `revert`를 사용해서는 안 됩니다. (revert는 메시지가 아니라 파일의 작업 내용을 되돌리는 명령임)
- 이 경우에는 공유 이력을 그대로 보존한 채, 관련 Issue/PR의 본문이나 코멘트를 통해 올바른 커밋 의도를 명시적으로 보완 설명하는 것이 실무 협업의 정석입니다.