---
sidebar_position: 1
---

# Basic Hooks
Hooks are built-in functions in React that do some things.

They can only be used within the Component function.

## useState

Hook to manage the Component's state. [Documentation](https://reactjs.org/docs/hooks-state.html).

```jsx
const [state, setState] = React.useState(defaultValue)
const [count, setCount] = React.useState(defaultValue)
const [user, setUser] = React.useState(defaultValue)
```

Returns an array of two items. 
First is a variable `state` that contains a state object or just value. You can name variable `state` however you want.

```jsx
const value = state
// or
const {userName, name, age} = user

```

Second is a function `setState` that you need to use to set a new state value.

```jsx
setState(newState)
// or
setState(prevState => {
  // some calculations
  return prevState * 2
})
//or
setState(10)
```

`defaultValue` is a value that we provide when the component is first created.
```jsx
const defaultValue = 10
// or
const defaultValue = {name: 'John', age: 40}
```

## useEffect

Hook that allows you to run some custom code after React renders (and re-renders) your component to the DOM. 

It accepts a callback function which React will call after the DOM has been updated.

And a dependency list in form of an array.

[Documentation]Look at the dependency list as a second argument to the hook. 

If you don't provide this array, useEffect will run after each render and re-render.

`[]` - hook will run only once after the Component is mounted.

`[count]` - hook will run after the Component is mounted and whenever the count value changes.

## useContext



## useReducer

