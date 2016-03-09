# JavaScript

## Uniformity

Code example for this section:

```js
/**
 * Handles the creation of an Person, who can do person stuff.
 *
 * @param {String} name - The name of the person.
 * @param {Number} age  - The age of the person.
 */
export default class Person {
  constructor(name, age = 0) {
    this.name = name;
    this.age = age;
  }

  /**
   * Make the person introduce themselves with their name.
   */
  sayHello() {
    // these are bad because they don't get used, but they demonstrate variable
    // declarations
    const sentence = `Hello World! My name is ${this.name}.`;
    let a, b, c;

    console.log(sentence);
  }
}

/**
 * Takes any number of Person objects and sorts them by age.
 *
 * @param    {Object}  ...persons - Any number of Person objects.
 * @returns  {Array} - All of the Persons given, sorted by age.
 */
function sortAges(...persons) {
  const sorted = persons.sort((a, b) => {
    if (a.age < b.age) {
      return -1;
    } else if (a.age > b.age) {
      return 1;
    }

    return 0;
  });

  return sorted;
}

const jane = new Person('Jane', 22);
const john = new Person('John', 25);
const jim = new Person('Jim', 24);
let sortedPeople = sortAges(jane, john, jim);
```

## Formatting

- Use hard-tab indentation.
- Statements end with a `;`.
- Variable and function names should use camelCase.
- Class names should use UpperCamelCase.
- All variables should be defined at the top of their scope.
- Initialized variables should each have their own declaration.
- Uninitialized variables should share a declaration.
- Groups of variable declarations should be followed by 1 empty line.
- Blocks should be separated by 1 empty line.
- Follow the [One True Brace style](https://en.wikipedia.org/wiki/Indent_style#Variant:_1TBS).
- `{` should have 1 space before.
- Use `===` and `!==` for comparisons.
- Wrap normal strings in single-quotes and escape double-quotes as necessary.
- Reserved keywords should have 1 space after.
- There should be 0 spaces between function names and their parentheses.
- Parentheses should not be padded with spaces at the beginning or end.
- `:` should have 0 spaces before and 1 space after. 2+ spaces after are allowed for alignment.
- Inline commas should have 0 spaces before and 1 space after.
- Logical and arithmetic operators should have 1 space before and after.
- The logical `!` operator should have 0 spaces before and after.
- Ternary operators should never be nested.
- Use object shorthand whenever possible.
- Use UNIX-style line endings (`LF`).
- Files should end with one blank line.


## Documentation

We follow the [JSDoc](http://usejsdoc.org/) style of documentation. It's recommended that you document your code as your go because it's probably easier than going back and doing it later.

- Documentation should go directly above the relevant code. This includes inline comments.
- Inside block comments, use full sentences, capitalization, and punctuation. Inline comments may be more casual.
- Classes and named functions require documentation. Variables do not.
- Separate class or function descriptions from parameter and return decriptions.
- Arguments and returns should be documented with their expected type and a short description.

```js
/**
 * Description of the function or class.
 *
 * @param {String} argName - Description of the argument.
 * @returns {Number} - Description of the return.
 */
```


## Types

### Initialization

When creating any kind of type, always use the literal syntax, not the constructor. In most cases, using the type constructor can cause unexpected results. Aside from that, it's just easier to use the literal syntax.

```js
// bad
// note: many of these don't return what you would expect - objects, not primitives
console.log(new Array(5))         // => [undefined x 5]
console.log(new Array(1, 2, 3));  // => [1, 2, 3]
console.log(new Boolean(false));  // => Boolean {[[PrimitiveValue]]: false}
console.log(new Number(0));       // => Number {[[PrimitiveValue]]: 0}
console.log(new Object());        // => Object {}
console.log(new String('Hi'));    // => String {0: 'H', 1: 'i', length: 2, [[PrimitiveValue]]: "Hi"}

// good
// note: these are all what you _really_ wanted in the first place
console.log([1, 2, 3]);           // => [1, 2, 3]
console.log(false);               // => false
console.log(0);                   // => 0
console.log({});                  // => {}
console.log('Hi');                // => "Hi"
```


## Variable Declarations

Use `const` and `let` instead of `var` when declaring variables. Keep in mind that they are **block scoped**.

### Immutability by Default

When declaring a variable, use `const` instead of `var`. This is to ensure that, by default, all of our variables are immutable when they are created.

```js
// bad
var foo = 0;

// good
const foo = 0;
```


### Mutability

When you do _need_ a variable that is mutable, use `let`.

```js
// bad
var foo = 0;

foo++;

// good
let foo = 0;

foo++;
```


### Grouping

Always group your variables by whether or not they're mutable, with immutable variables first.

```js
// bad
let foo = 0;
const bar = 'Hello World!';
let baz = 5;

// good
const bar = 'Hello World!';
let foo = 0;
let baz = 5;
```


## Strings

### Quotes

Always use single-quotes around _normal_ strings. Escape them when necessary.

```js
// bad
const quote = "There's a snake in my boot!";

// good
const quote = 'There\'s a snake in my boot!';
```


### Template Literals

Always use template strings instead of concatenation.

```js
// bad
const name = lastName + ', ' + firstName;

// good
const name = `${lastName}, ${firstName}`;
```


## Objects and Arrays

### Literal Syntax

Always use the literal syntax when creating objects and arrays. Using their constructor form can cause unexpected behavior.

```js
// bad
const a = new Array(1, 2, 3); // => [1, 2, 3]
const b = new Array(5);       // => [undefined x 5]
const o = new Object({});     // => Object {}

// good
const a = [1, 2, 3];          // => [1, 2, 3]
const b = [5];                // => [5]
const o = {};                 // => {}
```


### Object Shorthand

Always use the object property and method shorthand whenever possible. Put your shorthand properties _above_ other non-shorthand properties.

```js
// bad
const a = 'Hello';
const b = 'World!';
const o = {
    a: a,
    b: b,
    c: 10,
    d: function d() { ... }
};

// good
const a = 'Hello';
const b = 'World!';
const o = {
    a,
    b,
    d() { ... },
    c: 10
};
```


### Dot Notation

Always use dot notation whenever possible for accessing object properties.

```js
const userAge = {
    firstName: 'John',
    lastName: 'Smith',
    age: 22
};

// bad
const fullName = `${user['firstName']} ${user['lastName']}`;

// good
const fullName = `${user.firstName} ${user.lastName}`;
```


### Destructuring

Use object and array destructuring. When destructuring an object, don't go deeper than the first level as it can get very complex.

```js
// bad
function sayHello(user) {
    const firstName = user.firstName;
    const lastName = user.lastName;

    console.log(`Hello World! My name is ${firstName} ${lastName}.`);
}

// best
function sayHello({firstName, lastName}) {
    console.log(`Hello World! My name is ${firstName} ${lastName}.`);
}
```

When returning multiple values, return them as an object instead of an array. With object destructuring, you can cherry pick values from the returned object. Array destructuring requires that you always keep track of what order the values are in.

```js
// bad
function getColorValue() {
    return ['#ffffff', [255, 255, 255], [0, 0, 100]];
}

// let's say you don't need the hex...
const [, rgb, hsl] = getColorValue();

// good
function getColorValue() {
    return {
        hex: '#ffffff',
        rgb: [255, 255, 255],
        hsl: [0, 0, 100]
    };
}

// cherry pick the values you need...
const {rgb, hsl} = getcolorValue();
```


## Functions

### Declarations vs Expressions

Always use function declarations instead of function expressions. Function declarations are easier to identify within call stacks because they are named. Function declarations will also hoist both their name and their body, whereas function expressions will only hoist their name.

```js
// bad
sayHello(); // => ReferenceError

const sayHello = function () {
    // ...
};

// good
sayHello();

function sayHello() {
    // ...
}
```


### Constructor Functions

Don't use functions as constructors. Use classes, instead.

```js
// bad
function Person(name, age) {
    this.name = name;
    this.age = age;
}

Person.prototype.sayHello = function sayHello() {
    console.log(`Hello World! My name is ${this.name}.`);
}

// good

class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    sayHello() {
        console.log(`Hello World! My name is ${this.name}.`);
    }
}
```


### Default Parameters

Use the default parameter syntax rather than changing the value of the parameter within the function body.

```js
// bad
function sayHello(user) {
    user = user || {};
    // ...
}

// good
function sayHello(user = {}) {
    // ...
}
```


### Rest Parameters

Use rest parameters instead of `arguments`. `arguments` may not work as expected because it's not an actual array.


### Arrow Functions

When passing anonymous functions, always use an arrow function. Arrow functions bind themselves to the lexical `this`, so they work in a more expected fashion.

Also, always wrap arrow function parameters in parentheses and arrow function bodies in curly braces. This saves someone from accidentally making a mistake.

```js
const names = ['Jane', 'John', 'Jim'];

// bad
names.forEach(function (name) {
   // ...
});

// bad
names.forEach(function (name) {
    // ...
}.bind(this));

// bad
names.forEach(function (name) {
    // ...
}, this);

// good
names.forEach((name) => {
    // ...
});
```


## Modules

Always use ES6 modules over any other module system. Babel can transpile ES6 modules into any other module system.

### Exports

When authoring a module, always have a default export. Also, keep imports and exports separate, and don't export an import in one line.

```js
// bad
export {Person as default} from 'person';

// good
import Person from 'person';

export default Person;
```


# Vendor Libraries

Due to ever-increasing support for newer, more powerful versions of ECMAScript and standard browser APIs, we no longer need to rely on libraries for cross-browser compatibility, as much. Take the time to consider whether or not a project really needs to include a library for cross-browser compatibility.[^you-might-not-need-jquery]

## jQuery

### Variable Names

When assigning any sort of jQuery object to a variable, be sure to begin the variable name with a `$`. This includes collections of elements, as well as jQuery-wrapped events.

```js
// bad
const buttons = $('button');
buttons.on('click', (e) => {
    console.log('button clicked!');
});

// good
const $buttons = $('button');
$buttons.on('click', ($e) => {
    console.log('button clicked!');
});
```


### Caching

Always cache jQuery lookups.

```js
// bad
$('.nav').addClass('is-active');
// ...
$('.nav').removeClass('is-active');

// good
const $nav = $('.nav');

$nav.addClass('is-active');
// ...
$nav.removeClass('is-active');
```


# Transpiler

We use [Babel](http://babeljs.io/) to transpile our forward-looking code into something that can be run today in current browsers. A transpiler was chosen because it follows the ECMAScript standard without adding more to the language, which keeps the learning curve minimal. Babel was chosen, specifically, because it has the best coverage[^es6-compatibility-table] for the latest specification and it works well with the rest of our tools.

## Caveats

No transpiler, subset, or superset can have complete coverage for new language features. Keep this in mind when writing your JavaScript code. See the [Babel caveats](http://babeljs.io/docs/advanced/caveats/) page.


# Linting

We use [eslint](http://eslint.org/) with a custom configuration set up specifically for our standards. Always include it in your projects' build tool to help ensure we're all writing code in the same fashion. [Get our `.eslintrc`.](/resources/linters/eslintrc.txt)

## On-the-fly Rule Configuration

Do not change linting rules on-the-fly within any file using linter comments. The purpose of having and using a linter is to ensure that we're writing valid code that also meets standards. Changing the linting rules on-the-fly defeats this purpose.

The only exception to this is non-production code, such as Gulp or Webpack configuration files. Do not use linter comments to turn off linting completely, but use them to turn off specific rules on an as-needed basis. This allows the linter to pick up errors in your code while ignoring the code that you don't want it to pick up, such as `console.log`.

```js
// production code
// bad - you could forget about this line because the linter isn't warning you
//       about it
console.log('Hello World!') // eslint-disable-line
```


## Editor Plugins

If a linting plugin is available for your editor, it's strongly recommended that you install and use it.

- Sublime (Available through PackageControl)
    - [SublimeLinter](https://packagecontrol.io/packages/SublimeLinter)
    - [SublimeLinter-contrib-eslint](https://packagecontrol.io/packages/SublimeLinter-contrib-eslint)
- Atom
    - [linter](https://atom.io/packages/linter)
    - [linter-eslint](https://atom.io/packages/linter-eslint)
- WebStorm
    - [ESLint Settings](https://www.jetbrains.com/webstorm/help/eslint.html)
- PHPStorm
    - [ESLint Settings](https://www.jetbrains.com/phpstorm/help/eslint.html)


# Resources

Read the [ECMAScript 2015 spec](http://www.ecma-international.org/ecma-262/6.0/index.html).

## Websites & Blogs

- [ES6 Features](http://es6-features.org/)
- [ES6 Compatibility Table](https://kangax.github.io/compat-table/es6/)
- [Superhero.js](http://superherojs.com/)
- [2ality](http://www.2ality.com/)


## Books & Articles

- ["Exploring ES6" by Dr. Axel Rauschmayer](http://exploringjs.com/)
- ["JavaScript Patters" by Stoyan Stefanov](http://www.amazon.com/JavaScript-Patterns-Stoyan-Stefanov/dp/0596806752)
- [You Might Not Need jQuery](http://youmightnotneedjquery.com/)
- [lukehoban/es6features](https://github.com/lukehoban/es6features)


## Other

- ["What's New in ES6" Dev Meeting Presentation](https://docs.google.com/presentation/d/1OGym6E4znFOhGs1QSCp5DiwFOWQru_Bf24T4JbrQURI/edit?usp=sharing)


---

# Footnotes
{: .no_toc .h5 }

[^you-might-not-need-jquery]: [You Might Not Need jQuery](http://youmightnotneedjquery.com/)
[^es6-compatibility-table]: [ES6 Compatibility Table](https://kangax.github.io/compat-table/es6/)
