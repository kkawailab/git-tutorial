# 第6章：GitHub CLIの使い方

## GitHub CLIとは

GitHub CLI（gh）は、コマンドラインからGitHubの機能を直接操作できる公式ツールです。プルリクエストの作成、イシューの管理、リポジトリの操作などをターミナルから実行できます。

### GitHub CLIの主な利点
- ブラウザを開かずにGitHubの操作が可能
- 作業フローの自動化
- スクリプトでの利用が容易
- Git操作とGitHub操作をシームレスに統合

## GitHub CLIのインストール

### Windows
```bash
# Scoopを使用
scoop install gh

# またはChocolateyを使用
choco install gh
```

### macOS
```bash
# Homebrewを使用
brew install gh
```

### Linux (Ubuntu/Debian)
```bash
# 公式リポジトリを追加
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh
```

### インストールの確認

例題1：GitHub CLIのバージョンを確認
```bash
gh --version
```

## 認証設定

GitHub CLIを使用するには、まずGitHubアカウントで認証する必要があります。

例題2：GitHubアカウントで認証
```bash
gh auth login
```

例題3：認証状態を確認
```bash
gh auth status
```

例題4：複数のアカウントを管理
```bash
# 別のアカウントでログイン
gh auth login --hostname github.com

# アカウントを切り替え
gh auth switch
```

例題5：認証トークンを確認
```bash
gh auth token
```

## リポジトリ操作

### リポジトリの作成とクローン

例題6：新しいリポジトリを作成
```bash
# パブリックリポジトリを作成
gh repo create my-new-repo --public

# プライベートリポジトリを作成
gh repo create my-private-repo --private

# 説明付きで作成
gh repo create my-project --public --description "私のプロジェクト"
```

例題7：現在のディレクトリをGitHubリポジトリとして公開
```bash
# 既存のローカルリポジトリから
gh repo create --source=. --public
```

例題8：リポジトリをクローン
```bash
# 自分のリポジトリ
gh repo clone my-repo

# 他のユーザーのリポジトリ
gh repo clone owner/repo
```

例題9：フォークを作成
```bash
gh repo fork owner/original-repo
```

### リポジトリ情報の確認

例題10：リポジトリの詳細を表示
```bash
gh repo view

# 特定のリポジトリ
gh repo view owner/repo

# Webブラウザで開く
gh repo view --web
```

例題11：リポジトリ一覧を表示
```bash
# 自分のリポジトリ
gh repo list

# 特定のユーザーのリポジトリ
gh repo list username

# 条件を指定して検索
gh repo list --limit 10 --language javascript
```

## プルリクエスト操作

### プルリクエストの作成

例題12：プルリクエストを作成
```bash
# インタラクティブに作成
gh pr create

# タイトルと本文を指定
gh pr create --title "新機能追加" --body "ログイン機能を実装しました"

# ドラフトとして作成
gh pr create --draft
```

例題13：テンプレートを使用してPRを作成
```bash
gh pr create --template bug_report.md
```

例題14：レビュアーを指定してPRを作成
```bash
gh pr create --reviewer username1,username2
```

### プルリクエストの確認

例題15：プルリクエスト一覧を表示
```bash
# 現在のリポジトリのPR
gh pr list

# 自分がアサインされたPR
gh pr list --assignee @me

# 特定の状態のPR
gh pr list --state closed
```

例題16：プルリクエストの詳細を表示
```bash
gh pr view 123

# インタラクティブに選択
gh pr view

# Webブラウザで開く
gh pr view 123 --web
```

例題17：プルリクエストの差分を確認
```bash
gh pr diff 123
```

### プルリクエストの操作

例題18：プルリクエストをチェックアウト
```bash
gh pr checkout 123
```

例題19：プルリクエストをマージ
```bash
# 通常のマージ
gh pr merge 123

# スカッシュマージ
gh pr merge 123 --squash

# リベースマージ
gh pr merge 123 --rebase
```

例題20：プルリクエストを閉じる
```bash
gh pr close 123
```

例題21：プルリクエストにコメント
```bash
gh pr comment 123 --body "LGTMです！"
```

## イシュー操作

### イシューの作成

例題22：新しいイシューを作成
```bash
# インタラクティブに作成
gh issue create

# タイトルと本文を指定
gh issue create --title "バグ報告" --body "ログイン時にエラーが発生します"

# ラベルを付けて作成
gh issue create --label bug,urgent
```

例題23：テンプレートを使用してイシューを作成
```bash
gh issue create --template bug_report.md
```

### イシューの確認

例題24：イシュー一覧を表示
```bash
# すべてのイシュー
gh issue list

# 特定のラベルのイシュー
gh issue list --label bug

# 自分がアサインされたイシュー
gh issue list --assignee @me
```

例題25：イシューの詳細を表示
```bash
gh issue view 45

# コメントも含めて表示
gh issue view 45 --comments
```

### イシューの操作

例題26：イシューを閉じる
```bash
gh issue close 45
```

例題27：イシューを再開する
```bash
gh issue reopen 45
```

例題28：イシューにコメント
```bash
gh issue comment 45 --body "この問題を調査中です"
```

例題29：イシューを編集
```bash
gh issue edit 45 --title "新しいタイトル" --add-label priority-high
```

## ワークフロー操作

### GitHub Actionsの管理

例題30：ワークフロー一覧を表示
```bash
gh workflow list
```

例題31：ワークフローの実行履歴を確認
```bash
gh run list

# 特定のワークフロー
gh run list --workflow=ci.yml
```

例題32：ワークフローを手動実行
```bash
gh workflow run ci.yml
```

例題33：実行中のワークフローを確認
```bash
gh run watch
```

## リリース操作

### リリースの作成と管理

例題34：新しいリリースを作成
```bash
gh release create v1.0.0 --title "Version 1.0.0" --notes "初回リリース"
```

例題35：リリースノートを自動生成
```bash
gh release create v1.1.0 --generate-notes
```

例題36：アセットを含むリリースを作成
```bash
gh release create v1.2.0 ./dist/app.zip --title "Version 1.2.0"
```

例題37：リリース一覧を表示
```bash
gh release list
```

## 便利な機能

### Gist操作

例題38：Gistを作成
```bash
# ファイルからGistを作成
gh gist create script.sh

# 複数ファイルのGist
gh gist create file1.txt file2.txt --public
```

例題39：Gist一覧を表示
```bash
gh gist list
```

### エイリアスの設定

例題40：カスタムエイリアスを作成
```bash
# プルリクエストの状態を素早く確認
gh alias set prs 'pr list --assignee @me'

# よく使うリポジトリに移動
gh alias set myrepo 'repo view username/myrepo --web'
```

例題41：エイリアス一覧を表示
```bash
gh alias list
```

### API操作

例題42：GitHub APIを直接呼び出す
```bash
# ユーザー情報を取得
gh api user

# リポジトリ情報を取得
gh api repos/owner/repo

# GraphQLクエリ
gh api graphql -f query='
  query {
    viewer {
      login
      name
    }
  }
'
```

## 練習問題

### 問題1
GitHub CLIを使って新しいプライベートリポジトリ「gh-practice」を作成し、READMEファイルを追加してください。

### 問題2
作成したリポジトリに新しいイシューを作成してください。タイトルは「初めてのイシュー」、ラベルは「enhancement」を付けてください。

### 問題3
新しいブランチ「feature-test」を作成し、変更を加えた後、GitHub CLIを使ってプルリクエストを作成してください。

### 問題4
プルリクエストに自分でコメントを追加し、その後マージしてください。

### 問題5
GitHub CLIを使って、自分のリポジトリ一覧を表示し、最新の5つだけを表示してください。

## 解答例

### 解答1
```bash
# リポジトリを作成
gh repo create gh-practice --private --description "GitHub CLI練習用"

# クローン
gh repo clone gh-practice
cd gh-practice

# READMEを追加
echo "# GitHub CLI Practice" > README.md
git add README.md
git commit -m "Add README"
git push origin main
```

### 解答2
```bash
gh issue create \
  --title "初めてのイシュー" \
  --body "GitHub CLIから作成したイシューです" \
  --label enhancement
```

### 解答3
```bash
# ブランチを作成
git checkout -b feature-test

# 変更を加える
echo "テスト機能" > test.txt
git add test.txt
git commit -m "テスト機能を追加"
git push origin feature-test

# プルリクエストを作成
gh pr create \
  --title "テスト機能の追加" \
  --body "新しいテスト機能を実装しました"
```

### 解答4
```bash
# PRにコメント
gh pr comment --body "実装を確認しました。問題ありません。"

# マージ
gh pr merge --merge
```

### 解答5
```bash
gh repo list --limit 5
```

## まとめ

この章では、GitHub CLIの基本的な使い方から高度な機能まで学習しました。GitHub CLIを使うことで、ターミナルから離れることなくGitHubの機能を活用でき、作業効率が大幅に向上します。

特に以下の場面でGitHub CLIは威力を発揮します：
- 頻繁にプルリクエストを作成する開発フロー
- イシューの管理が多いプロジェクト
- CI/CDとの連携
- スクリプトによる自動化

GitHub CLIとGitコマンドを組み合わせることで、より効率的な開発ワークフローを構築できます。