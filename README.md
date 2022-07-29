# React JS 마스터클래스

## #2 STYLED COMPONENTS

### #2.0 Why Styled Components

- The best way to handle styles in React JS
- easy to implement light/dark mode

### #2.1 Our First Styled Component

- npm i styled-components
- `import styled from "styled-components";`
- write CSS between backticks

```
const Box = styled.div`
  background-color: teal;
  width: 100px;
  height: 100px;
`;
```

### #2.2 Adapting and Extending

- configurable property
- add extra property

```
const Box = styled.div`
  background-color: ${(props) => props.bgColor};
  width: 100px;
  height: 100px;
`;
const Circle = styled(Box)`
  border-radius: 50px;
`;

<Box bgColor="teal" />
<Circle bgColor="tomato" />
```

### #2.3 'As' and Attrs

- use the same styles in different tag
  - as
- save attributes in styled component
  - attrs

```
const Btn = styled.button`
  color: white;
  background-color: tomato;
  border: 0;
  border-radius: 15px;
`;
const Input = styled.input.attrs({ required: true })`
  background-color: tomato;
`;

<Btn as="a" href="/">Log in</Btn>
<Input />
<Input />
```

### #2.4 Animations and Pseudo Selectors

- { keyframes }
  - helper function
- CSS animation
  - from, to
  - 0%, 50%, 100%

```
const animation = keyframes`
  0% {
    transform: rotate(0deg);
    border-radius:0px;
  }
  50% {
    border-radius: 100px;
  }
  100% {
    transform:rotate(360deg);
    border-radius: 0px;
  }
`;

const Box = styled.div`
  animation: ${rotationAnimation} 1.5s linear infinite;
`;
```

- CSS center align

```
display: flex;
justify-content: center;
align-items: center;
```

- pseudo selector

```
span {
  font-size: 36px;
  &:hover {
    font-size: 48px;
  }
  &:active { // click
    opacity: 0;
  }
}
```

### #2.5 Pseudo Selectors part Two

- CSS center of the screen

```
display: flex;
height: 100vh;
width: 100vw;
justify-content: center;
align-items: center;
```

- target styled component

```
${Emoji}:hover {
  font-size: 98px;
}
```

### #2.7 Themes

- `import { ThemeProvider } from "styled-components";`

```
// index.js
const lightTheme = {
  textColor: "#111",
};

<ThemeProvider theme={lightTheme}>
  <App />
</ThemeProvider>

// App.js
const Title = styled.h1`
  color: ${(props) => props.theme.textColor};
`;
```

## #3 TYPESCRIPT

### #3.0 Introduction

- strongly-typed programming language
- check before the code runs
- https://www.typescriptlang.org/play

```
const plus = (a:number, b:number) => a + b;
```

### #3.1 DefinitelyTyped

- https://create-react-app.dev/docs/adding-typescript/
- https://github.com/DefinitelyTyped/DefinitelyTyped
  - npm i --save-dev @types/

### #3.2 Typing the Props

- interface
  - explain object shape to typescript

```
interface CircleProps {
  bgColor: string;
}

const Container = styled.div<CircleProps>`
  width: 200px;
  height: 200px;
  background-color: ${(props) => props.bgColor};
  border-radius: 100px; // half of the width
`;

function Circle({ bgColor }: CircleProps) {
  return <Container bgColor={bgColor} />;
}
```

### #3.3 Optional Props

- `optionalProp?: string;`
  - `optionalProp: string | undefined;`
- ?? (nullish coalescing operator)
  - optionalProp ?? "white"
  - if optionalProp is null or undefined, return "white"
- give default values to the props
  - `funcName({ bgColor, text = "default text" })`
  - boolean
    - `<Dummy active={true} /> // default: false`
    - `<Dummy active />`

### #3.4 State

- when use more than one types on useState
  - `const [value, Setvalue] = useState<number | string>(0);`

### #3.5 Forms

- protect events
  - https://reactjs.org/docs/events.html

```
const [value, setValue] = useState("");
const onChange = (event: React.FormEvent<HTMLInputElement>) => {
  const {
    currentTarget: { value },
  } = event;
  setValue(value);
};
const onSubmit = (event: React.FormEvent<HTMLFormElement>) => {
  event.preventDefault();
  console.log("hello", value);
};
```

### #3.6 Themes

- extend definitions
  - styled.d.ts
  - https://styled-components.com/docs/api#typescript

## #4 CRYPTO TRACKER

### #4.0 Setup

- npm i react-router-dom react-query
- Router.tsx

### #4.1 Styles

- Reset CSS
- createGlobalStyle
- Fragment
  - `<></>`
- font
  - https://fonts.google.com/
  - Source Sans Pro
- color
  - https://flatuicolors.com/palette/gb

### #4.2 Home part One

- Link (react-router-dom)
  - no refresh

```
a {
  text-decoration: none;
  color:inherit;
}
```

- transition
  - control animation speed when changing CSS properties
  - `transition: color 0.2s ease-in;`

### #4.3 Home part Two

- await
  - wait Promiss
  - use in **async function**
  - pause async function until Promise is fulfilled or rejected

```
(async () => {
  const response = await fetch("https://api.coinpaprika.com/v1/coins");
  const json = await response.json();
  setCoins(json.slice(0, 100));
})();
```

### #4.4 Route States

- useLocation
- useParams doesn't need interface
  - string | undefined

```
// Coins.tsx
<Link to={`/${coin.id}`} state={{ name: coin.name }}>

// Coin.tsx
const { coinId } = useParams();
const { state } = useLocation() as RouteState;
<Title>{state?.name || "Loading..."}</Title> // if state is null
```

### #4.6 Data Types

- put 'I' in front of interface name
- create interface quickly
  - `console.log(data);`
  - in Chrome, click 'Store as global variable'
  - `Object.keys(temp1).join()`
  - `Object.values(temp1).map(v => typeof v).join()`
  - use 'option + shift + i' to match each key and type
    - move cursor to end of all lines
  - watch out the object type
- json to interface
  - https://app.quicktype.io/?l=ts
  - http://json2ts.com/

### #4.7 Nested Routes part One

- route inside of another route
- '\*' indicates that a nested route can be render inside the route
  - `<Route path="/:coinId/*" element={<Coin />} />`

### #4.8 Nested Routes part Two

- useMatch
  - returns match data about a route at the given path relative to the current location
- Outlet
  - useful in nested routes
- NavLink
  - can use 'isActive'
- more about react router
  - https://reactrouter.com/docs/en/v6
- custom props on styled components

```
const Tab = styled.span<{ isActive: boolean }>`
  color: ${(props) =>
    props.isActive ? props.theme.accentColor : props.theme.textColor};
`;
```

### #4.9 React Query part One

- fetcher function
  - returns fetch promise
- useQuery(queryKey, fetcher function);
  - returns isLoading, data
  - keeps the data on the cache (caching)

```
const { isLoading, data } = useQuery<ICoin[]>("allCoins", fetchCoins);
```
