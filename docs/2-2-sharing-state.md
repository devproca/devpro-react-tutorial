# Sharing State Between Components


Sometimes you have two components that both need the same data, and it is important that the data is synchronized between both components. Implementing the same logic multiple times across different is a sure-fire way to run into bugs down the line.

To do this, state that is to be shared must be *lifted* to a level in the application where it can then be passed downwards into the components that require the data.

Lets say we have a todo-list application, and we have 3 components:
1. main todo app wraper
2. todo entry form
3. list displaying the todos

1. main todo app wrapper
```tsx
import {Form} './Form'
import {List} './List'

export default function ToDoList() {
    return (
        <Form></Form>
        <List></List>
    )
}
```

2. todo entry form
```tsx
import {useState} from 'react'

export default function Form() {

    const [value, setValue] = useState('');

    function handleSubmit(value) {
        // do something with the value
    }

    return (
        <input type="text" name="todo" value={value} onChange={(event) => setValue(event.target.value)}>
        <button onClick={handleSubmit}>Submit</button>
    )
}
```

3. todo list
```tsx
export default function ToDos() {

    const todos = [
        {id: 1, text: 'Go get groceries'},
        {id: 2, text: 'Go to the gym'},
        {id: 3, text: 'Go to the bank'},
        {id: 4, text: 'Do the dishes'},
    ]

    return (
        <ol>
            {todos.map({id, text} => <li key={id}>{text}</li>)
        </ol>
    )
}
```

Now, we want to be able to add a todo to the list. We need to be able to pass the value from the form to the list.
We can do this by lifting the state up to the parent component, and passing it down to the children as props.
We can also move the handler function up to the parent component, and pass it down to the form as a prop.

```tsx
import {Form} './Form'
import {List} './List'
import {useState} from 'react'

export default function ToDoList() {

    const [todos, setTodos] = useState([
        {id: 1, text: 'Go get groceries'},
        {id: 2, text: 'Go to the gym'},
        {id: 3, text: 'Go to the bank'},
        {id: 4, text: 'Do the dishes'},
    ])

    function handleSubmit(value) {
        setTodos([...todos, {id: todos.length + 1, text: value}])
    }

    return (
        <Form onSubmit={handleSubmit}></Form>
        <List todos={todos}></List>
    )
}
```

```tsx
import {useState} from 'react'

export default function Form({onSubmit}: {onSubmit: (value: string) => void}) {

    const [value, setValue] = useState('');

    return (
        <input type="text" name="todo" value={value} onChange={(event) => setValue(event.target.value)}>
        <button onClick={() => onSubmit(value)}>Submit</button>
    )
}
```

```tsx
export default function ToDos({todos}: {todos: {id: number, text: string}[]}) {
    return (
        <ol>
            {todos.map({id, text} => <li key={id}>{text}</li>)
        </ol>
    )
}
```

This is a very simple example, but the same concept can be applied to more complex situations.
Lifting state higher and higher up the component tree can be a pain, and can lead to prop drilling. 
There are solutions to this, which we will cover later.