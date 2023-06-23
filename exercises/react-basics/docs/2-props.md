# Part 2: Props

If you skipped part one, or had any issues with it, you can use the following code as a base for this part of the exercise:

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
function List() {
  return (
    <ol>
      <ListItem></ListItem>
      <ListItem></ListItem>
      <ListItem></ListItem>
      <ListItem></ListItem>
    </ol>
  );
}
function ListItem() {
  return <li>Buy milk</li>;
}
function ToDoList() {
  return (
    <div>
      <Form></Form>
      <h2>My ToDos:</h2>
      <List></List>
    </div>
  );
}

function Root() {
  return <ToDoList></ToDoList>;
}
```

Simply copy and paste the above code into the script tag of your `index.html` file, and you should be ready to go.

==========================================================

Now that we have our components, we can start to pass data between them. We can do this using props.

Props are passed to a component as an object. The object can contain any data you want to pass to the component. The component can then use that data to render itself.

Let's start by passing some data to our `ListItem` component. We will be passing the title of the todo item as a prop.

```tsx
function ListItem(props) {
  return <li>{props.title}</li>;
}
```

Remember, we can deconstruct the props object to make it easier to read:

```tsx
function ListItem({ title }) {
  return <li>{title}</li>;
}
```

Now that we are passing data to our `ListItem` component, we need to update the `List` component to pass the data to the `ListItem` component.

```tsx
function List() {
  return (
    <ol>
      <ListItem title="Buy milk"></ListItem>
      <ListItem title="Buy eggs"></ListItem>
      <ListItem title="Buy bread"></ListItem>
      <ListItem title="Go to the gym"></ListItem>
    </ol>
  );
}
```

Now, we can pass the data from the `List` component to the `ListItem` component. But this code is repetitive, and contains static data. We can improve this by using an array of todo items, and mapping over them to create the list items.

But where should that array of data live?

- [ ] In the `List` component
- [ ] In the `Root` component
- [ ] In the `ListItem` component
- [ ] In the `Form` component
- [ ] In the `ToDoList` component

<details>
<summary>Answer</summary>

- [ ] In the `List` component
- [ ] In the `Root` component
- [ ] In the `ListItem` component
- [ ] In the `Form` component
- [x] In the `ToDoList` component

The `ToDoList` component is the parent of both the `List` and `Form` components. It is the only component that has access to both the form data and the list data. Therefore, it is the best place to store the data.

</details>

Using this knowledge, update the `ToDoList` component to store the todo items in an array, and pass them to the `List` component, finally rendering them by mapping over the array. Remember, to map over an array, you need to pass a unique key to each item in the array, so include that as a part of your todo item data structure.

When you're ready, switch to [2 Props](./2-state.md) to learn about state.
