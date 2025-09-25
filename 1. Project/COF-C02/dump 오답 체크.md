#snowprocore #Snowflake #DataEngineering #cof-c02

간결한 대답 정답과 정답이 이유 한줄정도 간결하게. 영어 질문이지만 절대 한국어로 대답 문제에서 묻고 있는 것도 같이 해설.  
630問

1問 = 0.16%

100問 = 15.9%  
Pass = 15%



MODIFY = 수정하다.

점수: **11.9%** (75/630) -> 85
- [ ] NO.7 A  
- [ ] NO.9 CD  
- [ ] NO.13 D  
- [ ] NO.24 B  
- [ ] NO.27 A  
- [ ] NO.38 B  
- [ ] NO.53 C  
- [ ] NO.77 A  
- [ ] no.78 C  
- [ ] NO.79 BE  X  
- [ ] NO.88 BD  
- [ ] NO.89 CD  
- [ ] NO.91 A  
- [ ] NO.99 B  


점수: **9.68%** (61/630)  71

- [ ] NO.102 A
- [ ] NO.106 A 
- [ ] NO.108 B  
- [ ] NO.118 D  
- [ ] NO.135 BC  
- [ ] NO.137 AD  
- [ ] NO.153 C  
- [ ] NO.154 AD 
- [ ] NO.157 A 
- [ ] NO.161 C  
- [ ] NO.168 D 
- [ ] NO.191 D  


- [ ] NO.201 D
- [ ] NO.203 D
- [ ] NO.204 A
- [ ] NO.216 DE
- [ ] NO.220 C
- [ ] NO.227 D  
- [ ] NO.248 BE  
- [ ] NO.251 C  
- [ ] NO.264 BD  
- [ ] NO.265 B  
- [ ] NO.266 D  
- [ ] NO.272 DB  
- [ ] NO.273 A  
- [ ] NO.283 DE  
- [ ] NO.292 D  
- [ ] NO.299 C  

- [ ] NO.304 BE  
- [ ] NO.305 C  
- [ ] NO.306 C  
- [ ] NO.321 B  
- [ ] NO.322 BD  
- [ ] NO.339 DE  
- [ ] NO.340 B  
- [ ] NO.344 D  
- [ ] NO.354 C  
- [ ] NO.359 D  
- [ ] NO.362 D  
- [ ] NO.368 D  
- [ ] NO.374 AB  
- [ ] NO.375 C  
- [ ] NO.377 A  
- [ ] NO.382 A  
- [ ] NO.385 C  
- [ ] NO.386 D  
- [ ] NO.389 C  
- [ ] NO.395 C  
- [ ] NO.399 B  

- [ ] NO.405 BF policy_referrences, masking_policy  
- [ ] NO.413 BD  
- [ ] NO.417 A  
- [ ] NO.424 BE  
- [ ] NO.428 C  
- [ ] NO.430 D  
- [ ] NO.433 C  
- [ ] NO.442 D  
- [ ] NO.443 C  
- [ ] NO.444 A  

- [ ] NO.452 A E  
- [ ] NO.459 A  
- [ ] NO.460 C  
- [ ] NO.463 B  
- [ ] NO.466 CD  
- [ ] NO.470 C E  
- [ ] NO.472 C  
- [ ] NO.477 BD  
- [ ] NO.488 BD  
- [ ] NO.491 A  
- [ ] NO.492 CEF  
- [ ] NO.496 C  

- [x] NO.504 C,D ✅ 2025-09-19
- [x] NO.505 B ✅ 2025-09-19
- [x] NO.512 B ✅ 2025-09-19
- [x] NO.522 AD ✅ 2025-09-19
- [x] NO.531 B  Select LAST_QUERY_ID(2) ✅ 2025-09-19
- [x] NO.532 C $ ✅ 2025-09-19
- [x] NO.537 DE ✅ 2025-09-19
- [ ] NO.542 BC
- [ ] NO.546 BE


- [ ] NO.568 B
- [ ] NO.569 A  
- [ ] NO.571 A,E  
- [ ] NO.572 A  
- [ ] NO.576 B  

- [ ] NO.601 B,C  
- [ ] NO.602 A,D  
- [ ] NO.608 A  
- [ ] NO.609 C  
- [ ] NO.610 D  
- [ ] NO.611 B  
- [ ] NO.612 D  
- [ ] NO.613 B,C  
- [ ] NO.614 B,C

### A. FLATTEN
- **Keywords**: _explode_, _expand_, _rows from JSON array_, _table function_, _LATERAL_
---
### B. CHECK_JSON
- **Keywords**: _validate JSON_, _syntax check_, _returns NULL if valid_, _error string if invalid_
---
### C. PARSE_JSON
- **Keywords**: _string to VARIANT_, _convert to JSON object_, _queryable JSON_, _access with colon syntax (`:field`)_
---
### D. TO_VARIANT
- **Keywords**: _cast to VARIANT_, _wrap primitive types_, _store in semi-structured column_, _normalize data type_
---

## Quick Mnemonics
- **FLATTEN → “explode array”**
- **CHECK_JSON → “is it valid?”**
- **PARSE_JSON → “string → JSON object”**
- **TO_VARIANT → “primitive → VARIANT”**
## Snowflake 반정형 데이터 타입

- **VARIANT**
    - JSON, Avro, ORC, Parquet, XML 같은 반정형 데이터를 저장할 수 있는 가장 기본 타입
    - 구조가 유연해서 key-value 쌍이나 중첩 데이터 구조를 담을 수 있음
        
- **ARRAY**
    - 값들의 순서 있는 리스트
    - JSON 배열과 같은 구조를 직접 표현할 때 사용
        
- **OBJECT**
    - 키-값(Key-Value) 구조를 표현
    - JSON 오브젝트처럼 동작


