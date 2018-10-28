# React Guidelines

Writing a single-page React.js application can have it's challenges if a good set of best practices and guidelines are not followed.

This document tries to detail the best practices that have worked before on projects using React to build rich, interactive front-ends that may have complicated state management needs and user needs that will likely evolve as the project does.

## 1.  Getting Started

### Install via `create-react-app`
Installation of React is preferred to be done through [create-react-app](create-react-app). The [benefits](https://github.com/facebook/create-react-app#whats-included) of create-react-app are numerous, and it is the fastest way to get started working in a new project.

### Choosing the correct version
It's important to choose the version of React fits the needs of the project the best. Typically, this is the latest stable version of [version](https://reactjs.org/versions/). You will rarely start a project that isn't using the latest stable version of React at the time.

When choosing modules that enhance React's core functionality, it's important to ensure they are written in a way that works with the version of React you chose.

To see if a module supports the version of React you're using, look for a `peerDependencies` entry in the project's `package.json`.  For help reading `package.json`, [see this document on semver version](https://docs.npmjs.com/getting-started/semantic-versioning#semver-for-consumers) and how npm uses it.

The latest stable version of React as of this writing is React version [16.6.0](https://reactjs.org/versions/).
