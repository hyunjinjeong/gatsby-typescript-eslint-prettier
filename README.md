# Gatsby-TypeScript-ESLint-Prettier for Github Pages

This repository is to figure out how to set up Gatsby with TypeScript, ESLint and Prettier and deploy the project to Github Pages.

## Installation of Gatsby.js

Prerequisites: `node.js`, `npm`, `git`

Starter: In this project, I'm using `gatsby-starter-hello-world` as it is the most basic starter, but there are many different starters in [Gatsby Starters](https://www.gatsbyjs.org/starters/?v=2). You can choose any starter you want.

```shell
# Install Gatsby
npm install -g gatsby-cli

# Create a project using a starter
gatsby new REPO_NAME https://github.com/gatsbyjs/gatsby-starter-hello-world

# Move a directory
cd REPO_NAME

# Open a developer page
gatsby develop
```

If you can see the page, you installed Gatsby successfully.

## TypeScript

First, make sure that you have installed `TypeScript`.

```shell
npm install typescript
```

Then, there are two ways of applying TypeScript to the project.

### 1. Use a Starter

You can simply use this TypeScript starter when you create a project. I have no idea how it works because I haven't used it.

```shell
gatsby new REPO_NAME https://github.com/haysclark/gatsby-starter-typescript
```

### 2. Use a Plugin (Recommended)

Otherwise, you need to install a plugin for TypeScript:

```shell
npm install gatsby-plugin-typescript
```

Initialize a TypeScript configuration.

```shell
# Generate tsconfig.json
npx tsc --init
```

In `gatsby-config.js`, add the plugin.

```js
module.exports = {
  plugins: ['gatsby-plugin-typescript'],
};
```

If you don't install any other pacakges like ESLint, you need to install these type definition packages manually.

```shell
npm install --save-dev @types/react @types/react-dom @types/node
```

In `tsconfig.json`, these options should be set if you want to use project files as they are without getting errors.

```json
{
  "compilerOptions": {
    "allowJS": true /* Allow javascript files to be compiled. */,
    "jsx": "preserve" /* Specify JSX code generation: 'preserve', 'react-native', or 'react'. */,
    "noEmit": true /* Do not emit outputs. */
  },
  "include": ["src"]
}
```

For more information about `tsconfig.json`, visit [TypeScript Compiler Options](https://www.typescriptlang.org/docs/handbook/compiler-options.html)

You can now change the filename `index.js` to `index.tsx`.

## Apply ESLint and Prettier

### Install ESLint

`Prettier` is already installed. To install `ESLint`, run:

```shell
# ESLint
npm install --save-dev eslint
```

Since we use TypeScript, we also have to install packages for it.

```shell
# Required pacakges
npm install --save-dev @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

Then initialize ESLint.

```shell
npx eslint --init
```

During the initialization process, choose options whichever you prefer. However, the configuration steps will differ depending on what you chose. These are my recommendations.

- How would you like to use ESLint?
  **To check syntax and find problems**
- What type of modules does your project use?
  **JavaScript modules (import/export)**
- Which framework does your project use?
  **React**
- Does your project use TypeScript?
  **Yes**
- Where does your code run?
  **Browser, Node**
- What format do you want your config file to be in?
  **JSON**

It will also install `eslint-plugin-react@latest`, `@typescript-eslint/eslint-plugin@latest`, and `@typescript-eslint/parser@latest` on your project.

### Integrate ESLint with Prettier

You need to install `eslint-config-prettier` and `eslint-plugin-prettier` to use Prettier with ESLint.

```shell
npm install --save-dev eslint-config-prettier eslint-plugin-prettier
```

Now, let's add some settings to the `.eslintrc.json` config file in order to lint TypeScript files and apply Prettier:

```json
{
  "extends": [
    "plugin:@typescript-eslint/recommended",
    "plugin:@typescript-eslint/recommended-requiring-type-checking",
    "plugin:prettier/recommended",
    "prettier/react",
    "prettier/@typescript-eslint"
  ],
  "parserOptions": {
    "project": "./tsconfig.json"
  },
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": "error",
    "react/jsx-filename-extension": [
      1,
      {
        "extensions": [".jsx", ".tsx"]
      }
    ]
  },
  "settings": {
    "import/resolver": {
      "node": {
        "extensions": [".js", ".jsx", ".ts", ".tsx"]
      }
    },
    "react": {
      "version": "detect"
    }
  }
}
```

### (Optional) Use Airbnb's .eslintrc

Of many linting rules, Airbnb's rule is by far the most popular in the world. I recommend using this rule in your project.

Install the configuration.

```shell
npx install-peerdeps --dev eslint-config-airbnb
```

In `.eslintrc.json`, add it in 'extends'.

```shell
"extends": ["airbnb"]
```

### Prettier Setting

In the `.prettierrc` configuration file, you can customize options. Visit [Prettier Options](https://prettier.io/docs/en/options.html) for the detail. The options below are mine:

```json
{
  "printWidth": 80,
  "tabWidth": 2,
  "useTabs": false,
  "semi": true,
  "singleQuote": true,
  "quoteProps": "consistent",
  "jsxSingleQuote": false,
  "trailingComma": "all",
  "bracketSpacing": true,
  "jsxBracketSameLine": false,
  "arrowParens": "avoid",
  "endOfLine": "lf"
}
```

## Deploy the project to Github Pages

```shell
npm install --save-dev gh-pages
```

## You're good to go

You've just finished the setup using Gatsby, TypeScript, ESLint, Prettier and Github Pages, which is the most annoying part of developing.

## References

[TypeScript-ESLint - Getting Started](https://github.com/typescript-eslint/typescript-eslint/blob/master/docs/getting-started/linting/README.md)

[Gatsby - Tutorial](https://www.gatsbyjs.org/tutorial/part-zero/)

[Gatsby - How Gatsby Works with GitHub Pages](https://www.gatsbyjs.org/docs/how-gatsby-works-with-github-pages/)

[Prettier - Integrating with Linters](https://prettier.io/docs/en/integrating-with-linters.html)

[npm - eslint-config-airbnb](https://www.npmjs.com/package/eslint-config-airbnb)
