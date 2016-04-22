# Stylesheets

Use Sass for stylesheets. Use the SCSS syntax.

Organize partials into a logical folder structure. Recommended structure for most projects:

```
├── variables
├── tools (mixins and functions)
├── base (layout, elements, typography)
├── components
├── utils
└── main.scss
```

Use soft-tab indentation, 2 spaces.

```scss
// bad
.selector {
color: #000;
}

.selector {
	color: #000;
}

// good
.selector {
  color: #000;
}
```

Use hyphens when naming files, `variables`, `functions`, and `mixins`. Prefix local structures with an underscore.

```scss
// bad
$someVar: 13em;

@mixin some_mixin { ... }

.selector {
	$someVar: 14em;
}

// good
$some-var: 13em;

@mixin some-mixin { ... }

.selector {
	$_some-var: 14em;
}
```

Name you variables in a [modular way](http://webdesign.tutsplus.com/tutorials/htmlcss-tutorials/quick-tip-name-your-sass-variables-modularly/) - providing structure and logic.

Add modifiers to the end of the variable name.

```scss
// bad
$small: 35em;
$large: 82em;

// bad
$small-breakpoint: 35em;
$large-breakpoint: 82em;

// good
$breakpoint-small: 35em;
$breakpoint-large: 82em;
```

Place `@import`, `@include`, and `@extend` at the top of the definition

Place media queries after the declaration list, not at the end of the file.

```scss
// good
.selector {
	@include some-mixin;
	color: #000;

	@include breakpoint($breakpoint-md)  {
		color: #111;
	}
}
```

Selectors should be lowercase and dash-delimited.

```scss
// bad
.mySelector { ... }
.another_selector { ... }

// good
.my-selector { ... }
.another-selector { ... }
```

Use single-quotes around strings (including URLs).

Use double quotes for attribute selectors.

```scss
// bad
[data-foo=bar] {
	background-image: url(../../tidyman.jpg);
}

// good
[data-foo="bar"] {
	background-image: url('../../tidyman.jpg');
}
```

Each rule set should be separated by a blank line.

Each selector should be on a separate line.

There should be one space before the `{` in each rule set.

The closing `}` should be on its own line.

There should be one space after the `:` in a property declaration.

Include one space after each comma in property declarations.

End each property declaration with a `;`.

```scss
// bad
.selector { color: #000; font-weight: bold; }
.another-selector{
	color:#000
}

// good
.selector {
	color: #000;
	font-weight: bold;
}

.another-selector {
	color: #000;
}
```

Add empty lines between nested declaration blocks.

```scss
// bad
.selector {
	color: $black;
	width: 100%;
  	.selector-child {
  		color: $green;
  		font-size: 1rem;
  	}
  	.selector-child-alt {
  		color: $red;
  		font-size: 0.75rem;
  	}
}

// good
.selector {
	color: $black;
	width: 100%;

  	.selector-child {
  		color: $green;
  		font-size: 1rem;
  	}

  	.selector-child-alt {
  		color: $red;
  		font-size: 0.75rem;
  	}
}
```

Use a leading zero in decimal numbers: `0.5` not `.5`

Use space around operands: `$variable * 1.5` not `$variable*1.5`

Don't specify units for zero values: `padding: 0;` not `padding: 0px`

Don't specify units for line-height: `line-height: 1.5` not `line-height: 24px`

Prefer relative units `rems` and `ems`:

```scss
// bad
.selector {
	font-size: 20px;
	margin-top: 14px;
}

// good
.selector {
	font-size: 1.25rem;
	margin-top: 0.7em;
}
```

Use shorthand sparingly. Prefer clarity.

```scss
// bad
.selector {
	flex: 1;
	font: 1rem bold;
}

// good
.selector {
	flex-grow: 1;
	font-size: 1rem;
	font-weight: bold;
}
```

Avoid inefficient selectors by [understanding](http://css-tricks.com/efficiently-rendering-css/) how selectors are parsed.

```css
// bad
ul li a.menu-link {
    ...
}

// good
.menu-link {
    ...
}
```

Avoid unnecessary selectors; keep them as short as possible. Adhere to the "[Inception](http://thesassway.com/beginner/the-inception-rule)" rule.

```css
// bad
.one.too .many .levels .here {
    ...
}

// good
.too .levels {
    ...
}
```

Avoid element selectors (outside of [normalization](https://github.com/necolas/normalize.css)).

```css
// bad
header {
    background-color: #000;
}

// good
.selector {
    background-color: #000;
}
```
