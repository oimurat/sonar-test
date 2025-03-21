# React用各種設定テンプレート説明

## 1. .vscode/settings.json

#### 概要
React開発におけるVSCodeの設定が記載されています。

#### 内容
    "editor.formatOnSaveMode": "modificationsIfAvailable",
	"editor.formatOnSave": true
ファイル保存時に自動的にコード整形を行います。
1回目の保存時はコード全体を整形しますが、2回目以降は変更箇所のみを整形します。

####
    "[言語名]": {
            "editor.defaultFormatter": "esbenp.prettier-vscode"
	}
各言語のソースコードにおいて、整形ツールとしてprettierを使用するように指定しています。

## 2. .prettierrc

#### 概要
整形ツールとして使用するprettierの設定が記載されています。

#### 内容
    "tabWidth": 4
インデントのスペースの数を4にしています。

####
    "useTabs": false
インデントにタブではなくスペースを使用するようにしています。

####
    "semi": true
整形時に全ての文の最後にセミコロンを追加するようにしています。

####
    "singleQuote": true
整形時にダブルクォートをシングルクォートに変更するようにしています。

## 3. eslint.config.js

#### 概要
静的解析ツールとして使用するESLintの設定が記載されています。

#### 内容
    import eslintConfigPrettier from 'eslint-config-prettier';
    ...
                extends: [
			    ...
			    eslintConfigPrettier,
		    ],
整形ツールのprettierと競合を起こさないようにESLintの整形機能を無効化しています。

####
    '@typescript-eslint/naming-convention': [
	      'error',
          {
                  selector: 'ターゲットとする識別子',
                  format: ['一致させる型'],
          },
          ...
    ],
命名規則に指定されている型で記載されていない場合、コード上に赤波線が引かれるようにしています。

####
    settings: {
            react: {
                    version: 'detect',
			},
		},
ESLintがReactのバージョンを自動的に検出するように指示しています。