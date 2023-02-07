---
sidebar_position: 3
---

# Typing Class Components in React

---
## Typing Props and State

We need to use types twice. Once in the type parameter and again in the instance property.

```jsx
type CounterProps = {
    message: string;
}

type StateProps = {
    count: number;
}
class Counter extends React.Component<CounterProps, StateProps> {
    state: CounterProps = {
        count: 0,
    }
    // ... rest of the component
}
```