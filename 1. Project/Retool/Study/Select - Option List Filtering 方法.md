
  #Retool  #Career  #Component
  
### Select コンポーネント → Table フィルタ連動 の方法

---

# RetoolでSelectコンポーネントを使ってテーブルをフィルタする方法

## やりたいこと

CSVやDBから読み込んだテーブルに対して、**Selectコンポーネント（ドロップダウン）**で選んだ値に応じて、表示する行をフィルタする。

---

## 手順

### 1. Selectコンポーネントを用意

- 例：商品カテゴリを選ぶための `select1`
- オプションリスト（Option list）に「ノートPC」「スマートフォン」「マウス」などを設定
- `Value` はフィルタ条件で使う値、`Label` は画面に表示される文字列
    

---

### 2. Tableコンポーネントを用意
- CSVからインポートしたデータを表示する `table2`
- 今回は `Product name` という列を対象にフィルタする
    

---

### 3. Event Handlerを設定

1. **Event**: `Change` （select1の値が変わったとき）
2. **Action**: `Control component`
3. **Component**: `table2 (Table)`
4. **Method**: `Set filter`
5. **Filter ID**: 任意（例: `{{ self.id }}` でOK）
6. **Column**: フィルタ対象の列名 → `Product name`
7. **Operator**: `=` （完全一致）
    
8. **Value**: `{{ self.value }}` （選択した値がここに入る）
9. **Only run when**: `{{ select1.value }}` （値があるときだけ実行）
    

---

## 動作

- `select1` で「ノートPC」を選択すると、`table2` の `Product name` 列が「ノートPC」の行だけ表示される。
- 選択を変えると、その値に応じてテーブルが更新される。
    

---

## 応用ポイント

- **Operatorを変更**: `contains` にすれば部分一致検索ができる
- **フィルタ解除**: Clearボタンを付けて「Remove filter」アクションを追加すればリセット可能
- **複数条件**: Multiselectコンポーネントと組み合わせて `IN` 条件で複数選択フィルタも可能
    

---

✅ この方法を使えば、CSVやDBを再取得せずに、**クライアント側だけで直感的にデータを絞り込み**できる。

---
