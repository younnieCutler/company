#Retool #Career 

좋아 — Retool 공식 문서 + 사례 중심으로 자주 쓰이는 JS 스니펫들을 엄선해 줄게. 그냥 외우기보다는 “이런 패턴이 자주 출몰한다”는 감을 익히는 게 중요해.

---

## 자주 쓰이는 JS 스니펫 모음 + 설명

아래 스니펫들은 Retool 앱에서 데이터 가공, 쿼리 실행, UI 제어 등을 할 때 유용한 것들이야.

(“{{ … }}” 안쪽이든, Transformer/JS Query 코드든 형태만 약간 다를 뿐 개념은 비슷해.)

---

### 1. 기본 데이터 조작 / 접근

```js
// 배열에서 특정 필드 뽑기
{{ query1.data.map(item => item.name) }}

// 조건 필터링
{{ query1.data.filter(item => item.status === "active") }}

// 문자열 조작
{{ textinput1.value.toLowerCase().trim() }}

// 날짜 포맷 변환 (moment 라이브러리 사용 가능)
{{ moment(table1.selectedRow.date).format("YYYY-MM-DD") }}
```

* 이들은 대부분 `{{ }}` 내부에서 직접 쓰는 표현식 패턴이고, 문서에서 “Manipulating Data” 부분에 예로 나와 있음. ([Retool Docs][1])
* 필터링할 땐 주의: `query1.data.filter(...)`, **query1 자체가 아니라 `.data`** 에서 호출해야 한다는 커뮤니티 팁도 있어요. ([Stack Overflow][2])

---

### 2. Transformer 내부 로직 스니펫

Transformers는 동기적(synchronous)으로 실행되고, UI 제어나 쿼리 트리거는 못 하지만, 데이터 가공에 최고야. ([Retool Docs][3])

```js
// 쿼리 결과에서 특정 필드만 뽑아 배열로 반환
const users = {{ query1.data }};
return users.map(u => u.name);

// 승인된 사용자만 추출해서 크레딧 * 10 한 값 반환
var users = {{ query1.data }};
var approved = users.filter(u => u.approved === true);
return approved.map(u => u.credit_amount * 10);

// `rawData` 접근 (변형 전 원본 데이터)
const raw = {{ query1.rawData }};
return raw.map(r => r.someField);
```

* 여기서 `{{ query1.data }}` 처럼, Transformer 내부에서도 `{{ … }}` 표기법으로 쿼리 데이터를 참조할 수 있음. ([Retool Docs][3])
* Transformer는 **읽기 전용** 역할만 해야 한다는 문서 경고 있음 — UI 컴포넌트 조작이나 쿼리 트리거는 JS Query 쪽으로 빼야 함. ([Retool Docs][3])

---

### 3. JS Query / Run JS Code 스니펫 (로직 + 쿼리 제어 가능)

이런 스니펫은 버튼 클릭, 이벤트 핸들러, 복합 흐름 제어 등에 써.

```js
// 여러 행에 대해 쿼리 순차 실행 (Promise 체인 or 재귀)
var rows = table1.data;
var errors = "";

function runRow(i) {
  if (i >= rows.length) {
    console.log("Done all rows");
    return Promise.resolve();
  }
  return updateQuery.trigger({
    additionalScope: {
      i: i
    },
    onSuccess: function(data) {
      return runRow(i + 1);
    },
    onFailure: function(err) {
      errors += "Error at row " + i + ": " + err + "\n";
      return runRow(i + 1);
    }
  });
}
return runRow(0);
```

* 이 구조는 “각 행마다 API 호출/DB 쿼리 실행 → 다음” 흐름을 제어할 때 자주 나옴. 문서의 “Loop through table rows” 샘플과 거의 동일. ([Retool Docs][4])

```js
// 병렬 API 호출 + Promise.all
return Promise.all(
  csvFile.parsedValue.map(row => {
    return apiQuery.trigger({
      additionalScope: { id: row.id }
    });
  })
).then(results => {
  return results;
});
```

* 이건 “리스트/테이블의 각 행마다 외부 API를 호출해야 함” 같은 패턴에서 유용. 문서 “Run JS Code” 섹션에 예시로 나와 있어. ([Retool Docs][1])

```js
// 조건부 쿼리 실행 + 컴포넌트 조작
if (someInput.value > 10) {
  queryA.trigger();
  modal1.close();
} else {
  utils.showNotification({ title: "값이 유효하지 않음" });
}
```

* 이건 JS Query 내부에서 UI/쿼리 흐름을 제어할 때 기본 형태야. 문서 “JavaScript Best Practices” 에 이런 역할 구분 설명이 돼 있음. ([Retool Docs][5])

---

### 4. Repeatable / List View 관련 스니펫

리스트 뷰(Repeatables)나 동적 반복 UI 쪽에서는 `item`, `i`, `instanceValues` 이런 개념이 자주 나와.

```js
// repeatable List View 데이터 필터링
var arr = {{ listView1.data }};
return arr.filter(item => item.sales > 200);
```

* `item`은 각 반복 인스턴스의 현재 객체, `i`는 인덱스. 문서에서 이 패턴이 List View 설명 쪽에서 나옴. ([Retool Docs][6])

```js
// 반복되는 input 컴포넌트 값을 모아서 합산
const formData = {{ listView1.instanceValues }};
const sum = formData.reduce((acc, rec) => acc + rec.numberInput1, 0);
return sum;
```

* `instanceValues` 배열에는 각 반복 인스턴스의 입력 값 개체들이 담겨져 있음. 문서 List View 쪽 설명에 예시 있음. ([Retool Docs][6])

---

## 활용 팁 & 경계 조건

* Transformer는 **비동기(async)** 를 지원하지 않아 — `await` 나 `trigger()` 같은 비동기 함수는 JS Query 쪽으로 빼야 함. ([Retool Forum][7])
* JS Query는 `additionalScope` 옵션을 써서 외부 변수를 전달할 수 있음 (쿼리 내부 JS에서 `{{ }}` 구문 대신 직접 접근 가능) ([Retool Docs][8])
* 가능한 계산 로직은 Transformer 쪽에 두고, 쿼리 실행/UI 조작 쪽 코드는 JS Query 쪽으로 책임 분리하는 게 권장됨 (“관심사의 분리”) ([Retool Docs][5])

---

원한다면 이걸 엑셀/Markdown로 정리해서 너 주석 달린 버전으로 보내줄까? 그걸 보면서 직접 실습하면 기억도 빠르게 남아. 그렇게 할까?

[1]: https://docs.retool.com/queries/concepts/javascript?utm_source=chatgpt.com "JavaScript"
[2]: https://stackoverflow.com/questions/72033090/retool-javascript-filtering-doesnt-work-in-event-handlers?utm_source=chatgpt.com "retool - javascript filtering doesnt work in event handlers"
[3]: https://docs.retool.com/queries/guides/transformers?utm_source=chatgpt.com "Transform data with JavaScript"
[4]: https://docs.retool.com/queries/quickstart?utm_source=chatgpt.com "Queries and code quickstart"
[5]: https://docs.retool.com/education/coe/customer-resources/js-best-practices?utm_source=chatgpt.com "JavaScript Best Practices"
[6]: https://docs.retool.com/apps/guides/layout-structure/repeatables?utm_source=chatgpt.com "Build custom views using repeatable components"
[7]: https://community.retool.com/t/force-run-js-code-to-rerun-when-variable-changes/53085?utm_source=chatgpt.com "Force \"run JS code\" to rerun when variable changes"
[8]: https://docs.retool.com/queries/guides/javascript/?utm_source=chatgpt.com "Write and run JavaScript"
