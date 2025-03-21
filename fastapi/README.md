# FastAPI 用各種設定テンプレート説明

## 1. .vscode/settings.json

#### 概要

FastAPI 開発における VSCode の設定が記載されています。

#### 内容

    "editor.formatOnSaveMode": "modificationsIfAvailable",
    "editor.formatOnSave": true

ファイル保存時に自動的にコード整形を行います。
1 回目の保存時はコード全体を整形しますが、2 回目以降は変更箇所のみを整形します。

####

    "[python]": {
        "editor.defaultFormatter": "charliermarsh.ruff",
        "editor.codeActionsOnSave": {
            "source.fixAll": "explicit",
            "source.organizeImports": "explicit"
        }
    }

Python のソースコードにおいて、整形ツールとして Ruff を使用するように指定しています。
ファイル保存時に Ruff によるコードの修正が行われるようにしています。

####

    "mypy-type-checker.args": ["--config-file=pyproject.toml"]

型チェックの静的解析ツールとして使用する Mypy type checker の設定ファイルを指定しています。

## 2. pyproject.toml

#### 概要

整形ツール、静的解析ツールとして使用する Ruff の設定が記載されています。
型チェックの静的解析ツールとして使用する Mypy type checker の設定が記載されています。

> [!IMPORTANT]
> Ruff は、別途 pip でのインストールが必要です。

    pip install ruff

#### 内容

    [tool.ruff]
    line-length = 88

1 行の最大文字数を 88 文字に指定しています。
(Python の整形ツールとしてよく使われている Black formatter のデフォルトと同じ。)

####

    [tool.ruff.lint]
    select = [
        "E",
        "W",
        "F",
        "I",
        "B",
        "C4",
        "UP",
    ]

解析時に適用されるルールを指定しています。
`E`, `W`: pycodestyle(PEP8 に準拠しているかをチェック)のルールを適用しています。
`F`: pyflakes(未使用変数・未定義変数の検出)のルールを適用しています。
`I`: isort(インポート順序の整理)のルールを適用しています。
`B`: flake8-bugbear(潜在的なバグの検出)のルールを適用しています。
`C4`: flake8-comprehensions(非効率なリスト内包表記の指摘)のルールを適用しています。
`UP`: pyupgrade(最新バージョンにアップグレードするためのチェック)のルールを適用しています。

####

    ignore = [
        "E501",
        "B008",
        "C901",
        "W191",
        "B904",
    ]

解析時に無視されるルールを指定しています。
`E501`: 1 行が 88 文字を超えている際の警告を無視します。(整形ツールで処理するため。)
`B008`: 引数のデフォルト値に関数呼び出しを使用しないようにする警告を無視します。
`C901`: 関数の複雑度が高すぎる場合の警告を無視します。
`W191`: インデントに tab を使用した際の警告を無視します。
`B904`: `raise ... from ...`の形式になっていない際の警告を無視します。

####

    [tool.ruff.lint.per-file-ignores]
    "__init__.py" = ["F401"]

`__init__.py` 内での未使用のインポートを許可しています。

####

    [tool.ruff.lint.isort]
    known-third-party = ["fastapi", "pydantic", "starlette"]

`fastapi`、`pydantic`、`starlette`をサードパーティ製のライブラリとして認識するようにしています。

####

    [tool.mypy]
    disallow_untyped_defs = true
    ignore_missing_imports = true

全ての関数において、型ヒントを必須とするようにしています。
型情報のない外部ライブラリのエラーを無視するようにしています。

> [!NOTE]
> Mypy type checker をインストールするとルートディレクトリに.mypy_cache というフォルダが作成されます。(作成時に.gitignore も作成されるため git 管理対象外となります。)
