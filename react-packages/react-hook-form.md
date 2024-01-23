## How to - Register your form elements

- Import and call `useForm` from react hook form.
- Deconstruct `register` from the return
- Call register within the element, using the JavaScript escape hatch, and pass in the name of the element.
- Calling `register` returns onChange, onBlur, name, and ref, so we spread the result as attributes.

```ts
import { useForm } from "react-hook-form";

const MyFormComponent = () => {
  const { register } = useForm();

  return (
    <form>
      <label htmlFor="name">Enter Name:</label>
      <input type="text" id="name" {...register("name")} />
    </form>
  );
};
```

## How to - Handle form submission

- Calling useForm also returns a `handleSubmit` funciton
- This accepts an object of the form data
- We can pass in a custom handler that returns this object after first handling validation.

```ts
import { useForm } from "react-hook-form";

const MyFormComponent = () => {
  const { register, handleSubmit } = useForm();

  const onSubmit = (data) => {};

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <label htmlFor="name">Enter Name:</label>
      <input type="text" id="name" {...register("name")} />
    </form>
  );
};
```

## How to - Reset form after submission

- useForm returns a reset function which we can call on

```ts
import { useForm } from "react-hook-form";

const MyFormComponent = () => {
  const { register, handleSubmit, reset } = useForm();

  const onSubmit = (data) => {
    // do something with data
    reset();
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <label htmlFor="name">Enter Name:</label>
      <input type="text" id="name" {...register("name")} />
    </form>
  );
};
```

## How to - Validate entries (client-side)

- We can pass in an object of validation options as a second argument when registering elements.
- With each validation, we can provide the error message if validation fails.
- We can gain access to other form field values by also deconstructing `getValues` from useForm.
  - values are returned in string format. Numbers will need converting.
- Support is provided for the typical html validators
- We can create custom validators using the `validate` property which should be a callback func.
  - As it returns true or false, we can short circuit with `||` to return an error message if false.
  - it gains access to the current value by default.

```ts
import { useForm } from "react-hook-form";

const MyFormComponent = () => {
  const { getValues, register, handleSubmit, reset } = useForm();

  const onSubmit = (data) => {
    // do something with data
    reset();
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <label htmlFor="name">Enter Name:</label>
      <input
        type="text"
        id="name"
        {...(register("name"),
        {
          required: "The name field is required",
        })}
      />
      <label htmlFor="price">Price:</label>
      <input
        type="text"
        id="price"
        {...(register("price"),
        {
          required: "The price field is required",
          min: { value: 1, message: "Price cannot be lower than 1" },
        })}
      />
      <label htmlFor="discount">Enter Name:</label>
      <input
        type="text"
        id="discount"
        {...(register("discount"),
        {
          required: "The name field is required",
          min: { value: 0, message: "The discount cannot be less than 0" },
          validate: (value) =>
            +getValues().price >= +value ||
            "Discount cannot be greater than the price",
        })}
      />
    </form>
  );
};
```

## How to - handle errors

- Deconstruct `formState: { errors }` from `useForm`.
- Any error message generated will be a property of this `errors` object.
- We can then use short circuiting to display the messages

```ts
const {
  formState: { errors },
  getValues,
  register,
  handleSubmit,
  reset,
} = useForm();

// in the jsx

{
  errors?.name && <p>{errors.name.message}</p>;
}
```

- The extracted `handleSubmit` func also accepts a second callback for errors
- We therefore create an onError func to pass in.

```ts
<form onSubmit={handleSubmit(onSubmit, onError)}>
```
