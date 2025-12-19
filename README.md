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
