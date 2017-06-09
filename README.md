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
    "lint-staged": "lint-staged",
    "precommit": "lint-staged"
  }
```

たとえばこのように記述しておくと、コミットが行われる前に、lint-stagedが実行されます。そしてエラーが発見されたら、コミットが行われずに終了します。
