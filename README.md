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

### #4.10 React Query part Two

- Destructuring assignment

```
const { isLoading: infoLoading, data: infoData } = useQuery<InfoData>(
  ["info", coinId],
  () => fetchCoinInfo(coinId ?? "")
);
const { isLoading: tickersLoading, data: tickersData } = useQuery<PriceData>(
  ["tickers", coinId],
  () => fetchCoinTickers(coinId ?? "")
);
```

- when argument of fetchCoinInfo is only string
  - 'coinId' is never null
    - fetchCoinInfo(coinId!)
      - non-null assertion operator
  - 'coinId' can be null
    - fetchCoinInfo(coinId ?? "")
      - nullish coalescing operator

### #4.13 Price Chart part Two

- APEXCHARTS.JS
  - https://apexcharts.com/

### #4.15 Final Touches

- 3rd argument of useQuery
  - options object
    - refetchInterval
- react-helmet-async
  - document head

## #5 STATE MANAGEMENT

### #5.0 Dark Mode part One

- recoil
  - a state management library
    - good for small project

### #5.1 Dark Mode part Two

- interface of function

```
interface IRouterProps {
  toggleDark: () => void;
}
// need global state
```

### #5.2 Introduction to Recoil

- Recoil
  - RecoilRoot
  - atom({key, default})
  - useRecoilValue
    - getter
  - useSetRecoilState
    - setter
    - re-render
  - useRecoilState
    - [value, setValue]
    - similar to useState

### #5.5 To Do Setup

- handle a form in React.js

```
function ToDoList() {
  const [toDo, setToDo] = useState("");
  const onChange = (event: React.FormEvent<HTMLInputElement>) => {
    const {
      currentTarget: { value },
    } = event;
    setToDo(value);
  };
  const onSubmit = (event: React.FormEvent<HTMLFormElement>) => {
    event.preventDefault();
    console.log(toDo);
  };
  return (
    <div>
      <form onSubmit={onSubmit}>
        <input onChange={onChange} value={toDo} placeholder="Write a to do" />
        <button>Add</button>
      </form>
    </div>
  );
}
```

- destructuring

```
const {
  currentTarget: { value },
} = event;
==
const { value } = event.currentTarget;
```

### #5.6 Forms

- React Hook Form
  - https://react-hook-form.com/
  - useForm({ defaultValues: {} }?)
    - register(name, optionsObj?)
      - name
      - onBlur
      - onChange
      - ref
    - watch
    - handleSubmit(onValid, onInvalid?)
    - formState
    - setError(name, errorObj, { shouldFocus? })
    - setValue
  - register optionsObj
    - required
    - minLength
    - pattern
    - validate
- RegExp
  - https://www.regexpal.com/

```
function ToDoList() {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm<IForm>({ defaultValues: {} });
  const onValid = (data: any) => {
    console.log(data);
  };
  return (
    <div>
      <form onSubmit={handleSubmit(onValid)}>
        <input
          {...register("email", {
            required: "Email is required",
            pattern: {
              value: /^[A-Za-z0-9._%+-]+@naver.com$/,
              message: "Only naver.com emails allowed",
            },
          })}
          placeholder="Email"
        />
        <span>{errors?.email?.message}</span>
        <input
          {...register("password", {
            required: "Password is required",
            minLength: {
              value: 5,
              message: "Your password is too short.",
            },
          })}
          placeholder="Password"
        />
        <span>{errors?.password?.message}</span>
        <button>Add</button>
      </form>
    </div>
  );
}

```

### 5.9 Custom Validation

- setError(name, errorObj, { shouldFocus? })

```
const onValid = (data: IForm) => {
  if (data.password !== data.password1) {
    setError("password1", { message: "Password are not the same" });
  }
  // setError("extraError", { message: "Server offline." });
};
```

- validate

```
<input
  {...register("firstName", {
    required: "write here",
    validate: {
      noNico: (value) => !value.includes("nico") || "no nicos allowed",
      noNick: (value) => !value.includes("nick") || "no nicks allowed",
      // async (value) => check server
    },
  })}
  placeholder="First Name"
/>
```

### #5.11 Add To Do

- to add a new value to the old array in setter
  - `setToDos((oldToDos) => [{ text: toDo, category: "TO_DO" }, ...oldToDos]);`
    - spread syntax

### #5.13 Categories

- typescript tip
  - use element of interface
    - `newCategory: IToDo["category"]`
- receiving the name from the button via the event

```
const onClick = (event: React.MouseEvent<HTMLButtonElement>) => {
  const {
    currentTarget: { name },
  } = event;
};
```

### #5.14 Immutability part One

- update category with same order
  1. find index of the target to do based on id
  2. build a new to do
  3. replace the to do in the target index with new to do

```
setToDos((oldToDos) => {
  const targetIndex = oldToDos.findIndex((toDo) => toDo.id === id);
  const newTodo = { text, id, category: name as any };
  return [
    ...oldToDos.slice(0, targetIndex),
    newTodo,
    ...oldToDos.slice(targetIndex + 1),
  ];
});
```

- another way
  - splice
  - map

### #5.16 Selectors part One

- selector({ key, get })
  - derived state
  - modify output of atom

```
export const toDoSelector = selector({
  key: "toDoSelector",
  get: ({ get }) => {
    const toDos = get(toDoState);
    const category = get(categoryState);
    return toDos.filter((toDo) => toDo.category === category);
  },
});
```

### #5.18 Enums

- enum
  - https://www.typescriptlang.org/ko/docs/handbook/enums.html

```
export enum Categories {
  "TO_DO" = "TO_DO",
  "DOING" = "DOING",
  "DONE" = "DONE",
}

export const categoryState = atom<Categories>({
  key: "category",
  default: Categories.TO_DO,
});
```

### #5.19 Recap

- Recoil
  - https://recoiljs.org/
  - recoil-persist

## #6 TRELLO CLONE

### #6.0 Get Selectors

- string to number
  - `+"1"` -> `1`

### #6.1 Set Selectors

- useRecoilState(selector)
  - [0] -> value return by get property
  - [1] -> call set property
- set

```
export const hourSelector = selector<number>({
  key: "hours",
  get: ({ get }) => {
    const minutes = get(minuteState);
    return minutes / 60;
  },
  set: ({ set }, newValue) => {
    const minutes = Number(newValue) * 60;
    set(minuteState, minutes);
  },
});
```

### #6.2 Drag and Drop part One

- react-beautiful-dnd
  - https://github.com/atlassian/react-beautiful-dnd#readme
  - drop
    - provided
      - innerRef
      - droppableProps
      - placeholder
    - snapshot
      - isDraggingOver
      - draggingFromThisWith
  - drag
    - provided
      - innerRef
      - draggableProps
      - dragHandleProps
    - snapshot
      - isDragging

```
<DragDropContext onDragEnd={onDragEnd}>
  <Wrapper>
    <Boards>
      <Droppable droppableId="one">
        {(provided) => (
          <Board ref={provided.innerRef} {...provided.droppableProps}>
            {toDos.map((toDo, index) => (
              <Draggable draggableId={toDo} index={index}>
                {(provided) => (
                  <Card
                    ref={provided.innerRef}
                    {...provided.draggableProps}
                    {...provided.dragHandleProps}
                  >
                    {toDo}
                  </Card>
                )}
              </Draggable>
            ))}
            {provided.placeholder}
          </Board>
        )}
      </Droppable>
    </Boards>
  </Wrapper>
</DragDropContext>
```

### #6.4 Styles and Placeholders

- ts tip
  - right click -> Go to Type Definition

### #6.5 Reordering

1. Delete item on source.index
2. Put back the item on the destination.index

- splice(start, deleteCount?, ...items)

### #6.6 Reordering part Two

- never mutate in the state world
- key of Draggable needs to same as the draggableId

```
const onDragEnd = ({ draggableId, destination, source }: DropResult) => {
  if (!destination) return;
  setToDos((oldToDos) => {
    const toDosCopy = [...oldToDos];
    // 1) Delete item on source.index
    toDosCopy.splice(source.index, 1);
    // 2) Put back the item on the destination.index
    toDosCopy.splice(destination.index, 0, draggableId);
    return toDosCopy;
  });
};
```

### #6.7 Performance

- so many re-rendering
- react memo
  - prevents rendering of component when props did not change
  - optimization

```
export default React.memo(DragabbleCard);
```

### #6.8 Multi Boards

- Object.keys(o)
  - return key array
- Object.values(o)
  - return value array
- `Object.keys(o).map(id => o[id])`
  - can use id and values

### #6.9 Same Board Movement

- css tip
  - gap
- overwrite

```
if (destination?.droppableId === source.droppableId) {
  // same board movement.
  setToDos((allBoards) => {
    const boardCopy = [...allBoards[source.droppableId]];
    boardCopy.splice(source.index, 1);
    boardCopy.splice(destination.index, 0, draggableId);
    return {
      ...allBoards,
      [source.droppableId]: boardCopy,
    };
  });
}
```

### #6.10 Cross Board Movement

```
if (destination.droppableId !== source.droppableId) {
  // cross board movement.
  setToDos((allBoards) => {
    const sourceBoard = [...allBoards[source.droppableId]];
    const destinationBoard = [...allBoards[destination.droppableId]];
    sourceBoard.splice(source.index, 1);
    destinationBoard.splice(destination.index, 0, draggableId);
    return {
      ...allBoards,
      [source.droppableId]: sourceBoard,
      [destination.droppableId]: destinationBoard,
    };
  });
}
```

### #6.11 Droppable Snapshot

- css tip
  - flex-grow
- snapshot

```
const Area = styled.div<IAreaProps>`
  background-color: ${(props) =>
    props.isDraggingOver ? "pink" : props.isDraggingFromThis ? "red" : "blue"};
  flex-grow: 1;
  transition: background-color 0.3s ease-in-out;
`;

<Area
  isDraggingOver={snapshot.isDraggingOver}
  isDraggingFromThis={Boolean(snapshot.draggingFromThisWith)}
  ref={provided.innerRef}
  {...provided.droppableProps}
>
```

### #6.13 Refs

- reference
  - grab HTML element
  - to use the methods

```
const inputRef = useRef<HTMLInputElement>(null);
const onClick = () => {
  inputRef.current?.focus();
  setTimeout(() => {
    inputRef.current?.blur();
  }, 5000);
};

<input ref={inputRef} placeholder="grab me" />
<button onClick={onClick}>Click me</button>
```

### #6.14 Task Objects

- number to string
  - `1 + ""` -> `"1"`
