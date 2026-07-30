# TOOL LAB サイト デプロイ手順

## ファイル構成（このファイルをそのまま公開）
```
index.html          会社トップ（表玄関・会社名検索の着地）  ← NEW
tools.html          TOOL LAB ハブ（3ツールの入口）
itadori_free.html   板取り計算ツール（無料版・主役）
bar_free.html       切断ロス計算ツール（無料版）
master_bar.csv      ↑棒材の内蔵材種リスト（bar_free.htmlと同階層必須）
hayami.html         鋼材 重量早見表（20形状・456行／SEO検索の着地）
robots.txt          クロール許可＋sitemap案内
sitemap.xml         5ページのURL一覧
```
- 全ページ上部に共通ナビ（会社 ⇄ 無料ツール ⇄ 板取り／切断ロス／重量早見表）を設置済み。
- 会社名で検索した人は `/`（会社トップ）に、「板取り 無料」「アングル 重量」等で検索した人は各ツール・早見表ページに直接着地します。
- `株式会社橋本工業` は確定した社名です（差し替え不要）。
- ドメインは `hashimotokogyo.com` で確定・全ファイル反映済みです。
- `toollab.png`（ロゴ）は任意。無ければ自動でフォールバック表示されます。
- 会社トップの実績写真は差し替え用の枠（点線）になっています。`<div class="ph">…</div>` を `<div class="ph"><img src="works1.jpg" alt="製作物"></div>` の形に差し替えてください。

## 手順

### 1. ✅ ドメイン・社名は反映済み
`hashimotokogyo.com` / `株式会社橋本工業` に置換済みです（再置換は不要）。
対象：`sitemap.xml` / `robots.txt` / `index.html` / `itadori_free.html` / `bar_free.html` / `hayami.html`
（canonical・og:url・JSON-LD・sitemapのURLがすべて揃います）

例（Mac/Linuxのターミナルで、フォルダ内で実行）:
```
grep -rl "hashimotokogyo.com" . | xargs sed -i '' "s/hashimotokogyo.com/あなたのドメイン/g"
```

### 2. Vercelで公開
- Vercelにこのフォルダをドラッグ＆ドロップ（または GitHub連携）するだけ。ビルド設定不要の静的サイト。
- 独自ドメインはVercelの Settings → Domains で接続。
- ※ `bar_free.html` は同一オリジンHTTPS配信で `master_bar.csv` を自動読込します。`file://` で直接開くと読込が失敗する仕様のため、必ずWeb配信で確認してください。

### 3. 公開後にやること
1. **Google Search Console** にドメインを登録し、`sitemap.xml` を送信。
2. Note記事を「サイトへの入口」に改稿し、新サイトへリンク（被リンク獲得）。
3. Boothの商品を「Pro版」に位置づけ直し、説明文に「無料版はこちら→(サイト)」を追加。
4. 各ツール下部・ハブのBOOTHリンク（現状 `https://toollab.booth.pm/`）を実際のPro版商品URLに差し替え。
5. ハブの問い合わせ先（`mailto:` 空欄）と本業の連絡先を記入。

## 差し替えが必要なプレースホルダ一覧（ドメイン・社名は確定済み・対応不要）
| 箇所 | 現状 | 差し替え内容 |
|---|---|---|
| 会社トップ | 住所・TEL・メール（会社概要／問い合わせ／JSON-LD） | 実際の会社情報 |
| 会社トップ | 実績ギャラリーの点線枠 | 製作物・工事の写真 |
| BOOTHリンク | `https://toollab.booth.pm/` | Pro版商品URL |
| ロゴ | `toollab.png`（任意） | ロゴ画像（無くても可） |

## SEOの注意（重要）
新規ドメインはGoogleが評価を作るまで時間がかかります。GSCの表示・クリックが1〜2ヶ月ゼロでも、それはインデックス形成中のサインで失敗ではありません。**勝ち負けの判断は3〜6ヶ月**を目安に。この期間は表示回数・クロール状況の確認に留めてください。
