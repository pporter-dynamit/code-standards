# React Guidelines

Writing a single-page React.js application can have it's challenges if a good set of best practices and guidelines are not followed.

This document tries to detail the best practices that have worked on our teams and projects in the past, using React as the main client-side javascript framework to build rich, interactive single-page applications that can scale and evolve most easily.

_Note: This guide assumes you're building a client-rendered single page application (SPA). If you're looking to use React on the back-end, in a server-rendered environment, we'd recommend using [Next.js](https://nextjs.org/), but details about that implementation are not complete in this guide, although there will be some overlap, and many guidelines do apply._

## Getting Started

### Install via Create React App
Installation of React is preferred to be done through [Create React App](https://github.com/facebook/create-react-app). The [benefits](https://github.com/facebook/create-react-app#whats-included) of create-react-app are numerous, and it is the fastest way to get started working in a new project.

### Choosing the correct version
It's important to choose the version of React fits the needs of the project the best. Typically, this is the latest stable version of [version](https://reactjs.org/versions/). You will rarely start a project that isn't using the latest stable version of React at the time.

When choosing modules that enhance React's core functionality, it's important to ensure they are written in a way that works with the version of React you chose.

To see if a module supports the version of React you're using, look for a `peerDependencies` entry in the project's `package.json`.  For help reading `package.json`, [see this document on semver version](https://docs.npmjs.com/getting-started/semantic-versioning#semver-for-consumers) and how npm uses it.

The latest stable version of React as of this writing is React version [16.6.0](https://reactjs.org/versions/).

## Code Formatting

Having consistent code formatting and style is essential on projects or teams of one or more developers. It can help to reduce cognitive load when switching contexts and switching between projects.

We reach for [Prettier](https://prettier.io/) and [Eslint](https://eslint.org/) to ensure things like line length, variable naming conventions, and other general syntax rules are followed, and use available code editor [extensions](#step-4--install-extensions).

_Note: Create React App already comes with `eslint` configured. It does not, however, (at the time of writing) come with configuration for `prettier`. We find `prettier` to be crucial in achieving the DRY principle, so we recommend it on all of our projects._

### Prettier and Eslint Configuration

#### Step 1: Eject from Create React App

Assuming your created your application using Create React App, you will need to [eject](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#npm-run-eject) your react application to use `prettier`.

```
npm run eject
```

_Note: It is common to `eject` from `create-react-app`. You will lose the ability to get upstream changes from the `create-react-app` project, but it allows for much more fine-grained customization of the project. It will copy the `react-scripts` project dependencies into your project and update scripts in your `package.json`._

#### Step 2: Add Eslint and Prettier

To add `prettier` to your project, run the following command:

```
npm i --save-dev eslint eslint-plugin-prettier
```

#### Step 3: Configure Eslint and Prettier

Create a `.eslintrc` file at the root of your project and paste these contents:

```
{
  "extends": "react-app",
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": "error"
  }
}
```

If you are not happy with the default Prettier configuration, then create a `.prettierrc` file in the root of your project with any [options](https://prettier.io/docs/en/options.html) you'd like:

```
{
  "singleQuote": true,
  "trailingComma": "es5"
}
```

#### Step 4: Install extensions

Your editor likely has extension or plugins for Eslint and Prettier. To make the best of these tools, install the extensions so you can take advantage of auto-code formatting, syntax highlights, etc.

* Atom
  * [Eslint](https://atom.io/packages/linter-eslint)
  * [Prettier](https://atom.io/packages/prettier-atom)
* VSCode
  * [Eslint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
  * [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
* Webstorm
  * [Eslint](https://www.jetbrains.com/help/webstorm/eslint.html)
  * [Prettier](https://prettier.io/docs/en/webstorm.html)

