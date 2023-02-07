---
sidebar_position: 2
---

# Advanced types in React

---
## useState hook

This hook contains three parts:

```jsx

const [users, setUsers] = React.useState([]);
```
1. state `users` will contain an array of users we got from the server.
2. dispatch function `setUsers`.
3. initial state that is an empty array, but in the future, we know that there will be an array of users.

We can type it like this:

```jsx

type UserType = {
    id: number;
    username: string;
}

const [users, setUsers] = React.useState<UserType[]>([]);

// or we can start with `null` as a initial value but we know that there will be array of users
// so we can use OR operator - UserType[] OR null

const [users, setUsers] = React.useState<UserType[] | null>(null)

```
If we need to send users and/or dispatch function somewhere to the other component:

```jsx
type UserListProps = {
    users: UserType[];
    setUsers: React.Dispatch<React.SetStateAction<UserType[]>>
}

const UserList = ({users, setUsers} : UserListProps) => {

}
```
## Typing Forms

1. **Typing Events.** When we hover over the onChange property we will get a hint from the ide what type it is. We can then use it when we type the function that will be triggered.
```jsx
<input {...props} value={value} onChange={changeCount}/>
```

```jsx
const changeCount = (event: React.ChangeEvent<HTMLInputElement>) => {
    setCount(+event.target.value);
  };
  //...
  <input {...props} value={value} onChange={changeCount}/>
```
2. **Typing inline functions.** Typing this type of function is not necessary. Typescript will figure out what we want.

```jsx
<button onClick={() => setCounter(prev => prev++)}/>
<input 
    type="number" 
    value={value} 
    onChange={(event) => setValue(+event.target.value)}
/>
```

## Typing reducers
When a state gets complicated we often use reducers.

```jsx
const reducer = (state: any, action: any) => {
    // state computing
}
```
We know the shape of the state:
Next, we need to figure out the actions:
```jsx
type PizzaAction = {
    type:
        | "UPDATE_NUMBER_OF_PEOPLE"
        | "UPDATE_SLICES_PER_PERSON"
        | "UPDATE_SLICES_PER_PIE";
    payload: number;
}

const reducer = (state: PizzaState, action: PizzaAction) => {
    // state computing
}
```
:::tip Use constants
Instead of strings in action types create an enum.
:::

If we want to send dispatch action to some other components:

```jsx
const Calculator = ({ dispatch, state }: { 
        state: PizzaState;
        dispatch: React.Dispatch<PizzaAction>;
    }) => {
    //... calculator body
}
```