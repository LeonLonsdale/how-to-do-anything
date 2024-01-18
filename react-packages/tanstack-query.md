## How to - Create the Cache / Client

- Import `QueryClient()`
- Use this to create a new query client / cache and store the output.
- Pass in any default options

```ts
import { queryClient } from '@tanstack/react-query';

const queryClient = new QueryClient({
    defaultOptions: {
        queries: {
            staleTime: 1000 * 60; // 1 minute
        }
    }
})
```

## How to - provide our query data to the app

- Import `QueryClientProvider`
- Wrap the appropriate parts of the app in this component
- Pass our queryClient in as a client prop.

```ts
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";

const App = () => {
  // logic
  return (
    <QueryClientProvider client={queryClient}>
      // app / child components
    </QueryClientProvider>
  );
};
```

## How to - Fetch data

- Import the `useQuery` hook
- Use the hook to request the data and store the output.
- When calling the hook, we pass in an object.
- The object should contain:
  - `queryKey` : used to identify cache entries. Pass in as an array
  - `queryFunction` : A function that returns a promise, such as fetch
- The data returned will also be stored in the cache.
- This returns an object of properties, which includes:
  - Loading state (isLoading)
  - Our data (data)
  - Any errors (error)

```ts
import { useQuery } from "@tanstack/react-query";

const {
  data,
  isLoading,
  error,
} = () => {
  const data = useQuery({
    queryKey: ["UniqueIdentifier"],
    queryFn: fetch(), // or custom func
  });
};
```

## How to - Mutate data

- Import `useMutation` and `useQueryClient` hooks.
- Get a copy of / gain access to the queryClient
- Call the `useMutation` hook and pass in an object containing:
  - a mutation function
  - a success function which will invalidate the cache and cause a reload. Pass in the unique cache key for the data to be revalidated
- Deconstruct and store the neccessary outputs.
- One of the outputs is a `mutate` function, which we can use as an event handler.

```ts
import { useMutation, useQueryClient } from "@tanstack/react-query";

const MyComponent = () => {
  const queryClient = useQueryClient();

  const { mutate, isLoading } = useMutation({
    mutationFn: () => {},
    onSuccess: () => {
      queryClient.invalidateQueries({
        queryKey: ["UniqueIdentifier"],
      });
    },
  });
};
```

## How to - handle errors

- Both the useQuery and useMutation object arguments accept an error handling function under the key `onError`

```ts
// useQuery

const SomeComponent = () => {
  const data = useQuery({
    queryKey: ["UniqueIdentifier"],
    queryFn: fetch(), // or custom func
    onError: (error) => {},
  });
};

// useMutation
const { mutate, isLoading } = useMutation({
  mutationFn: () => {},
  onSuccess: () => {},
  onError: (error) => {},
});
```
