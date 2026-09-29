# 충돌 해결 종합 보고서 — 실제 기록 3건

- 대상 저장소: [beatles12/codyssey-b2-2-gitflow](https://github.com/beatles12/codyssey-b2-2-gitflow)
- 확인 기준: 2026-09-29, main `06ef0c10efeba1d9ecfff7a2d59bae0f617b417f`
- 공통 기준과 두 부모 커밋은 Git 이력으로 확인했다. 충돌 당시 출력은 각 실습 증빙 문서를 근거로 기록했다.

## 1. 충돌 1: 같은 줄 수정 — 리뷰 요청 가이드
- **참여자**: 김상교(변경 이유 추가·선병합), 장양환(검증 결과 추가·해결)
- **대상 파일**: `src/practice/review-request.md`
- **공통 기준 SHA**: `b6a572a8ecdef171c7809f005e27b8baa736d126`
- **병합 직전 작업 브랜치**: `551dab461e0901161f429e5b5756f92e64c89391`
- **병합한 main**: `a61b344a89ad35dffb4a5c19ea87f60d4cdcf21e`
- **관련 PR**: [선병합 #13](https://github.com/beatles12/codyssey-b2-2-gitflow/pull/13), [충돌 해결 #14](https://github.com/beatles12/codyssey-b2-2-gitflow/pull/14)
- **해결 커밋**: [ce78f45](https://github.com/beatles12/codyssey-b2-2-gitflow/commit/ce78f45eb352f271f10747d3208e56b8159c1243)
- **충돌 내용**: HEAD는 `리뷰 요청: PR 링크와 검증 결과를 공유한다.`, main은 `리뷰 요청: PR 링크와 변경 이유를 공유한다.`로 같은 줄을 다르게 수정했다.
- **판단 이유**: 변경 이유와 검증 결과가 모두 필요하므로 한 문장에 두 정보를 포함했다.
- **해결 절차**: `git fetch origin` → `git merge origin/main` → 양쪽 의도를 반영해 문장 수정 및 마커 제거 → `git add` → 머지 커밋 생성.
- **결과**: 리뷰 요청: PR 링크, 변경 이유와 검증 결과를 공유한다.
- **상세 증빙**: [conflict-ab.md](evidence/conflict-ab.md)
- **주의점과 배운 점**: 같은 부분의 수정은 Git이 자동 선택할 수 없으므로 두 사람의 의도를 확인하고 필요한 내용을 보존한다.

## 2. 충돌 2: 같은 줄 수정 — 동기화 시점 가이드
- **참여자**: 조은익(작업 시작 전 추가·선병합), 김건우(PR 병합 전 추가·해결)
- **대상 파일**: `src/practice/sync-timing.md`
- **공통 기준 SHA**: `a61b344a89ad35dffb4a5c19ea87f60d4cdcf21e`
- **병합 직전 작업 브랜치**: `2fc1ee4ee6e56944a90540df3f8613aebb79d85c`
- **병합한 main**: `dfad80634ec2ba70ba1124af3912ed01cfaecd8f`
- **관련 PR**: [선병합 #17](https://github.com/beatles12/codyssey-b2-2-gitflow/pull/17), [충돌 해결 #18](https://github.com/beatles12/codyssey-b2-2-gitflow/pull/18)
- **해결 커밋**: [877c3d8](https://github.com/beatles12/codyssey-b2-2-gitflow/commit/877c3d8b235824e3cce22a9b2154f242f9db4cd9)
- **충돌 내용**: HEAD는 `동기화: PR 병합 전에 원격 변경을 확인한다.`, main은 `동기화: 작업 시작 전에 원격 변경을 확인한다.`로 같은 줄을 다르게 수정했다.
- **판단 이유**: 작업 시작 전과 PR 병합 전 확인이 모두 필요하므로 두 시점을 보존했다.
- **해결 절차**: `git fetch origin` → `git merge origin/main` → 양쪽 의도를 반영해 문장 수정 및 마커 제거 → `git add` → 머지 커밋 생성.
- **결과**: 동기화: 작업 시작 전과 PR 병합 전에 원격 변경을 확인한다.
- **상세 증빙**: [conflict-cd.md](evidence/conflict-cd.md)
- **주의점과 배운 점**: 같은 부분의 수정은 Git이 자동 선택할 수 없으므로 두 사람의 의도를 확인하고 필요한 내용을 보존한다.

## 3. 충돌 3: 파일 삭제 vs 내용 수정 — 동기화 시점 가이드
- **참여자**: 조은익(파일 삭제·선병합), 김건우(확인 항목 추가·해결)
- **대상 파일**: `src/practice/sync-timing.md`
- **공통 기준 SHA**: `fd69265bc0dc394c5b6de84c8a38dbc5b66ded0e`
- **병합 직전 작업 브랜치**: `ec5e025eaf9353289ccccd3fce29c589eb9b63fd`
- **병합한 main**: `f721723200224b5f3fd5b35ce2dad3e2417fa1e7`
- **관련 PR**: [선병합 #21](https://github.com/beatles12/codyssey-b2-2-gitflow/pull/21), [충돌 해결 #22](https://github.com/beatles12/codyssey-b2-2-gitflow/pull/22)
- **해결 커밋**: [4c88be7](https://github.com/beatles12/codyssey-b2-2-gitflow/commit/4c88be797baaf1e4a4d2f913ef2298efaaf10b86)
- **충돌 내용**: main에서는 파일을 삭제했고 김건우 브랜치에서는 파일 내용을 수정했다. 증빙에 `CONFLICT (modify/delete)`와 `UD src/practice/sync-timing.md`가 기록되어 있으며 문장 충돌 마커는 없었다.
- **판단 이유**: 짧은 연습용 문서라 삭제하려 했지만, PR 병합 전에 계속 사용할 안내와 확인 항목이 필요하다는 이유로 파일을 유지했다.
- **해결 절차**: `git fetch origin` → `git merge origin/main` → 파일 유지 결정 → `git add src/practice/sync-timing.md` → 미해결 파일 목록 확인 → 증빙을 포함한 머지 커밋 생성.
- **결과**: 파일을 유지하고, 원래 동기화 문장 아래에 “확인 항목: 원격 변경 내용과 내 작업에 미치는 영향을 확인한다.”를 보존했다.
- **상세 증빙**: [conflict-delete-modify.md](evidence/conflict-delete-modify.md)
- **삭제 이유 답변**: [조은익의 답변](https://github.com/beatles12/codyssey-b2-2-gitflow/pull/21#discussion_r4130999727)
- **유지·해결 설명**: [김건우의 답변](https://github.com/beatles12/codyssey-b2-2-gitflow/pull/22#discussion_r4131095430)
- **리뷰 확인**: [장양환의 질문](https://github.com/beatles12/codyssey-b2-2-gitflow/pull/22#discussion_r4131086126), [승인](https://github.com/beatles12/codyssey-b2-2-gitflow/pull/22#pullrequestreview-5349538018)
- **합의 기록**: [PR #22에 포함된 판단·합의 기록](https://github.com/beatles12/codyssey-b2-2-gitflow/blob/4c88be797baaf1e4a4d2f913ef2298efaaf10b86/docs/evidence/conflict-delete-modify.md#L31-L36) — 삭제 이유와 유지 필요성을 비교한 뒤 파일과 확인 항목을 보존하기로 한 결정이 기록됨.
- **주의점과 배운 점**: 문장 마커가 없어도 충돌일 수 있다. `UD` 상태와 미해결 파일 목록을 확인하고 파일을 남길지 결정해야 한다.