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