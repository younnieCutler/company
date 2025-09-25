# PRD: Case Study ページ (業界カテゴリ中心設計)

## 📋 プロジェクト概要

### 目的

エイ・フォース(https://www.a-force.biz/)企業サイトに導入事例 (Case Study) ページを追加し、**ツール導入事例ではなく業界別課題解決経験**を中心に紹介する。業界特有の課題をどのように解決したかを強調することで、同業他社にも共感・適用可能性を伝える。

---

## 🎯 機能要求

### 1. ナビゲーション
- 
- **デスクトップ**: ヘッダーに "Case Study" メニュー追加 (Products と Education の間)
- **モバイル**: ハンバーガーメニューに "Case Study" 項目追加
- **URL**: `/case-studies`

### 2. メインページ (`/case-studies`)

- **ページタイトル**: "Case Study"
    
- **ページ説明**: 導入事例を業界別に紹介
    
- **フィルタリング機能 (優先順位順)**:
    
    1. 業界別 (例: 水産業、印刷・製造、アパレル・小売、企業グループ/ERP統制)
    2. 企業規模別 (スタートアップ、中小企業、大企業、官公庁)
    3. 課題カテゴリ別 (データ統制、作業効率化、安全性向上など)
    4. ツール別 (CELF, Salesforce, ProActive, MotionBoard など)
    5. 検索ワード入力
        
- **カードレイアウト**: グリッド形式 (PC: 3列, タブレット: 2列, モバイル: 1列)
- **推薦事例セクション**: 上部に featured 事例を表示
    

### 3. 詳細ページ (`/case-studies/[id]`)

- **基本情報**: 会社名、業界、企業規模、導入期間
- **課題セクション**: 業界特有の課題を強調 (例: Excel 管理限界、内部統制困難)
- **ソリューションセクション**: 解決アプローチと実施方法 (ツールは補助的に言及)
- **成果セクション**: 定量的・定性的な成果 (例: 作業時間短縮、エラー削減、統制レベル向上)
- **顧客コメント**: 推薦文 (任意)
- **関連事例**: 同じ業界の他事例 3 件
- **CTA**: 問い合わせ、製品紹介ページリンク
    

### 4. カードコンポーネント Variant

- **Featured**: 強調カード (背景グラデーション)
- **Default**: 標準カード (白背景)
- **Compact**: 関連事例用カード
    

---

## 🗂️ データ構造

```typescript
{
  id: string;
  title: string;                // 事例タイトル
  company: string;              // 会社名
  industry: string;             // 業界カテゴリ
  companySize: string;          // 企業規模
  challenge: string;            // 課題 (業界特有)
  solution: string;             // 解決アプローチ (ツール名は補助的)
  results: Result[];            // 成果指標
  testimonial?: string;         // 顧客コメント
  companyLogo?: string;         // 会社ロゴ
  implementationPeriod: string; // 導入期間
  featured: boolean;            // 推薦事例かどうか
  publishedDate: string;        // 公開日
  tags: string[];               // 業界・課題タグ
}
```

---

📁 Directory Structure

```
app/(contents)/case-studies/
├── types/
│   └── case-study.ts              # TypeScript 타입 정의
├── data/
│   └── case-studies.ts            # 데이터 저장소
├── components/
│   ├── CaseStudyCard.tsx          # 카드 컴포넌트
│   └── CaseStudyFilters.tsx       # 필터 컴포넌트
├── page.tsx                       # 메인 리스트 페이지
└── [id]/
    └── page.tsx                   # 상세 페이지
```

## 🔧 技術的考慮事項

1. **静的ビルド対応**: `generateStaticParams()` による動的ルーティング
    
2. **フィルタリング**: クライアントサイドで処理、レスポンス高速化
    
3. **SEO最適化**: 構造化データ、動的メタデータ生成
    
4. **レスポンシブ対応**: Tailwind CSS ブレークポイント利用
    

---

## 🎨 UI/UX ガイドライン

- **カラー**: ブランドカラー (af-orange, af-gray)
    
- **フォント**: 既存体系 (af-xs, af-sm, af-md)
    
- **余白**: 24px (モバイル), 80px (デスクトップ)
    
- **インタラクション**: hover エフェクト、300ms トランジション
    

---

## ✅ 完了基準

---

## 📅 今後の拡張

- フェーズ2: ページネーション、ソーシャルシェア、PDFダウンロード