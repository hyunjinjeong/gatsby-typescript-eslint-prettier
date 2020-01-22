# Gatsby-TypeScript-ESLint-Prettier for Github Pages

This repository is to figure out how to set up Gatsby with TypeScript, ESLint and Prettier and deploy the project to Github Pages.

## Installation of Gatsby.js

Prerequisites: `node.js`, `npm`, `git`

```shell
# Install Gatsby
npm install -g gatsby-cli

# Create a project
gatsby new REPO_NAME https://github.com/gatsbyjs/gatsby-starter-hello-world

# Move a directory
cd REPO_NAME

# Open a developer page
gatsby develop
```

## TypeScript

First, make sure that you have installed `TypeScript`.

```shell
npm install typescript
```

Then, there are two ways of applying TypeScript to the project.

### 1. Use a Starter

You can simply use this starter instead of the default starter when you set up.

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

In `gatsby-config.js`, add the plugin you installed.

```js
module.exports = {
  plugins: ['gatsby-plugin-typescript'],
};
```

In `tsconfig.json`, two options should be uncommented so that we can use typescript in the project.

```json
{
  "allowJS": true,
  "jsx": "preserve"
}
```

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
  **Browser**
- What format do you want your config file to be in?
  **JSON**

It will also install `eslint-plugin-react@latest`, `@typescript-eslint/eslint-plugin@latest`, and `@typescript-eslint/parser@latest` on your project.

### Integrate ESLint with Prettier

You need to install `eslint-config-prettier` and `eslint-plugin-prettier` to use Prettier with ESLint.

```shell
npm install --save-dev eslint-config-prettier eslint-plugin-prettier
```

Now, let us add some settings to the `.eslintrc.json` config file to lint TypeScript files and apply Prettier:

```json
{
  "extends": [
    "react-app",
    "plugin:@typescript-eslint/recommended",
    "plugin:@typescript-eslint/recommended-requiring-type-checking",
    "plugin:prettier/recommended",
    "prettier/react",
    "prettier/@typescript-eslint"
  ],
  "parserOptions": {
    "project": "./tsconfig.json"
  },
  "plugins": ["react", "@typescript-eslint", "prettier"],
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
    }
  }
}
```

## References

[TypeScript-ESLint - Getting Started](https://github.com/typescript-eslint/typescript-eslint/blob/master/docs/getting-started/linting/README.md)

[Gatsby - Tutorial](https://www.gatsbyjs.org/tutorial/part-zero/)

[Prettier - Integrating with Linters](https://prettier.io/docs/en/integrating-with-linters.html)
