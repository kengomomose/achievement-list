# 研究業績リスト（GitHub Pages）

Jekyll + GitHub Pages で管理する研究業績リストです。  
業績データは `_data/achievements.yml` に YAML 形式で記述し、テンプレートが書式ルールを自動適用します。

## セットアップ

### 1. リポジトリ作成

```bash
git init achievement-list
cd achievement-list
# このプロジェクトのファイルをすべてコピー
git add .
git commit -m "Initial commit"
```

### 2. GitHub にプッシュ

```bash
git remote add origin https://github.com/USERNAME/achievement-list.git
git push -u origin main
```

### 3. GitHub Pages を有効化

1. リポジトリの Settings → Pages
2. Source: "Deploy from a branch"
3. Branch: `main` / `/ (root)` を選択
4. Save

### 4. `_config.yml` を編集

```yaml
baseurl: "/achievement-list"   # ← リポジトリ名に合わせる
url: "https://USERNAME.github.io"  # ← 自分のアカウントに合わせる

applicant:
  name_en: "Firstname Lastname"  # ← 自分の名前（英語）
  name_ja: "姓名"               # ← 自分の名前（日本語）
```

---

## 業績の追加方法

`_data/achievements.yml` を編集してエントリを追加するだけです。  
以下にセクションごとのテンプレートを示します。

### (1) 査読付き論文（英語）

```yaml
# 出力: [N] Yuto Takemoto, Author2, and Author3, Title, Journal, Volume, Pages, Year
- lang: en
  authors:
    - { name: "Firstname Lastname", me: true }   # me: true → 太字＋下線
    - { name: "Author Two" }
    - { name: "Author Three" }
  last_sep: "and"         # 最後の著者の前: "and" or "&"
  title: "論文タイトル"
  journal: "雑誌名"
  volume: "Volume X, No. Y"
  pages: "100-110"
  year: 2024
  note: ""                # 補足（"(#:equal contribution)" など）
```

**equal contribution** がある場合:
```yaml
  authors:
    - { name: "Co-first Author", eq: true }
    - { name: "Firstname Lastname", me: true, eq: true }
```
→ 名前の後に `#`（上付き文字）が付きます。

### (2) 解説・総説（日本語）

```yaml
# 出力: [N] 姓名、「タイトル」、出版社、章節、ページ、年
- lang: ja
  authors:
    - { name: "姓名", me: true }
  title: "解説タイトル"
  publication: "出版社名"
  detail: "第X章、Y節"
  pages: "pXXX-XXX"
  year: 2024
```

### (3) 国際会議（英語）

```yaml
# 出力: [N] 〇Firstname Lastname, Author2, Title, Conference, Place, Month, Year, 査読あり
- lang: en
  presenter: true          # true → 〇マーク付き
  authors:
    - { name: "Firstname Lastname", me: true }
    - { name: "Author Two" }
  title: "発表タイトル"
  conference: "学会名"
  place: "開催地"
  month: "November"
  year: 2024
  peer_reviewed: true      # true → 「査読あり」が末尾に付く
```

### (4) 国内学会（日本語）

**自分の発表（口頭・ポスター）:**
```yaml
# 出力: [N] 〇姓名、共著者1、共著者2「タイトル」、学会名、場所、YYYY年M月
- lang: ja
  presenter: true
  authors:
    - { name: "姓名", me: true }
    - { name: "共著者一" }
  title: "発表タイトル"
  conference: "学会名"
  place: "場所"
  year: 2024
  month: 10
```

**共著者としての発表:**
```yaml
# 出力: [N] 第一著者、姓名、共著者「タイトル」、学会名、場所、YYYY年M月
- lang: ja
  presenter: false
  authors:
    - { name: "第一著者" }
    - { name: "姓名", me: true }
    - { name: "共著者" }
  title: "発表タイトル"
  conference: "学会名"
  place: "場所"
  year: 2024
  month: 10
```

### (5) 特許

```yaml
patents:
  - title: "特許名"
    status: "申請中"       # 申請中 / 公開中 / 取得
    number: "特願XXXX-XXXXXX"
    year: 2024
```

### (6) 受賞歴

```yaml
- organization: "授与元"
  award_name: "賞名"
  title: "対象発表タイトル"
  year: 2024
  month: 10
```

### (7) その他

```yaml
- text: "フリーテキスト YYYY年M月～"
```

---

## 書式ルール一覧

テンプレートが以下のルールを自動で処理します。

| ルール | 英語セクション | 日本語セクション |
|--------|---------------|-----------------|
| 項目間の区切り | `, `（半角カンマ＋半角スペース） | `、`（全角読点、スペースなし） |
| 著者間の区切り | `, ` / `and` / `&` | `、` |
| タイトル括弧 | なし（地の文） | `「」` |
| 日付形式 | `Month, Year` | `YYYY年M月` |
| 申請者名 | **太字＋下線** | **太字＋下線** |
| 発表者印 | `〇`（太字下線の外） | `〇`（太字下線の中） |

---

## ローカルプレビュー

```bash
gem install jekyll bundler
jekyll serve
# → http://localhost:4000/achievement-list/
```

## ライセンス

Private - 個人利用
