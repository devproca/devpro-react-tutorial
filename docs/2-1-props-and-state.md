# Props & State

Reviewing, the three React core concepts are:
1. components
2. props
3. state

In this lesson we will be going over props & state.

## Props

We will start with a basic component:

```jsx
export default function Nav() {
    return (
        <nav>
            <a href="/">
            <a href="/about">
            <a href="/contact">
        </nav>
    )
}
```

Now, lets say theres an admin-only page that requires special permission, and we need to show that link to ONLY admins.
On top of this, we want to be able to change the title of the home page, rather than statically defining it as 'Home'.

```jsx
export default function Nav() {
    return (
        <nav>
            <a href="/">Home</a> // We want to be able to change this.
            <a href="/about">About</a>
            <a href="/contact">Contact</a>
            <a href="/settings">Settings</a> // Must be only visible to admins.
        </nav>
    )
}
```

We need to get some data into this component. Just like normal html elements with their attributes, React components behave similarly. You can pass data in via attributes. These are called <b>props</b>. Props are passed from the top of the component tree downwards. This is described as *one-way data flow*.

For our component, we need to pass a flag that tells the component if the current user is an admin or not.
We also want to pass in a new name for the home page.

```jsx
export default function Header() {
    return (
        <header>
            <Nav homePageTitle="Welcome!" userIsAdmin={true}>
        </header>
    )
}
```

As you can see above, just like you'd set the `src` attribute on an `<img>` element, you can set attributes on React components.

Now, we need to access these in the `Nav` component. Props are passed to React components as the <b>first</b> first function parameter.

```jsx
export default function Nav(props) {
    console.log(props) // {homePageTitle: 'Welcome!', userIsAdmin: false}
    // return (
    //     <nav>
    //         <a href="/">Home</a> // We want to be able to change this.
    //         <a href="/about">About</a>
    //         <a href="/contact">Contact</a>
    //         <a href="/settings">Settings</a> // Must be only visible to admins.
    //     </nav>
    // )
}
```

Using *destructuring*, we can easily pull the attributes we set out of the props parameter within the function definition.

```jsx
export default function Nav({homePageTitle, userIsAdmin}) {
    console.log(props) // {homePageTitle: 'Welcome!', userIsAdmin: true}
    // return (
    //     <nav>
    //         <a href="/">Home</a> // We want to be able to change this.
    //         <a href="/about">About</a>
    //         <a href="/contact">Contact</a>
    //         <a href="/settings">Settings</a> // Must be only visible to admins.
    //     </nav>
    // )
}
```

If using typescript, you can also type the props:

```tsx
export default function Nav(
    {homePageTitle, userIsAdmin}: {homePageTitle: string, userIsAdmin: boolean}
) {
    console.log(homePageTitle) // 'Welcome!'
    console.log(userIsAdmin) // true
    // return (
    //     <nav>
    //         <a href="/">Home</a> // We want to be able to change this.
    //         <a href="/about">About</a>
    //         <a href="/contact">Contact</a>
    //         <a href="/settings">Settings</a> // Must be only visible to admins.
    //     </nav>
    // )
}
```

Now, we can use these values in the returned JSX:

```tsx
export default function Nav(
    {homePageTitle, userIsAdmin}: {homePageTitle: string, userIsAdmin: boolean}
) {
    return (
        <nav>
            <a href="/">{homePageTitle}</a>
            <a href="/about">About</a>
            <a href="/contact">Contact</a>
            {userIsAdmin && <a href="/settings">Settings</a>}
        </nav>
    )
}
```

To then use the component within another component, you just import it, and pass the required props.

```tsx
// layout.tsx
import Nav from './components/Nav'

export default function RootLayout() {
  return (
    <html lang="en">
      <Nav homePageTitle='Home' userIsAdmin={false} />
      <body>{'...'}</body>
    </html>
  )
}
```


## State

State & event handlers are how you add interactivity to a component.
State is initialized and is stored within a component, while props are passed into a component. This is the main difference between the two.

Lets add a logout button to our nav. We want to change state when the button is clicked, so we can create a function and use the `onClick` event handler on the `<button>`.


```tsx
export default function Nav(
    {homePageTitle, userIsAdmin}: {homePageTitle: string, userIsAdmin: boolean}
) {
    function logoutClicked() {
        console.log('Logout clicked!')
    }

    return (
        <nav>
            <a href="/">{homePageTitle}</a>
            <a href="/about">About</a>
            <a href="/contact">Contact</a>
            {userIsAdmin && <a href="/settings">Settings</a>}

            <button onClick={logoutClicked}>Logout<button>
        </nav>
    )
}
```

Now that we are handling the interaction from a user, we can start dealing with the state of the component.
To get started with hooks, we will introduce a React function called `useState`.
`useState` is just one of multiple functions that React provides for adding additional features and logic to your components.

`useState()` returns an array with two values, and we will use *array destructuring* to extract these into variables in one line.

```tsx
import {useState} from 'react'

export default function Nav(
    {homePageTitle, userIsAdmin}: {homePageTitle: string, userIsAdmin: boolean}
) {

    const [isLoggedIn, setIsLoggedIn] = useState()
    // This is the same as:
    // 
    // const state = useState()
    // const isLoggedIn = state[0]
    // const setIsLoggedIn = state[1]

    function logoutClicked() {
        console.log('Logout clicked!')
    }

    return (
        <nav>
            <a href="/">{homePageTitle}</a>
            <a href="/about">About</a>
            <a href="/contact">Contact</a>
            {userIsAdmin && <a href="/settings">Settings</a>}

            <button onClick={logoutClicked}>Logout</button>
        </nav>
    )
}
```

`isLoggedIn` is how you access the current value of that piece of state.
`setIsLoggedIn` is a function that you use to change the value of `isLoggedIn`.
We can initialize this value by passing the initial value into the `setState` function.

```tsx
const [isLoggedIn, setIsLoggedIn] = useState(true)
console.log(isLoggedIn) // true
```

We can check if this initial value is working by logging it in our `logoutClicked` function:

```tsx
function logoutClicked() {
    console.log('Logout clicked!')
    console.log(isLoggedIn)
}
```


Finally, we can use the `setIsLoggedIn` function within the click handler to change the state.

```tsx
function logoutClicked() {
    setIsLoggedIn(false)
}
```

Now we can use the value of `isLoggedIn` to change the UI:

```tsx
import {useState} from 'react'

export default function Nav(
    {homePageTitle, userIsAdmin}: {homePageTitle: string, userIsAdmin: boolean}
) {

    const [isLoggedIn, setIsLoggedIn] = useState(true)
    
    function logoutClicked() {
        setIsLoggedIn(false)
    }

    if (isLoggedIn) {
        return (
            <nav>
                <a href="/">{homePageTitle}</a>
                <a href="/about">About</a>
                <a href="/contact">Contact</a>
                {userIsAdmin && <a href="/settings">Settings</a>}

                <button onClick={logoutClicked}>Logout</button>
            </nav>
        )
    } else {
        return <p>Please Login!</p>
    }
}
```

With that, we now have user interraction that can change the state of a component, and props that also change the UI.