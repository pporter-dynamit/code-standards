# Front-end Code Standards

* [HTML](html.html)
* [Stylesheets](stylesheets.html)
* [JavaScript](javascript.html)

# Dynamit's Front-end Playbook

---

# Table of Contents

1. [Development Process](#development-process)
  * [Version Control](#version-control)
  * [Code Quality](#code-quality)
  * [Ops](#ops)
  * [Preventative Maintenance](#preventative-maintenance)
2. [Markup](#markup)
3. [Style Sheets](#style-sheets)
4. [JavaScript](#javascript)
5. [Performance](#performance)
6. [SEO & Meta](#seo--meta)
7. [Accessibility](#accessibility)

---

# Purpose of Standards
This repo contains a list of code standards for the Dynamit Front End Development team. What follows is a starting point for new developers. This is _not_ a strict set of rules, but more like guidelines. To continue to grow and innovate, we do not hold these to be all encompassing. **Do not** let this document hinder you from trying new ideas or technologies.

# Development Process

## Version Control

- Use Git.
- Use [semver](https://semver.org/) for versioning.
- Get familiar with [Git Flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow). Determine with project team preferred Git workflow.
- Associate a ticket number with a commit when applicable. Should also be in the branch name.

## Code Quality
- Read through the individual pages to find more specific code quality guidelines

## Ops

- Use [CodePen](https://codepen.io/) or [Web Maker](https://chrome.google.com/webstore/detail/web-maker/lkfkkhfhhdkiemehlpkgjeojomhpccnh?hl=en) to rapidly prototype ideas.
- Use the [Front End Boilerplate](https://github.com/Dynamit/front-end-boilerplate) when starting a project. Fork and submit pull requests for improvements.
- Build Process - Gulp - Use gulp to manage the asset compilation pipeline
- Build Process - Webpack - Use webpack for asset bundling

## Preventative Maintenance

- keep tooling up to date
- keep disk perms clean

# Markup

- use semantic markup 
- structure pages (headings, sections) in logical, linear order
- only 1 `<h1>` per page
- all pages must have a `<main>`
- [Full HTML guidelines](html.html)

# Style Sheets

- Sass is preferred
- use low-specificty selectors. avoid ids, tags, combining selectors, prefer classes and attr selectors
- compose styles mobile-first. example: @media (min-width: 768px) as opposed to @media (max-width: 767px)
- use bullet-proof font-face declaration

- use BEM or ABEM, hyphenated, single dash modifier with property prefixes but no parent prefix 
```html
<div class="teaser"></div><!-- block -->
<div class="content-block"></div><!-- block -->
<div class="content-block__title"></div><!-- element -->
<div class="content-block__title -color-green"></div><!-- modifier -->
<div class="content-block__image cover"></div><!-- global utility -->
```
- no double-dash modifiers `--color-green` as that will not work in IE
- [DRY (don't repeat yourself)](https://vanseodesign.com/css/dry-principles/)
- [Full Stylesheet Guidelines](stylesheets.html)


# JavaScript

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

# Performance

- use [Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
- turn on server-side caching
- develop for mobile users on 3G (slower) networks
- test on real devices
- use progressive jpgs
- use [resource hints](https://www.keycdn.com/blog/resource-hints/)
- prevent render-blocking javascript using [async or defer](http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html)
- gzip
- minify scripts and stylesheets
- turn off sourcemaps in production
- reduce http requests
- lazy-load [css](https://github.com/filamentgroup/loadCSS) and [js](https://webpack.js.org/guides/lazy-loading)
- lazy load [images](https://github.com/aFarkas/lazysizes)

# SEO & Meta

Include a canonical url tag on each page. Use [trailing slashes](http://googlewebmastercentral.blogspot.com/2010/04/to-slash-or-not-to-slash.html) appropriately. Prefer `https` when available.

```html
<link rel="canonical" href="https://example.com/some-page" />
```

- use a well-formatted title tag on every page
- include social meta data https://adactio.com/journal/9881
- include a retina favicon https://daringfireball.net/2013/01/retina_favicons
- add schema.org tags

# Testing
* Use IE VMS to test code (or [BrowserStack](https://www.browserstack.com))

# Accessibility
[Full documentation](accessibility.html)

# General Resources
* [Dynamit Only Resource](https://docs.google.com/document/d/1iYwcqdtfH6Lv0_SBRX4HF91fqD7soP3uD1KkeyNUFD0/edit?usp=sharing)
* Prototyping
* * [codepen.io](https://codepen.io/)
* * [Chrome Web Maker](https://chrome.google.com/webstore/detail/web-maker/lkfkkhfhhdkiemehlpkgjeojomhpccnh?hl=en) - local browser version of codepen (works offline)
* Build Tools
* * [Webpack](https://webpack.js.org/)
* * [Gulp](https://gulpjs.com/)
* * [Parcel](https://parceljs.org/)
* Technologies
* * Sass
* * ES6
* * Handlebars
* * Twig
* * Laravel
* * Phalcon
* * Babel
* * NODE && NPM
* IDE’s
* * Sublime Text 3
* * Atom
* * VS Code
* * PHPStorm
* Mac Stuff
* * [Alfred](https://www.alfredapp.com/)
* * [Nice extra pull down clipboard](https://unclutterapp.com/)
* Tools
* * Visualize Git with Kracken
* * Source Tree Git Manager
* * Page Speed
* * http://cssstats.com/http://cssstats.com/
* * Modular Scale
* * CSS Triangle Generator
* * Favicon Generator
* * Contrast Tester
* * Keycode Info
* * Cubic Bezier Tester
* * CSS Gradients
* * ASCII Generator
* Podcasts
* * https://play.pocketcasts.com/web/podcasts/index#/podcasts/show/7a564520-1cc3-0135-52f8-452518e2d253
* * http://www.jupiterbroadcasting.com/
* * https://spec.fm/podcasts/developer-tea
* * https://developer.telerik.com/
* * http://fitsandstarts.fm/
* * http://founderstalk.com/
* * https://frontendfive.codeschool.com/
* * http://frontendhappyhour.com/
* * http://www.fullstackradio.com/
* * https://www.hanselminutes.com/
* * https://devchat.tv/js-jabber//
* * https://laravel-news.com/podcast
* * http://www.northmeetssouth.audio/
* * http://shoptalkshow.com/
* * https://syntax.fm/
* * http://bikeshed.fm/
* * http://www.fiveminutegeekshow.com/
* * https://laravel.com/
* * http://threedevsandamaybe.com/
* * http://twentypercent.fm/
* * http://www.jupiterbroadcasting.com/show/error/
* * http://www.ycombinator.com/
