# Sass

## Structure

Being diligent about keeping a well-organized Sass structure is beneficial. It's not only easier to find the styling that is specific to certain components, it's also apparent when portions of your Sass are tightly coupled with others.

## Recommended Structure

<dl class="list-definition">
	<dt>main.scss</dt>
	<dd>This is where all of your Sass comes together. The main sass file imports all other Sass files. This file shouldn't have anything in it, aside from <code>@import</code> rules.</dd>
	<dt>base/</dt>
	<dd>For styling elements directly, files that live in this directory can include things like typography, a reset, etc.</dd>
	<dt>components/</dt>
	<dd>Styling that is specific to components - small, reusable chunks of HTML - lives within this directory. Each component should have its own file (<code>_&lt;component-name&gt;.scss</code>).</dd>
	<dt>globals/</dt>
	<dd>Many reusable Sass constructs don't actually output any CSS on their own, but are used in other Sass files to output CSS. These constructs include functions, mixins, placeholders, and variables. Any reusable constructs that don't output CSS should live within this directory, split by type (<code>_functions.scss</code>, <code>_variables.scss</code>, etc.).</dd>
	<dt>partials/</dt>
	<dd>Styling for partials - larger chunks of HTML, possibly composed of smaller components - should live within this directory. E.g. <code>_navigation.scss</code>, <code>_article.scss</code>.</dd>
	<dt>vendor/</dt>
	<dd>Throw any sort of vendor styling into this directory and import it into the main sass file.</dd>
</dl>

## Formatting

- Use hard-tab indentation.
- Use single-quotes around strings (including URLs).
- Use double-quotes around attribute values - useful for copy/paste.
- Selectors should be lowercase.
- Each rule set should be separated by a blank line.
- Each selector should be on a separate line.
- There should be one space before the `{` in each rule set.
- Property declarations should be indented once from their parent rule set.
- Put each property declaration on its own line.
- There should be one space after the `:` in a property declaration.
- Include one space after each comma in property declarations.
- End each property declaration with a `;`.
- The closing `}` should be on its own line.
- Nested rulesets should start at the same indentation as property declarations in the parent rule set.


```scss
.selector-one,
.selector-two {
	background: url("../path/to/an/image.jpg");
	line-height: 1;
	margin: 0;
	padding: 0;

	.selector-three {
		display: block;
		font-size: 1.2em;
	}
}

.selector-four {
	position: absolute;
	z-index: 1;
}
```

## Single Property Rulesets

If a rule set only has only one property declaration, the `{`, `}`, and the property declaration in between them can be collapsed onto one line.

```scss
.selector-one,
.selector-two { margin: 0; }
```

## Style

Omit leading zeros in values. E.g. `padding: .5em;`.
Don't specify units for zero values. E.g. `padding: 0;`.
The value in attribute selectors should be quoted. `[data-ui-open="true"]`.

## Box Sizing

Use a default `box-sizing` value of `border-box`, and make it easy to be overridden.

```scss
*,
*:before,
*:after {
	box-sizing: inherit;
}

html {
	box-sizing: border-box;
}
```

## Maintainability

### Choice of Selectors

To keep specificity at bay and decouple HTML from CSS, **only use classes and attributes for selectors**. IDs are generally too specific, making it difficult to override styles if needed, and element selectors reduce the flexibility of styles by coupling styling directly to HTML.

Element selectors should only be used when a particular element cannot appear outside of its parent selector. An `<li>` may only appear within a `<ul>` or `<ol>`, for instance. Even in this case, use element selectors with caution.

### Class Naming

Class names should not have presentational elements to them. Keep the names of classes purposeful and meaningful. E.g. `.button-primary` rather than `.button-blue`

### Saving Visual State

In cases where you need to save visual state in some way (and you're not using a framework), it's preferable to use `data-ui-<state>` attributes in HTML. This provides an easy way to recognize what kinds of state are being manipulated with JavaScript, and creates flexibility by separating state from normal classes. In cases where `data-*` attributes cannot be used for saving visual state, use `js-*` classes, instead.

```html
<nav class="nav-primary" data-ui-open="false">
	...
</nav>
<div class="js-active">
	...
</div>
```

### Nesting
Only make your selectors as specific as they need to be. While rule sets can be nested many levels, **nesting should be limited to 3 children at most** for performance and good architecture. This does not include chained or pseudo selectors.

Requiring more levels of nesting is often a sign of tight coupling with HTML, poor reusability, and poor flexibility with too much specificity. In this case, it is recommended to take a step back and refactor your HTML and CSS to meet these guidelines. If you absolutely *need* to nest more than these guidelines allow, comment that section with an explanation of why it needs to be done.

### Media Queries

Media queries should not be grouped at the bottom of your main Sass file. The styles within media queries should be grouped with the components and partials that they affect. This makes it convenient to find all of the styling for one particular component or partial because it will all be in one place. Any affect on file size caused by this practice will be negligible after the CSS has been compressed and gzipped.

### Reusable Sass Constructs
Most Sass constructs (functions, mixins, placeholders, variables) are reusable and global, so they should go in their respective files within the `globals` directory. If you need to define a construct that is local to a particular ruleset or component, **prefix the local construct with an underscore**.

Variables that are specific to a particular ruleset should be defined *within* that ruleset.

Functions, mixins, and placeholders that are specific to a particular component or partial should be defined within the same file as that component or partial.
