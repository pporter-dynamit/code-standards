# React Guidelines

Writing a single-page React.js application can have it's challenges if a good set of best practices and guidelines are not followed.

This document tries to detail the best practices that have worked on our teams and projects in the past, using React as the main client-side javascript framework to build rich, interactive single-page applications that can scale and evolve most easily.

_Note: This guide assumes you're building a client-rendered single page application (SPA). If you're looking to use React on the back-end, in a server-rendered environment, we'd recommend using [Next.js](https://nextjs.org/), but details about that implementation are not complete in this guide, although there will be some overlap, and many guidelines do apply._

## Getting Started

### Install via Create React App
Installation of React is preferred to be done through [Create React App](https://github.com/facebook/create-react-app). The [benefits](https://github.com/facebook/create-react-app#whats-included) of create-react-app are numerous, and it is the fastest way to get started working in a new project.

### Choosing the correct version
It's important to choose the version of React fits the needs of the project the best. Typically, this is the latest stable [version](https://reactjs.org/versions/). You will rarely start a project that isn't using the latest stable version of React at the time.

When choosing modules that enhance React's core functionality, it's important to ensure they are written in a way that works with the version of React you chose.

To see if a module supports the version of React you're using, look for a `peerDependencies` entry in the project's `package.json`.  For help reading `package.json`, [see this document on semver version](https://docs.npmjs.com/getting-started/semantic-versioning#semver-for-consumers) and how npm uses it.

The latest stable version of React as of this writing is React version [16.6.0](https://reactjs.org/versions/).

## Code Formatting

Having consistent code formatting and style is essential on projects or teams of one or more developers. It can help to reduce cognitive load when switching contexts and switching between projects.

We reach for [Prettier](https://prettier.io/) and [ESLint](https://eslint.org/) to ensure things like line length, variable naming conventions, and other general syntax rules are followed, and use available code editor [extensions](#step-4--install-extensions).

_Note: Create React App already comes with `eslint` configured. It does not, however, (at the time of writing) come with configuration for `prettier`._

### Prettier and ESLint Configuration

_Source: [Using Prettier with VS Code and Create React App](https://medium.com/technical-credit/using-prettier-with-vs-code-and-create-react-app-67c2449b9d08)_

#### Step 1: Install Prettier and ESLint Plugin

```
yarn add --dev --exact prettier
yarn add --dev eslint-plugin-prettier
```

#### Step 2: Create the Prettier and ESLint Configuration files

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

#### Step 3: Install extensions

Your editor likely has extension or plugins for ESLint and Prettier. To make the best of these tools, install the extensions so you can take advantage of auto-code formatting, syntax highlights, etc.

* Atom
  * [ESLint](https://atom.io/packages/linter-eslint) / [Prettier](https://atom.io/packages/prettier-atom)
* VSCode
  * [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) / [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
* Webstorm
  * [ESLint](https://www.jetbrains.com/help/webstorm/eslint.html) / [Prettier](https://prettier.io/docs/en/webstorm.html)

Each editor's extension for Prettier and ESlint will work a little bit differently.

If you're using VSCode, you can simply right click on any issues and click "Fix this prettier/prettier problem" or click "Fix all auto-fixable problems" (if the option appears).

#### Step 4: Formatting via the Command Line (optional)

Using Prettier is most easily done directly through your code editor using one of the above extensions, however it's also possible to use Prettier via the Command Line interface.

```
npx prettier --write src/**/*.js
```

The above command will read in any Javascript file in a `src` directory and overwrite its contents after being formatted through Prettier.

##### Add a Pre-Commit Hook for Prettier

_Note: This is unnecessary if you're already using `precommit-hook-eslint` since we configured eslint to use Prettier._

It's possible to run the prettier formatting pre-commit to ensure no files get committed without following Prettier rules:

```
yarn add --dev pretty-quick husky
```

And add the following entry to your package.json:

```
"husky": {
  "hooks": {
    "pre-commit": "pretty-quick --staged"
  }
}
```


## Components

In a React application, Components are the first-class citizens that make your app work.

### Naming Components

Components should be named with an `U`ppercase letter to begin, and simple names should be preferred over complex names.

### Functional Components

Use a stateless functional component to author components that don't need to take advantage of the [React component lifecycle methods](https://reactjs.org/docs/react-component.html#the-component-lifecycle) and don't need to hold local state. In other words, if all the component needs to render is a set of _pre-determined_ data, then a function is all your need.

```javascript
import React from 'react';

const Greeting = props => {
  <h1>Hello, {props.name}!</h1>
}

export default Greeting;
```

_Note: Function components will always re-render, even if no new props were received. If you're using `React ^16.6`, you can use the [memo](https://reactjs.org/blog/2018/10/23/react-v-16-6.html#reactmemo) function to help performance._

#### PropTypes for Components

All components, whether stateless or stateful, should implement `PropTypes` definitions when they are able to receive props.

```javascript
import React from 'react';
import PropTypes from 'prop-types';

const Greeting = props => {
  <h1>Hello, {props.name}!</h1>
}

Greeting.propTypes = {
  name: PropTypes.string.isRequired
};

export default Greeting;
```

This can be very helpful in debugging.

#### Naming Functional Components

Prefer to name the component as simple as possible when creating a functional component. For example, a `Button`, which is usually a candidate for a functional component over a class component, should be named `Button` instead of `ButtonComponent`.

### Class Components

A class component can take advantage of the lifecycle methods and local state that React's core Component class provides. Choose this type of component when you need a component to hold it's own state and/or use lifecycle hooks.

```javascript
import React, { Component } from 'react';

class GreetingComponent {
  state = {
    name: 'Nobody'
  };

  componentDidMount() {
    this.setState({ name: 'Matt' });
  }

  render() {
    <h1>Hello, {this.state.name}</h1>
  }
}

export default GreetingComponent;
```

The above component renders first `Hello, Nobody` then immediately re-renders itself and reads `Hello, Matt`.

#### Default State and Props

ES6 classes have the ability to define methods and properties on class instances. Make use of this when setting up a component by adding `state` and `defaultProps` when you need them, as opposed to setting up state or props in a `constructor`. This will lead to more readability and fewer bugs.

```javascript
// Bad
export default class GreetingComponent {
  constructor(props) {
    if (!props.name) {
      this.props.name = 'Nobody';
    }
  }
}

// Good
export default class GreetingComponent {
  static defaultProps: {
    name: 'Nobody'
  };
}

// Bad
export default class GreetingComponent {
  constructor(props) {
    super(props);
    this.state = { name: 'Nobody' };
  }
}

// Good
export default class GreetingComponent {
  state = {
    name: 'Nobody'
  };
}
```

#### Destructure in your Render Method

The `render` method of a React component can become large in some cases, and can have a lot of dependencies.

When data for your component comes from `state` or `props`, be sure to [destructure](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) your data before using it in JSX.

The following examples are simple, but most real-world scenarios will involve getting data from complex objects, so destructuring is best.

```javascript
// Bad
export default class GreetingComponent {
  render() {
    <div>
      <p>Here is a sentence that depends on {this.state.name} (a user's name).</p>
    </div>
  }
}

// Good
export default class GreetingComponent {
  render() {
    const { name } = this.state;
    <div>
      <p>Here is a sentence that depends on {name} (a user's name).</p>
    </div>
  }
}
```

## Routing

Routing should be achieved using [React Router](https://reacttraining.com/react-router/web/guides/quick-start) using the [react-router-dom](https://github.com/ReactTraining/react-router/tree/master/packages/react-router-dom) package.

At the time of writing, Create React App does not come with React Router installed, so you must add it manually.

```
yarn add --dev react-router-dom
```

### Scroll to top

As a best practice for a SPA, ensure users are not stuck at the bottom of a page when navigating Back from a page. To achieve this, see the official docs on [scroll restoration](https://reacttraining.com/react-router/web/guides/scroll-restoration) and implement a `<ScrollToTop />` component in your project.

```javascript
import React from "react";
import { BrowserRouter as Router } from "react-router-dom";

class ScrollToTop extends Component {
  componentDidUpdate(prevProps) {
    if (this.props.location !== prevProps.location) {
      window.scrollTo(0, 0);
    }
  }

  render() {
    return this.props.children;
  }
}

export default withRouter(ScrollToTop);

// Then render it at the top of your app, but below Router
const App = () => (
  <Router>
    <ScrollToTop>
      <App/>
    </ScrollToTop>
  </Router>
)
```

