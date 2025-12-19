# sample プロジェクト

## 環境構築

```powershell
# フォルダ内に.venv作成
python -m venv .venv

# 仮想環境を有効化
.\.venv\Scripts\Activate.ps1

# VS Codeにvenvを認識させる★
# コマンドプロンプト起動ctrl+shift+P
# Python: Select Interpreterで選択
Python 3.14.x ('.venv': venv)

# requirements.txtを作成
pip install -r requirements.txt

# ライブラリインポート
pip install black

# requirements.txtにライブラリ追加
pip freeze > requirements.txt
```

### requirements.txtに書くもの

「このプロジェクトが動くために必要なもの」
numpy,matplotlib
(jupyterや日本語化は別)

### 別環境での再現(試し)

1. 仮想環境にいるときは抜ける
deactivate
2. 一度VS Codeを閉じる
3. VS Codeのpowershellを開いて削除(注意)
cd python-projects\sample
Remove-Item .venv -Recurse -Force
4. requirements.txtから復元

```powershell
# venv作成
python -m venv .venv

# 仮想環境有効化
.\.venv\Scripts\Activate.ps1

# プロジェクト環境を丸ごと再現
pip install -r requirements.txt

# 確認
pip show black
```

## .gitignore について

このプロジェクトでは、Git で管理する必要のないファイルやフォルダを
`.gitignore` によって除外しています。

### 除外しているもの

- `.venv/`  
  仮想環境のフォルダ。  
  OS や Python のバージョンに依存し、`requirements.txt` から再作成できるため、
  Git では管理しません。

- `__pycache__/` / `*.pyc`  
  Python の実行時に自動生成されるキャッシュファイル。
  再生成可能なため管理対象外としています。

- `.vscode/`  
  VS Code のエディタ設定ファイル。
  個人の開発環境に依存するため、このプロジェクトでは除外しています。

### 補足

`.venv` フォルダ内には、Python の `venv` によって自動生成された
`.gitignore` が存在しますが、これは仮想環境内部を誤って
Git 管理しないためのものです。

プロジェクト全体の管理方針としては、
`sample` フォルダ直下にある `.gitignore` のみを編集・管理します。

### Git / GitHub 初期セットアップ手順（忘れない用メモ）

このドキュメントは **VS Code + Windows** 環境で、
Git をインストールして **最初のコミットまで** 行った手順をまとめたものです。

---

## 前提環境

- Windows
- VS Code インストール済み
- Python 仮想環境（.venv）あり ※Gitとは無関係

---

## 1. Git が使えるか確認

VS Code のターミナル（PowerShell）で実行：

```powershell
git --version
```

成功例：

'''
git version 2.52.0.windows.1
'''

※ これが出れば Git は正しく認識されている

---

## 2. ユーザー名・メールアドレス設定（初回のみ）

```powershell
git config --global user.name "yuta"
git config --global user.email "kyuta255@gmail.com"
```

確認：

```powershell
git config --global --list
```

表示例：

```
user.name=yuta
user.email=kyuta255@gmail.com
```

※ 本名でなくてOK
※ メールは後から変更可能

---

## 3. Git 管理を開始する

プロジェクトフォルダで実行：

```powershell
git init
```

結果：

```
Initialized empty Git repository in .../.git/
```

→ このフォルダが Git 管理対象になる

---

## 4. 現在の状態を確認

```powershell
git status
```

例：

```
On branch master
No commits yet

Untracked files:
  .gitignore
  README.md
  main.py
  rensyu.ipynb
  requirements.txt
```

意味：

- まだ履歴に入っていないファイルがある

---

## 5. ファイルを履歴に追加（ステージ）

全ファイルを対象にする場合：

```powershell
git add .
```

※ warning（LF / CRLF）が出ても問題なし

---

## 6. 初コミット（最初の保存）

```powershell
git commit -m "Initial commit"
```

成功例：

```
[root-commit] 090b61f
 5 files changed
```

→ この時点の状態にいつでも戻せる

---

## Git 用語の超簡単まとめ

| コマンド       | 意味           |
| ---------- | ------------ |
| git init   | Git 管理を始める   |
| git status | 今の状態を見る      |
| git add    | 保存したいファイルを選ぶ |
| git commit | 履歴として保存する    |

---

## メモ

- `.venv` が表示されていても Git には影響しない
- `.gitignore` は最初から入れておくと安心
- Git = **ファイルの履歴を残すタイムマシン**

---

## 次にやる予定（未実施）

- GitHub リポジトリ作成
- リモートリポジトリ登録（git remote add）
- push / pull
- SSH設定（必要になったら）

---

※ このファイル自体も Git で管理すると復習しやすい
