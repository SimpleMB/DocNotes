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

type User = {
    id: number;
    username: string;
}

const [users, setUsers] = React.useState<User[]>([]);

```
If we need to send users and/or dispatch function somewhere to the other component:

```jsx
type UserListProps = {
    users: User[];
    setUsers: React.Dispatch<React.SetStateAction<User[]>>
}

const UserList = ({users, setUsers}) => {

}
```