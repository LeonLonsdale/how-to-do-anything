# How to - reuse code with the Render Props Pattern

- This pattern gives complete control over what the component renders by passing in a func that describes what to render.
- Pass in a prop called `render`.
- We pass in a function that returns the element to be rendered
- Therefore, the component will look different depending on the render prop, and is reusable as a result.

```ts
// pass in the render function
<List
  title="Products"
  items={products}
  render={(product) => <ListItem key={productId} product={product} />}
/>;

// in the component
export const List = ({ title, items, render }) => {
  // logic
  render(
    <>
      <h1>{title}</h1>
      <ul>{items.map(render)}</ul>
    </>
  );
};
```
