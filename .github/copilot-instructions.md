# GitHub Copilot コーディング規約

## 技術スタック
- React / TypeScript

## UIコンポーネント規約
- ボタンやヘッダーなどのメイン要素には、プライマリカラー（オリーブ色: `#808000`）を適用してください。

## コンポーネントおよびファイル構造規約

新しいコンポーネントや機能を作成・提案する場合は、必ず以下のディレクトリ構成に従ってください。

### 1. ディレクトリ構造のルール
各機能（コンポーネント）ごとに専用のフォルダを作成し、その中に HTML, JavaScript, CSS の 3 つのファイルを同名で作成します。

フォルダ・ファイル構成の形式：
`src/components/[feature-name]/`
├── `[feature-name].html`
├── `[feature-name].js`
├── `[feature-name].jsx`
├── `[feature-name].ts`
├── `[feature-name].tsx`
└── `[feature-name].css`

### 2. 具体的な構成例
例：「ユーザープロフィール (user-profile)」コンポーネントを作成する場合

src/components/user-profile/
├── user-profile.html
├── user-profile.js
└── user-profile.css

### 3. 命名規則
- **フォルダ名・ファイル名**: すべて **kebab-case（小文字＋ハイフン区切り）** を使用してください。（例: `shopping-cart`, `user-profile`）
- **構成要素**: 1 つの機能フォルダ内には、必ず対応する `.html`, `.js`, `.css` の 3 種類のファイルをセットで配置してください。
- 複合的なコンポーネントを作成するコード生成や提案では、上記のファイル構成を前提としたファイル作成パスやコード構成を記述してください。

## ローカルファイル表示時の注意事項
- ローカルの `file:///...` パスで HTML を直接開く場合、`<script type="module">` はブラウザのセキュリティ制約で読み込まれないことがあるため、通常の `<script src="..."></script>` を使うこと。
- そのため、単体の HTML をファイルから直接開く場合でも、依存する CSS/JS の参照が正しく解決できるようにすること。
- 画面表示の入口は `index.html` のようなトップページに統一し、機能ごとのコンポーネントはそのページから読み込む形にすること。
- 事前に `file:///C:/.../index.html` で表示確認を行い、ローカル開発時の参照失敗を防ぐこと。

## UIのHTML/JS分離ルール
- UIの構造は HTML ファイルに定義し、イベント処理やDOM操作は JS ファイルに分離すること。
- 例: `login-page.html` にフォームのマークアップを置き、`login-page.js` には `submit` イベントや `FormData` の処理を記述する。
- HTML は「見た目の定義」、JS は「動作の定義」として役割を分け、両者が同じファイルに混在しないようにすること。
- ただし、ローカルの `file://` での表示を考慮し、HTML そのものを直接開く前提ではなく、`index.html` から読み込む入口構造を優先すること。

## レイアウト中央寄せの基本ルール
- 画面全体のメインカードやフォームは、親コンテナの中央に配置することを基本とする。
- ルートの `body` またはメインコンテナに `display: flex; align-items: center; justify-content: center;` を設定して、縦横方向の中央揃えを確保すること。
- 画面サイズに応じて幅を調整する場合は、`width: min(...)` と `margin: 0 auto` を併用して、左右の余白が極端にならないようにすること。
- 画面が中央に寄らない場合は、親要素の `display` や `height`、`width`、`margin` の設定を優先して確認すること。

## 再発防止の具体例
- 例: ログイン画面の表示に失敗した場合、`type="module"` を使っているかどうかを確認する。
- 例: `index.html` から `login-page.js` と `login-page.css` を読み込む構成にし、単独の `login-page.html` だけでは動作しない前提を明確にする。
- 例: HTML と JS が分離されている場合、`#app` などの親要素が存在するか、ファイルの読み込み順序が正しいかを確認する。
- 例: `login-page.html` に UI を定義した場合でも、ブラウザの直接表示より `index.html` 経由で確認する運用を守る。
- 例: 画面が中央に寄らない場合、`body` や親コンテナの `display: flex` と `justify-content: center` を確認する。