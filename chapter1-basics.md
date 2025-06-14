# 第1章：Gitの基本とインストール

## Gitとは何か

Gitは、ファイルの変更履歴を記録・管理するための分散型バージョン管理システムです。プログラマーがコードの変更を追跡し、他の開発者と協力して作業するために使用されます。

### Gitの主な特徴

- **バージョン管理**: ファイルの変更履歴を保存
- **分散型**: 各開発者が完全なリポジトリのコピーを持つ
- **ブランチ機能**: 並行して複数の機能を開発可能
- **コラボレーション**: 複数人での共同作業が容易

## Gitのインストール

### Windows
1. [Git公式サイト](https://git-scm.com/)からインストーラをダウンロード
2. インストーラを実行し、デフォルト設定でインストール

### macOS
```bash
# Homebrewを使用する場合
brew install git

# または、Xcodeコマンドラインツールをインストール
xcode-select --install
```

### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install git
```

### インストールの確認

ターミナルで以下のコマンドを実行してみましょう：

```bash
git --version
```

例題1：バージョンを確認する
```bash
$ git --version
git version 2.34.1
```

## 初期設定

Gitを使い始める前に、ユーザー名とメールアドレスを設定する必要があります。

### ユーザー名の設定

例題2：ユーザー名を設定する
```bash
git config --global user.name "山田太郎"
```

### メールアドレスの設定

例題3：メールアドレスを設定する
```bash
git config --global user.email "taro.yamada@example.com"
```

### 設定の確認

例題4：現在の設定を確認する
```bash
git config --list
```

例題5：特定の設定項目を確認する
```bash
git config user.name
git config user.email
```

### エディタの設定

Gitで使用するデフォルトのテキストエディタを設定できます。

例題6：VSCodeをデフォルトエディタに設定
```bash
git config --global core.editor "code --wait"
```

例題7：Vimをデフォルトエディタに設定
```bash
git config --global core.editor "vim"
```

### 日本語ファイル名の文字化け対策

例題8：日本語ファイル名を正しく表示する設定
```bash
git config --global core.quotepath false
```

## Gitのヘルプ

Gitコマンドの使い方が分からない時は、ヘルプを参照できます。

例題9：gitコマンドの一般的なヘルプを表示
```bash
git help
```

例題10：特定のコマンドのヘルプを表示
```bash
git help config
git config --help
```

例題11：簡易ヘルプを表示
```bash
git config -h
```

## 練習問題

### 問題1
Gitがインストールされているか確認し、バージョンを表示してください。

### 問題2
以下の情報でGitの初期設定を行ってください：
- ユーザー名: あなたの名前
- メールアドレス: あなたのメールアドレス

### 問題3
設定したユーザー名とメールアドレスが正しく登録されているか確認してください。

### 問題4
デフォルトのテキストエディタをあなたが普段使用しているエディタに変更してください。

### 問題5
`git status`コマンドのヘルプを3つの異なる方法で表示してください。

## 解答例

### 解答1
```bash
git --version
# 出力例: git version 2.34.1
```

### 解答2
```bash
git config --global user.name "佐藤花子"
git config --global user.email "hanako.sato@example.com"
```

### 解答3
```bash
# 方法1: すべての設定を表示
git config --list

# 方法2: 個別に確認
git config user.name
git config user.email

# 方法3: globalの設定のみ表示
git config --global --list
```

### 解答4
```bash
# VSCodeの場合
git config --global core.editor "code --wait"

# Nanoの場合
git config --global core.editor "nano"

# Emacsの場合
git config --global core.editor "emacs"
```

### 解答5
```bash
# 方法1: helpコマンドを使用
git help status

# 方法2: --helpオプションを使用
git status --help

# 方法3: -hオプションで簡易ヘルプ
git status -h
```

## まとめ

この章では、Gitの基本概念とインストール方法、初期設定について学びました。次の章では、実際にGitリポジトリを作成し、ファイルを管理する方法を学習します。

設定が完了したら、[第2章：リポジトリの初期化と基本コマンド](chapter2-repository.md)に進みましょう！