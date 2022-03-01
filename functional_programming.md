# Javascript function specific behavior

- functions that are not returning anything will return undefined
- functions can be called without parameters even if function is defined with parameters


## `rest` and `spread` operator

```javascript
// if ... in function declaration, then its called a rest operator and will collect all arguments into an array
function listFruits (...fruits) {
    // if we want to spread an array into individual elements, then use spread
    return [...fruits]
}
```

# Writing pure function
Functions should do one thing, pass to the function what is needed and not pollute the environment
- return exactly same result when called with same parameters - we can predict the results
- don't have any side effects 
- don't mutate the input
- there are passed exactly what they need to run

# Data types in JavaScript
## Primitive - not mutable
these pass by value
- boolean
- strings
- numbers
- undefined
- null
- symbols

```javascript
// example of imutable behaviour

let word1 = 'hello'
let word2 = word1
// word2 = 'hello'
word1 = 'something else'
// word2 still 'hello'
```

## Collections - mutable
When creating a collection, the name is only referencing the collection
- arrays
- objects

```javascript
const arr1 = [1, 2, 3]
const arr2 = arr1
arr1.push(4)
// arr1 = [1, 2, 3, 4]
// arr2 = [1, 2, 3, 4]

arr2.push(5)
// arr1 = [1, 2, 3, 4, 5]
// arr2 = [1, 2, 3, 4, 5]

// important to copy - shallow and deep
arr2 = [...arr1] // example of shallow copy
```

# Pure functions
```javascript
// this will affect the array
let arr = [3, 2];
function addOneToArray (arr) {
    arr.push(1)
    return arr
}

// this is better
function addOneToArray (arr) {
    return [...arr, 1]
}
```

# Performance consideration
```javascript
// two different performance consideration - memory and computation
const reversed = reverseStr('string')
const firstLetter = first(reversed)
const shoutLetter = shout(firstLetter)
// this three variables will be stored in the working memory until all code is run

// one way to fix this is to chain it
shoutLetter = shout(fist(reversed('string')))
// but thats really bad readibility 

// this improves readibility as well as performance as variables are dropped once the function returns
function shoutLastLetter (str) {
    const reversed = reverseStr('string')
    const firstLetter = first(reversed)
    const shoutLetter = shout(firstLetter)
    return shoutLetter
}
```
