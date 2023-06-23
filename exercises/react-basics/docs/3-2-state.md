## Part 3.2: Adding state to the ToDoList component

If you skipped part 3.1, or had any issues with it, you can use the following code as a base for this part of the exercise:

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

Now that we have added state to the `Form` component, we can add state to the `ToDoList` component. We will be modifying it to store the todo items in state, rather than in a static array.

We will also create a function that will add a new todo item to the list of todo items. We will pass this function to the `Form` component, so that it can add new todo items to the list.

When changing the state of an array, it is important to remember that you should never mutate the array directly. Instead, you should create a new array, and then set the state to the new array. This is because React uses a technique called [shallow comparison](https://reactjs.org/docs/shallow-compare.html) to determine if the state has changed. If you mutate the array directly, React will not detect the change, and will not re-render the component.

Question: When updating the state of an array, what would be considered the correct way to do it in the `addFruit` function below?

```tsx
function Fruits() {
  const [fruits, setFruits] = React.useState(["apple", "banana", "orange"]);

  function addFruit(fruit) {}
}
```

- [ ] `setFruits(fruits.push(fruit))`
- [ ] `setFruits([...fruits, fruit])`
- [ ] `fruits.push(fruit)`
- [ ] `fruits.concat(fruit)`

<details>
<summary>Answer</summary>

- [ ] `setFruits(fruits.push(fruit))`
- [x] `setFruits([...fruits, fruit])`
- [ ] `fruits.push(fruit)`
- [ ] `fruits.concat(fruit)`

When updating the state of an array in React, it's important to create a new array instead of mutating the existing one directly. Option B uses the spread operator (...) to create a new array that includes all the elements from the existing fruits array and adds the new fruit to the end. By calling setFruits with the new array, React will properly detect the state change and trigger a re-render of the component

</details>

With this knowledge, add the todo list state and change handlers to the `ToDoList` component.

When you're ready, switch to [3-3 Form Submission](./3-3-form-submission.md) to learn how to pass data between components.
