# little steps — GitHub Pagesで公開する手順

このフォルダの中身だけで動く、単体のWebアプリ(PWA)です。ビルドや`npm install`は不要です。

```
little-steps-pwa/
├── index.html              ← アプリ本体
├── manifest.json           ← ホーム画面アイコンの設定
├── sw.js                   ← オフラインでも開けるようにする仕組み
├── icon-192.png            ← アイコン画像
├── icon-512.png            ← アイコン画像
├── icon-maskable-512.png   ← アイコン画像(Android用)
├── apple-touch-icon.png    ← アイコン画像(iOS用)
└── README.md
```

すべて同じ階層(フォルダなし)に置く構成です。

## 1. GitHubにリポジトリを作る

1. GitHubで新しいリポジトリを作成(例: `little-steps`)。Public / Privateどちらでも可(Privateの場合はGitHub Pagesが有料プラン限定になる場合があります。迷ったらPublicでOKです)
2. このフォルダの中身(`index.html`・`manifest.json`・`sw.js`・アイコン画像4つ)をそのリポジトリの**直下**にすべてアップロード
   - GitHubのWeb画面右上「Add file → Upload files」でドラッグ&ドロップでもOK

## 2. GitHub Pagesを有効にする

1. リポジトリの `Settings` タブを開く
2. 左メニューの `Pages` を選択
3. 「Build and deployment」の `Source` を `Deploy from a branch` に設定
4. `Branch` を `main`(または使っているブランチ)、フォルダを `/ (root)` にして `Save`
5. 数十秒〜数分待つと、ページ上部に公開URLが表示されます
   - `https://<あなたのユーザー名>.github.io/<リポジトリ名>/` の形式です

## 3. スマホのブラウザで開いてホーム画面に追加

- **iPhone(Safari)**: 発行されたURLを開く → 共有ボタン → 「ホーム画面に追加」
- **Android(Chrome)**: URLを開く → 右上の「⋮」メニュー → 「アプリをインストール」または「ホーム画面に追加」
  - manifest.jsonとsw.jsがあるので、Chromeが自動で「インストール」の案内バナーを出すこともあります

アプリ内の「ホーム画面に追加」ボタンからも、開いている端末に応じた手順が表示されます。

## データについて

目標や進捗はこの端末の**ブラウザ内(localStorage)**にだけ保存されます。他の端末やブラウザとは同期されません。ブラウザの履歴やサイトデータを消去すると、保存した目標も消えるのでご注意ください。

## 更新するときは

`index.html`などを直したら、同じ場所にファイルを再アップロードして上書きするだけで反映されます(GitHub Pagesが自動で再デプロイします)。ただし`sw.js`の`CACHE_NAME`の値(例: `little-steps-v1` → `little-steps-v2`)を変えないと、インストール済みの端末に古いキャッシュが残ることがあります。
