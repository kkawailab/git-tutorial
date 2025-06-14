# 第2章：リポジトリの初期化と基本コマンド

## リポジトリとは

リポジトリ（repository）は、Gitがファイルの変更履歴を保存する場所です。プロジェクトのすべてのファイルとその変更履歴が含まれます。

## リポジトリの作成

### 新規リポジトリの初期化

例題1：新しいプロジェクトフォルダを作成してGitリポジトリを初期化
```bash
mkdir my-first-project
cd my-first-project
git init
```

例題2：既存のフォルダをGitリポジトリにする
```bash
cd existing-project
git init
```

### リポジトリの状態確認

例題3：リポジトリの現在の状態を確認
```bash
git status
```

出力例：
```
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

## ファイルの追加とコミット

### ファイルの作成

例題4：新しいファイルを作成して状態を確認
```bash
echo "# My First Project" > README.md
git status
```

出力例：
```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md

nothing added to commit but untracked files present (use "git add" to track)
```

### ステージングエリアへの追加

例題5：ファイルをステージングエリアに追加
```bash
git add README.md
git status
```

例題6：複数のファイルを一度に追加
```bash
echo "Hello, Git!" > hello.txt
echo "print('Hello, World!')" > hello.py
git add hello.txt hello.py
git status
```

例題7：すべての変更をステージングエリアに追加
```bash
git add .
```

例題8：特定のパターンにマッチするファイルを追加
```bash
git add *.txt
```

### コミットの作成

例題9：ステージングエリアの内容をコミット
```bash
git commit -m "初めてのコミット"
```

例題10：詳細なコミットメッセージを書く
```bash
git commit
# エディタが開くので、詳細なメッセージを記入
```

例題11：ステージングとコミットを一度に行う
```bash
echo "追加のテキスト" >> README.md
git commit -am "READMEを更新"
```

## 変更の確認

### ファイルの差分確認

例題12：作業ディレクトリの変更を確認
```bash
echo "新しい行" >> hello.txt
git diff
```

例題13：ステージングエリアの変更を確認
```bash
git add hello.txt
git diff --staged
```

例題14：特定のファイルの差分を確認
```bash
git diff hello.txt
```

## 履歴の表示

### コミット履歴の確認

例題15：コミット履歴を表示
```bash
git log
```

例題16：簡潔な形式で履歴を表示
```bash
git log --oneline
```

例題17：グラフ形式で履歴を表示
```bash
git log --oneline --graph
```

例題18：特定の件数だけ履歴を表示
```bash
git log -3
```

例題19：特定のファイルの履歴を表示
```bash
git log README.md
```

例題20：統計情報付きで履歴を表示
```bash
git log --stat
```

## ファイルの操作

### ファイルの削除

例題21：Gitで管理されているファイルを削除
```bash
git rm hello.txt
git status
git commit -m "hello.txtを削除"
```

例題22：ファイルをGitの管理から外すが、ファイルは残す
```bash
git rm --cached hello.py
```

### ファイルの移動・名前変更

例題23：ファイル名を変更
```bash
git mv README.md README_JP.md
git status
git commit -m "READMEファイル名を変更"
```

## 変更の取り消し

### ステージングの取り消し

例題24：ステージングエリアから特定のファイルを取り除く
```bash
echo "間違った内容" > mistake.txt
git add mistake.txt
git restore --staged mistake.txt
```

### 作業ディレクトリの変更を取り消し

例題25：ファイルを最後のコミット時の状態に戻す
```bash
echo "間違った変更" >> README_JP.md
git restore README_JP.md
```

### コミットの修正

例題26：直前のコミットメッセージを修正
```bash
git commit --amend -m "修正後のコミットメッセージ"
```

例題27：直前のコミットにファイルを追加
```bash
echo "忘れていた内容" > forgotten.txt
git add forgotten.txt
git commit --amend --no-edit
```

## 練習問題

### 問題1
新しいディレクトリ「git-practice」を作成し、Gitリポジトリとして初期化してください。

### 問題2
以下の3つのファイルを作成し、それぞれ別々のコミットとして記録してください：
- `index.html`: "Hello, Git!"という内容
- `style.css`: "body { color: blue; }"という内容
- `script.js`: "console.log('Git練習中');"という内容

### 問題3
`index.html`に新しい行を追加し、変更前と変更後の差分を確認してから、コミットしてください。

### 問題4
これまでのコミット履歴を、以下の3つの形式で表示してください：
- 通常の形式
- 一行形式
- グラフ付き一行形式

### 問題5
`style.css`のファイル名を`main.css`に変更し、その変更をコミットしてください。

## 解答例

### 解答1
```bash
mkdir git-practice
cd git-practice
git init
```

### 解答2
```bash
# index.htmlを作成してコミット
echo "Hello, Git!" > index.html
git add index.html
git commit -m "index.htmlを追加"

# style.cssを作成してコミット
echo "body { color: blue; }" > style.css
git add style.css
git commit -m "style.cssを追加"

# script.jsを作成してコミット
echo "console.log('Git練習中');" > script.js
git add script.js
git commit -m "script.jsを追加"
```

### 解答3
```bash
# 新しい行を追加
echo "<p>Gitを学習中です</p>" >> index.html

# 差分を確認
git diff index.html

# ステージングしてコミット
git add index.html
git commit -m "index.htmlに段落を追加"
```

### 解答4
```bash
# 通常の形式
git log

# 一行形式
git log --oneline

# グラフ付き一行形式
git log --oneline --graph
```

### 解答5
```bash
git mv style.css main.css
git status
git commit -m "style.cssをmain.cssに名前変更"
```

## まとめ

この章では、Gitリポジトリの作成から基本的なファイル操作、コミットの作成、履歴の確認まで学びました。これらのコマンドはGitを使用する上で最も頻繁に使うものです。

次の章では、Gitの最も強力な機能の一つである「ブランチ」について学習します。

[第3章：ブランチとマージ](chapter3-branching.md)に進みましょう！