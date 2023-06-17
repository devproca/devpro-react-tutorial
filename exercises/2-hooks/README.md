# Hooks: Fetching Data and Custom Hooks

In this exercise, you will learn how to fetch data from an API using React Hooks.
You will also learn how to create your own custom hooks, which are a great way to share logic between components.

We are familiar with `useState`, which is also a hook, but there are many more hooks that we can use to make our code more concise and easier to read. We will be covering `useEffect` and custom hooks in this exercise.

> Note: This exercise builds on [Exercise 1](../1-react-basics/README.md)'s ToDoList component. If you have not completed that exercise, you should do so before continuing. However, the completed code from Exercise 1 is provided in the `index.html` file.

# Part 1: Fetching Data with the useEffect Hook

The `React.useEffect` hook is a great way to fetch data from an API. It is also a great way to introduce bugs into your application if you are not careful.

The `useEffect` hook is a function that takes two arguments: a function and an array of dependencies. The function is called every time the component is rendered. The array of dependencies is used to determine if the function should be called again.

<details>
  <summary>useEffect Examples</summary>

For example, if you want to fetch data from an API when the component is rendered, you can do something like this:

```tsx
function MyComponent() {
  const [data, setData] = React.useState(null);

  React.useEffect(() => {
    fetch("https://api.example.com/data")
      .then((response) => response.json())
      .then((data) => setData(data));
  }, []);

  return (
    <div>
      {data ? <pre>{JSON.stringify(data, null, 2)}</pre> : "Loading..."}
    </div>
  );
}
```

In this example, the `useEffect` hook is called every time the component is rendered. The `fetch` function is called, and the data is set in state. The second argument to the `useEffect` hook is an empty array, which means that the function will only be called once.

If you want to refetch the data when a dependency changes, you can add that dependency to the array:

```tsx
function MyComponent() {
  const [data, setData] = React.useState(null);
  const [id, setId] = React.useState(1);

  React.useEffect(() => {
    fetch(`https://api.example.com/data/${id}`)
      .then((response) => response.json())
      .then((data) => setData(data));
  }, [id]);

  return (
    <div>
      <input value={id} onChange={(e) => setId(e.target.value)} />
      {data ? <pre>{JSON.stringify(data, null, 2)}</pre> : "Loading..."}
    </div>
  );
}
```

In this example, the `useEffect` hook is called every time the component is rendered. The `fetch` function is called, and the data is set in state. The second argument to the `useEffect` hook is an array containing the `id` state variable. This means that the function will be called every time the `id` state variable changes.

</details>

We will be adding the `useEffect` funtion to our `ToDoList` component to fetch data from an API.

We will be using the [JSONPlaceholder](https://jsonplaceholder.typicode.com/) API to fetch data. This API provides a fake REST API for testing and prototyping.
Specifically, we will be using the [Todos](https://jsonplaceholder.typicode.com/todos) endpoint to fetch a list of todos.

Each todo has the following shape:

```json
{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}
```

Use the browsers `fetch` API to fetch the todos from the API, and update the state. You can use the `fetch` API like this:

```tsx
fetch("https://some-api.com/data").then((response) => response.json()); // parse the response as JSON
```

This is the function you will be modifying:

```tsx
function ToDoList() {
  // Since we are fetching data from an API, we don't need to initialize the state with any data.
  const [todos, setTodos] = React.useState([
    { id: 1, text: "Buy milk" },
    { id: 2, text: "Buy eggs" },
    { id: 3, text: "Buy bread" },
    { id: 4, text: "Go to the gym" },
  ]);

  // add the useEffect hook here

  function addTodoItem(text) {
    setTodos([...todos, { id: todos.length + 1, text }]);
  }

  return (
    <div>
      <Form addTodoItem={addTodoItem}></Form>
      <List todos={todos}></List>
    </div>
  );
}
```

When you're ready, switch to the `2-hooks-part-2` branch to continue.

# Part 2: Creating a custom `useToDos` hook

If you skipped part one, or had any issues with it, you can use the following code and update the `ToDoList` component in the `index.html` file:

```tsx
function ToDoList() {
  const [todos, setTodos] = React.useState([]);

  React.useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/todos")
      .then((response) => response.json())
      .then((data) => setTodos(data));
  }, []);

  function addTodoItem(title) {
    setTodos([...todos, { id: todos.length + 1, title }]);
  }

  return (
    <div>
      <Form addTodoItem={addTodoItem}></Form>
      <List todos={todos}></List>
    </div>
  );
}
```

In this part, you will be creating a custom hook to fetch data from the API. This will allow you to reuse the logic in other components.

It is important to note that hooks are just functions. You can create your own custom hooks by creating a function that calls other hooks. They do not share state, so you can use them in multiple components.

Hooks _must_ start with the word `use`. This is how React knows that it is a hook. You can name your custom hooks anything you want, as long as they start with the word `use`, just like components must start with a capital letter.

For example, lets create a custom hook that monitors the window network status:

```tsx
function useNetworkStatus() {
  const [isOnline, setIsOnline] = React.useState(navigator.onLine);

  React.useEffect(() => {
    function handleOnline() {
      setIsOnline(true);
    }

    function handleOffline() {
      setIsOnline(false);
    }

    window.addEventListener("online", handleOnline);
    window.addEventListener("offline", handleOffline);

    return () => {
      window.removeEventListener("online", handleOnline);
      window.removeEventListener("offline", handleOffline);
    };
  }, []);

  return isOnline;
}
```

This hook uses the `useEffect` hook to add event listeners to the `window` object. It returns the current network status.

You can use this hook in your components like this:

```tsx
function MyComponent() {
  const isOnline = useNetworkStatus();

  return <div>{isOnline ? "Online" : "Offline"}</div>;
}
```

It can be used in any component, completely independent of other calls to the hook.

with this knowledge, lets create a custom hook that uses the `useEffect` hook to fetch data from the API, and return the todos and setTodos function.

We will be updating the following code:

```tsx
function useToDos() {
  // write your hook here
  return [todos, setTodos];
}

function ToDoList() {
  const [todos, setTodos] = useToDos();

  function addTodoItem(title) {
    setTodos([...todos, { id: todos.length + 1, title }]);
  }

  return (
    <div>
      <Form addTodoItem={addTodoItem}></Form>
      <List todos={todos}></List>
    </div>
  );
}
```

When you're ready, switch to the `2-hooks-complete` branch to continue.

# Review

The finished code for this exercise can be found in the `index.html` file.

In this exercise, we have learned how to:

- Use the `useState` hook to manage state in a functional component
- Use the `useEffect` hook to perform side effects in a functional component
- Create a custom hook to make the logic reusable

#### Examples

<details>
<summary>Example: A custom hook to handle authentication headers on fetch requests</summary>

```tsx
function useAPI(url) {
  const [data, setData] = React.useState(null);
  React.useEffect(() => {
    fetch(url, {
      headers: {
        Authorization: `Bearer ${localStorage.getItem("token")}`,
      },
    })
      .then((response) => response.json())
      .then((data) => setData(data));
  }, [url]);

  return data;
}

function useUser() {
  return useAPI("https://some-private-api.com/user");
}

function MyComponent() {
  const user = useUser();
  if (user) {
    return <p>{user.name}</p>;
  } else {
    return <p>Loading...</p>;
  }
}
```

</details>

<details>
<summary>Example: A custom hook to handle user login status</summary>

```tsx
function useLoggedIn() {
  const [isLoggedIn, setIsLoggedIn] = React.useState(false);

  React.useEffect(() => {
    const token = localStorage.getItem("token");
    if (token) {
      setIsLoggedIn(true);
    }
  }, []);

  return isLoggedIn;
}
```

<details>
