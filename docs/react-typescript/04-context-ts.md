---
sidebar_position: 4
---

# React Context in Typescript
I prefer to create an abstraction - a custom react hook for the context API.

Abstraction consists of three parts:
1. createContext()
2. Context.Provider (exported)
3. custom hook (exported)
---
## Typing React.createContext()
When we create context it's ok to provide an empty object as a default value but we need to use [as] keyword. We have to do this so Typescript knows what will be there in the future.
```jsx
const ColorContext = React.createContext<ColorContextType>({} as ColorContextType);
```

## Typing Context Provider
It's better to encapsulate Context.Provider in abstraction with its logic. This way we don't need to accept [value] prop later when we use it somewhere. It will only accept [children] prop that we type as an React.ReactNode.
```jsx
function ColorContextProvider({ children }: { children: React.ReactNode }) {
  const [rgb, dispatch] = React.useReducer(reducer, {
    red: 0,
    green: 0,
    blue: 0
  });
  
  // ^^ This is the logic that will be shared across the components in the tree^^

  return (
    <ColorContext.Provider value={{ rgb, dispatch }}>    // here we provide [value] from the internal logic
      {children}
    </ColorContext.Provider>
  );
}
```

## Typing custom hook
Typescript will appreciate that we think about saving our asses so it's better to check if our useContext hook receives a context from the provider. If not, then we used this hook in the wrong component. There is also a possibility that we wrapped not what we wanted with the Provider.

```jsx
function useColorContext() {
  const context = React.useContext(ColorContext);
  if (!context) {
    throw new Error('useColorContext must be used inside ColorContextProvider');
  }
  return context;
}
```

---
## Full context file

Here we have how to build a custom context hook with the provider - fully typed.
It's better to move shared logic into Provider eg., reducer.



```jsx
import * as React from 'react';
import { AdjustmentAction, reducer } from './reducer';
import { RGBColorType } from './types';

type ColorContextType = {
  rgb: RGBColorType;
  dispatch: React.Dispatch<AdjustmentAction>;
};

const ColorContext = React.createContext<ColorContextType>(
  {} as ColorContextType
);

function ColorContextProvider({ children }: { children: React.ReactNode }) {
  const [rgb, dispatch] = React.useReducer(reducer, {
    red: 0,
    green: 0,
    blue: 0
  });
  return (
    <ColorContext.Provider value={{ rgb, dispatch }}>
      {children}
    </ColorContext.Provider>
  );
}

function useColorContext() {
  const context = React.useContext(ColorContext);
  if (!context) {
    throw new Error('useColorContext must be used inside ColorContextProvider');
  }
  return context;
}

export { ColorContextProvider, useColorContext };
```