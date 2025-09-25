
DuckDB의 공식 설명은 다음과 같다:

---

### **DuckDB란 무엇인가?**

  

DuckDB는 **인프로세스(in-process) SQL OLAP 데이터베이스 관리 시스템(DBMS)** 이다.

쉽게 말하면, 별도의 서버를 띄우지 않고 **어플리케이션 내부에서 바로 실행되는 데이터베이스**로, 파이썬이나 R 같은 환경에서 직접 사용하기 편리하다.

  
공식 문서에 따르면 DuckDB는 다음과 같은 특성을 갖는다:

1. **OLAP 지향 (Online Analytical Processing)**  
    - 대량의 데이터를 효율적으로 읽고 집계/분석하는 데 최적화되어 있다.
    - 전통적인 트랜잭션 지향 DBMS(OLTP, 예: MySQL, PostgreSQL)과 달리, 다량의 데이터를 스캔하고 복잡한 분석 쿼리를 수행하는 데 강하다.
        
    
2. **인프로세스(in-process) 실행**
    - 서버/클라이언트 아키텍처 없이 라이브러리처럼 애플리케이션 내부에서 실행된다.
    - SQLite가 “경량 OLTP”에 특화된 인프로세스 DB라면, DuckDB는 “경량 OLAP”에 특화된 인프로세스 DB라고 할 수 있다.
        
    
3. **SQL 지원**
    - ANSI SQL을 준수하면서도, 분석 쿼리에 특화된 기능들을 제공한다.
    - JOIN, GROUP BY, 윈도우 함수, 서브쿼리 등 고급 SQL 기능을 모두 지원한다.
        
    
4. **컬럼 지향 저장 방식(Columnar Storage)**
    
    - 데이터를 행(row) 단위가 아니라 열(column) 단위로 저장하여, 대량 데이터 집계·분석 시 빠른 성능을 제공한다.
    - 이는 Parquet, Arrow 같은 최신 분석 포맷과 호환성을 높여준다.
        
    
5. **통합성**
    
    - Python, R, C++ 등 다양한 언어에서 쉽게 사용할 수 있도록 API를 제공한다.
    - Pandas, Polars, Arrow 같은 데이터프레임과 직접 연동할 수 있다.
        
    

---

### **공식 문서 링크**
- 홈페이지: [https://duckdb.org/](https://duckdb.org/)
- 공식 문서: [https://duckdb.org/docs/](https://duckdb.org/docs/)
- GitHub: [https://github.com/duckdb/duckdb](https://github.com/duckdb/duckdb)
---

DuckDB는 요약하면 **“분석에 특화된 SQLite”**라고 보면 된다.
데이터 엔지니어링/데이터 사이언스 환경에서 가볍게 임베드하여, 대량 데이터를 빠르게 분석할 수 있는 도구라는 점이 핵심이다.
```
dbt 가상환경 Activation
conda activate dbt_learning
```