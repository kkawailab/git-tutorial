# 第4章：リモートリポジトリとコラボレーション

## リモートリポジトリとは

リモートリポジトリは、インターネット上やネットワーク上に存在するGitリポジトリです。GitHub、GitLab、Bitbucketなどのサービスがよく使われます。

### リモートリポジトリの利点
- コードのバックアップ
- チームでの共同作業
- コードの公開と共有
- 継続的インテグレーション（CI/CD）の実現

## リモートリポジトリの設定

### リモートの追加

例題1：リモートリポジトリを追加
```bash
git remote add origin https://github.com/username/repository.git
```

例題2：現在のリモート設定を確認
```bash
git remote -v
```

例題3：リモートの詳細情報を表示
```bash
git remote show origin
```

### リモートの変更と削除

例題4：リモートURLを変更
```bash
git remote set-url origin https://github.com/username/new-repository.git
```

例題5：リモートを削除
```bash
git remote remove origin
```

例題6：リモートの名前を変更
```bash
git remote rename origin upstream
```

## プッシュ（Push）

### 基本的なプッシュ

例題7：現在のブランチをリモートにプッシュ
```bash
git push origin main
```

例題8：初めてのプッシュ（上流ブランチを設定）
```bash
git push -u origin main
```

例題9：すべてのブランチをプッシュ
```bash
git push origin --all
```

### タグのプッシュ

例題10：特定のタグをプッシュ
```bash
git tag v1.0.0
git push origin v1.0.0
```

例題11：すべてのタグをプッシュ
```bash
git push origin --tags
```

### 強制プッシュ

例題12：履歴を書き換えた後の強制プッシュ（注意が必要）
```bash
git push --force origin main
# または安全な強制プッシュ
git push --force-with-lease origin main
```

## プル（Pull）とフェッチ（Fetch）

### フェッチ

例題13：リモートの変更を取得（マージはしない）
```bash
git fetch origin
```

例題14：すべてのリモートから取得
```bash
git fetch --all
```

例題15：フェッチ後の状態確認
```bash
git fetch origin
git status
git log HEAD..origin/main --oneline
```

### プル

例題16：リモートの変更を取得してマージ
```bash
git pull origin main
```

例題17：リベースを使ったプル
```bash
git pull --rebase origin main
```

例題18：すべてのブランチを更新
```bash
git pull --all
```

## クローン（Clone）

### リポジトリのクローン

例題19：リポジトリをクローン
```bash
git clone https://github.com/username/repository.git
```

例題20：別名でクローン
```bash
git clone https://github.com/username/repository.git my-project
```

例題21：特定のブランチをクローン
```bash
git clone -b develop https://github.com/username/repository.git
```

例題22：浅いクローン（履歴を限定）
```bash
git clone --depth 1 https://github.com/username/repository.git
```

## ブランチの追跡

### リモートブランチの確認

例題23：リモートブランチを表示
```bash
git branch -r
```

例題24：すべてのブランチ（ローカル＋リモート）を表示
```bash
git branch -a
```

### リモートブランチの追跡

例題25：リモートブランチを追跡する新しいブランチを作成
```bash
git checkout -b feature-x origin/feature-x
```

例題26：既存のローカルブランチにリモートブランチを設定
```bash
git branch -u origin/feature-y feature-y
```

## コラボレーションのワークフロー

### 基本的なワークフロー

例題27：機能開発の典型的なフロー
```bash
# 1. 最新の状態を取得
git checkout main
git pull origin main

# 2. 新機能用のブランチを作成
git checkout -b feature-user-profile

# 3. 開発作業
echo "ユーザープロフィール機能" > profile.js
git add profile.js
git commit -m "ユーザープロフィール機能を追加"

# 4. リモートにプッシュ
git push -u origin feature-user-profile

# 5. プルリクエスト/マージリクエストを作成（GitHub/GitLab上で）
```

### フォークとプルリクエスト

例題28：オープンソースプロジェクトへの貢献
```bash
# 1. フォークしたリポジトリをクローン
git clone https://github.com/your-username/forked-repo.git
cd forked-repo

# 2. 本家のリポジトリを追加
git remote add upstream https://github.com/original-owner/original-repo.git

# 3. 本家の最新状態を取得
git fetch upstream
git checkout main
git merge upstream/main

# 4. 機能ブランチで作業
git checkout -b fix-typo
# 修正作業...
git commit -m "ドキュメントの誤字を修正"

# 5. フォークにプッシュ
git push origin fix-typo

# 6. GitHub上でプルリクエストを作成
```

## コンフリクトの解決（リモート編）

### プル時のコンフリクト

例題29：プル時にコンフリクトが発生した場合
```bash
# プルを実行（コンフリクト発生）
git pull origin main

# コンフリクトの確認
git status

# ファイルを編集してコンフリクトを解決
# コンフリクトマーカーを削除し、正しい内容に修正

# 解決後、ファイルをステージング
git add conflicted-file.txt

# マージを完了
git commit -m "プル時のコンフリクトを解決"
```

### リベース時のコンフリクト

例題30：リベース中のコンフリクト解決
```bash
# リベースを開始（コンフリクト発生）
git pull --rebase origin main

# コンフリクトを解決
# ファイルを編集

# 解決後、リベースを続行
git add conflicted-file.txt
git rebase --continue

# リベースを中止したい場合
# git rebase --abort
```

## 練習問題

### 問題1
新しいローカルリポジトリを作成し、GitHubの架空のリモートリポジトリ（`https://github.com/your-username/practice-repo.git`）を追加してください。

### 問題2
以下の手順で作業を行ってください：
1. `README.md`と`index.html`を作成してコミット
2. リモートの`main`ブランチにプッシュ
3. `develop`ブランチを作成し、新しいファイルを追加
4. `develop`ブランチもリモートにプッシュ

### 問題3
別のディレクトリで同じリポジトリをクローンし、`develop`ブランチに切り替えて、新しい変更を加えてプッシュしてください。

### 問題4
最初のディレクトリに戻り、リモートの変更をフェッチして、どのような変更があったか確認してから、プルしてください。

### 問題5
以下のシナリオでコンフリクトを解決してください：
1. 両方のディレクトリで同じファイルの同じ行を異なる内容に変更
2. 一方の変更をプッシュ
3. もう一方でプルを実行し、コンフリクトを解決

## 解答例

### 解答1
```bash
# ローカルリポジトリを作成
mkdir practice-repo
cd practice-repo
git init

# リモートを追加
git remote add origin https://github.com/your-username/practice-repo.git

# 確認
git remote -v
```

### 解答2
```bash
# ファイルを作成してコミット
echo "# 練習用リポジトリ" > README.md
echo "<h1>ホームページ</h1>" > index.html
git add README.md index.html
git commit -m "初期ファイルを追加"

# mainブランチにプッシュ
git push -u origin main

# developブランチを作成
git checkout -b develop
echo "開発中の機能" > feature.js
git add feature.js
git commit -m "新機能を追加"

# developブランチをプッシュ
git push -u origin develop
```

### 解答3
```bash
# 別のディレクトリでクローン
cd ..
git clone https://github.com/your-username/practice-repo.git practice-repo-2
cd practice-repo-2

# developブランチに切り替え
git checkout develop

# 新しい変更
echo "追加の機能" >> feature.js
git add feature.js
git commit -m "機能を拡張"
git push origin develop
```

### 解答4
```bash
# 最初のディレクトリに戻る
cd ../practice-repo

# フェッチして確認
git fetch origin
git log HEAD..origin/develop --oneline

# プル
git pull origin develop
```

### 解答5
```bash
# ディレクトリ1で変更
cd practice-repo
echo "ディレクトリ1の変更" > conflict.txt
git add conflict.txt
git commit -m "ディレクトリ1から変更"
git push origin develop

# ディレクトリ2で異なる変更
cd ../practice-repo-2
echo "ディレクトリ2の変更" > conflict.txt
git add conflict.txt
git commit -m "ディレクトリ2から変更"

# プル（コンフリクト発生）
git pull origin develop

# コンフリクトを解決
echo "両方の変更を統合" > conflict.txt
git add conflict.txt
git commit -m "コンフリクトを解決"
git push origin develop
```

## まとめ

この章では、リモートリポジトリを使った協働作業の方法を学びました。プッシュ、プル、フェッチなどの基本的なコマンドから、フォークやプルリクエストを使ったオープンソース貢献の方法まで幅広く扱いました。

次の章では、Gitのより高度な機能について学習します。

[第5章：Gitの高度なテクニック](chapter5-advanced.md)に進みましょう！