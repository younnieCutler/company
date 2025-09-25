
 **Retool公式ドキュメント＋事例ベースの「よく使うJSスニペット集」** 

---

## Retoolでよく使われるJavaScriptスニペットと解説

ただ丸暗記するよりも、「このパターンはよく登場するな」という感覚を身につけることが大事です。

---

### 1. 基本的なデータ操作 / アクセス

```js
// 配列から特定のフィールドを取り出す
{{ query1.data.map(item => item.name) }}

// 条件でフィルタリング
{{ query1.data.filter(item => item.status === "active") }}

// 文字列操作
{{ textinput1.value.toLowerCase().trim() }}

// 日付フォーマット変換 (momentライブラリ利用可)
{{ moment(table1.selectedRow.date).format("YYYY-MM-DD") }}
```

---

### 2. Transformer 内での処理例

```js
// クエリ結果から特定フィールドだけ抽出
const users = {{ query1.data }};
return users.map(u => u.name);

// 承認されたユーザーだけ抽出し、credit_amountを10倍して返す
const users = {{ query1.data }};
const approved = users.filter(u => u.approved === true);
return approved.map(u => u.credit_amount * 10);

// rawDataを利用する場合
const raw = {{ query1.rawData }};
return raw.map(r => r.someField);
```

- Transformerは **同期処理専用**。非同期処理やクエリのトリガーは不可。
    
- データの整形・加工に特化。
    

---

### 3. JavaScript Query のスニペット

```js
// 複数行に対して順次クエリを実行する例
const rows = table1.data;
function runRow(i) {
  if (i >= rows.length) return Promise.resolve();
  return updateQuery.trigger({
    additionalScope: { i },
    onSuccess: () => runRow(i + 1),
    onFailure: (err) => runRow(i + 1)
  });
}
return runRow(0);
```

```js
// 複数APIを並列で呼び出す例
return Promise.all(
  csvFile.parsedValue.map(row =>
    apiQuery.trigger({ additionalScope: { id: row.id } })
  )
).then(results => results);
```

```js
// 条件付きクエリ実行 + UI制御
if (input1.value > 10) {
  queryA.trigger();
  modal1.close();
} else {
  utils.showNotification({ title: "入力値が無効です" });
}
```

---

### 4. Repeatable / List View の利用例

```js
// List Viewデータをフィルタリング
const arr = {{ listView1.data }};
return arr.filter(item => item.sales > 200);
```

```js
// 繰り返しインスタンスの値を合計
const formData = {{ listView1.instanceValues }};
return formData.reduce((acc, rec) => acc + rec.numberInput1, 0);
```

---
### まとめ

- **Transformer** → データ加工専用、非同期処理不可
- **JS Query** → 非同期処理・クエリ実行・UI制御が可能
- 計算・フォーマット処理は Transformer、処理フローやイベント制御は JS Query に分けるのがベストプラクティス
---


