# Javascript Guidelines #

## Source format ##

All text files should:

- use `UTF-8` as charset
- use Unix-style line endings
- use `.js` extension
- use **soft-tabs** with a **two space** indent. Don't use hard tabs at all.
- never leave trailing whitespace
- end with a blank newline

Try to avoid long lines as much as possible, split statement on multiple lines.

Always use English for everything everywhere.

## Coding Style ##

It can be a little annoying to change your coding style if you're used to something else but we need to use only one style to ease code reading.

### Spaces ###

Add spaces:

- around operators
- before leading curly braces
- after commas
- after colons
- after semicolons

Example:

```javascript
var x = y + 5;

function test() {
  console.log('test');
}

dog.set('attr', {
  age: '1 year',
  breed: 'Bernese Mountain Dog'
});
```

Don't add spaces:

- around parentheses
- around brackets
- after exclamation marks
- before commas
- before semicolons

Example:

```javascript
some(arg).other();
[1, 2, 3].length;
if (!boolean) {}
```

### Naming ###

Using good names for your classes, methods, variables and files is *very important* because it helps the reader to easily understand what kind of information the variable stores. Always use *clear and descriptive* names:

- use English only
- avoid single letter names — be descriptive with your naming
- use camelCase with first letter downcased for objects, variables, functions and instances
- use snake_case for file and directory names
- use plural names for arrays, hashes and other collections
- use CamelCase for classes and constructors
- use a leading `_` for private properties
- use `_this` when saving a reference to `this`
- always name your functions to ease debugging

### Accessors ###

Use a consistent naming for your accessors since it will help developers to remind their names easier:

- use dot notation when accessing properties
- use `[]` notation when accessing properties with a variable
- accessor functions for properties are not required
- custom getter functions should use `getVal()`
- custom setter functions should use `setVal()`
- for boolean use `isVal()`

```javascript
dog.name;
dog.getAge();
dog.setAge(2);
dog.isMale();

function getProp(prop) {
  return dog[prop];
}
```

### Commas ###

Use trailing commas to separate keys, parameters, etc. Don't add a trailing comma at the end of the list:

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

### Breaking up long method calls ###

If you have a long line with multiple method calls, try to break it up on multiple lines:

```javascript
$('#items')
  .find('.selected')
    .highlight()
    .end()
  .find('.open')
    .updateCount();
```

## Variables ##

You should always use `var` keyword to declare your variables. If you don't you'll end up with a global variable defined and you certainly don't want that.

Use one `var` per variable, that's just easier to handle. Assign variables at the top of their scope.

```javascript
var items   = getItems();
var isHuman = true;
var length;
```

## Control structures ##

Control structures are the basis of the code logic, be consistent:

- use `===` and `!==` over `==` and `!=`
- `if` / `else` / `for` / `while` / `try` always have braces and always go on multiple lines
- for simple single line conditionals use ternary operator
- avoid more than three levels of block

Conditional expressions are evaluated using coercion:

- `Objects` evaluate to `true`
- `Undefined` evaluates to `false`
- `Null` evaluates to `false`
- `Booleans` evaluate to the value of the boolean
- `Numbers` evaluate to `false` if `+0`, `-0`, or `NaN`, otherwise `true`
- `Strings` evaluate to `false` if an empty string '', otherwise `true`

Knowing these simple rules, use shortcuts for your conditions:

```javascript
if (name) {
  // name isn't an empty string
}

if (collection.length) {
  // collection.length is not 0
}
```

## Constructors ##

Javascript is based on constructors and prototypes, you must master it and use it has it's intended to write solid and effective code:

```javascript
function Fighter() {
  console.log('new fighter entering the arena');
}

Fighter.prototype.hit = function hit() {
  console.log('hitting');
  return this;
};

Fighter.prototype.block = function block() {
  console.log('blocking');
  return this;
};

andersonSilva = new Fighter();
andersonSilva.hit().block();
```

It's often a good idea to return `this` in methods so that you can chain method calls.

## Objects ##

- use the literal syntax for object creation
- don't use [reserved words](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Reserved_keywords_as_of_ECMAScript_6) as keys as it won't work in IE8

Example:

```javascript
var items = {};

var fighter = {
  name: "Georges St-Pierre",
  age: "30",
  champion: true
};
```
## Functions ##

When writing functions stick to the following rules:

- never put a space between a function name and the opening parenthesis
- always set sensible defaults for arguments if possible
- use an empty line before the return value unless it's a one-liner
- use empty lines to break up method into logical blocks
- avoid long methods, break it in smaller ones
- avoid long parameter lists

Example:

```javascript
function coolFunc() {
  // body omitted
}

function funcWithArgs(arg1, arg2) {
  // body omitted
}

function function_with_default_args(arg1, arg2) {
  arg1 = typeof arg1 !== 'undefined' ? arg1 : 42;
  arg2 = typeof arg2 !== 'undefined' ? arg2 : 'default_b';

  // more code
}

function isBar() {
  return true;
}
```

## Arrays ##

Arrays are what you'll use the most along with strings. There's some gotcha you must know to use them at their best:

- create array using `[]` literal
- use `Array#push` to add to the array
- use `Array#slice` to copy an array
- use `Array#slice` to convert an array-like object to an array

Example:

```javascript
var items = [];
items.push('guitar');
itemsCopy = items.slice();
```

## Events triggering ##

You'll often need to trigger some custom events from your classes and functions. It's recommended to use a hash as the data payload so it's easily extensible. This way it's easy to add more data to the payload without having to update every handler using this event:

```javascript
$(this).trigger('newMessage', { message : message });

$(this).on('newMessage', function(e, data) {
  // do something with data.message
});
```

## Documentation ##

*Always* use English!

Use [JSDoc](http://usejsdoc.org). It's an API documentation generation tool for Javascript which is customizable using templates.

Example:

```javascript
/**
 * Converts the object into textual markup given a specific format.
 *
 * @param {string} format - the format type, `text` or `html`
 * @return {string} the object converted into the expected format
 * /
function toFormat(format) {
  // format the object
}
```

### Comments ###

Try to write self-documenting code as much as possible.

Avoid writing comments to explain bad code. If an explanation is needed then the code probably needs a refactor to become self-explanatory.

- use /** ... */ for multi-line comments
- use // for single line comments

### Annotations ###

Annotations should usually be written on the line immediately above the relevant code. The annotation keyword is followed by a colon and a space, then a note describing the problem:

- use `TODO` to note missing features or functionality that should be added at a later date
- use `FIXME` to note broken code that needs to be fixed
- use `OPTIMIZE` to note slow or inefficient code that may cause performance problems
- use `HACK` to note code smells where questionable coding practices were used and should be refactored.

## Libraries ##

There's a lot of projects where you'll need external libraries to ease development and avoid reinventing the wheel.

### Handling dates ###

In Javascript working with dates can be a real pain in the ass. If you have to work with date and time extensively, consider using [moment.js](http://momentjs.com) which is a library dedicated to parse, validate, manipulate, localize and display dates.

### Helpers ###

[Underscore.js](http://underscorejs.org) provides functional helpers such map, filter, invoke as well as more specialized goodies for function, templating, objects and so on.

There are helpers for collections, functions, templating and much more.

Any project really using Javascript needs Underscore.js to write shorter and more efficient code and avoid creating custom solution to common needs.

### Creating and manipulating SVG ###

[d3.js](http://d3js.org) is a Javascript library for manipulating documents based on data. If you need to create, update, animate any SVG based on data, D3 is for you.

### jQuery ###

Ok I'm not a big fan of jQuery but I have to admit that it's so widely used that it's hard to ban it nowadays. So here are some recommendations dedicated to jQuery usage:

- prefix jQuery object variables with a `$`
- cache jQuery lookups
- use cascading `$('.sidebar ul')` or parent > child `$('.sidebar > ul')`
- use `find` with scoped jQuery object queries

```javascript
var $sidebar = $('.sidebar');

$sidebar.hide();
$sidebar.css({
  'background-color': 'pink'
});

$sidebar.find('ul').hide();
```

## CoffeeScript ##

[CoffeeScript](http://coffeescript.org) provides sugars to the Javascript language. It tries to ease writing by shortening code and brings some missing pieces to the language.

Please use CoffeeScript as much as possible.

When using CoffeeScript you should stick to some conventions:

- use `@` rather than `this`
- use `is` rather than `===`
- use `isnt` rather than `!==`
- use `and` rather than `&&`
- use `or` rather than `||`
- use postfixed conditionals for one-liners conditions
- use `unless` rather than `if not`
- use `=>` when you need to keep track of the context
- use CoffeeScript classes and inheritance
- use CoffeeScript default value system if you need it for your functions
- use `for in` comprehensions to iterate over array or simulate `map` / `filter` functions
- use `for of` comprehensions to iterate over key / values of an object
- use splats and multiple assignments
- use existential operator
- use string interpolation

Example:

```coffeescript
# Class
class Fighter

  constructor: (@name) ->
    @life = 100

  hit: (bodyPart = "head") ->
    "#{@name} hit #{bodyPart}'s opponent"

  alive: ->
    @life > 0

ken = new Fighter "Ken"

# Postfixed conditional
alert "Critical Hit!" if round is 1 and ken.life < 30

# Comprehensions
foods = ['toast', 'cheese', 'wine', 'chocolate']

eat food for food in foods
eat food for food in foods when food isnt 'chocolate'

childAges = max: 10, ida: 9, tim: 11

for child, age of yearsOld
  console.log "#{child} is #{age}"

# Splats and multiple assignments 
peoples = (first, others...) ->
  star = first
  anonymous = others # This is an array

theBait   = 1000
theSwitch = 0

[theBait, theSwitch] = [theSwitch, theBait]

# Existential operator

# true if variable isn't null or undefined
console.log "There's something in it" if someVar?

# Set variable if it's null or undefined
speed ?= 15

# Set footprints to the value of yeti variable if it exists or use "bear"
footprints = yeti ? "bear"
```

## Linters ##

Use [JSHint](http://jshint.com) and [JSlint](http://jslint.com) to detect errors and potential problems with your code.

Most of the text editors have a plugin to embed these linters.

## Tests ##

As Javascript code base keep growing up in modern applications, it's a good thing to test your code to be confident about it. You'll be able to ship robust features and ensure you're not breaking anything.

[Jasmine](http://jasmine.github.io/2.1/introduction.html) is a behavior-driven development framework that will fit the job nicely.

Example:

```javascript
describe("A suite is just a function", function() {
  // Setup and teardown
  beforeEach(function() {
    this.a = null;
  });

  afterEach(function() {
    this.foo = 0;
  });

  // Specs
  it("and so is a spec", function() {
    this.a = true;

    expect(this.a).toBe(true);
  });

  it("can have a negative case", function() {
    expect(false).not.toBe(true);
  });
});
```

Jasmine comes with a nice set of matchers, a mocking / stubbing mechanism, asynchronous support and much more.

Your test suite will be even more concise and readable if you use CoffeeScript ;-)
