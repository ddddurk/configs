# @ddddurk/configs

Configs for using [commitlint](https://commitlint.js.org/#/), [eslint](https://eslint.org), [husky](https://typicode.github.io/husky), [lint-staged](https://github.com/okonet/lint-staged), [prettier](https://prettier.io), [typescript](https://www.typescriptlang.org), with [yarn](https://yarnpkg.com).

## Installation

```bash
yarn add @commitlint/cli @commitlint/config-conventional @ddddurk/configs @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint eslint-config-prettier eslint-plugin-simple-import-sort eslint-plugin-unused-imports husky lint-staged prettier typescript -D
```

### Setup

1. Create `prepare` script to initialize `husky` in `package.json`:

```json
{
  "scripts": {
    "prepare": "husky install"
  }
}
```

2. Run `prepare` script:

```bash
yarn prepare
```

## Usage

### `commitlint`

1. Create `.commitlintrc.js`:

```js
module.exports = {
  ...require("@ddddurk/configs/commitlint.json")
};
```

2. Create `.husky/commit-msg`:

```bash
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npx --no -- commitlint --edit ${1}
```

### `eslint` and `prettier`

1. Create `.d-eslint.js`:

```js
module.exports = require("@ddddurk/configs/eslint.json");
```

2. Create `.prettierrc.js`:

```js
module.exports = {
  ...require("@ddddurk/configs/prettier.json")
};
```

3. Create `.eslintrc.js`:

```js
module.exports = {
  extends: ["./.d-eslint", "prettier"]
};
```

4. Create `.lintstagedrc.js`:

```js
module.exports = {
  ...require("@ddddurk/configs/lint-staged.json")
};
```

5. Create `lint` script in `package.json`:

```json
{
  "scripts": {
    "lint": "eslint --fix './**/*.{js,json,jsx,ts,tsx}' && prettier --write .",
    "prepare": "husky install"
  }
}
```

6. Create `.husky/pre-commit`:

```bash
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npx lint-staged
```

### `typescript`

1. Create `tsconfig.json`:

```json
{
  "extends": "@ddddurk/configs/tsconfig.json"
}
```
