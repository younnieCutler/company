#cof-c02 #DataEngineering #Snowflake 

---

## **0) 시험 정보 / 로드맵**

  

□ 공식 인증 페이지: https://learn.snowflake.com/ko/certifications

□ Core Prep 코스: https://learn.snowflake.com/ko/courses/OD-COREPREP

□ 아키텍처 키 콘셉트: https://docs.snowflake.com/ko/user-guide/intro-key-concepts

---

## **1) 보안/RBAC/계정 관리**

- Access Control 구성
    https://docs.snowflake.com/ko/user-guide/security-access-control-configure
    
- Privileges 목록
    https://docs.snowflake.com/ko/user-guide/security-access-control-privileges
    
- Access Control 베스트프랙티스
    https://docs.snowflake.com/ko/user-guide/security-access-control-considerations
    
- SNOWFLAKE DB Roles
    https://docs.snowflake.com/ko/sql-reference/snowflake-db-roles
    
- SHOW ROLES
    https://docs.snowflake.com/ko/sql-reference/sql/show-roles
    
```
sql
SHOW ROLES;
GRANT ROLE ANALYST TO USER alice;
GRANT USAGE ON WAREHOUSE WH_XS TO ROLE ANALYST;
```


---

## **2) 조직(Organization) & ORG 관리**

- 조직/계정 관리 개요
    
    https://docs.snowflake.com/ko/guides-overview-manage
    
- Organization accounts
    
    https://docs.snowflake.com/ko/user-guide/organization-accounts
    
- ORGANIZATION_USAGE 뷰
    
    https://docs.snowflake.com/ko/sql-reference/organization-usage
    

---

## **3) 컴퓨트/웨어하우스/리소스 제어**

- Warehouses 개요
    https://docs.snowflake.com/ko/user-guide/warehouses
    
- Multi-cluster Warehouses
    https://docs.snowflake.com/ko/user-guide/warehouses-multicluster
    
- Resource Monitors
    https://docs.snowflake.com/ko/user-guide/resource-monitors
    

  

연습 SQL

CREATE WAREHOUSE WH_XS WITH WAREHOUSE_SIZE=‘XSMALL’ AUTO_SUSPEND=60 AUTO_RESUME=TRUE;

CREATE RESOURCE MONITOR RM_MONTHLY WITH CREDIT_QUOTA=500

TRIGGERS ON 80 PERCENT DO NOTIFY

ON 100 PERCENT DO SUSPEND;

---

## **4) 쿼리 성능/캐시/프로파일**

- Query Profile
    https://docs.snowflake.com/ko/user-guide/ui-snowsight-activity
    
- Persisted Query Results
    https://docs.snowflake.com/ko/user-guide/querying-persisted-results
    
- Search Optimization Service
    https://docs.snowflake.com/ko/user-guide/search-optimization-service
    
- Materialized Views
    https://docs.snowflake.com/ko/user-guide/views-materialized
    

  

연습 SQL

SELECT * FROM TABLE(SNOWFLAKE.ACCOUNT_USAGE.QUERY_HISTORY());
SELECT * FROM TABLE(RESULT_SCAN(LAST_QUERY_ID()));

---

## **5) 데이터 로딩/언로딩/스테이징**

- COPY INTO 
    
    https://docs.snowflake.com/ko/sql-reference/sql/copy-into-table
    
- COPY INTO 
    
    https://docs.snowflake.com/ko/sql-reference/sql/copy-into-location
    
- VALIDATE
    
    https://docs.snowflake.com/ko/sql-reference/functions/validate
    
- Snowpipe Streaming
    
    https://docs.snowflake.com/ko/user-guide/data-load-snowpipe-streaming-overview
    
- External Tables
    
    https://docs.snowflake.com/ko/user-guide/tables-external-intro
    

---

## **6) 파이프라인(Streams & Tasks) / UDF / 반정형**

- Streams & Tasks
    https://docs.snowflake.com/ko/user-guide/data-pipelines-intro
    
- UDF
    https://docs.snowflake.com/ko/developer-guide/udf/udf-overview
    
- Stored Procedures
    https://docs.snowflake.com/ko/developer-guide/stored-procedure/stored-procedures-overview
    
- FLATTEN 함수
    https://docs.snowflake.com/ko/sql-reference/functions/flatten
    

---

## **7) 보호/공유/BCDR**

- Time Travel
    https://docs.snowflake.com/ko/user-guide/data-time-travel
    
- Fail-safe
    https://docs.snowflake.com/ko/user-guide/data-failsafe
    
- Zero-copy Clone
    https://docs.snowflake.com/ko/sql-reference/sql/create-clone
    
- 계정 복제/Failover
    https://docs.snowflake.com/ko/user-guide/account-replication-intro
    
- Secure Data Sharing
    https://docs.snowflake.com/ko/user-guide/data-sharing-intro
    

---

## **8) 테이블/스토리지 타입**

- Temp/Transient 테이블
    https://docs.snowflake.com/ko/user-guide/tables-temp-transient
    
- Iceberg 테이블
    https://docs.snowflake.com/ko/user-guide/tables-iceberg
    
- Hybrid 테이블
    https://docs.snowflake.com/ko/user-guide/tables-hybrid
    
- Unstructured Data
    https://docs.snowflake.com/ko/user-guide/unstructured-intro
    

---

## **9) 데이터 거버넌스**

- Dynamic Data Masking
    https://docs.snowflake.com/ko/user-guide/security-column-ddm-use
    
- Row Access Policy
    https://docs.snowflake.com/ko/user-guide/security-row-intro
    
- Tag-based Masking
    https://docs.snowflake.com/ko/user-guide/tag-based-masking-policies
    
- Data Classification
    https://docs.snowflake.com/ko/user-guide/classify-intro
    
- Access History
    https://docs.snowflake.com/ko/user-guide/access-history
    

---

## **10) 인증/네트워크**

- Federated SSO
    https://docs.snowflake.com/ko/user-guide/admin-security-fed-auth-overview
    
- MFA
    https://docs.snowflake.com/ko/user-guide/security-mfa
    
- Key-pair Auth
    https://docs.snowflake.com/ko/user-guide/key-pair-auth
    
- OAuth
    https://docs.snowflake.com/ko/user-guide/oauth-snowflake-overview
    
- Network Policy
    https://docs.snowflake.com/ko/user-guide/network-policies
    

---

## **11) SQL 참조**

- DDL 요약
    https://docs.snowflake.com/ko/sql-reference/sql-ddl-summary
    
- DML 요약
    https://docs.snowflake.com/ko/sql-reference/sql-dml
    
- 트랜잭션
    https://docs.snowflake.com/ko/sql-reference/transactions
    
- GET_DDL
    https://docs.snowflake.com/ko/sql-reference/functions/get_ddl
    

---

## **최종 점검**

  

□ 모든 문서 링크 1회 이상 학습

□ QUERY_HISTORY / 프로파일 직접 실행

□ COPY/VALIDATE/RESULT_SCAN 각 1회 이상

□ Time Travel/Clone 복구 시나리오 재현
