**SEO 점검 결과**

- src/app/layout.tsx:6, src/app/(top)/layout.tsx:9는 title/description만 설정되어 있습니다. metadataBase, alternates.canonical, openGraph/twitter 설정, 핵심 키워드를 추가해 전역 메타 정보를 강화하세요.
- src/app/sitemap.ts, src/app/robots.ts가 없어 정적 내보내기 시 크롤러 안내가 부족합니다. 도메인을 명시한 sitemap/robots 엔드포인트를 추가해 인덱싱을 지원하세요.
- 대부분의 페이지가 PageTitle 컴포넌트(src/app/_components/common/page_title.tsx:8)로 h2만 렌더링합니다. 페이지마다 h1을 노출하도록 구조를 조정해 SEO·접근성을 개선하세요.
- 빈 alt 속성이 다수 존재합니다(src/app/(top)/page.tsx:51, src/app/footer.tsx:118, src/app/_components/common/Button.tsx:21 등). 의미 있는 이미지에는 설명을, 장식용에는 aria-hidden 등을 적용해 보조공학·검색 가독성을 높이세요.
- 새 창 링크에 rel="noopener noreferrer"가 빠져 있습니다(src/app/header.tsx:138, src/app/footer.tsx:178). 보안·SEO 권장사항에 맞춰 추가하세요.
- 문의 페이지 iframe이 title과 loading="lazy"를 갖추지 못했습니다(src/app/(contents)/contact/page.tsx:11). 접근성과 성능을 위해 보완하세요.
- 사례 페이지 메타가 기본 수준입니다(src/app/(contents)/case-studies/page.tsx:3, [id]/page.tsx:41). BreadcrumbList·Article JSON-LD를 Script로 주입해 풍부한 검색 결과 노출을 노려볼 수 있습니다.
- 톱 페이지 히어로 섹션(src/app/(top)/page.tsx:270 근처)에 브랜드·서비스를 설명하는 평문 텍스트와 내부 링크를 추가해 주요 키워드 신호를 강화하세요.

**추천 후속 작업**

1. 전역/페이지 메타데이터 확장 및 sitemap·robots 구현 후, 정적 빌드에 반영하세요.
2. 제목 계층, alt 텍스트, 외부 링크 rel, iframe 속성을 정리하고 npm run lint로 검증하세요.
3. JSON-LD(회사·사례)와 톱 페이지 키워드 블록을 도입한 뒤 Lighthouse SEO·접근성 점검을 재실행해 개선 효과를 확인하세요.