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
##useEffect hook
