# Part 3: State

If you skipped part two, or had any issues with it, you can use the following code as a base for this part of the exercise:

```tsx
function Form() {
  return (
    <form>
      <label>
        What do you need to do?
        <input type="text" value="" />
      </label>
      <button>Add</button>
    </form>
  );
}
function List({ todos }) {
  return (
    <ol>
      {todos.map(({ id, title }) => (
        <ListItem key={id} title={title}></ListItem>
      ))}
    </ol>
  );
}
function ListItem({ title }) {
  return <li>{title}</li>;
}
function ToDoList() {
  const todos = [
    { id: 1, title: "Buy milk" },
    { id: 2, title: "Buy eggs" },
    { id: 3, title: "Buy bread" },
    { id: 4, title: "Go to the gym" },
  ];
  return (
    <div>
      <Form></Form>
      <List todos={todos}></List>
    </div>
  );
}

function Root() {
  return <ToDoList></ToDoList>;
}
```

Simply copy and paste the above code into the script tag of your `index.html` file, and you should be ready to go.

==========================================================

Now that we have our components, we can start to manage the state of our application. Remember, state is data that changes over time. In our application, the state is the todo items. We can add, remove, and update the todo items, and the state of our application will change.

We can manage the state of our application using the `React.useState` hook. The `useState` hook returns an array with two items in it.

## Part 3.1: Adding state to the Form component

Lets start by adding the `React.useState` hook to our `Form` component. We will use it to store the value of the input field, and also implement a handler that will log the value of the input field to the console when the form is submitted.

```tsx
function Form() {
  // add the React.useState hook here

  // pass the state to the value attribute of the input field
  // use the onChange event handler on the input field to update the state

  // add function handleSubmit(event) here

  // Note: the handleSubmit function will receive an event object as an argument. The default behavior of a form is to submit the form and refresh the page. We want to prevent this default behavior, so we need to call event.preventDefault() in our handleSubmit function.

  // add the handleSubmit function to the onSubmit event handler of the form

  return (
    <form>
      <label>
        What do you need to do?
        <input type="text" />
      </label>
      <button>Add</button>
    </form>
  );
}
```

When you're ready, switch to [3-2 State](./3-2-state.md) to learn how to pass data between components.
