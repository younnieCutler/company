

본 문서는 현재 RSX 기반 Retool 템플릿을 미쓰이식품의 Retool–Snowflake 연계 PoC(재고/배송 가시화 + CRUD 운영패널)로 전환하기 위한 실무 가이드입니다.

---

## 1) 템플릿 구조 요약
- 레이아웃/컴포넌트: `main.rsx`, `src/container*.rsx`, `sidebar.rsx`
- 전역 쿼리: `functions.rsx` (`getData`)
- 차트/SQL 리소스: `lib/*.json`, `lib/getData.sql`
- 메타/배치: `.positions.json`, `metadata.json`

---

## 2) 핵심 매핑(템플릿 → PoC)
- 데이터 소스: `retool_db` → Snowflake 리소스(계정/웨어하우스/역할)로 교체
- 메인 목록: `retail_dashboard04` → `mart` 계층 뷰(예: `MART_INVENTORY_PRODUCT`)
- 필터: `textInput1`(검색), `dateRange1`(기간) → Snowflake SQL WHERE 반영
- 차트: 데모용 랜덤 데이터 → 월별 판매/입출고/채널비중 집계 쿼리로 대체
- CRUD: 테이블 저장 → `DIM_PRODUCT`(재주문점/안전재고) 또는 `OPS_EXCEPTIONS` 테이블 업데이트

---

## 3) 화면 전환 설계
- container3(테이블): 재고/입출고/유통기한 핵심 목록. 컬럼 예시
  - `product_name, sku, category, inventory_level, reorder_point, expiry_risk`
- container4(드릴다운): 선택 품목의 월별 출고/폐기/반품 추이 + 액션 버튼
  - "View Details": 모달 열기 + 상세 쿼리 실행
  - "Check Report": 필터 기준 리포트 다운로드(PDF/CSV)
- container1/2(상단 지표/차트): SLA/리드타임, 임박 유통기한 수량, 백오더, 센터/채널별 분포
- 사이드바: “가시화 대시보드”, “운영 패널(CRUD)”, “리포트”로 네비게이션

---

## 4) Snowflake 리소스 설정
- 연결: Retool → Snowflake 계정/창고/DB/스키마/역할 지정(SSO/OAuth 권장)
- 비용 제어: X‑Small/Small WH, Auto‑Suspend 60s, Auto‑Resume
- 보안: 역할 기반 권한, 필요시 Row Access Policy / Dynamic Masking 시범 적용

---

## 5) 쿼리 치환 가이드

### 5.1 목록 조회(`lib/getData.sql`)
```sql
SELECT 
  id,
  product_name,
  sku,
  category,
  price,
  quantity_sold,
  supplier,
  inventory_level,
  reorder_point,
  reorder_amount,
  photo
FROM mart.MART_INVENTORY_PRODUCT
WHERE 1=1
  AND product_name ILIKE {{ '%' + textInput1.value + '%' }}
  AND snapshot_date BETWEEN 
      TO_DATE({{ dateRange1.value.start }}) 
  AND TO_DATE({{ dateRange1.value.end }});
```

### 5.2 채널 비중(파이 차트)
```sql
SELECT channel, SUM(qty) AS qty
FROM mart.FACT_SALES
WHERE order_date BETWEEN 
  TO_DATE({{ dateRange1.value.start }}) AND TO_DATE({{ dateRange1.value.end }})
GROUP BY channel
ORDER BY qty DESC;
```

### 5.3 월별 추이(라인/막대)
```sql
SELECT TO_CHAR(order_date, 'YYYY-MM') AS ym, SUM(qty) AS qty
FROM mart.FACT_SHIPMENT
WHERE order_date BETWEEN 
  TO_DATE({{ dateRange1.value.start }}) AND TO_DATE({{ dateRange1.value.end }})
GROUP BY 1
ORDER BY 1;
```

---

## 6) CRUD(운영패널) 설계
- 편집 대상: `reorder_point`, `reorder_amount`, `supplier` 등
- 저장 쿼리 예시(행 단위 업데이트):
```sql
UPDATE dim.DIM_PRODUCT
SET 
  reorder_point = {{ table1.record.reorder_point }},
  reorder_amount = {{ table1.record.reorder_amount }},
  supplier = {{ table1.record.supplier }}
WHERE id = {{ table1.record.id }};
```
- 예외 처리: `OPS_EXCEPTIONS(product_id, exception_type, qty, note, status, created_at)`
```sql
INSERT INTO ops.OPS_EXCEPTIONS 
  (product_id, exception_type, qty, note, status, created_at)
VALUES
  ({{ table1.selectedRow.id }}, {{ selectExceptionType.value }}, {{ qtyInput.value }}, {{ noteInput.value }}, 'REQUESTED', CURRENT_TIMESTAMP);
```

---

## 7) 지표·KPI 계측 방법
- 리드타임: Retool 쿼리 실행/다운로드 시간 로깅(앱 이벤트)
- 활용도: Retool 접속 로그, Snowflake Query History
- 재고효율: 폐기/결품 지표를 상단 카드로 노출하여 전후 비교

---

## 8) 아키텍처 정합성
- 데이터 계층: `stg_ → core_ → mart_`(조회), 쓰기 작업은 `dim_`/`ops_` 테이블로 분리
- 증분/스케줄: Snowflake Task/Stream으로 마트 갱신, Retool 캐시로 응답 최적화

---

## 9) 변경 체크리스트
- [ ] Retool 리소스: `functions.rsx`의 `retool_db` → Snowflake 리소스명 교체
- [ ] SQL: `lib/getData.sql`을 Snowflake 마트 기준으로 수정(ILIKE/DATE 호환)
- [ ] 차트: `lib/*.data.json`(데모) → 쿼리 결과 + JS 변환으로 연결
- [ ] 버튼 액션: 모달/다운로드/승인 흐름 연결
- [ ] 스타일: `lib/$appStyles.css`로 브랜딩 컬러/폰트 반영

---

## 10) 8주 로드맵 매핑
- 1–2주: 스키마 합의, 마트 뷰/지표 정의, Snowflake 리소스 설정
- 3–6주: 템플릿 기반 대시보드·CRUD 구현, 파일럿/UAT, 권한·감사 설정
- 7–8주: KPI 측정, 운영/비용 튜닝, 본사업 전환안 정리

---

## 11) 다음 단계
- Snowflake 리소스명(DB/스키마/뷰/업데이트 테이블) 확정
- `getData.sql` 및 차트용 SQL 구체화 → RSX 바인딩 적용
- CRUD(저장/승인) 쿼리와 모달 추가, 테스트 데이터로 UAT 진행

부가 지원이 필요하면 Snowflake 스키마/테이블 명세를 공유해 주세요. 해당 값들에 맞춰 RSX/SQL을 바로 패치해 드리겠습니다.

