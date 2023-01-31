---
sidebar_position: 1
---

# Basic Hooks

Hooks are built-in functions in React that do some things. [Docs❤️](https://beta.reactjs.org/reference/react)

They can only be used only in function Components.

## useState

Hook to manage the Component's state. [Docs❤️](https://reactjs.org/docs/hooks-state.html).

```jsx
const [state, setState] = React.useState(defaultValue);
const [count, setCount] = React.useState(defaultValue);
const [user, setUser] = React.useState(defaultValue);
```

Returns an array of two items.
First is a variable `state` that contains a state object or just value. You can name variable `state` however you want.

```jsx
const value = state;
// or
const { userName, name, age } = user;
```

Second is a function `setState` that you need to use to set a new state value.

```jsx
setState(newState);
// or
setState((prevState) => {
  // some calculations
  return prevState * 2;
});
//or
setState(10);
```

`defaultValue` is a value that we provide when the component is first created.

```jsx
const defaultValue = 10;
// or
const defaultValue = { name: "John", age: 40 };
```

## useEffect

[Docs❤️](https://reactjs.org/docs/hooks-effect.html)

Hook that allows you to run some custom code after React renders (and re-renders) your component to the DOM.

It accepts a callback function which React will call after the DOM has been updated.

And a dependency list in form of an array.

```jsx
useEffect(() => {
    // Update the document title after the component is mounted
    document.title = `Hello mthrfkr`;

    // No deps array
  });
```
```jsx
useEffect(() => {
    document.title = `You clicked ${count}} times`;
  }, [count]);
```
```jsx
useEffect(() => {
    // Update the document title after the component is mounted
    cosnt idx = setInterval(someFunction, 1000);
    return () => {
      clearIndex(idx)
    }
  }, []);
```

Look at the dependency list as a second argument to the hook.

If you don't provide this array, useEffect will run after each render and re-render.

`[]` - hook will run only once after the Component is mounted.

`[count]` - hook will run after the Component is mounted and whenever the count value changes.

## useContext
Hook that lets you read and subscribe to context from your component. [Docs❤️](https://beta.reactjs.org/reference/react/useContext)

First create a React Context.

```jsx
const SomeContext = React.createContext()
const SomeContext = React.createContext(defaultValue)
```

Then we can create to provide this context to other comoponents in the tree.
```jsx
<SomeContext.Provider value={someValue}>
  <OtherComponent>
<SomeContext.Provider>
```
In the OtherComponent we can access this context.
```jsx
const value = useContext(SomeContext)
```
Use in the custom hooks will be described later.

## useReducer
