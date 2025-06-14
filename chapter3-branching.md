# 第3章：ブランチとマージ

## ブランチの概念

ブランチは、プロジェクトの開発を並行して進めるための仕組みです。メインの開発ラインから分岐して、独立した作業を行うことができます。

### ブランチを使う利点
- 新機能の開発を安全に行える
- 複数人が同時に異なる機能を開発できる
- 実験的な変更を本番コードから分離できる
- バグ修正と新機能開発を並行して進められる

## ブランチの基本操作

### ブランチの確認

例題1：現在のブランチを確認
```bash
git branch
```

例題2：リモートブランチも含めてすべてのブランチを表示
```bash
git branch -a
```

例題3：各ブランチの最新コミットも表示
```bash
git branch -v
```

### ブランチの作成

例題4：新しいブランチを作成
```bash
git branch feature-login
git branch
```

例題5：ブランチを作成して同時に切り替え
```bash
git checkout -b feature-header
```

例題6：新しい方法でブランチを作成して切り替え（Git 2.23以降）
```bash
git switch -c feature-footer
```

### ブランチの切り替え

例題7：既存のブランチに切り替え
```bash
git checkout main
git checkout feature-login
```

例題8：新しい方法でブランチを切り替え（Git 2.23以降）
```bash
git switch main
git switch feature-header
```

## ブランチでの作業

### 実践例：ログイン機能の開発

例題9：ログイン機能のブランチで作業
```bash
# mainブランチから始める
git checkout main

# ログイン機能用のブランチを作成して切り替え
git checkout -b feature-login

# ログインページを作成
echo "<form>ログインフォーム</form>" > login.html
git add login.html
git commit -m "ログインページを追加"

# ログイン処理を追加
echo "function login() { /* ログイン処理 */ }" > login.js
git add login.js
git commit -m "ログイン処理を実装"

# 作業内容を確認
git log --oneline -3
```

## マージ

### Fast-forwardマージ

例題10：単純なマージ（Fast-forward）
```bash
# mainブランチに切り替え
git checkout main

# feature-loginブランチをマージ
git merge feature-login

# マージ結果を確認
git log --oneline --graph -5
```

### 3-wayマージ

例題11：並行開発後のマージ
```bash
# mainブランチで作業
git checkout main
echo "メインページの更新" >> index.html
git add index.html
git commit -m "メインページを更新"

# 新機能ブランチを作成
git checkout -b feature-sidebar
echo "<aside>サイドバー</aside>" > sidebar.html
git add sidebar.html
git commit -m "サイドバーを追加"

# mainブランチに戻ってマージ
git checkout main
git merge feature-sidebar

# マージコミットが作成されたことを確認
git log --oneline --graph -5
```

## コンフリクトの解決

### コンフリクトの発生

例題12：意図的にコンフリクトを発生させる
```bash
# 準備：共通のファイルを作成
git checkout main
echo "共通のコンテンツ" > shared.txt
git add shared.txt
git commit -m "共通ファイルを追加"

# ブランチAで編集
git checkout -b branch-a
echo "ブランチAの変更" > shared.txt
git add shared.txt
git commit -m "ブランチAで変更"

# mainブランチに戻って別の編集
git checkout main
echo "mainブランチの変更" > shared.txt
git add shared.txt
git commit -m "mainブランチで変更"

# マージを試みる（コンフリクトが発生）
git merge branch-a
```

### コンフリクトの解決方法

例題13：コンフリクトを手動で解決
```bash
# コンフリクトの状態を確認
git status

# ファイルの内容を確認
cat shared.txt

# エディタでファイルを開いて修正
# <<<<<<< HEAD
# mainブランチの変更
# =======
# ブランチAの変更
# >>>>>>> branch-a

# 修正後の内容（例）
echo "mainブランチとブランチAの変更を統合" > shared.txt

# 解決したファイルをステージング
git add shared.txt

# マージを完了
git commit -m "コンフリクトを解決してマージ"
```

## ブランチの管理

### ブランチの削除

例題14：マージ済みのブランチを削除
```bash
git branch -d feature-login
```

例題15：マージされていないブランチを強制削除
```bash
git branch -D experimental-feature
```

### ブランチの名前変更

例題16：ブランチ名を変更
```bash
# 現在のブランチの名前を変更
git branch -m new-branch-name

# 別のブランチの名前を変更
git branch -m old-name new-name
```

## 高度なブランチ操作

### ブランチの比較

例題17：ブランチ間の差分を確認
```bash
git diff main..feature-header
```

例題18：ブランチ間のコミットの違いを確認
```bash
git log main..feature-header
```

### Cherry-pick

例題19：特定のコミットを別のブランチに適用
```bash
# コミットIDを確認
git log --oneline feature-sidebar

# 特定のコミットをmainブランチに適用
git checkout main
git cherry-pick abc1234  # abc1234は実際のコミットIDに置き換え
```

## 練習問題

### 問題1
新しいリポジトリを作成し、`main`ブランチに`README.md`ファイルを追加してコミットしてください。その後、`develop`ブランチを作成して切り替えてください。

### 問題2
`develop`ブランチで以下の作業を行ってください：
1. `app.js`ファイルを作成（内容：`console.log("アプリ開始");`）
2. `config.js`ファイルを作成（内容：`const config = {};`）
3. それぞれ別々にコミット

### 問題3
`main`ブランチに戻り、`develop`ブランチの変更をマージしてください。マージ後、ブランチの履歴をグラフ形式で確認してください。

### 問題4
以下の手順でコンフリクトを発生させ、解決してください：
1. `main`ブランチで`version.txt`を作成（内容：`v1.0.0`）
2. `hotfix`ブランチを作成し、`version.txt`を`v1.0.1`に変更
3. `main`ブランチに戻り、`version.txt`を`v2.0.0`に変更
4. `hotfix`ブランチをマージし、コンフリクトを解決

### 問題5
不要になったブランチ（`develop`と`hotfix`）を削除してください。

## 解答例

### 解答1
```bash
# 新しいリポジトリを作成
mkdir branch-practice
cd branch-practice
git init

# README.mdを作成してコミット
echo "# ブランチ練習用リポジトリ" > README.md
git add README.md
git commit -m "README.mdを追加"

# developブランチを作成して切り替え
git checkout -b develop
```

### 解答2
```bash
# app.jsを作成してコミット
echo 'console.log("アプリ開始");' > app.js
git add app.js
git commit -m "app.jsを追加"

# config.jsを作成してコミット
echo "const config = {};" > config.js
git add config.js
git commit -m "config.jsを追加"
```

### 解答3
```bash
# mainブランチに戻る
git checkout main

# developブランチをマージ
git merge develop

# 履歴をグラフ形式で確認
git log --oneline --graph --all
```

### 解答4
```bash
# mainブランチでversion.txtを作成
echo "v1.0.0" > version.txt
git add version.txt
git commit -m "バージョン1.0.0をリリース"

# hotfixブランチを作成して変更
git checkout -b hotfix
echo "v1.0.1" > version.txt
git add version.txt
git commit -m "緊急修正: バージョン1.0.1"

# mainブランチで別の変更
git checkout main
echo "v2.0.0" > version.txt
git add version.txt
git commit -m "メジャーアップデート: バージョン2.0.0"

# マージ（コンフリクト発生）
git merge hotfix

# コンフリクトを解決
echo "v2.0.1" > version.txt  # 両方の変更を考慮
git add version.txt
git commit -m "コンフリクトを解決: バージョン2.0.1"
```

### 解答5
```bash
# マージ済みのブランチを削除
git branch -d develop
git branch -d hotfix

# ブランチの一覧を確認
git branch
```

## まとめ

この章では、Gitの強力な機能であるブランチについて学習しました。ブランチを使うことで、安全に新機能の開発や実験を行うことができます。また、コンフリクトの解決方法も理解しました。

次の章では、リモートリポジトリを使った協働作業について学習します。

[第4章：リモートリポジトリとコラボレーション](chapter4-remote.md)に進みましょう！