## General Concepts

[Code Sandbox](https://codesandbox.io/s/general-fqjg6)

### single page applications (SPAs)

react applications are also called single page applications - meaning that the application code is only loaded once (as opposed to a new request being made to the server to deliver a new page / data)

### navigation

since SPAs get rid of the default browser navigation, URLs must be managed manually. this part of the application is called the __router__. in react it is common to use the [React Router](https://github.com/ReactTraining/react-router) library to do this (which leverages / interacts with the browser's History API).


### declaritive

react is considered a "declaritive approach to build UIs" - meaning that you can build web interfaces without ever touching the DOM directly and/or can have an entire system without having to interact with the actual DOM Events. 

### immutability 

an immutabile variable can never be changed. to update it's value, you create a new variable. for example, instead of changing an array to add a new item you actually create a whole new array by concatenating the old array plus the new item. similarly, an object is never updated - it is first copied then changes applied. 

in React, this applies in many places. for example, you should never mutate the `state` property directly but only through the `setState()` method. the advantages of leveraging immutability in React are namely __predictabilty__ and __performance__.

### purity

in JavaScript, when a function does not mutate objects but just returns a new object, it's called a _pure function_. a pure function does not cause side effects nor does it ever change the input that was passed. all functional components are pure components.

```javascript
const Button = props => {
    return <button>{props.message}</button>
}
```

### composition

allows you to build more complex functionality by combining small & focused functions. for example, using `map()` to create an new array from an existing set and then using `filter()` to filter results.

```javascript
const myList = ['Alpha', 'Bravo', 'Charlie']
// create new array with first characters and filter to items that are 'a'
myList.map(item => item[0]).filter(item => item === 'A')
```

react is all about creating small & lean components that are _composed_ to create more functionality ontop of them (whole is greater than the sum of its parts)

 - create specialized version of component:
  ```javascript
  const Button = props => {
      return <button>{props.text}</button>
  }

  const SubmitButton = () => {
      return <Button text="Submit" />
  }

  const LoginButton = () => {
      return <Button text="Login" />
  }
  ```

  ### passing methods as props

  a component can focus on tracking a click event (for example) and what actually happens when the click event happens is up to the container component 

  ```javascript
  const Button = props => {
      return <button onClick={props.onClickHandler}>{props.text}</button>
  }

  const AlertButton = props => {
      return <Button text="Trigger Alert" onClickHandler={props.onClickHandler} />
  }

  const Container = () => {
      const onClickHandler = () => {
          alert('Alert Button was Clicked!')
      }
      return <AlertButton onClickHandler={onClickHandler} />
  }
  ```


### using children

the `props.children` property allows you to inject components inside of other components

```javascript
const Sidebar = props => {
    return <aside>{props.children}</aside>
}

// then transparently embed more components into it
<Sidebar>
    <Link title="First Item" />
    <Link title="Second Item" />
</Sidebar>
```

when a component recieves a (child) component as a prop and returns a component, it is called a __higher order component__
 





