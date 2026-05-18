# Extension Gallery

社内向け Chrome 拡張機能アーカイブ。ZIP を直接配布するスタイル。

## ファイル構成

```
extension-gallery/
├── index.html          ← トップページ(これだけで動く)
├── extensions.json     ← 拡張のメタ情報。新規追加時はここを編集
├── assets/
│   └── icons/          ← 各拡張のアイコン(任意)
└── downloads/
    └── *.zip           ← 配布用ZIP
```

## 新しい拡張を追加する手順

1. ZIPファイルを `downloads/` に置く
   - 命名規則: `<id>-v<version>.zip` (例: `my-ext-v1.0.0.zip`)
2. アイコン画像があれば `assets/icons/<id>.png` に置く(128x128推奨)
3. `extensions.json` の `extensions` 配列にエントリを追加:

```json
{
  "id": "my-ext",
  "name": "My Extension",
  "version": "1.0.0",
  "description": "短い説明(1〜2行)",
  "long_description": "モーダル表示用の詳細説明",
  "tags": ["タグ1", "タグ2"],
  "icon": "assets/icons/my-ext.png",
  "zip": "downloads/my-ext-v1.0.0.zip",
  "updated_at": "2026-05-18",
  "author": "Kai",
  "permissions_summary": "アクセス先の概要",
  "manifest_version": 3
}
```

4. git push する(GitHub Pages デプロイ時)

## ホスティング

### GitHub Pages の場合

1. リポジトリを作成(Public、社員にURLを共有する前提)
2. このフォルダ全体を push
3. Settings → Pages → Source を `main` ブランチに設定
4. 公開URL(例: `https://<user>.github.io/extension-gallery/`)を社員に共有

### ローカル確認

```bash
cd extension-gallery
python3 -m http.server 8000
# → http://localhost:8000 を開く
```

`file://` で直接開くと `extensions.json` の fetch が失敗するので、必ずサーバー経由で。

## ZIPの作り方

拡張機能のフォルダ(`manifest.json` が直下にあるフォルダ)を ZIP化。
**フォルダの二重構造に注意**(`my-ext/my-ext/manifest.json` ではなく `my-ext/manifest.json` になるように)。

```bash
cd path/to/parent
zip -r my-ext-v1.0.0.zip my-ext
```

## 社員への案内テンプレ

```
社内Chrome拡張機能ギャラリーを公開しました 🎉
https://<URL>

使い方:
1. 欲しい拡張のカードから「download .zip」
2. 解凍して、chrome://extensions で「パッケージ化されていない拡張機能を読み込む」
3. 解凍したフォルダを選択して完了

「install →」ボタンで手順の詳細が出ます。
```
