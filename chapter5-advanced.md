# 第5章：Gitの高度なテクニック

## リベース（Rebase）

リベースは、コミット履歴を整理するための強力な機能です。ブランチの基点を変更したり、コミット履歴を綺麗に保つことができます。

### 基本的なリベース

例題1：feature ブランチを main の最新状態にリベース
```bash
# 準備
git checkout main
echo "メインの更新" >> main.txt
git add main.txt
git commit -m "メインブランチを更新"

# featureブランチで作業
git checkout -b feature-rebase
echo "新機能" > feature.txt
git add feature.txt
git commit -m "新機能を追加"

# mainの最新にリベース
git rebase main
```

### インタラクティブリベース

例題2：コミット履歴を整理
```bash
# 複数のコミットを作成
echo "作業1" > work1.txt
git add work1.txt
git commit -m "WIP: 作業1"

echo "作業2" > work2.txt
git add work2.txt
git commit -m "WIP: 作業2"

echo "作業3" > work3.txt
git add work3.txt
git commit -m "WIP: 作業3"

# 直近3つのコミットを整理
git rebase -i HEAD~3
```

例題3：コミットメッセージの編集
```bash
# インタラクティブリベースでrewordを使用
git rebase -i HEAD~2
# エディタでpickをrewordに変更
```

例題4：コミットの結合（squash）
```bash
# 複数の細かいコミットを1つにまとめる
git rebase -i HEAD~3
# エディタで2番目と3番目のpickをsquashに変更
```

### リベース時のコンフリクト解決

例題5：リベース中のコンフリクトを解決
```bash
# コンフリクトが発生した場合
git status
# ファイルを編集してコンフリクトを解決
git add resolved-file.txt
git rebase --continue

# リベースを中止したい場合
# git rebase --abort
```

## スタッシュ（Stash）

スタッシュは、作業中の変更を一時的に保存する機能です。

### 基本的なスタッシュ

例題6：現在の変更をスタッシュ
```bash
# 作業中の変更
echo "未完成の作業" > incomplete.txt
git add incomplete.txt

# スタッシュに保存
git stash
```

例題7：スタッシュにメッセージを付けて保存
```bash
echo "別の未完成作業" > another.txt
git stash push -m "ログイン機能の途中"
```

### スタッシュの管理

例題8：スタッシュの一覧を表示
```bash
git stash list
```

例題9：スタッシュの内容を確認
```bash
git stash show
git stash show -p  # 詳細な差分を表示
```

例題10：特定のスタッシュの内容を確認
```bash
git stash show stash@{1}
```

### スタッシュの適用

例題11：最新のスタッシュを適用
```bash
git stash pop  # 適用して削除
# または
git stash apply  # 適用するが削除しない
```

例題12：特定のスタッシュを適用
```bash
git stash apply stash@{1}
```

例題13：スタッシュを削除
```bash
git stash drop stash@{0}  # 特定のスタッシュを削除
git stash clear  # すべてのスタッシュを削除
```

## タグ（Tags）

タグは、特定のコミットに名前を付ける機能です。リリースバージョンの管理によく使われます。

### 軽量タグ

例題14：軽量タグを作成
```bash
git tag v1.0.0
```

例題15：特定のコミットにタグを付ける
```bash
git tag v0.9.0 abc1234  # abc1234はコミットID
```

### 注釈付きタグ

例題16：注釈付きタグを作成
```bash
git tag -a v2.0.0 -m "メジャーリリース版"
```

例題17：タグの情報を表示
```bash
git show v2.0.0
```

### タグの管理

例題18：タグの一覧を表示
```bash
git tag
git tag -l "v1.*"  # パターンマッチング
```

例題19：タグを削除
```bash
git tag -d v1.0.0
```

例題20：リモートのタグを削除
```bash
git push origin --delete v1.0.0
```

## .gitignoreの活用

.gitignoreファイルを使って、Gitで管理したくないファイルを指定できます。

### 基本的な.gitignore

例題21：.gitignoreファイルを作成
```bash
cat > .gitignore << EOF
# ビルド成果物
build/
dist/
*.exe

# 依存関係
node_modules/
vendor/

# 環境設定
.env
.env.local

# IDE設定
.vscode/
.idea/
*.swp

# OS関連
.DS_Store
Thumbs.db

# ログファイル
*.log
logs/

# 一時ファイル
*.tmp
*.temp
temp/
EOF

git add .gitignore
git commit -m ".gitignoreを追加"
```

### グローバル.gitignore

例題22：グローバルな.gitignoreを設定
```bash
# グローバル設定ファイルを作成
cat > ~/.gitignore_global << EOF
.DS_Store
*.swp
.idea/
EOF

# Gitに設定
git config --global core.excludesfile ~/.gitignore_global
```

### .gitignoreの確認

例題23：無視されるファイルを確認
```bash
git status --ignored
```

例題24：特定のファイルが無視されるか確認
```bash
git check-ignore -v filename.log
```

## 高度な履歴操作

### リセット（Reset）

例題25：直前のコミットを取り消し（ファイルは保持）
```bash
git reset --soft HEAD~1
```

例題26：直前のコミットとステージングを取り消し
```bash
git reset --mixed HEAD~1  # または単に git reset HEAD~1
```

例題27：完全に直前のコミットをなかったことに
```bash
git reset --hard HEAD~1  # 注意: 変更が失われる
```

### リバート（Revert）

例題28：特定のコミットを打ち消す新しいコミットを作成
```bash
git revert abc1234  # abc1234は取り消したいコミットID
```

例題29：マージコミットをリバート
```bash
git revert -m 1 merge-commit-id
```

### reflog

例題30：Git操作の履歴を確認
```bash
git reflog
```

例題31：誤って削除したコミットを復元
```bash
# reflogで削除前のコミットIDを確認
git reflog
# 復元
git reset --hard HEAD@{2}
```

## 便利なGitエイリアス

例題32：よく使うコマンドのエイリアスを設定
```bash
# ステータスの短縮形
git config --global alias.st status

# ログの見やすい表示
git config --global alias.lg "log --oneline --graph --all"

# 最後のコミットを修正
git config --global alias.amend "commit --amend --no-edit"

# ブランチの一覧（最終更新日付き）
git config --global alias.br "branch -v"

# 差分を見やすく
git config --global alias.df "diff --word-diff"
```

## 練習問題

### 問題1
3つの連続したコミットを作成し、インタラクティブリベースを使って1つのコミットにまとめてください。

### 問題2
作業中の変更をスタッシュに保存し、別のブランチで緊急の修正を行った後、元のブランチに戻ってスタッシュを適用してください。

### 問題3
プロジェクトに以下の要件で.gitignoreを作成してください：
- `*.log`ファイルを無視
- `temp/`ディレクトリを無視
- ただし`temp/important.txt`は追跡する

### 問題4
v1.0.0、v1.1.0、v2.0.0の3つのタグを作成し、v1.1.0だけを削除してください。

### 問題5
最新の3つのコミットをなかったことにして、その変更を1つの新しいコミットとして作り直してください。

## 解答例

### 解答1
```bash
# 3つのコミットを作成
echo "機能A" > feature-a.txt
git add feature-a.txt
git commit -m "機能Aを追加"

echo "機能B" > feature-b.txt
git add feature-b.txt
git commit -m "機能Bを追加"

echo "機能C" > feature-c.txt
git add feature-c.txt
git commit -m "機能Cを追加"

# インタラクティブリベースで結合
git rebase -i HEAD~3
# エディタで2番目と3番目のpickをsquashに変更
# 新しいコミットメッセージを入力
```

### 解答2
```bash
# 作業中の変更を作成
echo "作業中" > work-in-progress.txt
git add work-in-progress.txt

# スタッシュに保存
git stash push -m "機能Xの作業中"

# 別のブランチで緊急修正
git checkout -b hotfix
echo "緊急修正" > urgent-fix.txt
git add urgent-fix.txt
git commit -m "緊急のバグを修正"

# 元のブランチに戻ってスタッシュを適用
git checkout main
git stash pop
```

### 解答3
```bash
# .gitignoreを作成
cat > .gitignore << EOF
# ログファイルを無視
*.log

# tempディレクトリを無視
temp/

# ただしimportant.txtは追跡
!temp/important.txt
EOF

# ディレクトリとファイルを作成してテスト
mkdir temp
echo "重要" > temp/important.txt
echo "ログ" > temp/debug.log

git add .
git status  # important.txtだけがステージングされることを確認
```

### 解答4
```bash
# タグを作成
git tag v1.0.0
git tag v1.1.0
git tag v2.0.0

# タグを確認
git tag

# v1.1.0を削除
git tag -d v1.1.0

# 削除後の確認
git tag
```

### 解答5
```bash
# 最新3つのコミットをソフトリセット
git reset --soft HEAD~3

# 変更がステージングエリアにあることを確認
git status

# 1つの新しいコミットとして作成
git commit -m "機能A、B、Cを統合"
```

## まとめ

この章では、Gitの高度な機能について学習しました。リベース、スタッシュ、タグなどの機能を使いこなすことで、より効率的で整理されたGit運用が可能になります。

これで基本的なGitチュートリアルは完了です。実際のプロジェクトでこれらの機能を使いながら、さらに理解を深めていってください。

お疲れさまでした！