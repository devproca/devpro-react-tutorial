## Part 3.3: Handling the form submission

If you skipped part 3.2, or had any issues with it, you can use the following code as a base for this part of the exercise:

```tsx
function Form() {
  const [value, setValue] = React.useState("");

  function handleSubmit(event) {
    event.preventDefault();
    console.log(value);
  }

  return (
    <form onSubmit={handleSubmit}>
      <label>
        What do you need to do?
        <input
          type="text"
          value={value}
          onChange={(event) => setValue(event.target.value)}
        />
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
  const [todos, setTodos] = React.useState([
    { id: 1, title: "Buy milk" },
    { id: 2, title: "Buy eggs" },
    { id: 3, title: "Buy bread" },
    { id: 4, title: "Go to the gym" },
  ]);

  function addTodoItem(title) {
    setTodos([...todos, { id: todos.length + 1, title }]);
  }

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

Just like regular data, functions can be passed as props to child components. We will be passing the `addTodoItem` function to the `Form` component, so that it can add new todo items to the list.

Update the `Form` component to call the `addTodoItem` function when the form is submitted.

When you're ready, switch to [4 Hooks](./3-3-form-submission.md) to learn how to pass data between components.
