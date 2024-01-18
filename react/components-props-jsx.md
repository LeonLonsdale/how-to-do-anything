## How to - create a component

- A component is a piece of the overall UI.
- It is a function that returns JSX to be rendered in the HTML.
- It may have it's own logic and state.
- It can be a regular function or arrow function, and can be exported.
- Its name must be capitalised or React will not recognise it

```ts
const MyComponent = () => {
    // logic
    return (
        // JSX
    )
}

export default MyComponent;
```

## How to - embed a component

- A component is rendered by including it in some JSX in a child of the main/app file.
- The syntax is similar to HTML
- It can self close, or wrap around other JSX

```ts
const App = () => {
  // logic
  return <MyComponent />;
};
```

## How to - pass props to a component

- Components accept props in the same way HTML elements accept attributes
- They can accept props any any form - arrays, functions, other components, strings, booleans, objects etc.,
- They cannot accept:
- Props must always be wrapped in `{ }` unless you are directly passing a string.

```ts
const App = () => {
  const dataString = "This is a prop";
  return <MyComponent string="This is a prop" dataString={dataString} />;
};
```

## How to - receive and use props

- All components have access to props via a `props` object that is passed in by default.
- All props passed to the component are properties of this object.
- They are typically deconstructed immediately.
- They can then be used within the component, or passed as props to a child component (`prop drilling`)

```ts
const MyComponent = ({ string, stringData }) => {
  // logic
  return <MyChildComponent dataString={dataString} />;
};
```

## How to - include JavaScript in JSX

- JSX provides an way to escape back to JavaScript to include data and logic within the JSX
- To do so we wrap the JavaScript in `{ }`
- This does mean that when using an object, we have a weird looking syntax of `{{ }}`

```ts
const Header = () => {
  const isLoggedIn = false;
  return (
    <header>
      <Logo />
      {isLoggedIn && <Button>Logout</Button>}
      {!isLoggedIn && <Button>Login</Button>}
    </header>
  );
};
```

## How to - avoid prop drilling with child components

- There are various ways to avoid prop drilling:
  - Context API
  - Packages such as Redux and Zustand
  - Passing components as children using opening and closing tags
- When using opening and closing tags, the props can be passed directly to the child

```ts
const App = () => {
  const propData = "This is a prop";
  return (
    <MyComponent>
      <MyChildComponent propData={propData} />
    </MyComponent>
  );
};
```

## How to - use the children prop

- The `children` prop is another property on the props object.
- It represents any children of the prop when the prop is used with an opening and closing tag in a return statement within another component.

```ts
const MyComponent = ({ children }) => {
  // logic
  return { children };
};
```

## How to - return more than one element/component in JSX

- JSX rules only allow a single element or component to be returned from a component.
- To return more than one, we wrap them in a parent element
- If we don't want unnecessary parent elements in our HTML, we can use a React Fragment
- The react fragment is an empty set of angle brackets which counts as a single element, but is not included in the HTML.

```ts
const App = () => {
  // logic
  return (
    <>
      <Header />
      <Sidebar />
      <Main />
      <Footer />
    </>
  );
};
```

## How to - type props in TypeScript

- Conventionally, we create a type with a name postfixed with 'Props'

```ts
type MyComponentProps = {
  children: React.ReactNode;
  propData: string;
};

const MyComponent = ({ children, propData }: MyComponentProps) => {
  // logic
  return { children };
};
```
