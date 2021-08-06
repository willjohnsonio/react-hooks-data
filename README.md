# Fetch Data with the React Hooks

## What do need to know?
* Familiar with React, JSX, and props and function components
* Familiar with JavaScript features such as template literals, fetch API, modules, object and array destructuring.

## What are React Hooks?

Hooks are unique features you can add to or "hook" into functional React components to add new features. You can think of React components like LEGO blocks. Individual LEGOs by themselves aren't that useful, but when you connect them together, you can build a house, a car, or whatever you like. React components are similar, a button or a like icon may not be useful on its own, but you can have a tweet composer or a user profile page when you connect components together.

Hooks are like the wheels or windows that come with LEGO sets. Every piece you build doesn't need wheels or windows, and every React component doesn't need the features that Hooks add for you. There are [several Hooks](https://reactjs.org/docs/hooks-reference.html) in React, this blog post will cover the [useState](https://reactjs.org/docs/hooks-state.html) and [useEffect](https://reactjs.org/docs/hooks-effect.html) Hooks.
 
## What are you building?

You'll be adding the `useState` and `useEffect` Hooks to two React components to get data from the GitHub API. You have an input that the user will type in their GitHub username and press the submit button. Once the data is submitted and returned, the users name and avatar will display on the page under the submit button.

You'll be working in the `app.js` file. It will have a `GitHubUser` component and an `App` component. Usually, components are kept in separate files. To keep it simple today you'll put both components inside of `app.js.`

**app.js**
```jsx
function GitHubUser() {

  return "";
}

export default function App() {
  return (
    <div className="container">
      <div className="App">
        <form>
          <h1>Enter Your GitHub Username</h1>
          <input />
          <button type="submit" className="button">
            Submit
          </button>
        </form>
        <GitHubUser />
      </div>
    </div>
  );
}
```

In `app.js`: 

* there's a `GitHubUser` function component that returns an empty string, so nothing displays on the page when it loads. 
* An `App` component also returns a `form` that includes the `h1`, `input`, and`button` elements. 
* The `<GitHubUser>` component below the `form`. 
* Everything is wrapped in two divs with the class names `container` and `app`.

## Add useState Hook
The first hook you'll add is useState. To oversimplify what state is, it's what your application looks like at any given time. State can change depending on the users' actions. For example, if you remove the wheels from a LEGO car, it's no longer a car the *state* changed because you made a change and removed the wheels. Right now, your app has no state. Nothing can be changed. 

> **Note:** Dive deeper into state with [this article](https://daveceddia.com/visual-guide-to-state-in-react/) from Dave Ceddia.

To add state and make changes, you need to bring `useState` into the application. You import `useState` from `react` at the top of `app.js`.

**app.js**
```jsx
import { useState } from 'react';
```
This lets you dig into your React LEGO bag and pull out the "wheels" so you can add them to the `App` component. `useState` is a function that returns two values a state variable that stores the state and a function that changes it. Next, add useState to the `App` component and go over what is happening after.

**app.js**
```diff
export default function App() {
+   const [user, setUser] = useState("");
  return (
    <div className="container">
      <div className="App">
        <form>
          <h1>Enter Your GitHub Username</h1>
          <input />
          <button type="submit" className="button">
            Submit
          </button>
        </form>
        <GitHubUser />
      </div>
    </div>
  );
}
```
**What did you just do?**

* Used array destructuring to pull out the state variable and the state changing function from the return of the `useState()` function.
* Declared the state variable as `user` (you can name this anything you like).
* Named the state changing function `setUser` (you can name this anything). It's common practice to use `set` then the same name as your state variable.
* Set the initial value of the `user` state variable to an empty string by passing `""` as an argument to the `useState()` function.

Now that you add state to the `App` component, you'll create a function that changes the state variable based on the user input. Create a `handleSubmit` that calls the `setUser()` function.

**app.js**
```jsx
export default function App() {
  const [user, setUser] = useState("");

  function handleSubmit(event) {
    event.preventDefault();
   setUser(event.target.elements.user.value);
  }
```
In the `handleSubmit` function:

* You passed in the `event` you want the function to handle. In this case, it's a button submit.
* Added `event.preventDefault()` to stop the default submit behavior of the browser and let React handle it with its synthetic event system.
* Passed the `setUser()` function the value we want to change the `user` state variable to. Which will be what's typed into the input element with the id of `user`, which we will set later.

> **Note:** Learn more about event.preventDefault() by reading [this article](https://www.robinwieruch.de/react-preventdefault) by Robin Wierch


Next, make changes to the return of the `App` component. On the `<form>` element, add the `onSubmit` event handler and call your `handleSubmit` function inside JSX. Set the `id` of the input to `user`. That makes it so that what is typed into the input field is linked to the `user` state variable. 

**app.js**
```jsx
   return (
    <div className="container">
      <div className="App">
         <form onSubmit={handleSubmit}>
          <h1>Enter Your GitHub Username</h1>
           <input id="user" />
          <button type="submit" className="button">
            Submit
          </button>
        </form>
        <GitHubUser />
      </div>
    </div>
  );
}
```

The last thing to do inside the `App` component is to pass `user` as props to the `<GitHubUser />` component. 

**app.js**
```diff
-  <GitHubUser />
+  <GitHubUser user={user} />
```

**What did you just do?**

* Created a prop attribute called `user`.
* Assign it to the `user` state variable. That value changes when the `onSubmit` event is fired. 
* Remember that `onSubmit` calls the `handleSubmit()` function you created earlier.

Now, you have a form that takes users' input. When the user clicks the submit button, the state variable `user` changes to what the user typed in. Then you take what's stored inside `user` and pass it or give it to the `GitHubUser` component.

## Add useEffectHook
