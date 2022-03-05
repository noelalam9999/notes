# Advanced JS

## Types in JavaScript

###Primitives - IMUTABLE
- String, Number, Boolean, Symbol, null, undefined
- Reassigning value is not mutating the variable

### Objects - MUTABLE
- Objects, Arrays, Functions
- collection of properties
```javascript
const
        cat = {
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

## Delegation chain
- Properties lookup in JS objects follows a delegation “chain” (aka the “prototype chain”).
- To set a link in this chain when creating a new object use Object.create(parentObj).
- If a property lookup fails until the last step in the chain, undefined is returned.
- When a property is defined on an object down the chain, it “obfuscates” the same property in other objects up the chain.

```javascript
const arr = [];
arr.push(3)
arr.hasOwnProperty('push') // false
Array.prototype.hasOwnProperty('push') // true
```
you can check where the delegation is by typing
```javascript
arr.__proto__ === Array.prototype // true
```

you can also assing delegation, should not really be done - leads to slow operation in modern engines
```javascript
const team = {learning: 'code'}
const student = Object.create(team) // creates the delegation link
student.name = 'Sarah'
student.learning // accessible and returns 'code'
// BUT
console.log(student)  // only has {'name': Sarah}

student.__proto__ == team // true
```

Use `__.proto__` on instances and use `.prototype` on constructor. 
`Array.__proto__` actually returns to prototype function, 

## Classes and subclasses
- Help with `Dont repeat yourself`
- In programming, “class” is a term used to define a group of elements that exhibit the same properties (very much like in natural language).
- The main 3 instantiation styles are: functional, pseudo-classical, and ES6.
- A sub-class has all the properties and methods of its parent class, plus other ones that are unique to it.
- Real classes have instances who are completely independent from each other.
- In JS this doesn’t exist when you use delegation, as modifying an object up the chain affects all objects that delegate to it.

- the classes are actually forced to javascipt as many developers came from java which uses classes
- javascript is functional, prettily separating methods and variables, and classes actually mix methods and variables together
- classes are human concept, do not have a physical representation in memory

### Functional
Simple function that crates a object and copies methods from shared object and returns

```javascript
// class
function Phone (number) {
  var result = {};
  result.number = number;
  Object.assign(result, phoneMethods); 
  return result;
};

var phoneMethods = {};
phoneMethods.dial = function (number) {
  console.log('Dialing', number);
};

var motorola = Phone(695323871);
```

```javascript
// Sub-class

function SmartPhone (number, email) {
  var result = Object.create(Person.prototype) // delegate to the methods 
  result = Phone(number);
  result.email = email;
  // Object.assign(result, smartPhoneMethods); // due to delegation no need for this line
  return result;
};

SmartPhone.prototype.sendEmail = function (email) {  // assign directly to SmartPhone prototype to access
  console.log('Emailing', email);
};

var iPhone = SmartPhone(642503917, 'jack@apple.com');
```

### Pseudo classical approach
Stores shared methods in the prototype
JS does magic for you - new keyword to initiate, assign the functions


```javascript
// Class

function Phone (number) {
  // var this = Object.create(Phone.prototype);
  this.number = number;
  // return this;
};

Phone.prototype.dial = function (number) {
  console.log('Dialing', number);
};

var motorola = new Phone(695323871);
```

```javascript
// Sub-class

function SmartPhone (number, email) {
  // var this = Object.create(SmartPhone.prototype);
  Phone.call(this, number);  // gotta bind the context to the parent class !!
  this.email = email;
  // return this;
};

SmartPhone.prototype = Object.create(Phone.prototype);  // gotta delegate to the parent
SmartPhone.prototype.constructor = SmartPhone;  // also need to correct constructor for it to point to itself
SmartPhone.prototype.sendEmail = function (email) {
  console.log('Emailing', email);
};

var iPhone = new SmartPhone(642503917, 'jack@apple.com');
```

### ES6
still need to use new keyword
only syntactic sugar, it all works as in the pseudo classical approach
```javascript
class Phone {
  constructor (number) {
    this.number = number;
  }
  dial (number) {
    console.log('Dialing', number);
  }
}

// Sub-class

class SmartPhone extends Phone { // inheritance
  constructor (number, email) {
    super(number);  // this just says to call the constructor of parent class and pass the arguments that the parent class needs
    this.email = email;
  }
  sendEmail (email) {
    console.log('Emailing', email);
  }
}
```

## ESNext
- The next release that is coming up in javascript
- JavaScript is based on a standard, named “ECMAScript”.
- The standard keeps evolving: new language features are introduced (i.e. syntax and functionality), some can be removed.
- ES6 introduces some new interesting concepts, for example: let and const, arrow functions, default and trailing function parameters, the spread operator, template literals, enhanced object properties, modules (import / export), class definitions, symbols, maps / sets, and promises.
### ES6 biggest releases
### const and let
- `const` vs `let` - before only `var` and the difference was indicated for constances with all capitals and underscores and variables with camelCase
- `var` element is on global scope, so in two nested loops the var would be the same. so lets not use those

### arrow functions
- no access to arguments object and this is not bound to the function! also cannot be refferenced after before declaring
- very useful for anonymous callbacks
```javascript
function sayHi () {
  console.log('Hi')
}

const sayHi = () => {
  // no arguments object
  // no this of function but enclosing scope
  console.log('Hi')
}
```
### default function parameters
```javascript
function sayHi (name = 'there') {
  console.log(`Hi ${name}`)
}
```

### spread operator
```javascript
const mains = ['sandwich', 'salad']
const desserts = ['icecream', 'brownie']

const menu = [].concat(mains).concat(desserts)
const menu = [...mains, ...desserts]
```
```javascript
// in es9 added for object as well!
const mains = {sandwich: 8, salad: 3}
const deserts = {icecream: 4, brownie: 5}

const menu = Object.assign({}, mains, desserts)
const menu = {...mains, ...deserts}
```

### template literals
```javascript
const songNum = 376
const msg = 'Hello you have' + songNum + 'songs.'
const msg = `Hello you have ${songNum} songs.`
```

### Enhanced object properties
```javascript
const color = 'red'
const btn =  {
  // props...
  color: color
}

// same as 
const btn =  {
  // props...
  color
}
```

### Modules
- export functions, variables
- import them in different files

## Polyfilling and transpilling
- You can fully control your code environment in a server, but not in a browser.
- Remember to check what language features are supported where your code needs to be executed.
- Polyfilling means adding the code required for the new feature to run properly.
- Transpiling is a way to translate code that uses new features into the equivalent code if it was using older features. Most popular library is [babel](https://babeljs.io/)
- to check for support of features in browsers [caniuse.com](http://caniuse.com/)
- to check for backend node.js [node.green](http://node.green/)
