# 登録有形文化財（建造物）全件マップ — 写真抜き公開版

文化庁「国指定文化財等データベース」の登録有形文化財（建造物）全12分類・14,885件を地図で閲覧する静的サイトです。
**写真は含みません。** 各物件のカードから文化庁の詳細ページ（写真あり）へリンクしています。

## 構成

| パス | 内容 |
|---|---|
| `index.html` | ビューア本体 |
| `data/index.js` | 地図用の索引（全件） |
| `data/detail_00.js` 〜 `detail_11.js` | 分類ごとの詳細（解説文・構造・所在地など。ピンを押したときに該当分類だけ読む） |
| `.nojekyll` | GitHub Pages にファイルをそのまま配信させるための空ファイル（消さない） |

外部依存は CDN のみ（Leaflet / Leaflet.markercluster / Google Fonts / Esri の地図タイル）。サーバー側の処理はありません。

## GitHub Pages で公開する手順

1. GitHub で新しいリポジトリを作る（例: `bunkazai-map`）。公開（Public）にする。
2. **このフォルダ（`site/`）の中身**をリポジトリの直下に置く。`index.html` がリポジトリのトップに来るようにする。
   - ブラウザだけで行う場合: リポジトリの「Add file → Upload files」に、`index.html`・`data` フォルダ・`.nojekyll`・`README.md` をドラッグして「Commit changes」。
     （`.nojekyll` はエクスプローラーで隠しファイル扱いになることがあるので、見えない場合は「隠しファイルを表示」にする）
   - git を使う場合:
     ```
     cd dist/site
     git init
     git add .
     git commit -m "写真抜き公開版"
     git branch -M main
     git remote add origin https://github.com/<ユーザー名>/bunkazai-map.git
     git push -u origin main
     ```
3. リポジトリの **Settings → Pages** を開き、「Build and deployment」の Source を **Deploy from a branch**、
   Branch を **main / (root)** にして Save。
4. 1〜2分で `https://<ユーザー名>.github.io/bunkazai-map/` に公開される（Pages の画面上部に URL が出る）。

更新するときは、手元で `python build_dist.py` を実行して出来た `dist/site/` の中身で置き換え、コミット・プッシュする。

### 補足

- 「近くの文化財」（現在地）は https でのみ動く。GitHub Pages は https なのでそのまま使える。
  取得できない場合は地図をクリックして基点を置ける。現在地は外部に送信しない。
- 絞り込みや開いている物件は URL の `#` 以降に入るので、そのURLを共有すれば同じ状態で開ける。

## 出典・利用条件

- 出典: 文化庁「国指定文化財等データベース」 https://kunishitei.bunka.go.jp/
- 文字情報は、出典を記載の上で自由に利用できる（同データベースの利用規約による）。
- 画像は第三者が権利を持つものがあり、作品ごとに個別の許諾が必要なため、この版には含めていない。
- `type_guess`（分類推定）と竣工年の範囲（「江戸後期」などの幅）は、名称や年代表記からの推定を含む。詳しくは画面上部の「データについて」。
- 利用規約: https://kunishitei.bunka.go.jp/top/policy
