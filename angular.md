# Front-end frameworks

Basic files
- html
- css
- JavaScript

Frontend frameworks help us to write html and css

##History
- jQuery very widely adopted - browser compability, manipulation of DOM
- frameworks emerged as the need to easier build large applications
- code should be maintainable (easy to read test and change)
- complex interfaces should be built from simple parts
- DOM manipulations are slow, perform as few as possible 
- stop reinventing the wheel - follow conventions that work

## Front end frameworks
- Front-end frameworks provide a set of pre-built functionality to facilitate the creation of client apps.
- Some frameworks are more opinionated and favor “convention over configuration” to speed-up the development process and enforce certain patterns, whereas others are more flexible and leave more choices to the developer.
- initial file and directory structure
- boilerplate code for common functionalities
- a set of design principles
- common are React, Vue and Angular

## components
- small reusable pieces of the user interface
- have their own logic, html and css
- combining these blocks allows us to build complex apps

## Single-page applications
- SPAs use JavaScript to update the content of a single web page, fetching the required data from the server API, instead of fetching the rendered HTML of different pages. 
- No reloading during use
- SPAs initially need more time to load all the required scripts and render the content, but offer a more responsive UX from that moment onwards.
- high degree of user interaction - follow this pattern to be faster than multipage app


## Angular
- from Google
- scalable for building scalable web applications
- Angular and Angular JS NOT COMPATIBLE
- designed to build single page applications
- first party libraries - fully equipped 
  - routing, forms, httpClient, animations, pwa
- suite of developer tools - Angular CLI
- testing setup - very straight forward - Jasmine and Karma 
- security is core characteristics
- written in TypeScripts
- class based components only

## Angular components
- A component-based architecture allows you to abstract what are the core elements of your app, by defining them once and using them wherever needed, avoiding code repetitions and increasing maintainability.
- Components are the building blocks of an Angular app, where each one represents a portion of the view, and is made of HTML, CSS and TypeScript.
- custom CSS selector <MyComponent>
- By switching out components, we can produce interactive UIs and simulate page changes.
- To simplify the creation of new components you can use the Angular CLI.
- @Component - decorator elevates these classes to blocks that angular then knows how to assemble
- 
## Angular services
- reuse logic across application, between components
- @Injectable

## Angular modules
- group components and services that are similar together
- @NgModule


## TypeScript
- TypeScript is a strongly typed superset of JavaScript.
- TypeScript needs to be compiled to JavaScript to be executed.
- A strongly typed code environment is more reliable and less prone to bugs
  - Less developer error
  - Debugging is easier - very detailed messages
  - readability is also great advantage
  - better developer in the long run - think about edge cases
- Angular is written in TypeScript, however TS is not directly linked to Angular and can be used separately.
- Decorators are a TypeScript feature to add functionality to a class, method, accessor, property, or parameter.
- Angular uses decorators to register components, services and other features.
- Interfaces - to type out object types
  - question mark - optional
  - can be extended - everything that parent has PLUS extra fields
  - dynamic keys - [key: string]: number | string - can have any other keys that are string but value only number or string
- add types into functions as well, void - no return statement
  - can also return type Promise<HERE COMES THE INTERFACE>
- class interfaces

```typescript
interface DataService {
  [key: string]: Function
}

interface Component {
  name: string
}


class Component implements Component {
  constuctor(name: string, dataService: DataService) {
    this.name = name
    this.age = 5 // this will cause an error
  }
}
```
- generics
  - any - can be anything
  - generics can accept a value and once they do, that type is registered
```typescript
function test<T> (arg: T) : T {
    return arg
}

let a = test(5) //type is number
a = 'string' // throws error
```
