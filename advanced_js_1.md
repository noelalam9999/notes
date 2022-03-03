# Advanced JS

## Types in JavaScript

###Primitives - IMUTABLE
- String, Number, Boolean, Symbol, null, undefined
- Reassigning value is not mutating the variable

### Objects - MUTABLE
- Objects, Arrays, Functions
- collection of properties
```javascript
const cat = {
    name: "Fluffy",
    age: 3,
}
```
Each property has 4 attributes:
- value - any type, the actual value of property, by default undefined
- writable - boolean, can the value be changed, by default false
- enumerable - boolean, can be listed in a for in enumeration, by default false
- configurable - boolean, can property be deleted or change any of above attributes apart from value, by default false

```javascript
Object.getOwnPropertyDescriptor(cat, 'name')
// returns
const attributes = {
  value: 'Fluffy',
  writable: true,
  enumerable: true,
  configurable: true
}

```
We can then assign different value to the attributes and hence change the behvaiour of the object.

### Two ways to assign value to object
Direct
```javascript
obj.foo = 'bar'
```

Through object.defineProperty()
```javascript
Object.defineProperty(obj, 'foo', {value: 'bar'})
```

This is how it is not possible for string.length to  be changed

## Passing variables
When you pass a variable you’re passing its value.
Objects are passed around as the value of their reference.
```javascript
function change (obj) {
    obj = {name: "Sarah"} // new obj gets assign a new space in memory
}

var person = {name: 'Mark'}
change(person); // {name: 'Mark'}


function change(obj) {
    obj.name = 'Sarah';  // references to the same object in memory
}
change(person); // {name: 'Sarah}

```
## Closure
Something keeps reference to a function scope after the function has returned.
This is useful when a function returns another second function. The second function will be able to access the arguments of the first function.


## Strict mode
It limits potentially harmful language features.
It’s a scope-wide declaration that is activated inserting 'use strict'; as the first code statement.
It’s good practice to use it, unless you have a specific reason not to.
Guarantees some engine optimizations (i.e. makes your code run faster).
It’s activated by default when using ES6 modules and classes.
```javascript
const name = 'Laura'
name.length // 5
name.length = 3 // still 5, will not have any effect

// if we put 'use strict' at the beginning

name.length = 3 // will throw an error

```
- implicit assignment of global variables (without var keyword)
- failed assignment of non writable properties (like string.length reassignment)
- failed deletion of undeletable properties
- duplicate function parameter names

## Context
- The concept of “context” is a programming convenience, and in JS it’s assigned to the variable this.
- `this` is a binding that is made when a function is invoked, and what it references to is determined entirely by the call-site of the function, according to some rules.
- The simplest way to frame these rules is: this is what is to the left of the dot at call-site.
- The only exceptions to this rule are:
    - Standalone function invocations (“nothing to the left of the dot”), it binds to the global object.
    - If you make an explicit binding, it binds to whatever you choose (if null or undefined, the global object).
    - If you use the new keyword, it binds to the new class instance created inside the constructor.
    - If you use arrow functions, they don’t have a context, and hence inherit it from the enclosing scope.
```javascript
function speedUp(context, increase) { //can change context into this
    console.log(context.speed + increase);
}

var car = {speed: 55}
speedUp(car, 10) // 65
```
Creating function as a method of object:
```javascript
var car = {
    speed: 55,
    speedUp: function (increase) {
        console.log(this.speed + increase);
    }
}

// common invocation
car.speedUp(10); //65 javascript here making our life easier by allowing us to access this

// what really happens
car.speedUp.call(car, 10); // 65
```
`THIS is the thing to the left of the dot AT CALL SITE` unless changed by `bind`, `call`, `apply`

### Exceptions
```javascript
function logContext() {
    console.log(this); // returns window in browser, global in node - GLOBAL OBJECT
}

function logContext() {
    'use strict'
    console.log(this); // returns undefined
}

function logContext(null) {
    console.log(this); // global object or undefined in strict mode, standard function invokation
}
```

## The binary system and floating point numbers
- Bit means “binary digit” (i.e. it can only have 2 values, like 0/1), and it’s the basic unit of information in computing.
- Byte is a group of 8 bits
- Binary numbers are series of zeroes and ones that represent a sum of powers of 2. (normal life uses decimal system)
- JavaScript uses 64-bit floating point representation for numbers.
- Fractions where the denominator is not a power of 2 can’t be exactly represented.
- The best way to handle monetary calculations in JS is to always do the required operations in cents (i.e. using integers: multiply the original amount by 100 at the beginning, and then divide by 100 again at the end).

All code is actually converted to binary 