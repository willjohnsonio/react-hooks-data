# Fetch Data with the React Hooks

## What do need to know?
* Familiar with React and function components
* Familiar with JavaScript features such as template literals, fetch API, object and array destructuring.


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
