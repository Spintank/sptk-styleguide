# sptk-styleguide-javascript
*The Javascript styleguide of Spintank*

## Table of Contents

  1. [Introduction](#introduction)
  1. [ES5 Practices](#es5-practices)
      1. [Types](#types)
      1. [Objects](#objects)
      1. [Arrays](#arrays)
      1. [Strings](#strings)
      1. [Functions](#functions)
      1. [Properties](#properties)
      1. [Variables](#variables)
      1. [Comparison Operators & Equality](#comparison-operators--equality)
      1. [Blocks](#blocks)
      1. [Comments](#comments)
      1. [Commas](#commas)
      1. [Semicolons](#semicolons)
      1. [Type Casting & Coercion](#type-casting--coercion)
      1. [Naming Conventions](#naming-conventions)
      1. [Constructors](#constructors)
      1. [Modules with browserify](#modules-with-browserify)
  1. [Ressources](#ressources)


## Introduction

This javascript styleguide is inspired by [airbnb javascript styleguide](https://github.com/airbnb/javascript).
- In first time, use ES5. We work hard to learn ES6, promise :)
- Please comment your code and use [JSDOC](usejsdoc.org/)
- Use soft tabs (2 spaces) for indentation
- Use module to clarify your code. If it's possible one module by features. To do modules we use [Browserify](http://browserify.org/)

## ES5 Practices

### Types

- **Primitives**: When you access a primitive type you work directly on its value.

+ `string`
+ `number`
+ `boolean`
+ `null`
+ `undefined`

    ```javascript
    var foo = 1;
    var bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```
- **Complex**: When you access a complex type you work on a reference to its value.

+ `object`
+ `array`
+ `function`

    ```javascript
    var foo = [1, 2];
    var bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
    ```

### Objects

- To create an object.

    ```javascript
    var item = {};
    ```

- Don't use [reserved words](http://es5.github.io/#x7.6.1) as keys. It won't work in IE8. [More info](https://github.com/airbnb/javascript/issues/61).

- Use readable synonyms in place of reserved words.

    ```javascript
    // bad
    var superman = {
      class: 'alien'
    };

    // bad
    var superman = {
      klass: 'alien'
    };

    // good
    var superman = {
      type: 'alien'
    };
    ```

### Arrays

- To create an array

    ```javascript
    var items = [];
    ```

- To add items to an array : Array#push

    ```javascript
    var someStack = [];

    someStack.push('abracadabra');
    ```

- To copy an array : [Array#slice](http://jsperf.com/converting-arguments-to-an-array/7)

    ```javascript
    var len = items.length;
    var itemsCopy = [];
    var i;

    // bad
    for (i = 0; i < len; i++) {
      itemsCopy[i] = items[i];
    }

    // good
    itemsCopy = items.slice();
    ```

- To convert an array-like object to an array : Array#slice.

    ```javascript
    function trigger() {
      var args = Array.prototype.slice.call(arguments);
      ...
    }
    ```

### Strings

- Strings longer than 100 characters should be written across multiple lines using string concatenation.
- Note: If overused, long strings with concatenation could impact performance. [jsPerf](http://jsperf.com/ya-string-concat) & [Discussion](https://github.com/airbnb/javascript/issues/40).

    ```javascript
    // bad
    var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

    // bad
    var errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // good
    var errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';
    ```

### Functions

- Function expressions:

    ```javascript
    // anonymous function expression
    var anonymous = function () {
      return true;
    };

    // named function expression
    var named = function named() {
      return true;
    };

    // immediately-invoked function expression (IIFE)
    (function () {
      console.log('Welcome to the Internet. Please follow me.');
    }());
    ```

- **Never** declare a function in a non-function block (if, while, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently, which is bad news bears.

    ```javascript
    // bad
    var test;
    if (currentUser) {
      test = function test() {
        console.log('Yup.');
      };
    }
    ```

- Never name a parameter `arguments`. This will take precedence over the `arguments` object that is given to every function scope. Use `args`.

    ```javascript
    function yup(name, options, args) {
      // ...stuff...
    }
    ```

### Properties

- Use dot notation when accessing properties.

    ```javascript
    var luke = {
      jedi: true,
      age: 28
    };

    var isJedi = luke.jedi;
    ```

- Use subscript notation `[]` when accessing properties with a variable.

    ```javascript
    var luke = {
      jedi: true,
      age: 28
    };

    function getProp(prop) {
      return luke[prop];
    }

    var isJedi = getProp('jedi');
    ```

### Variables

- Always use `var` to declare variables. Not doing so will result in global variables. We want to avoid polluting the global namespace.

    ```javascript
    var superPower = new SuperPower();
    ```

- Use one `var` declaration per variable.
It's easier to add new variable declarations this way, and you never have
to worry about swapping out a `;` for a `,` or introducing punctuation-only
diffs.

    ```javascript
    var items = getItems();
    var goSportsTeam = true;
    var dragonball = 'z';
    ```

- Declare unassigned variables last. This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.

    ```javascript
    var items = getItems();
    var goSportsTeam = true;
    var dragonball;
    var length;
    var i;
    ```

- Assign variables at the top of their scope. This helps avoid issues with variable declaration and assignment hoisting related issues.

    ```javascript
    function () {
      var name = getName();

      test();
      console.log('doing stuff..');

      //..other stuff..

      if (name === 'test') {
        return false;
      }

      return name;
    }
    ```

### Comparison Operators & Equality

- Use `===` and `!==` over `==` and `!=`.
- Conditional statements such as the `if` statement evaluate their expression using coercion with the `ToBoolean` abstract method and always follow these simple rules:

+ **Objects** evaluate to **true**
+ **Undefined** evaluates to **false**
+ **Null** evaluates to **false**
+ **Booleans** evaluate to **the value of the boolean**
+ **Numbers** evaluate to **false** if **+0, -0, or NaN**, otherwise **true**
+ **Strings** evaluate to **false** if an empty string `''`, otherwise **true**

    ```javascript
    if ([0]) {
      // true
      // An array is an object, objects evaluate to true
    }
    ```

- Use shortcuts.

    ```javascript
    // bad
    if (name !== '') {
      // ...stuff...
    }

    // good
    if (name) {
      // ...stuff...
    }

    // bad
    if (collection.length > 0) {
      // ...stuff...
    }

    // good
    if (collection.length) {
      // ...stuff...
    }
    ```

### Blocks

- Use braces with all multi-line blocks.

    ```javascript
    // bad
    if (test)
      return false;

    // good
    if (test) {
      return false;
    }

    // bad
    function () { return false; }

    // good
    function () {
      return false;
    }
    ```

- If you're using multi-line blocks with `if` and `else`, put `else` on the same line as your
`if` block's closing brace.

    ```javascript
    if (test) {
      thing1();
      thing2();
    } else {
      thing3();
    }
    ```

### Comments

- Use [JSDOC](usejsdoc.org/).

- Use `/** ... */` for multi-line comments. Include a description, specify types and values for all parameters and return values.

    ```javascript
    /**
     * make() returns a new element
     * based on the passed in tag name
     *
     * @param {String} tag
     * @return {Element} element
     */
    function make(tag) {

      // ...stuff...

      return element;
    }
    ```

- Use `//` for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment.

    ```javascript
    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      var type = this.type || 'no type';

      return type;
    }
    ```

### Commas

- Put commas at the end, execept for the last item

    ```javascript
    var story = [
      once,
      upon,
      aTime
    ];

    var hero = {
      firstName: 'Bob',
      lastName: 'Parr',
      heroName: 'Mr. Incredible',
      superPower: 'strength'
    };
    ```

### Naming Conventions

- Use descriptive names.

    ```javascript
    function query() {
      // ..stuff..
    }
    ```

- Use camelCase when naming objects, functions, and instances. No underscores, no dash.

    ```javascript
    var thisIsMyObject = {};
    function thisIsMyFunction() {}
    ```

- Use PascalCase when naming constructors or classes.

    ```javascript
    function User(options) {
      this.name = options.name;
    }

    var good = new User({
      name: 'yup'
    });
    ```

- If it's possible, don't save references to this. Use Function#bind.

    ```javascript
    function () {
      return function () {
        console.log(this);
      }.bind(this);
    }
    ```

- Name your functions. This is helpful for stack traces.

    ```javascript
    var log = function log(msg) {
      console.log(msg);
    };
    ```

- If your file exports a single class, your filename should be exactly the name of the class.

    ```javascript
    // file contents
    class CheckBox {
      // ...
    }
    module.exports = CheckBox;

    // in some other file
    var CheckBox = require('./CheckBox');
    ```

### Constructors

- Assign methods to the prototype object, instead of overwriting the prototype with a new object. Overwriting the prototype makes inheritance impossible: by resetting the prototype you'll overwrite the base!

    ```javascript
    function Jedi() {
      console.log('new jedi');
    }

    Jedi.prototype.fight = function fight() {
      console.log('fighting');
    };

    Jedi.prototype.block = function block() {
      console.log('blocking');
    };
    ```

- Methods can return `this` to help with method chaining.

    ```javascript
    Jedi.prototype.jump = function jump() {
      this.jumping = true;
      return this;
    };

    Jedi.prototype.setHeight = function setHeight(height) {
      this.height = height;
      return this;
    };

    var luke = new Jedi();

    luke.jump()
      .setHeight(20);
    ```

### Modules with browserify

- Use Browserify to create your modules

    ```javascript
        /*nameofTheModule.js*/
        module.exports = function nameofTheModule() {
          //Module's code
        }

        /*app.js*/
        var nameofTheModule = require('modules/nameofTheModule.js');

        nameofTheModule();
    ```

## Ressources

- [Airbnb Javascript](https://github.com/airbnb/javascript)
- [You don't know Javascript](https://github.com/getify/You-Dont-Know-JS)
- [You might not need jQuery](http://youmightnotneedjquery.com/)

## THE END

**Made with love at Spintank &#9996;**
