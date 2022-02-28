Contributing to package-template
===================

## コミットメントにあたってのルールや注意点

<!-- パッケージを開発するにあたって注意する点などあれば記載する -->

### コミットルール

<!-- テンプレートの内容 -->
git commit ではなく、可能な限り yarn commit を使用してください。 

yarn commit では [git-cz](https://github.com/streamich/git-cz) というコミットメッセージを [Conventional Commits](https://www.conventionalcommits.org/ja/v1.0.0/) の規約に合わせてコミットするようになっています。

GitHub Actions の production workflow では [semantic-release](https://github.com/semantic-release/semantic-release) というライブラリを使用して下記ファイルの自動更新とリリースを行いますが、 適切なバージョニングや関連ファイルの の更新のためにコミットメッセージを Conventional Commits の規約に合わせておく必要があり、そのために git cz の使用を推奨しています。

```text
- CHANGELOG.md: commit message からバージョニングごとに内容を記載しています。
- package.json: commit 内容を精査してバージョニングをします。
- git tag: package.json に合わせた tag 生成をします。
```

yarn commit が面倒であれば、git cz を global install して bashrc や zshrc で alias を貼っておくのがよいでしょう。

または、通常の git commit -m を使用するかです。当パッケージには（テンプレートのものを外していなければ） husky の commit hook で Conventional Commits の commitlint が実行されるようになっており、規約を違反している場合に commit を拒否するルールが設定されているので安心してください。
<!-- テンプレートの内容 -->


### バージョニングの仕組み

<!-- テンプレートの内容 -->
| prefix          | 結果              | 
|-----------------|-----------------|
| feat            | minor ( 1.x.0 ) |
| fix             | patch ( 1.0.x ) |
| refactor        | patch ( 1.0.x ) |
| chore           | patch ( 1.0.x ) |
| BREAKING CHANGE | major ( x.0.0 ) |
| others          | not update      |
<!-- テンプレートの内容 -->

## ブランチ管理

<!-- ブランチ名に対する役割などを記載する。 -->

<!-- テンプレートの内容 -->
| ブランチ | 内容       | 
|------|----------|
| main | リリースブランチ |
<!-- テンプレートの内容 -->

## リリース工程

<!-- ブランチ運用やリリース工程があれば記載する。 -->

<!-- テンプレートの内容 -->
1. main branch から開発するための feature branch ( feature/hoge ) を作成
2. main に対して PR を立てて内容を記載
3. GitHub Actions の Pretest workflow が success になるのを待ち merge（fail の場合はログを見てエラー対応をする）
4. merge 後、GitHub Actions の Production workflow が動作し、バージョニング・リリース・リリース関連ファイルの更新を実施
5. Repository の actions で workflow の status を確認し、success の場合はローカル環境で main branch に移動して `git pull`
6. 関連チャンネルでリリースを通知
<!-- テンプレートの内容 -->
