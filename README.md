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
- https://www.typescriptlang.org/play

```
const plus = (a:number, b:number) => a + b;
```
