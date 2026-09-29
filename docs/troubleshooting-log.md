# Git 4대 트러블슈팅 실습 기록

대상: [beatles12/codyssey-b2-2-gitflow](https://github.com/beatles12/codyssey-b2-2-gitflow) / 확인 기준: 2026-09-29

## 1. amend — 김상교
- **상황**: 원격에 올리기 전 로컬 커밋 메시지의 오타 수정.
- **명령**: `git commit --amend -m "feat: Record amend practice with corrected commit message"`
- **증빙 문서에 기록된 이전 SHA**: `38eaa9998342e3787dd2281f522179d0bfad7bbd` (로컬에서 교체된 이력이며 원격에서 직접 확인한 커밋으로 간주하지 않음).
- **원격에서 확인한 수정 후 커밋**: [24444d3](https://github.com/beatles12/codyssey-b2-2-gitflow/commit/24444d3b2555316734453af0d29779ff1591fd4c)
- **결과**: 증빙에는 파일 내용 유지와 메시지 변경이 기록되어 있음.
- **주의점**: 이미 공유한 커밋에 무리하게 amend와 강제 푸시를 적용하지 않음.
- **관련 링크**: [#11](https://github.com/beatles12/codyssey-b2-2-gitflow/issues/11), [PR #13](https://github.com/beatles12/codyssey-b2-2-gitflow/pull/13), [amend 증빙](evidence/sangkyo-amend.md)

## 2. reset --soft — 장양환
- **상황**: 직전 로컬 커밋을 취소하되 파일과 스테이징 상태는 유지.
- **명령**: `git reset --soft HEAD~1`
- **증빙 문서의 취소 대상 SHA**: `ecdac5a` (로컬 기록).
- **reset 직후 HEAD**: `b6a572a8ecdef171c7809f005e27b8baa736d126`
- **기록된 상태**: `A  src/practice/yanghwan-recovery.txt`
- **재커밋**: [5bb0b18](https://github.com/beatles12/codyssey-b2-2-gitflow/commit/5bb0b185f192c0602a2f2d855cbe21f3013dd953)
- **주의점**: 이 실습은 미푸시 커밋을 대상으로 수행. 공유 이력을 강제로 덮어쓰지 않음.
- **관련 링크**: [#12](https://github.com/beatles12/codyssey-b2-2-gitflow/issues/12), [PR #14](https://github.com/beatles12/codyssey-b2-2-gitflow/pull/14), [reset 증빙](evidence/yanghwan-reset.md)

## 3. revert — 조은익
- **상황**: 증빙에 따르면 원격에 먼저 공유한 잘못된 변경을 취소.
- **명령**: `git revert --no-commit HEAD` 후 역커밋 생성 및 푸시.
- **원본 커밋**: [8a3deb9](https://github.com/beatles12/codyssey-b2-2-gitflow/commit/8a3deb979893e71db17db3d28734867b1381a3fd)
- **역커밋**: [f1cf34a](https://github.com/beatles12/codyssey-b2-2-gitflow/commit/f1cf34a5eba6b0fdb1261ebb88cd007eb8d24341)
- **결과**: 원격 Git 이력에 원본과 역커밋이 모두 남아 있음. 푸시를 먼저 했다는 실행 순서는 실습 증빙의 기록을 근거로 함.
- **주의점**: 공유 이력을 지우지 않고 취소 내용을 새 커밋으로 남김.
- **관련 링크**: [#16](https://github.com/beatles12/codyssey-b2-2-gitflow/issues/16), [PR #17](https://github.com/beatles12/codyssey-b2-2-gitflow/pull/17), [revert 증빙](evidence/eunik-revert.md)

## 4. stash / pop — 김건우 요청, Codex 실행으로 재실습 증빙 보완
- **상황**: 미완성 변경을 보관한 뒤 main을 확인하고 작업 브랜치로 돌아와 복원.
- **실행 시각**: 2026-09-29T20:16:29+09:00
- **참여**: 김건우(papawolf42)가 보완을 요청하고 Codex가 별도 복제본에서 실제 명령 실행 및 기록 작성.
- **명령**: `git stash push -m stash-rerun-before-branch-switch -- src/practice/gunwoo-recovery.txt` → `git checkout main` → 작업 브랜치 복귀 → `git stash pop`.
- **결과**: 보관 후 작업 공간이 깨끗하고 main에서 기준 내용이 유지됨. pop 후 보관 전후 diff 및 파일 SHA-256이 동일하며 stash 목록이 비어 있음.
- **선택 이유**: 커밋할 단계가 아닌 미완성 작업을 잠시 보관하는 상황이므로 stash를 사용함.
- **기록 범위**: 과거 기록의 누락을 새 재실습으로 보완함. 기존 PR #18의 실행 출력을 복원하거나 사람이 직접 입력한 기록으로 주장하지 않음.
- **주의점**: stash는 로컬 기록이며 pop 충돌 시 상태 확인 필요. 공유 main의 초기화나 강제 push는 하지 않음.
- **관련 링크**: [기존 PR #18](https://github.com/beatles12/codyssey-b2-2-gitflow/pull/18), [보완 이슈 #32](https://github.com/beatles12/codyssey-b2-2-gitflow/issues/32), [실제 명령·출력과 전후 비교](evidence/gunwoo-stash.md)
