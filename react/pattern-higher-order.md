# How to - reuse code with Higher Order Component Pattern

- A higher order component is a component that takes in a component and returns an enhanced version of it.
- Conventionally, HoC are named prefixed with `with`.

```ts
// basic component that will be passed into a hoc
const List = ({ title, items }) => {
  return (
    <ul>
      {items.map((item) => (
        <ListItem key={item.id} item={item} />
      ))}
    </ul>
  );
};
```

- Now we can return a new List component that has the ability to toggle whether or not the passed component is displayed by adding a toggle button.
- With this pattern we could also perform logic on `props.items` should we wish, before passing the result to the wrapped component.

```ts
const withToggles = (WrappedComponent) => {
  return function List (props) {
    const [isOpen, setIsOpen] = useState();

    const handleToggle = () => {
      setIsOpen(cur => !cur)
    }
    return (
      <section>
        <heading><h2>{props.title}</h2></heading>
        <button onClick={handleToggle}>
          {isOpen ? <span>&or;</span> : <span>&and;</span>}
        </button>
        {isOpen ? <WrappedComponent {...props} items={props.items}}
      </section>
    )
  }
}
```

- Now store the outputted component

```ts
export default const ProductListWithToggles = withToggles(List)
```

- And then use our new component as normal

```ts
<ProductListWithToggles title="Product List" items={products} />
```
