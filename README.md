# 拾得物管理 PWA — ジャンボカラオケ広場 三条河原町店

カラオケ店内でのお客様の忘れ物を管理するPWA。`index.html` 単独動作（localStorage）で複数PC同期はSupabaseまたはGASで実現します。

## ファイル構成
```
.
├── index.html               # アプリ本体
├── manifest.webmanifest     # PWAマニフェスト
├── sw.js                    # サービスワーカー（オフラインキャッシュ）
└── icons/
    ├── icon-192.svg         # アプリアイコン
    ├── icon-512.svg         # アプリアイコン
    └── icon-maskable-512.svg # マスカブルアイコン
```

## GitHub Pages にデプロイする手順（最短）

### A. ブラウザから行う方法（推奨）
1. GitHub にログイン → 右上の「＋」→「New repository」
2. Repository name: `sanjo` / Public を選択 → Create
3. 作成された画面で「uploading an existing file」リンクをクリック
4. このフォルダの **中身すべて**（`index.html` / `manifest.webmanifest` / `sw.js` / `icons/` フォルダ）をドラッグ＆ドロップでアップロード
5. リポジトリの **Settings → Pages** を開く
6. **Source: Deploy from a branch** → Branch: `main` / `/ (root)` → Save
7. 数分後、`https://<あなたのユーザー名>.github.io/sanjo/` で公開されます

### B. git push で行う方法
```bash
cd sanjo-pwa
git init
git add .
git commit -m "deploy: lost-and-found PWA"
gh repo create sanjo --public --source=. --push
# 以降の更新は: git add . && git commit -m "..." && git push
```
GitHub Pages は上記 A と同じく Settings → Pages で有効化。

### C. 別の無料ホスティングに置く場合
- **Netlify Drop**：https://app.netlify.com/drop にフォルダをドラッグするだけで公開URL発行
- **Cloudflare Pages**：GitHub連携で自動デプロイ
- **Vercel**：`vercel deploy` で即URL発行

## アプリ機能（変更点なし）
- 新規登録 → 自動採番（月-連番／月が変わるとリセット）
- データ一覧（管理番号クリックで問い合わせ登録・色分け・行削除）
- 別シート（受渡済／交番届出済）
- 交番届出準備 → 印刷ビュー → 警察提出用PDFとして保存
- 複数PC同期（Supabase REST または Google Apps Script）

## 同期を有効化する手順
1. `⚙ 同期設定` を開く
2. Supabase または GAS を選んで接続情報を貼り付け
3. `保存して同期開始`
4. 同じ接続情報を別PCにも貼り付ければ双方向同期

詳細は `index.html` 内の `同期設定` モーダル参照。
