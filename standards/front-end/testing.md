# Unit Testing

The goal of this document is to help get someone set up and running JavaScript unit tests or end to end tests (depending on the needs of the project) quickly and to provide a reference for hard/unanswered questions and gaps in official documentation. 

Paired with the official documentation for each technology, this guide should help fill in the blanks on how to get started painlessly. Please update and contribute as needed, as every project has different needs and quirks!

## Jasmine & Karma

The goal of this section is to help someone get set up using Jasmine unit tests with Karma as a test runner in less than 3 days. Follow this guide to get Jasmine and Karma set up on your project.

### Jasmine

FAQ/things they don’t tell you in the documentation:

* Import your functions/components that you’re testing -- this is pretty basic, but you can’t test the function/component without importing it into your test file
* If you get errors and you don’t know why, you probably need to bundle your files:
  * You can use [karma-webpack](https://github.com/webpack-contrib/karma-webpack) if you’re using Karma...and Webpack
  * You do need webpack configuration if you go that route

--

**Step 1.** Getting Started with Jasmine (from their docs)

Add Jasmine to your project:

`npm install --save-dev jasmine`

Initialize Jasmine:

`node node_modules/jasmine/bin/jasmine init`

Set jasmine as your test script in your package.json:

`"scripts": { "test": "jasmine" }`

Thinking ahead, you may also want to do something like this in your package.json file if you’re using Karma:

`"test": "karma start karma.conf.js"`

^ this way, when you run `npm test` in the command line, Karma starts running/watching your tests for you!

-- 

**Step 2.** Writing a test in Jasmine

This is what Jasmine shows in their docs:

```javascript
describe("A suite", function() {
  it("contains spec with an expectation", function() {
    expect(true).toBe(true);
  });
});
```

**Describe**: this is for grouping related specs. Typically, each test file has one at the top of the file, and includes multiple `its`. Describe can contain any executable JS code needed.

**A suite**: naming the collection of specs in your test file, this is just plain English, not code. These should read as full sentences in traditional Behavior Driven Development (BDD) style.

**It**: this is a global Jasmine function. Its can also contain executable JS, scoped inside of the it function.

**contains spec with an expectation**: this is the title of the spec, this is also plain English and not code. Be descriptive. Did I mention unit tests also serve as documentation and are a great way of describing what a function or component is trying to do?

**expect(true).toBe(true);**: this is an assertion that is either true or false. True tests pass, false tests fail.

Other examples of assertions in Jasmine:

```javascript
expect(false).not.toBe(true);
expect(this.foo).toEqual(0);
expect(foo.setBar).toHaveBeenCalled(); (when using a “spy”)
expect(bar).toBeNull();
expect(foo).toBeDefined();
```

--

**Step 3.** Set up a test runner (let’s use Karma)

Add Karma to your project:

`npm install karma --save-dev`

The Karma docs also say to install other plugins your project needs. Do this carefully:

`npm install karma-jasmine karma-chrome-launcher jasmine-core --save-dev`

^ because you might not end up using the chrome launcher. Maybe you’ll use [PhantomJS](https://www.npmjs.com/package/karma-phantomjs-launcher) as a launcher instead. Do some research to see what will work best for you. 

Run Karma:

`./node_modules/karma/bin/karma start`

--

**Step 4** Karma configuration

The easiest way to generate an initial configuration file is by using the `karma init` command. This will generate a configuration file for you.

Example configuration file with comments:

```javascript
// Karma configuration
// Generated on Wed Sep 05 2018 13:50:10 GMT-0400 (EDT)
// When you install Karma and run ‘Karma init’, a config file will be generated for you

module.exports = function (config) {
 config.set({

   // base path that will be used to resolve all patterns (eg. files, exclude)
   basePath: '',

   // frameworks to use
   // available frameworks: https://npmjs.org/browse/keyword/karma-adapter
   frameworks: ['jasmine'],

   // list of files / patterns to load in the browser
   // this part is confusing, some docs say to specify dist and spec files, but we’re just specifying spec/test files here based on what we saw in another webpack/karma config example
   files: ['spec/*.spec.js'],

   // list of files / patterns to exclude
   exclude: [
   ],

   // if you install/use plugins, make sure to put them here or you’ll get some command line errors that will tell you to put them here
   plugins: [
     'karma-phantomjs-launcher',
     'karma-jasmine',
     'karma-webpack',
   ],

   // preprocess matching files before serving them to the browser
   // available preprocessors: https://npmjs.org/browse/keyword/karma-preprocessor
   preprocessors: {
     'spec/*.spec.js': ['webpack'],
   },

   // test results reporter to use
   // possible values: 'dots', 'progress'
   // available reporters: https://npmjs.org/browse/keyword/karma-reporter
   reporters: ['progress'],

   // web server port
   port: 9876,

   // enable / disable colors in the output (reporters and logs)
   colors: true,

   // level of logging
   // possible values: config.LOG_DISABLE || config.LOG_ERROR || config.LOG_WARN || config.LOG_INFO || config.LOG_DEBUG
   logLevel: config.LOG_INFO,

   // enable / disable watching file and executing tests whenever any file changes
   autoWatch: true,

   // start these browsers
   // available browser launchers: https://npmjs.org/browse/keyword/karma-launcher
   browsers: ['PhantomJS'],

   // Continuous Integration mode
   // if true, Karma captures browsers, runs the tests and exits
   singleRun: false,

   // Concurrency level
   // how many browser should be started simultaneous
   concurrency: Infinity,

   webpack: {
     // webpack configuration
     // karma watches the test entry points
     // (you don't need to specify the entry option)
     // in karma-webpack’s documentation, there’s nothing in this section. But you need stuff in this section. Below is what we’ve taken from our webpack.config file:
     module: {
       loaders: [
         {
           test: /\.js$/,
           loader: 'babel-loader',
           exclude: /node_modules/,
         },
         {
           test: /\.vue$/,
           loader: 'vue-loader',
         },
       ],
     },
   },
 })
}
```

Code/test examples for Jasmine & Karma:

```javascript
import { formatBasicCurrency } from 'scripts/shared/utils/misc';

/*
  This is what formatBasicCurrency looks like:
  export function formatBasicCurrency(amount) {
    const formatted = parseFloat(amount).toFixed(2).replace(/(\d)(?=(\d{3})+\.)/g, "$1,");
    return `$${formatted}`;
  }
*/

describe('Formats currency from a number/string to a $XX.XX format', () => {
  it('takes a string and turns it into money', () => {
    const string = '144.444';
    const formattedString = formatBasicCurrency(string);
    expect(formattedString).toEqual('$144.44');
  });

  it('takes a decimal and turns it into money', () => {
    const dec = 800.451234;
    const formattedDec = formatBasicCurrency(dec);
    expect(formattedDec).toEqual('$800.45');
  });

  it('takes a number and turns it into money with 0s included', () => {
    const number = 45;
    const formattedNum = formatBasicCurrency(number);
    expect(formattedNum).toEqual('$45.00');
  });

  it('will not return correct money if it cannot be formatted', () => {
    const random = 'apples';
    const formattedRand = formatBasicCurrency(random);
    expect(formattedRand).toEqual('$NaN');
  });
});
```

## Cypress

Sometimes, even with this document, unit tests can be difficult to set up and it can be hard to know where to start. This is especially true if you’re setting something up on an existing project. In these cases, Cypress may prove useful for unit, integration, and end-to-end testing of applications.

It’s also very easy to set up and learn in general. Big fan.

**Step 1**. Get started with [Cypress](https://docs.cypress.io/guides/getting-started/installing-cypress.html#System-Requirements)

`npm install cypress --save-dev`

**Step 2**. Running Cypress

`./node_modules/.bin/cypress open` (or shortcuts you can create within package.json -- [example: `"cypress:open": "cypress open"`] and then run `npm run cypress:open`)

**Step 3**. Writing a Cypress test

Cypress is very UI-based, which you’ll see when you run Cypress. When writing a test, you interact with the UI of a page by visiting that page. For example, the following test goes to a page and clicks on a button:

```javascript
describe('My First Test', function() {
  it('Visits the Kitchen Sink', function() {
    cy.visit('https://example.cypress.io')
    cy.contains('button').click()
  })
})
```

If the page won’t load or the button doesn’t exist/isn’t clickable, the test will fail.

As with other unit testing libraries and tools, you’ll be writing assertions for the page that is visited in Cypress. Cypress has a great reference for which words you can use to make assertions and what the correct syntax should be: [https://docs.cypress.io/guides/references/assertions.html#BDD-Assertions](https://docs.cypress.io/guides/references/assertions.html#BDD-Assertions)

Note: One thing I thought was weird is the syntax for ‘should’, example for should vs. should not:

```javascript
cy.get('li.selected').should('have.length', 3)
cy.get('form').find('input').should('not.have.class', 'disabled')
```

Code/text example with Cypress:

```javascript
describe('My website form', () => {
  it('Enrolls the user when they fill out the form', () => {
    cy.visit('/form.html');

    // Fill out the enrollment form
    // The form consists of an email input and a checkbox to agree to the terms and conditions
    cy.get('#email').type('myemail@test.co');
    cy.get('#email-agree').click();

    // Submit the form
    cy.get('.submit').should('not.be.disabled');
    cy.get('.submit').click();

    // In this case, enrolling shows a success message
    cy.get('.alert--success').should('be.visible');
  });
});
```

## vue-test-utils

Things they don’t tell you in the documentation:
* HTML templates aren’t supported (as of June 19, 2018)
* Have to test components, no way to test mounted Vue instance

Coming soon!

## Tools for testing React (Jest, Chai, Enzyme)

**Note: this section is exploratory so far (working in [Code Sandbox](https://codesandbox.io/) - which I believe uses create-react-app) and I haven’t implemented it on a project.**

### Jest

Jest is a popular tool for testing JavaScript (not React-specific, but v popular for React). According to jestjs.io, “One of Jest's philosophies is to provide an integrated "zero-configuration" experience”

There’s a whole section in the documentation for testing react apps: [https://jestjs.io/docs/en/tutorial-react](https://jestjs.io/docs/en/tutorial-react)

Create-react-app ships with Jest out of the box

## Chai

In examples I’ve seen, Chai is often used to help make writing assertions easier (from the docs: Chai is a BDD / TDD assertion library for node and the browser that can be delightfully paired with any javascript testing framework.) So, although this is not Jest and certainly not React-specific, I did find it was easy to use with that setup.

## Enzyme

Enzyme allows you to shallow mount, mount, and render a React component when writing a unit test for the component

https://airbnb.io/enzyme/docs/api/ 

When importing and using Enzyme for testing components, the Enzyme adapter for React must also be imported

```javascript
import Adapter from "enzyme-adapter-react-16";

Enzyme.configure({ adapter: new Adapter() });
```

Example of a React test (tests `App` component):

```javascript
import React from "react";
import { expect } from "chai";
import Enzyme, { shallow, mount } from "enzyme";
import App from "../src/index";
import Adapter from "enzyme-adapter-react-16";

Enzyme.configure({ adapter: new Adapter() });

describe("<App />", () => {
  it("renders a div", () => {
    const wrapper = shallow(<App />);
    expect(wrapper.find("div").length === 1);
  });

  it("allows us to set props", () => {
    const wrapper = mount(<App name="Fred" />);
    expect(wrapper.props().name).to.equal("Fred");
    wrapper.setProps({ name: "George" });
    expect(wrapper.props().name).to.equal("George");
  });
});
```

