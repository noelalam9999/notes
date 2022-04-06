# React
- created by facebook
- also react native, framework for native apps for android and ios
- framework - convention over configuration
- react is a library and is unopinionated (no router added)
- data flows in one direction from parent to child components
- component based - recive props and handles its own state
- component returns a JSX template that then gets transpiled into HTML
- declarative approach - react rerenders if props or state changes

##Components
- Piece of user interface, app is basically a tree of components
- Root component - the whole app, probably called App
- Can be classes or functions that contain logic and return JSX syntax.
- JSX is a superset of JavaScript and HTML that React compiles to JavaScript and renders as HTML elements in the browser.
- JSX is a syntaxt extension - write html in react 
- can write logic in {}
- function components are considered industry standard

Class component
```jsx
class Header extends React.Component {
  render() {
    return <h2>Welcome</h2>
  }
}
```

Function component
```jsx
function Header () {
  return <h2>Welcome</h2>
}
```

## Props 
- React allows to pass data from a parent component to its children through “props”, which are made of a key and value pair, and are similar to HTML attributes.
- Props should be immutable, do not change the value of props - help us to write reusable components

Class component
```jsx
class Header extends React.Component {
  render() {
    return <h2>Welcome {this.props.name}</h2>
  }
}
```

Functional component
```jsx
function Header (props) {
  return <h2>Welcome {props.name}</h2>
}
```

## State
- Class components can have an internal “state” which is an object that contains data that is local to the component.
- You can access the state in a class component with this.state.<propertyName> and update any value by using the this.setState() function (never directly modify the state object).
- Function components instead use the useState hook to read and update their internal state.
- Whenever you update the state in a component, React re-renders that element in the browser.
- state exists inside of the component
- state can change / mutable - useState() to change state

Class component
```jsx
class Header extends React.Component {
  constructor (props) {
    super(props)
    this.state = {greeting: 'Welcome'}
  }
  
  render () {
    return <h2>{this.state.greeting} {this.props.name}</h2>
  }
}
```

Functional component
```jsx
function Header (props) {
  const [greeting, setGreeting] = useState('Welcome')
  return <h2>{greeting} {props.name}</h2>
}
```

## Conditionals and lists
- Since JSX is a superset of JS, you can use conditional logic to show different data in the browser based on certain conditions (e.g. through if...else statements or ternary operators).
- If you have an array of data, and need to render each element in a separate component of the same type, you can use the map() function to programmatically generate the required JSX syntax.

Class component
```jsx
class ShowFriends extends React.Component {
  render() {
    const friendsList = [
      { name: 'Tom', status: 'online' },
      { name: 'Richard', status: 'online' },
      { name: 'Harry', status: 'offline' }
    ]
    const onlineFriends = friendsList.map(
      (friend) => (friend.status === 'online') && <h3>{friend}</h3>
    )
    return <>{onlineFriends}</>
  }
}
```

Functional component
```jsx
function ShowFriends() {
  const friendsList = [
    { name: 'Tom', status: 'online' },
    { name: 'Richard', status: 'online' },
    { name: 'Harry', status: 'offline' }
  ]
  const onlineFriends = friendsList.map(
    (friend) => (friend.status === 'online') && <h3>{friend}</h3>
  )
  return <>{onlineFriends}</>
}
```

## Handling events
- React provides several built-in JSX attributes that allow you to handle events by assigning a callback function to them.
- Native event handlers in React use camel case spelling (e.g. onChange for an input, or onClick for a button), versus the small cap version of the corresponding native event in the browser (e.g. onchange, or onclick

Class component
```jsx
class Header extends React.Component {
  constructor(props) {
    super(props)
    this.state = { greeting: 'Welcome' }
    // This binding is necessary to make `this` work in the callback
    this.handleLogOut = this.handleLogOut.bind(this);
  }

  handleLogOut() {
    this.setState({ greeting: 'Goodbye' })
  }

  render() {
    return (
      <>
        <h2>{this.state.greeting} {this.props.name}</h2>
        <button onClick={this.handleLogOut}>Log Out</button>
      </>
    )
  }
}
```

Functional component
```jsx
function Header(props) {
  const [greeting, setGreeting] = useState('Welcome')

  function handleLogOut() {
    setGreeting('Goodbye')
  }
  return (
    <>
      <h2>{greeting} {props.name}</h2>
      <button onClick={handleLogOut}>Log Out</button>
    </>
  )
}
```

##Lifecycle methods
- Are used to trigger a custom logic in certain pre-defined moments of a class component life.
- componentDidMount is invoked after the first render of a component. We use this method to perform actions that cause side effects (e.g. fetching data from an API).
- componentDidUpdate is invoked after every render (excluding the first one) and is used to perform actions that need to happen when changes have occurred.
- componentWillUnmount is called when a component is going to be removed from the DOM, and should be used to perform any cleanup logic (e.g. clearing an interval).

## Hooks
- functions that give us special functionalities
- must be called at top level and inside a rect function unless using custom hooks

- Allow us to gain all the functionality available to class components, inside functional components.
- The useState() hook can be called inside a function component to add local state to it. It’s a function that takes the initial state value and returns an array with two elements: a variable that is tied to the current state value, and a function to update it.
- The useEffect() hook gives the ability to perform side effects from a function component, implementing logic that is executed after the render phase. It serves the same purpose as componentDidMount(), componentDidUpdate(), and componentWillUnmount() in React classes, but unified into a single API. It takes two arguments. The first one is the callback that contains the side effects logic. The second one is the “dependency array” and is optional.
- The dependency array indicates to React what you want to “track”. Depending on the dependency array status, the useEffect() function is run according to the following rules:
- If there is no array, at initial render and after every update (track everything).
- If the array is empty, only after the initial render (don’t track anything).
- If the array contains elements, after the initial render and every time the data changes (track specific elements).
- You can also build custom hooks, which can combine multiple hooks to provide reusable functionality across your app.
- Hooks can only be called inside React function components or custom hooks and should never be invoked conditionally.

## useState
- updating the state
- takes only initial state as argument
- setter are async so use ReactDevTools

## useEffect
- dependency array
- can have multiple useEffects in a component

Class component
```jsx
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    this.setState({ count: this.state.count + 1 })
  }
  componentDidMount() {
    document.title = `You clicked ${this.count} times`;
  }
  render() {
    return (
      <>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.handleClick()}>
          Click me
        </button>
      </>
    )
  }
}
```

Function component
```jsx
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  return (
    <>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </>
  );
}
```

## Context
- to avoid props drilling
- Is generated using `React.createContext()` and allows to directly share data across different components.
- Data can be consumed invoking the useContext() hook and passing the desired context as argument.
- Data can also be shared across components by using the context Provider and Consumer property.
- create context, context provider (takes value), useContex hook
- 

## Forms
- React forms replace the default HTML form behaviour, and allow to add custom submission logic, gaining access to the form data.
- You can save input, textArea and select values in a component state through onChange handlers. These values in the state are then connected back to the HTML form through the value property of the original field, thus creating a single source of truth. This is also known as two-way binding.
- You can reset the form fields at any time by modifying the component state, and you can add a custom submit handler using the onSubmit prop.
- controlled component

Class component
```jsx
class MyForm extends React.Component {
  state = { name: '' }
  handleChange = (event) => {
    this.setState({ name: event.target.value })
  }
  handleSubmit = (event) => {
    event.preventDefault()
    // add custom submit logic here...
    this.setState({ name: '' }) // reset the input field
  }
  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <input type="text" value={this.state.name} onChange={this.handleChange} />
        <button type="submit"> Submit </button>
      </form>
    )
  }
}
```

Functional component
```jsx
function MyForm() {
  const [name, setName] = useState('')
  function handleChange(event) {
    setName(event.target.value)
  }
  function handleSubmit(event) {
    event.preventDefault()
    // add some logic here 
    setName('') // reset the input field 
  }
  return (
    <form onSubmit={handleSubmit}>
      <input type="text" value={name} onChange={handleChange} />
      <button type="submit"> Submit </button>
    </form>
  )
}
```