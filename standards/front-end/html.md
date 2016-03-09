# HTML

## Formatting

- Use hard-tab indentation.
- Only use lowercase characters for element names and attributes.
- Nested block-level elements should be indented once.
- Don't use trailing slashes for self-closing elements. E.g. `<br>`, `<img>`, `<input>`.
- Enclose attribute values with double quotes.
- Omit values for boolean attributes (not including custom attributes). If you can't, the value must be empty or equal to the name of the attribute. E.g. `<input required>` rather than `<input required="required">`.

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8">
	<title>Example</title>
	<link rel="stylesheet" href="//site.tld/stylesheet.css">
</head>
<body>
	<div class="foo">
		<p>Lorem ipsum dolor sit amet, consectetur. Facere!</p>
	</div>
	<script src="//cdn.tld/script.js"></script>
</body>
</html>
```

## Style
- Always define a doctype to enforce standards mode and a more consistent rendering.
- Use UTF-8 with the charset meta tag and don't use entity references except for characters with special meanings.
- Don't include the `type` attribute when including stylesheets and scripts.
- Use scheme-relative URLs (omit http/https).
- Feel free to separate chunks of HTML with a blank line.

## Attribute Order

For the sake of consistency and quick readability, write your attributes in this order:

- `class`
- `id`
- `name`
- `type`
- `*`
- `role`
- `aria-*`

## Semantics

Use tags according to their purpose. For instance, don't use an `<a>` tag when a `<button>` is more appropriate. Aside from making our code more meaningful, using the correct tags has a huge benefit for accessibility.
