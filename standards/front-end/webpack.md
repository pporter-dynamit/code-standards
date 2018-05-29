# Webpack


## Long-Term Caching

Webpack gives us the ability to use long-term caching for our production builds. The means that:

- Users will only have to download only those files that have changes.
- Improves performance on future visits because of this.
- You will need to use the [chunkHash](https://webpack.js.org/guides/caching/#output-filenames) in order to take advantage of long-term [caching](https://webpack.js.org/guides/caching/).

## Code Splitting

Webpack allows us to seperate our code into multiple bundles in the following ways:

- Using [entry points](https://webpack.js.org/guides/code-splitting/#entry-points)
- Using [dynamic imports](https://webpack.js.org/guides/code-splitting/#dynamic-imports)

## HMR (Hot Module Replacement)

Taking advantage of [HMR](https://webpack.js.org/guides/hot-module-replacement/) helps to speed up the development process. It allows to update modules without the need for a full page refresh.

## Utilizing Tree Shaking

Eliminating dead code is another way Webpack can help optimize your production builds. Since the UglifyJSPlugin and production mode [in Webpack 4] will minify and remove unused code it is best to use these features in production.

## Monitoring Build Performance

There are a lot of useful tools to help aid in monitoring your Webpack builds. Here are a few:

- [The official analyse tool](https://github.com/webpack/analyse)
- [Webpack Visualizer](https://chrisbateman.github.io/webpack-visualizer/)
- [Webpack Bundle Analyzer](https://www.npmjs.com/package/webpack-bundle-analyzer)
- [Webpack Monitor](http://webpackmonitor.com/)

## Setting Performance Goals

Using the [performance](https://webpack.js.org/configuration/performance/) property you can set the following:

- Hints or Warnings if chunks go over a specific max file size.
- Max entry point size
- Max asset size

## Setting Global Variables

When setting anything that would need to be globabl (ir tokens) they can be created using the [DefinePlugin](https://webpack.js.org/plugins/define-plugin/#components/sidebar/sidebar.jsx)