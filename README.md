# @flynncao/eslint-config

[![npm](https://img.shields.io/npm/v/@flynncao/eslint-config?color=444&label=)](https://npmjs.com/package/@flynncao/eslint-config) 

This repository was highly inspired by [antfu](https://github.com/antfu) 's related [ESLint presets](https://github.com/antfu/eslint-config), probing to avoid using prettier in VSCode while keep code clean and beneficial for teamwork.

- Single quotes, no semi
- Auto fix for formatting (aimed to be used standalone **without** Prettier)
- Designed to work with TypeScript, Vue out-of-box
- Lint also for json, yaml, markdown
- Sorted imports, dangling commas
- Reasonable defaults, best practices, only one-line of config
- **Style principle**: Minimal for reading, stable for diff
- Case Checking with [Case Police](https://github.com/antfu/case-police)

## Usage

### Install

```bash
pnpm add -D eslint @flynncao/eslint-config
```

### Config `.eslintrc`

```json
{
  "extends": "@flynncao"
}
```

> You don't need `.eslintignore` normally as it has been provided by the preset.

### Add script for package.json

For example:

```json
{
  "scripts": {
    "lint": "eslint .",
    "lint:fix": "eslint . --fix"
  }
}
```

### VS Code support (auto fix)

Install [VS Code ESLint extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

Add the following settings to your `settings.json`:

```jsonc
{
  "prettier.enable": false,
  "editor.formatOnSave": false,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true,
    "source.organizeImports": false
  },

  // The following is optional.
  // It's better to put under project setting `.vscode/settings.json`
  // to avoid conflicts with working with different eslint configs
  // that does not support all formats.
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "typescript",
    "typescriptreact",
    "vue",
    "html",
    "markdown",
    "json",
    "jsonc",
    "yaml"
  ]
}
```

### TypeScript Aware Rules

Type aware rules are enabled when a `tsconfig.eslint.json` is found in the project root, which will introduce some stricter rules into your project. If you want to enable it while have no `tsconfig.eslint.json` in the project root, you can change tsconfig name by modifying `ESLINT_TSCONFIG` env.

```js
// .eslintrc.js
process.env.ESLINT_TSCONFIG = 'tsconfig.json'

module.exports = {
  extends: '@flynncao'
}
```

### Lint Staged

If you want to apply lint and auto-fix before every commit, you can add the following to your `package.json`:

```json
{
  "simple-git-hooks": {
    "pre-commit": "pnpm lint-staged"
  },
  "lint-staged": {
    "*": "eslint --fix"
  }
}
```

and then

```bash
npm i -D lint-staged simple-git-hooks
```

## FAQ by Antfu

### Prettier?

[Why I don't use Prettier](https://flynncao.me/posts/why-not-prettier)

### How to lint CSS?

This config does NOT lint CSS. I personally use [UnoCSS](https://github.com/unocss/unocss) so I don't write CSS. If you still prefer CSS, you can use [stylelint](https://stylelint.io/) for CSS linting.

### I prefer XXX...

Sure, you can override the rules in your `.eslintrc` file.

<!-- eslint-skip -->

```jsonc
{
  "extends": "@flynncao",
  "rules": {
    // your rules...
  }
}
```

Or you can always fork this repo and make your own.

## FAQ 
To be continued.
## Check Also

- [flynncao/vscode-settings](https://github.com/flynncao/vscode-settings) - My VS Code settings

## License

[MIT](./LICENSE) License &copy; 2019-PRESENT [Flynn Cao](https://github.com/flynncao)
