Template package-template
===================

## 概要

テンプレートから新規パッケージを作成するためのドキュメント。

## 利用方法

### 1. テンプレート取り込み
**use this template** から新規リポジトリを作成する（fork とは異なりテンプレートを用いて 0 からリポジトリを生成する形）

テンプレートの構成については **テンプレートのディレクトリ・ファイル構成** 、運用については **テンプレートの初期運用** のセクションを参照することを推奨。

![gitbub_1](https://user-images.githubusercontent.com/23420162/156067429-1a7bf66c-d31a-4449-a3c1-7e00fd13cdfc.png)

### 2. 環境構築

```sh
$ git clone ${新規パッケージのリポジトリの ssh code}
$ cd ${新規パッケージ} 
$ git switch -c feature/initialization
$ yarn 
```

### 3. 不要なファイルの削除

下記ファイルはパッケージに不要なファイルのため削除する。

- TEMPLATE.md

### 4. package の名称置換

下記ファイルの "package-template" を新規 package の名称にすべて置換する。
　
- package.json
- README.md
- CONTRIBUTING.md

### 5. パッケージの実装

この辺は自由。アプリケーションでどのような機能を共通化したいかなどによってテンプレートに追加・変更を加えていく。

テンプレート通りであれば、 `./src/**/*` に機能の実態を実装して、build 結果を `./dist` に出力した後、 `package.json` の files（publish するファイルの指定） や main（パッケージを読み込んだ時にルートに指定するファイル）、 type（esm や cjs の指定）、types（型ファイルの指定） などを調整する。

▼参考
- [package.json のフィールド一覧](https://docs.npmjs.com/cli/v8/configuring-npm/package-json)
- [公式ドキュメント](https://docs.npmjs.com/cli/v8/configuring-npm/package-json)
- その他多くの OSS

### 6. リリースのコメントアウトを解除

.github/workflows/production.yml の Release job のコメントアウトを解除する。

### 7. ドキュメントの更新

パッケージの内容や運用に合わせてドキュメントの追加・改修をする。

- README.md
  - Getting Started を削除
  - その他セクションはパッケージの内容に沿ったものに書き換え
- CONTRIBUTING.md
  - 必要に応じてセクションと内容を追加
  - テンプレートの内容とコメントで囲まれた内容についてはパッケージに合わせて書き換え
- .github/ISSUE_TEMPLATE/*.md
  - 必要に応じて issue file と内容を追加
  - 01 と 02 はデフォルトで用意しているものなので、必要に応じて内容を変更
- .github/workflows
  - 運用に合わせて workflow を追加
  - pretest と production はデフォルトで用意しているものなので、必要に応じて内容を変更
- .github/pull_request_template.md
  - 運用に合わせて内容を変更
- package.json
  - 必要に応じて内容を追加・変更

### 8. 認証情報の登録

パッケージのリポジトリの **Settings** > **secrets** > **repository environment** に **NODE_AUTH_TOKEN** の key と personal access token ( packages:write 権限 ) の value を登録する。

## テンプレートのディレクトリ・ファイル構成
```text
.
├── .commitlintrc.js // commitlint の設定ファイル
├── .editorconfig    // editorconfig の設定ファイル
├── .eslintignore    // eslint で除外をしたいパスを指定するファイル
├── .eslintrc.js     // eslint の設定ファイル
├── .github
│   ├── ISSUE_TEMPLATE           // issue 作成時に選択してテンプレート生成する機能のテンプレートファイルの格納場所
│   ├── pull_request_template.md // GitHub で　Pull Request を作成するときにテンプレートとなるファイル
│   └── workflows                // GitHub actions の設定ファイルの格納場所
├── .gitignore
├── .husky              // husky が実行するシェルの格納場所
├── .huskyrc.js         // husky の設定ファイル
├── .node-version       // nodejs のバージョンファイル
├── .npmrc              // npm の設定ファイル
├── .prettierignore     // prettier で除外をしたいパスを指定するファイル 
├── .prettierrc.js      // prettier の設定ファイル
├── .releaserc.js       // semantic-release の設定ファイル
├── CHANGELOG.md        // semantic-release によって更新されるバージョンごとのコミットをまとめたファイル
├── CONTRIBUTING.md     // リポジトリでコミットメントをするときにまず初めに参照するファイル
├── README.md
├── TEMPLATE.md         // package-template の使い方
├── changelog.config.js // git cz の設定ファイル
├── package.json
└── src                 // 開発ディレクトリ
```

## テンプレートの初期運用

[CONTRIBUTING.md](./CONTRIBUTING.md) を参照。

## [WIP] QA

