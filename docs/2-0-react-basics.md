# React Basics

The three core concepts of React are:
1. components
2. props
3. state

Below, we will be covering the first, components, at a high level. We will explore what components are, the format of a component, and the contents of components, namely JSX.

## Components

### "What is a component?"

A component is a logical separation of concerns and code in terms of UI structure. If you've used frameworks like Angular before, this method of splitting your code should feel familiar.

For example, instead of keeping everything in a single file, you can move self-contained chunks into their own files.

```html
<body>
    <nav>
        ...
    </nav>
    <main>
        ...
    </main>
    <footer>
        ...
    </footer>
</body>
```
Converting the above to show what the template could like with components:
```html
<body>
    <Nav />
    <Main />
    <Footer />
</body>
```
This results in simpler components that are easier to test and read.

### "What is a REACT component?"

In React, components are defined by two things:
1. it is a function with a capital letter. e.g. Profile, Menu, Sidebar
2. it returns a single node of JSX.

Below is an example of a simple navigation React component:

```tsx
export default function Nav() {
    return (
        <nav>
            <a href="/">Home</a>
            <a href="/products">Products</a>
            <a href="/contact">Contact</a>
        </nav>
    )
}
```

`export default` denotes the function as the primary export of the file. To import and use the component would look like

```jsx
import Nav from './Nav.jsx'

export default function App() {
    return (
        <body>
            <Nav />
        </body>
    )
}
```


## JSX

React uses a special JavaScript extension called JSX for rendering HTML. What *looks* like HTML in React components is *actually* JSX. As such, your components template will always live directly next to the component logic, they're both technically JavaScript after all!

Keeping rendering logic tightly coupled to the template helps to keep things consistent and more easily visually represent a component through the code that makes it.

> .jsx files are JavaScript, and .tsx files are TypeScript.

```tsx
export default function Profile({user}: {user: {name: string, email: string}}) {
    if (!user) {
        return <a href="/login">Login</a>
    }
    return (
        <p>
            {user.name} <small>{user.email}</small>
        </p>
    )
}
```

In the above example, we see a very clear indication of when the UI will reder different states. If there is no user, the JSX for a login link is returned. If there is a user, then the component will display its default view, the user's name and email.
This guide will refer to JSX as a catch-all for both JSX and TSX.

### Classes & Styles

While it looks very similar or almost exactly like HTML markup, JSX has some key differences. One of the biggest you will encounter is the changes to styling your markup.

In HTML, you add styles to an element in a number of ways, but most typically through inline styles and classes...

```html
<button class="blue-background round-edges">
    Classes
</button>

<button style="background: blue; border-radius: 5px;">
    Inline Styles
</button>
```

...but in JSX, you use `className` to denote classes, and an *object* for style...

```jsx
<button className="blue-background round-edges">
    Classes
</button>

<button style={{background: 'blue', borderRadius: '5px'}}>
    Inline Styles
</button>
```

The `style` object is a collection of the *camelCase* css properties, with the value as a string or number.

- `background-color` => `backgroundColor`
- `font-size` => `fontSize`
- `padding-left` => `paddingLeft`

### Events

Events in React such as onclick, onmouseenter, etc, are accessed basically the same, but these are also camelCase.

- `onclick` => `onClick`
- `onkeyup` => `onKeyUp`
- `onmouseenter` => `onMouseEnter`

You can handle these events inline with an arrow function:

```jsx
<button onClick={() => handle("button clicked")}>
    Click Me
</button>
```
Or with a regular function:

```jsx
function clickHandler() {
    console.log('button clicked')
}

return (<button onClick={clickHandler}>
    Click Me
</button>)
```

### Iterating
A common situation is needing to display a list of data.
To do this in JSX, you need to map the list of data to their corresponding JSX elements.

```jsx
export function UserList() {
  const users = ['Austin', 'Danish', 'Aravindh', 'Michael', 'Emmanuel', 'Favor']
  return (
      <ul>
        {users.map(name => {
            return <li key={name}>{name}</li>
        })}
      </ul>
  )
}
```

`key` is important because React uses it to track which elements to update. As such, every `key` must be unique.


The above is a very quick overview of the first few tools you'll need to build your first React app.