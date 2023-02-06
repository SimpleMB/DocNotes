---
sidebar_position: 1
---

# Basic types in React

---
## JSX.Element

Every component in React has a type: [Docs❤️](https://reactjs.org/docs/hooks-state.html).

```jsx
// JSX.Element
const Form = () => JSX.Element
```

## PropTypes
When a component gets some props we can type them like this:

```jsx
type PropTypes = {
    id: number;
    username: string;
    age: number;
    articles?: Article[]; // optional
    admin?: boolean       // optional
}

const User = (props: PropTypes) => {
    const {id, username, age} = props;
    // component body
}

// or desctructure

const User = ({id, username, age}: PropTypes) => {
    const {id, username, age} = props;
    // component body
}


```

## Typing Children
When a component receives children or an array of children we need to type it. We can use an internal React type called `React.ReactNode`. Doesn't matter if we have a single child or multiple, it's a string, component or HTMLElement.

```jsx
type UserListProps = {
    children: React.ReactNode;
}

const UserList = ({children} : UserListProps) => {

    return {children}
}

```
## Typing Styles
Sometimes in props, we can receive special styling for our component. Here is how to type it:

```jsx
type UserListProps = {
    children: React.ReactNode;
    style?: React.CSSProperties
}

const UserList = ({children, style = {}} : UserListProps) => {

    return (
        <div style={style}>
            {children}
        <div/>
    )
}

```