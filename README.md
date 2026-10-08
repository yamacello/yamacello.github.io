# yamamoto games

やまもと しょう（[@moya_vc](https://x.com/moya_vc)）のブラウザゲーム置き場。

- サイト: https://yamamotogames.com/
- GitHub Pages（リポジトリ `yamacello/yamacello.github.io`）で公開し、独自ドメインは Cloudflare で管理。

## ファイル構成

```
CNAME                                   独自ドメイン（yamamotogames.com）。消さないこと
index.html                              トップページ（作品一覧）。新作はここにリンクを追加
favicon.svg                             サイトのアイコン
hoshi-no-matataki/                      「数えよう！ 星のまたたき」 → /hoshi-no-matataki/
  index.html                            ゲーム本体（HTML・CSS・JavaScript すべてここ）
  art/bedroom-wide.png                  背景画像（1024x1536。目の位置は index.html の EYES で指定）
  sound/kira.mp3                        光が出たときの効果音
  fonts/little-lights-round.ttf         丸ゴシックのフォント（Zen Maru Gothic のサブセット）
  favicon.svg                           タブのアイコン
```

ビルドは不要。ファイルを編集して GitHub の `main` に反映すれば、GitHub Pages で自動的に公開される。
新しいゲームは `新しいゲーム名/index.html` のようにフォルダを作り、トップの `index.html` にリンクを足す。

## 「星のまたたき」を編集するとき（Claude / ChatGPT 向けメモ）

- 変更するのは基本的に `hoshi-no-matataki/index.html` だけ。ライブラリやビルドツールは使っていない素の HTML/JS。
- ゲームの調整値は `<script>` 冒頭の「設定」ブロックにまとまっている：
  - `EYE_ORDER` 光る目の順番（長さ＝光の総数）
  - `GAPS` 光と光の間隔（秒）。`EYE_ORDER` より1つ少ない数にする
  - `FIRST_GAP` / `INTRO_SECONDS` / `CLOSE_SECONDS` 各タイミング
  - `REVEAL` / `REVEAL_BLINKS` 最後の演出のタイミング
  - `SHARE_TEXT` / `SHARE_URL` 「Xでシェア」の投稿内容
  - `KIRA_SRC` / `KIRA_VOLUME` 効果音
- 効果音は Web Audio で鳴らしている（`Sound` クラス）。＋ボタンの音は `tap()`、光の音は `kira()`。
- 画面の文言（タイトル、お礼文など）は `<body>` 内の HTML に直接書いてある。
- 画像を差し替える場合は同じ 1024x1536 のサイズにし、`EYES` の座標を合わせ直すこと。

## ローカルで動かす

画像のピクセルを読む処理があるため、ファイルを直接開くのではなく簡易サーバー経由で開く。

```bash
python3 -m http.server 8000
```

→ http://localhost:8000/ （ゲームは http://localhost:8000/hoshi-no-matataki/ ）
