#cof-c02 #DataEngineering #Snowflake 

---

## **0) 試験情報 / ロードマップ**

  

□ 公式認定ページ: https://learn.snowflake.com/ko/certifications

□ Core Prepコース: https://learn.snowflake.com/ko/courses/OD-COREPREP

□ アーキテクチャのキーコンセプト: https://docs.snowflake.com/ko/user-guide/intro-key-concepts

---

## **1) セキュリティ/RBAC/アカウント管理**

- Access Controlの構成
    https://docs.snowflake.com/ko/user-guide/security-access-control-configure
    
- Privilegesリスト
    https://docs.snowflake.com/ko/user-guide/security-access-control-privileges
    
- Access Controlのベストプラクティス
    https://docs.snowflake.com/ko/user-guide/security-access-control-considerations
    
- SNOWFLAKE DB Roles
    https://docs.snowflake.com/ko/sql-reference/snowflake-db-roles
    
- SHOW ROLES
    https://docs.snowflake.com/ko/sql-reference/sql/show-roles
    
```sql
SHOW ROLES;
GRANT ROLE ANALYST TO USER alice;
GRANT USAGE ON WAREHOUSE WH_XS TO ROLE ANALYST;
```


---

## **2) 組織(Organization) & ORG管理**

- 組織/アカウント管理の概要
    
    https://docs.snowflake.com/ko/guides-overview-manage
    
- Organization accounts
    
    https://docs.snowflake.com/ko/user-guide/organization-accounts
    
- ORGANIZATION_USAGEビュー
    
    https://docs.snowflake.com/ko/sql-reference/organization-usage
    

---

## **3) コンピュート/ウェアハウス/リソース制御**

- Warehousesの概要
    https://docs.snowflake.com/ko/user-guide/warehouses
    
- Multi-cluster Warehouses
    https://docs.snowflake.com/ko/user-guide/warehouses-multicluster
    
- Resource Monitors
    https://docs.snowflake.com/ko/user-guide/resource-monitors
    

  

練習SQL

CREATE WAREHOUSE WH_XS WITH WAREHOUSE_SIZE=‘XSMALL’ AUTO_SUSPEND=60 AUTO_RESUME=TRUE;

CREATE RESOURCE MONITOR RM_MONTHLY WITH CREDIT_QUOTA=500

TRIGGERS ON 80 PERCENT DO NOTIFY

ON 100 PERCENT DO SUSPEND;

---

## **4) クエリパフォーマンス/キャッシュ/プロファイル**

- Query Profile
    https://docs.snowflake.com/ko/user-guide/ui-snowsight-activity
    
- Persisted Query Results
    https://docs.snowflake.com/ko/user-guide/querying-persisted-results
    
- Search Optimization Service
    https://docs.snowflake.com/ko/user-guide/search-optimization-service
    
- Materialized Views
    https://docs.snowflake.com/ko/user-guide/views-materialized
    

  

練習SQL

SELECT * FROM TABLE(SNOWFLAKE.ACCOUNT_USAGE.QUERY_HISTORY());
SELECT * FROM TABLE(RESULT_SCAN(LAST_QUERY_ID()));

---

## **5) データローディング/アンローディング/ステージング**

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

## **6) パイプライン(Streams & Tasks) / UDF / 半構造化**

- Streams & Tasks
    https://docs.snowflake.com/ko/user-guide/data-pipelines-intro
    
- UDF
    https://docs.snowflake.com/ko/developer-guide/udf/udf-overview
    
- Stored Procedures
    https://docs.snowflake.com/ko/developer-guide/stored-procedure/stored-procedures-overview
    
- FLATTEN関数
    https://docs.snowflake.com/ko/sql-reference/functions/flatten
    

---

## **7) 保護/共有/BCDR**

- Time Travel
    https://docs.snowflake.com/ko/user-guide/data-time-travel
    
- Fail-safe
    https://docs.snowflake.com/ko/user-guide/data-failsafe
    
- Zero-copy Clone
    https://docs.snowflake.com/ko/sql-reference/sql/create-clone
    
- アカウント複製/フェイルオーバー
    https://docs.snowflake.com/ko/user-guide/account-replication-intro
    
- Secure Data Sharing
    https://docs.snowflake.com/ko/user-guide/data-sharing-intro
    

---

## **8) テーブル/ストレージタイプ**

- Temp/Transientテーブル
    https://docs.snowflake.com/ko/user-guide/tables-temp-transient
    
- Icebergテーブル
    https://docs.snowflake.com/ko/user-guide/tables-iceberg
    
- Hybridテーブル
    https://docs.snowflake.com/ko/user-guide/tables-hybrid
    
- Unstructured Data
    https://docs.snowflake.com/ko/user-guide/unstructured-intro
    

---

## **9) データガバナンス**

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

## **10) 認証/ネットワーク**

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

## **11) SQL参照**

- DDL要約
    https://docs.snowflake.com/ko/sql-reference/sql-ddl-summary
    
- DML要約
    https://docs.snowflake.com/ko/sql-reference/sql-dml
    
- トランザクション
    https://docs.snowflake.com/ko/sql-reference/transactions
    
- GET_DDL
    https://docs.snowflake.com/ko/sql-reference/functions/get_ddl
    

---

## **最終点検**

  

□ 全てのドキュメントリンクを1回以上学習

□ QUERY_HISTORY / プロファイルを直接実行

□ COPY/VALIDATE/RESULT_SCANを各1回以上

□ Time Travel/Cloneの復旧シナリオを再現