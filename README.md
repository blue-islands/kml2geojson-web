# kml2geojson-web

KML ファイルを **GeoJSON** または **レイヤ別 ZIP** に変換してダウンロードできる、シンプルなフロントエンドアプリです。  
変換処理そのものは API 側で実行し、このリポジトリはユーザー操作用の Web UI を提供します。

https://kml2geojson.netlify.app/

## 特徴

- ドラッグ＆ドロップで KML ファイルを選択
- 出力形式を選択
  - ZIP（レイヤごと）
  - 単一 GeoJSON（全件マージ）
- 出力ファイル名の接頭辞（任意）を指定可能
- アップロード / ダウンロード進捗表示
- 変換完了後に自動ダウンロード

## 画面構成

アプリ本体は `docs/index.html` に実装されています。  
GitHub Pages などの静的ホスティングでそのまま配信できます。

- エントリポイント: `docs/index.html`
- アイコン類: `docs/favicon*`

## API 仕様（フロントエンド側）

フロントエンドから以下の固定 URL へリクエストします。

- `https://app.livlog.xyz/webapi/kml2geojson`

クエリパラメータ:

- `format`: `zip` または `geojson`
- `basePrefix`（任意）: 出力ファイル名接頭辞

送信データ:

- `multipart/form-data`
- フィールド名 `file` に `.kml` ファイルを添付

## ローカル確認手順

静的ファイルのみで構成されているため、任意の HTTP サーバーで確認できます。

```bash
# リポジトリルートで実行
python3 -m http.server 8080
```

ブラウザで `http://localhost:8080/docs/` を開いて動作確認してください。

## ディレクトリ構成

```text
.
├─ docs/
│  ├─ index.html
│  └─ favicon*.png / favicon.ico
└─ README.md
```

## 注意事項

- 変換処理は外部 API に依存します。
- オフライン環境では変換機能は利用できません。
- `docs/index.html` は Tailwind CSS CDN を利用しています。
