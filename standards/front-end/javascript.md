# JavaScript

We follow the community-driven [Airbnb Style Guide](https://github.com/airbnb/javascript), with the following exceptions:

Rule | Setting
--- | ---
[no-console](http://eslint.org/docs/rules/no-console) | Not enforced
[arrow-body-style](http://eslint.org/docs/rules/arrow-body-style) | Not enforced
[quote-props](http://eslint.org/docs/rules/quote-props) | "consistent-as-needed"
[comma-dangle](http://eslint.org/docs/rules/comma-dangle) | "always-multiline"
[max-len](http://eslint.org/docs/rules/max-len) | Not enforced

## General Best Practices at Dynamit
- Vanilla JavaScript
- use [axios](https://github.com/axios/axios) for ajax
- For carousels/sliders, use [Flickity](https://flickity.metafizzy.co/)
- For browser cookie getting/setting, use [js-cookie](https://github.com/js-cookie/js-cookie)
- write in [modules](https://eloquentjavascript.net/10_modules.html)
- prefer libraries to full-blown frameworks
- write [modern javascript](https://babeljs.io/) when you can
- keep bundles small (< 50k), consider [lazy-loading](https://webpack.js.org/guides/lazy-loading) pages / components (or [chunking](https://medium.com/react-weekly/code-chunking-with-webpack-a-pragmatic-approach-e17e8bcc6453) with webpack)
- Thoroughly document code use [JSDoc](http://usejsdoc.org/) conventions
- [Full JavaScript Guidelines](javascript.html)
