# Accessibility
## Visually Hide Text, But Allow Screen Readers to Read

```css
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip-path: rect(0,0,0,0);
  border: 0;
}
```

## Links
- Avoid using ALL CAPS (even `text-transform: uppercase` can make it sound like a screen reader is yelling at you)
- All links need to have discernible text
- - Use visually hidden spans to add additonal context
```html
<!-- not much context -->
<a href="tel:18885555555">1-888-555-5555</a>

<!-- text is hidden visually, but screen reader can read it -->
<a href="tel:18885555555"><span class="visually-hidden">For more information on XYZ Corp. call</span> 1-888-555-5555</a>
```

- Don't use URLs as link text. Link text should be discernible and help the user contextually.
- When a link will do something unexpected, announce that to the user
- Don't use `target="_blank"` (confusing to the user, removes back button functionality)
- If `target="_blank"` must be used, inform the user they will be taken away from the site
- Font icon / SVG links need to have, at the very least, complimentary text that explains the link
- For internal actions, use `<button>`
- For taking users away from the current page, use `<a>`
- `<a>` must always have an `href`
- Don't bother using [`title`](https://www.paciellogroup.com/blog/2012/01/html5-accessibility-chops-title-attribute-use-and-abuse/)

## Skip Links / Bypass Blocks
This can be wrapped in pretty much any way, but at its core, a bypass block looks like this:
```html
<a href="#main-content" class="skip-nav-link button" data-skip-to-content>Skip to Content</a>
<a href="/sitemap" class="skip-nav-link button">Skip to Sitemap</a>
```
with CSS the links are hidden until they have focus (this is just the example from donatos.com)
```css
.skip-nav-link, a.skip-nav-link {
  position: absolute;
  top: -300px;
  left: 5px;
  height: 1px;
  width: 1px;
  overflow: hidden;
  transition: top .4s ease;
  line-height: 44px;
}

.skip-nav-link:focus {
  height: 46px;
  width: 200px;
  position: absolute;
  top: -3px;
  left: 5px;
  z-index: 500;
  text-align: center;
}
```
In the above, when a user clicks "Skip to Content" they will be focused on the `<main>` on the page (with `id="main-content"`). This helps a user because they won't need to go through the full navigation each page refresh

## Visible Focus
- [WCAG 2.4.7](http://www.w3.org/TR/2012/NOTE-UNDERSTANDING-WCAG20-20120103/navigation-mechanisms-focus-visible.html) - Any keyboard operable user interface has a mode of operation where the keyboard focus indicator is visible. (Level AA)
- Never use `outline: none`
- Can update the outline so it looks different than default, but a visible border must be displayed
- Common failure is using `blur()` to take off focus, instead focus on another item
- Give your elements `:focus` wherever you have `:hover` in your CSS
- Focus needs to be taken into account when using `.hover()`
- Typical failures occur for dropdown navigation not shown when the user focuses on a the top level menu item

## Images
- Always have alt text of some sort
```html
<!-- screen reader will attempt to read the src name -->
<img src="../images/big-ol-dog.png">
<!-- indicates the image is decorative and does not have text in the image -->
<img alt="" src="../..">

<!-- the image alt text will be read by the screen reader -->
<img alt="This text should be descriptive/informative, but not repeat information that is already present" src="../..">
```
- `alt` text should be kept under [125 characters](https://www.washington.edu/accessit/print.html?ID=1257)
- Items like charts or maps that represent a lot of information, `<caption>` or `longdesc` should be used
- GIFs should not have more than 3 flashes per second (higher rate could trigger siezures)
- If possible, don't play GIF until hovered over
- Never use the filename as alt text
- Images with text in them need alt text equal to the text on the image

```html
<!-- src will be read and user has no idea what the coupon is for -->
<img src="../my-great-coupon.jpg">

<!-- will read the alt text which reflects the text on the image -->
<img src="../my-great-coupon.jpg" alt="Buy one pizza get one free. Starts at $8.99">

## Headings
- [Use semantic markup and structure your page with one](http://adrianroselli.com/2013/12/the-truth-about-truth-about-multiple-h1.html) `<h1>`
- Think of your page as the table of contents
- Turn off styling to test if the visual heirarchy makes sense
- Screen readers can use headings as hot key points (see Voiceover [Web Rotor](http://etc.usf.edu/techease/4all/vision/how-do-i-use-webrotor-in-voiceover/))

## Color Contrast
- #000 on #fff background is not the best for readability and can [cause eye strain](http://ux.stackexchange.com/questions/53264/dark-or-white-color-theme-is-better-for-the-eyes)
- Ratio of 4.5:1 must be met for regular text
- 19px and bold is 3:1, 24px and basic color is 3:1
- Dyslexics do better with unique fonts (Comic Sans all characters are unique)
- Automated testing tools can't judge color contrast of text over an image
- Images with text in them need to have this contrast level and alt text equal to the text on the image
- [Testing color contrast] (http://jxnblk.com/colorable/demos/text/)

## Tab Order
- `tabindex="0"` and `tabindex="-1"` are all that should ever be used
- Never use `tabindex="1+"`
- Seriously. Don't.
- `tabindex="-1"` removes the element from the default tab order but allows you to focus on it programatically
- `tabindex="0"` places the element in the default tab order
- Proposal is in to deprecate any tab index that is greater than 0

## Form Elements
- All `<input>` must have `<label>` associated with them
- The `name` attribute does not have to match
- The `for` should link to an input `id`
- When possible, wrap the `input` with the label itself
```html
<label for="theinput">
  Input here:
  <input type="text" name="whatever" id="theinput">
</label>
```

## Random Tidbits
- Include a `lang=` attribute on the `<html>` tag
- Don't use `<meta name="viewport" content="user-scalable=no" />`. Users must be able to zoom
- Take into account that users should be able to go to zoom in to 200% and have the site still work

## Further Reading
An excellent resource on accessibility for the web: [eBay MIND Patterns](http://ianmcburnie.github.io/mindpatterns/)