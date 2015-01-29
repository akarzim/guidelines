# CoffeeScript Guidelines #

[CoffeeScript](http://coffeescript.org) provides sugars to the Javascript language. It tries to ease writing by shortening code and brings some missing pieces to the language.

You should follow Javascript guidelines except for the following subjects where CoffeeScript brings its sugar.

## Coding Style ##

It can be a little annoying to change your coding style if you're used to something else but we need to use only one style to ease code reading.

## Variables ##

You **must not** use `var` keyword to declare your variables. CoffeeScript will add it for you when it's needed.

If you need to declare global variables you can set it on `window`:

```coffeescript
window.myGlobalVar = "foo"
```

### Strings ###

CoffeeScript provides an interpolation mechanism for strings use it over concatenation:

```coffeescript
name = "Foo"
alert "His name is #{foo}"
```

## Keywords ##

CoffeeScript brings some new keywords whether to enhance readability or to avoid some common mistakes. Use them rather than the raw javascript equivalent:

- use `@` rather than `this`
- use `is` rather than `===`
- use `isnt` rather than `!==`
- use `and` rather than `&&`
- use `or` rather than `||`

## Conditionals ##

CoffeeScript adds some sugar to conditionals so you can:

- use postfixed conditionals for one-liners conditions
- use `unless` rather than `if not`

Example:

```coffeescript
alert "Crappy Debug!" if something < 30
alert "Var is undefined or null" unless var?
```

## Functions ##

When writing functions with defaults for arguments use CoffeeScript mechanism:

```coffeescript
function_with_default_args = (arg1 = 42, arg2 = 'default_b') ->
  // body omitted
```

## Classes ##

CoffeeScript has its own system of classes which provides a more classical inheritance system:

```coffeescript
class Fighter

  constructor: (@name) ->
    @life = 100

  hit: (bodyPart = "head") ->
    "#{@name} hit #{bodyPart}'s opponent"

  alive: ->
    @life > 0

ken = new Fighter "Ken"
```

## Comprehensions ##

Comprehensions replace (and compile into) `for` loops, with optional guard clauses and the value of the current array index. Unlike `for` loops, array comprehensions are expressions, and can be returned and assigned:

- use `for in` comprehensions to iterate over array or simulate `map` / `filter` functions
- use `for of` comprehensions to iterate over key / values of an object
- use splats and multiple assignments

Example:

```coffeescript
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
```

## Existential operator ##

It's difficult to check for the existence of a variable in JavaScript. `if variable` will fail with zero, empty string, and `false`. CoffeeScript's existential operator `?` returns `true` unless a variable is `null` or `undefined`, which makes it analogous to Ruby's `nil?`.

Example:

```coffeescript
# log if someVar isn't null or undefined
console.log "There's something in it" if someVar?

# Set variable if it's null or undefined
speed ?= 15

# Set footprints to the value of yeti variable if it exists or use "bear"
footprints = yeti ? "bear"
```

## Documentation ##

*Always* use English!

Use [JSDoc](http://usejsdoc.org). It's an API documentation generation tool for Javascript which is customizable using templates.

Example:

```coffeescript
###*
# Converts the object into textual markup given a specific format.
#
# @param {string} format - the format type, `text` or `html`
# @return {string} the object converted into the expected format
###
toFormat: (format) ->
  // format the object
```
