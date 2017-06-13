# Engine Vol. 11 - エラーのあるファイルがコミットされるのを防ぐ仕組みを作る

## lint-staged

[lint-staged](https://github.com/okonet/lint-staged)を使うと、Gitのステージングエリアにステージされたファイルを対象に、何かすることができます。

```
  "lint-staged": {
    "*.css": "stylelint",
    "*.js": "eslint"
  },
  "scripts": {
    "lint-staged": "lint-staged"
  }
```

例えばこのようにpackage.jsonに記述しておくと、`npm run lint-staged`でlint-stagedが走ります。そして、拡張子がcssのファイルがステージされていれば、stylelintがそのファイルに対して実行され、拡張子がjsのファイルがステージされていれば、eslintがそのファイルに対して実行されます。

## huskey

[huskey](https://github.com/typicode/husky)を使うと、Gitの特定のアクションが発生したときに、コマンドを実行できます。

```
  "lint-staged": {
    "*.css": "stylelint",
    "*.js": "eslint"
  },
  "scripts": {
    "precommit": "lint-staged"
  }
```

たとえばこのようにpackage.jsonに記述しておくと、コミットが行われる前に、lint-stagedが実行されます。そしてエラーが発見されたら、コミットが行われずに終了します。

## 応用編

lint-stagedとhuskeyで、コミット前に自動修正をする仕組みを作ることができます。

```
  "lint-staged": {
    "*.js": ["eslint --fix", "git add"]
  },
  "scripts": {
    "precommit": "lint-staged"
  }
```

このようにpackage.jsonに記述しておくと、コミットが行われる前に、ステージされたjsファイルに対して次の処理が走ります。

* ESLintが自動修正をする（`eslint --fix`）
    * 自動修正できない問題があれば、それで処理は終了し、コミットは行われない
* 修正後の変更内容をステージする（`git add`）
