# Front-end Code Standards

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
7. [Testing](#testing)
8. [Accessibility](#accessibility)
9. [General Resources](#general-resources)

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
* Supported 
  * Desktop: Chrome (latest), Firefox (latest), IE 11, Edge. 
  * Mobile: Chrome/Android 6, Mobile Safari/iOS 10.
* Write unit/end-to-end/integration tests as needed. [See additional documentation](testing.html).

# Accessibility
[Full documentation](accessibility.html)

# General Resources
* [Dynamit Only Resource](https://docs.google.com/document/d/1iYwcqdtfH6Lv0_SBRX4HF91fqD7soP3uD1KkeyNUFD0/edit?usp=sharing)
* Prototyping
   * [codepen.io](https://codepen.io/)
   * [Chrome Web Maker](https://chrome.google.com/webstore/detail/web-maker/lkfkkhfhhdkiemehlpkgjeojomhpccnh?hl=en) - local browser version of codepen (works offline)
* Build Tools
   * [Webpack](https://webpack.js.org/)
   * [Gulp](https://gulpjs.com/)
   * [Parcel](https://parceljs.org/)
* Technologies
   * [Sass](https://sass-lang.com/)
   * [ES6](http://es6-features.org/)
   * [Handlebars](https://handlebarsjs.com/)
   * [Twig - PHP](https://twig.symfony.com/)
   * [Laravel - PHP](https://laravel.com/)
   * [Phalcon - PHP](https://phalconphp.com/en/)
   * [Babel - JS](https://babeljs.io/)
   * [NODE && NPM](https://nodejs.org/en/)
* IDE’s
   * [Sublime Text 3](https://www.sublimetext.com/3)
   * [Atom](https://atom.io/)
   * [VS Code](https://code.visualstudio.com/)
   * [PHPStorm](https://www.jetbrains.com/phpstorm/)
* Mac Stuff
   * [Alfred](https://www.alfredapp.com/)
   * [Nice extra pull down clipboard](https://unclutterapp.com/)
* Tools
   * Visualize Git with [GitKraken](https://www.gitkraken.com/)
   * [Source Tree Git Manager](https://www.sourcetreeapp.com/)
   * [Page Speed](https://developers.google.com/speed/pagespeed/insights/)
   * [CSS Stats](http://cssstats.com/http://cssstats.com/)
   * [Parker - Stylesheet analysis tool](https://github.com/katiefenn/parker)
   * [Modular Scale](http://www.modularscale.com/?1,50&em&1.125)
   * CSS Triangle [Generator](http://apps.eky.hk/css-triangle-generator/)
   * Favicon [Generator](https://realfavicongenerator.net/)
   * Color Contrast [Tester](http://contrast-ratio.com/)
   * [Keycode Info](http://keycode.info/)
   * Cubic Bezier [Tester](http://cubic-bezier.com/#.17,.67,.83,.67)
   * [CSS Gradients](https://www.grabient.com/)
   * ASCII [Generator](http://patorjk.com/software/taag/#p=display&f=Graffiti&t=Dynamit%0A)
* Podcasts
   * https://play.pocketcasts.com/web/podcasts/index#/podcasts/show/7a564520-1cc3-0135-52f8-452518e2d253
   * http://www.jupiterbroadcasting.com/
   * https://spec.fm/podcasts/developer-tea
   * https://developer.telerik.com/
   * http://fitsandstarts.fm/
   * http://founderstalk.com/
   * https://frontendfive.codeschool.com/
   * http://frontendhappyhour.com/
   * http://www.fullstackradio.com/
   * https://www.hanselminutes.com/
   * https://devchat.tv/js-jabber//
   * https://laravel-news.com/podcast
   * http://www.northmeetssouth.audio/
   * http://shoptalkshow.com/
   * https://syntax.fm/
   * http://bikeshed.fm/
   * http://www.fiveminutegeekshow.com/
   * https://laravel.com/
   * http://threedevsandamaybe.com/
   * http://twentypercent.fm/
   * http://www.jupiterbroadcasting.com/show/error/
   * http://www.ycombinator.com/
* News
   * [Hacker News](https://news.ycombinator.com/)
   * [Product Hunt](https://www.producthunt.com/)
   * [Hacker Noon](https://hackernoon.com/)
* Videos
   * [Vue JS by Jefferey Way @ Laracasts](https://laracasts.com/series/learning-vue-step-by-step)
   * [Maintainable Scalable Applications](https://scaleyourcode.com/)
   * [ES6 Jquery Free Tutorials from Javascript 30](https://javascript30.com/)
   * [Uncle Bob (Martin Fowler) SOLID Design Principles](https://www.youtube.com/watch?v=QHnLmvDxGTY)
* Tutorials
   * [Git repos on Git Hub](http://kbroman.org/github_tutorial/pages/init.html)
   * [https://scotch.io/](https://scotch.io/)
   * [More GIT](https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud)
   * [CSS Transitions and Transforms](https://robots.thoughtbot.com/transitions-and-transforms)
   * [Sass Control Directives](http://thesassway.com/intermediate/if-for-each-while)
   * [Dev Tools Tip Gifs](https://umaar.com/dev-tips/)
   * [SVGs](https://css-tricks.com/using-svg/) && and [SVG Sprites](https://24ways.org/2014/an-overview-of-svg-sprite-creation-techniques/) && [SVG Fonts](https://css-tricks.com/icon-fonts-vs-svg/)
   * [More SVG](https://svgontheweb.com/)
   * [Functions](https://javascriptweblog.wordpress.com/2010/07/06/function-declarations-vs-function-expressions/)
   * [Template Literals](https://ponyfoo.com/articles/es6-template-strings-in-depth)
   * [Default Parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)
   * [Async vs Defer](http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html)
   * [DOM Manipulation without jQuery](https://www.sitepoint.com/dom-manipulation-vanilla-javascript-no-jquery/)
   * [CSS Specifics explained](https://css-tricks.com/specifics-on-css-specificity/)
* Cheat Sheets!
   * [Plain JS, jQuery Conversion Cheat Sheet](https://plainjs.com/)
   * [You might not need jQuery](http://youmightnotneedjquery.com/)
   * [Sans jQuery](https://gist.github.com/joyrexus/7307312)
   * [Oh shit, git!](http://www.ohshitgit.com/)
   * [Shoestring Lib](http://filamentgroup.github.io/shoestring/dist/docs/shoestring.js.html)
   * [Accessibility](https://www.w3.org/WAI/WCAG20/quickref/#qr-navigation-mechanisms-skip)
   * [WebAIM](https://webaim.org/blog/aria-cause-solution/)
   * [Ebay Mind Patterns](https://ebay.gitbooks.io/mindpatterns/content/)
   * [http://youmightnotneedjqueryplugins.com/](http://youmightnotneedjqueryplugins.com/)
   * [SOFTWARE LICENSES. AKA DONT GET SUED](https://tldrlegal.com/)
   * [Flexbox](https://www.flexboxpatterns.com/) && [Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
   * [Device Resolutions](http://mydevice.io/devices/)
   * [ALL THE DOCS EVER FOR EVERYTHING EVER PERIOD.](http://devdocs.io/)
   * [Favicons](https://github.com/audreyr/favicon-cheat-sheet)
   * [Mac Keyboard Shortcuts](https://support.apple.com/en-us/HT201236)
   * [Dictionary for DEVS](https://sidewaysdictionary.com/#/)
* Libraries
   * Accessibility
     *  [DT Flyout by MVM](https://stash.dynamit.com/projects/FEC/repos/dt-flyout/browse)
   * Resources
     *  [Google Fonts](https://fonts.google.com/)
     *  [Typekit](https://typekit.com/)
   * Javascript
     *  [Window Events by Pete Droll](https://www.npmjs.com/package/windowevents)
     *  [Drop Zone File Uploader](http://www.dropzonejs.com/)
     *  [Vue JS Plugins](https://github.com/vuejs/awesome-vue)
     *  [https://vuejs.org/](https://vuejs.org/)
     *  [Moment.js](https://momentjs.com/docs/#/parsing/)
     *  [Flickity Carousel](https://flickity.metafizzy.co/)
     *  [Responsive Tables](https://gist.github.com/mavame/a3676391690425d992e5267e6e085541) with [TableSaw](https://github.com/filamentgroup/tablesaw)
     *  [Bulma](https://bulma.io/)
* Chrome Extensions
   * [Toby (Tab Management)https://todoist.com/](https://chrome.google.com/webstore/detail/toby-for-chrome/hddnkoipeenegfoeaoibdmnaalmgkpip)
   * [Web Developer (The best damn thing ever)](https://chrome.google.com/webstore/detail/web-developer/bfbameneiokkgbdmiekhjnmfkcnldhhm)
   * [Link Checker](https://chrome.google.com/webstore/detail/check-my-links/ojkcdipcgfaekbeaelaapakgnjflfglf)
   * [Built With](https://chrome.google.com/webstore/detail/builtwith-technology-prof/dapjbgnjinbpoindlpdmhochffioedbn)
   * [BrowserStack](https://chrome.google.com/webstore/detail/browserstack/nkihdmlheodkdfojglpcjjmioefjahjb)
   * [Toggl](https://chrome.google.com/webstore/detail/toggl-button-productivity/oejgccbfbmkkpaidnkphaiaecficdnfn)
   * [JSON Viewer](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc)
   * [Tab && Memory Manger](https://chrome.google.com/webstore/detail/the-great-suspender/klbibkeccnjlkjkiokjodocebajanakg)
   * [Window Resizer](https://chrome.google.com/webstore/detail/window-resizer/kkelicaakdanhinjdeammmilcgefonfh)
   * [Edit this cookie (Cookie Editor)](https://chrome.google.com/webstore/detail/editthiscookie/fngmhnnpilhplaeedifhccceomclgfbg?hl=en)
   * [ColorZilla (Color picker)](https://chrome.google.com/webstore/detail/colorzilla/bhlhnicpbhignbdhedgjhgdocnmhomnp)
   * [Boomerang (Send emails later)](https://chrome.google.com/webstore/detail/boomerang-for-gmail/mdanidgdpmkimeiiojknlnekblgmpdll)
   * [Link Clump (Open many links at once)](https://chrome.google.com/webstore/detail/linkclump/lfpjkncokllnfokkgpkobnkbkmelfefj)
   * [Vue.js Devtools](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd)
   * [Copy all open tabs to clipboard](https://chrome.google.com/webstore/detail/copy-all-urls/djdmadneanknadilpjiknlnanaolmbfk)
   * [One Tab (Quickly save all open tabs](https://chrome.google.com/webstore/detail/onetab/chphlpgkkbolifaimnlloiipkdnihall?hl=en)


