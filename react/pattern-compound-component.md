# How to - reuse code with the Compound Component Pattern

- This pattern makes for very self-contained components that manage their own state.
- Achieved using a context that makes the state available to its children.

```ts
// create the context
const CounterContext = createContext();

// create parent component
function Counter({ children }) {
  const [count, setCount] = useState();
  const handleInc = () => setCount((cur) => cur + 1);
  const handleDec = () => setCount((cur) => cur - 1);

  return (
    <CounterContext.Provider value={{ count, handleInc, handleDec }}>
      <span>{children}</span>
    </CounterContext.Provider>
  );
}

// create the child components
const Count = () => {
  const { count } = useContext(CounterContext);
  return <span>{count}</span>;
};
const Label = ({ children }) => <span>{children}</span>;
const Increase = ({ icon }) => {
  const { handleInc } = useContext(CounterContext);
  return <button onClick={handleInc}>{icon}</button>;
};
const Decrease = ({ icon }) => {
  const { handleDec } = useContext(CounterContext);
  return <button onClick={handleDec}>{icon}</button>;
};

// add children as properties of parent
Counter.Count = Count;
Counter.Label = Label;
Counter.Increase = Increase;
Counter.Decrease = Decrease;
```

- This can now be used as follows:

```ts
return (
  <Counter>
    <Counter.Label>My Counter</Counter.Label>
    <Counter.Count />
    <Counter.Increase icon="+" />
    <Counter.Decrease icon="-" />
  </Counter>
);
```

- We can now freely change the order that the different children are displayed.
