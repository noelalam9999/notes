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

## Templates
- any component
- support special syntax
- Templates allow us to dynamically render content on the page by interpolating special syntax with the data that we provide.
- Such syntax also allows us to access methods and properties from the component that the template belongs to.
- interpolation - access variables from the code
- pipes - transform strings to different types - date, currency, uppercase, decimal, percentage - can be chained
- property binding - to pass down to children, one way binding - to the template
- event binding - method indication in a string - to the component
  - two way data binding - syntax of their own, mainly in forms
- directives - conditional and repetitive rendering
  - ng template - shown only if there are no people
  - 

```angular2html
<!-- interpolation -->
<h3>Welcome, {{username}}</h3>

<!--  pipes -->
<p>Your total: {{amount | currency:'EUR'}}</p>
<p>{{deadline | date | uppercase}}</p>  <!--  chained -->

<!--  property binding -->
<button type="button" [disabled]="isDisabled">Submit</button> 
<!--isDisabled is a property of parent, disabled property of child-->
<!--use @input in children property to access-->

<!--  event binding -->
<button (click)="handleSave()">Save</button>

<!--  ngIf -->
<div> *ngIf="people.length > 0 else nopeople">
  ...
</div>

<ng-template #nopeople> <!--  only shown if no people -->
  <p>There are no people to show</p>
</ng-template>

<!-- ngFor -->
<ul>
  <li *ngFor="let person of people">
    {{person.name}}
  </li>
</ul>
```

## Passing data
- data are scoped to the component, if a child needs something, parent has to pass it to it.
- We can pass data down the component tree from parent to child through the @Input binding.
- We can pass data up the component tree through the use of custom events and handler functions with the @Output binding.
```typescript
// friend-list.component.ts

import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-friend-list',
  templateUrl: './friend-list.component.html',
  styleUrls: ['./friend-list.component.css']
})

export class FriendListComponent implements OnInit {

  friends = [
    {name: 'Alisha', favourite: false},
    {name: 'Alex', favourite: false},
    {name: 'Guillem', favourite: false},
  ]

  constructor() {}
  
  ngOnInit(): void {
  }

  addToFavourites(name: String) {
    this.friends.map(friend => {
      if (friend.name === name) {
        friend.favourite = true;
      }
    })
    console.log(this.friends);
  }

}
```

```html
<!-- friend-list.component.html -->

<div *ngFor="let friend of friends">
  <app-friend-card
    [friend]="friend"
    (newFavouriteEvent)="addToFavourites($event)" <!-- custom event -->
  >
  </app-friend-card>
</div>
```

```typescript
// child
@Output();  // each of the output (or input) variables need to have their own decorator
newFavourite = new EventEmitter();

addFavourite () {  <!-- bind to a button -->
    this.newFavourite.emit(this.friend.name)
}
```

## Services
- Services are modules that include reusable logic across our application.
- We can inject these services into our components through dependency injection.
- An example could be an API service that provides the functionality to interact with the back-end API.
- The Angular HttpClient module is the standard way to make HTTP requests in Angular.
- once in constructor, all methods in service is available in the component

```typescript
export class FriendList implements OnInit {
  friends: any[] = [];

  constructor(private friendService: FriendService) {
      this.friends = this.friendService.getFriends()
  }
}
```
## Async code in Angular, RxJS and observables
- Built-in async functionality in Angular uses observables, provided by the RxJS library.
- Observables are a way of handling asynchronous actions through streams.
  - not native to javascript nor angular
- They can be seen as promises that can resolve multiple times (so multiple events)
  - subscribe method will resolve every time there is a change
- Subscribing to an observable allows to define a handler that executes each time there’s a new output.
- httpClient needs to be put into `app.module.ts`
- lifecycle - ngOnInit - any initialization calls

```typescript
// quote.service.ts

import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})

export class QuoteService {

  rootUrl = 'https://cw-quotes.herokuapp.com/api/quotes/random';

  constructor(private http: HttpClient) {}

  getQuote (): Observable<any> {
    return this.http.get(this.rootUrl);
  }
}
```

```typescript
// quote.component.ts

import { QuoteService } from './../quote.service';
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-quote',
  templateUrl: './quote.component.html',
  styleUrls: ['./quote.component.css']
})

export class QuoteComponent implements OnInit {

  quote = "When life gives you lemons...";

  constructor(private quoteService: QuoteService) {}

  ngOnInit(): void {
    this.quoteService.getQuote().subscribe(response => {
      this.quote = response.result.text;
    });
  }

}
```

```angular2html
<!-- quote.component.html -->

<h1>{{quote}}</h1>
```