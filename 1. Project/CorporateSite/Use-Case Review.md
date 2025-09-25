
도입사례 페이지 본문들 글씨체가 작아서 키워야함.
해상도 호환 같은데..
연습용으로 했던 BI프로덕트 부분 제거
• Updated Plan
  └ □ /case-studies 페이지 및 상세 페이지에서 본문 글자 크기 기준을 분석하고 Tailwind 클래스 조정 방식을 결정한다.
    □ BI 프로덕트 관련 연습용 섹션/파일을 찾아 영향 범위를 파악하고 제거 전략을 세운다.
    □ 폰트 사이즈 수정과 BI 프로덕트 제거 작업 순서를 정하고, 린트/검증 포함한 대응 계획을 정리한다.
    > - 폰트 규격 확인: /case-studies 목록/상세 컴포넌트에서 본문이 text-sm(Tailwind 14px) 위주라 가독성이 떨어지므로, PRD 폰트 가이드(af-xs=16px, af-sm=24px)에 맞춰 본문·설명 문단을 text-af-xs 이상으로 조정하고, 모바일/데스크톱 차이를 Tailwind 브레이크포인트로 재검토합니다.
      - BI 프로덕트 연습 섹션 파악: 기존에 연습용으로 남아 있는 BI 프로덕트 영역(컴포넌트/페이지/데이터)을 찾기 위해 rg로 “BI” “product” 등 키워드 검색 → 실제 노출 위치 확인 → 관련 파일/라우트 정리 후 제거 범위를 확정합니다.
      - 수정·검증 순서: 폰트 크기 변경부터 적용(리스트·필터·카드·상세 전체 문단 조정) → BI 프로덕트 섹션 삭제/정리(필요 시 라우트 리다이렉트 안내) → npm run lint와 브라우저 확인(여러 해상도에서 본문 크기/레이아웃 확인) → 변경 사항을 개발 로그에 기록하고 공유 드릴 계획입니다.

▌ 다음에 도입사례 관련 코드 수정해야하는데 뭐라고 설명해야 작업 내용을 기억해?

> 도입사례 영역을 다시 손봐야 할 때, 아래 키워드로 기억해두면 빠르게 감 잡을 수 있어요:

  - src/app/(contents)/case-studies/ 전체가 도입사례 전용 구조 — 타입(types/case-study.ts), 데이터(data/case-studies.ts), 컴포넌트(components/CaseStudyCard.tsx, CaseStudyFilters.tsx, CaseStudiesPageContent.tsx), 페이지(page.tsx, [id]/page.tsx)가 한 폴더에 모여 있음.
  - 데이터 추가·수정은 case-studies.ts의 caseStudies/caseStudyFilterMeta를 만지는 것으로 시작하고, 가이드 문서 AddCaseGuide.md를 참고하면 필수 필드와 절차를 바로 확인 가능.
  - UI 규칙: 카드와 상세 페이지 모두 “業界課題 → 解決アプローチ → 成果” 순서, 업계 필터 최상단, 툴은 보조적 언급만.
  - Lint/포맷 확인은 항상 npm run lint로 마무리 — 기존 app/layout.tsx 경고만 남는 상태가 기준.

  이 네 가지 포인트만 메모해두면, 다음 작업 때 핵심 기억이 빠르게 되살아날 거예요.
