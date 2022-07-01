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
