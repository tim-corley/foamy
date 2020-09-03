## Render Props

[Code Sandbox](https://codesandbox.io/s/render-props-6w6kq?)

[Code Sandbox](https://codesandbox.io/s/render-props02-66bsr)

- https://github.com/gopinav/React-Tutorials/tree/master/React%20Fundamentals/advanced-guide-demo/src/components
- https://www.youtube.com/watch?v=EZil2OTyB4w

a technique for **sharing code** between react components by using a **prop whose value is a function**

**NOTE:** hooks is now a better approach to share code amongst components (see: https://www.youtube.com/watch?v=35Xi8ssyfMk)

a common pattern used to share state between components is to use the `children` prop. inside of a component JSX you can render `{this.props.children}` which automatically injects any JSX passed in the parent component as a children:

```javascript
class Parent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      user: "tester",
      loggedIn: false,
    };
  }

  render() {
    return <div>{this.props.children}</div>;
  }
}

const Children01 = () => {};

const Children02 = () => {};

const App = () => (
  <Parent>
    <Children01 />
    <Children02 />
  </Parent>
);
```

however, there is a problem here: the state of the parent component cannot be accessed from the children. to be able to share state, you need to use a render prop component and, instead of passing components as children of the parent component, you pass a function which you then execute in `{this.props.children()}`. the function can accept arguments.

```javascript
// App.js
import React from "react";
import { Parent, Children01, Children02 } from "./Render";
import "./styles.css";

const App = () => (
  <Parent
    newprop01={(user) => <Children01 user={user} />}
    newprop02={(count) => <Children02 count={count} />}
  />
);

export default App;

// Render.js
import React from "react";

class Parent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      user: "tester",
      count: 3,
    };
  }

  render() {
    return (
      <div>
        <p>TEST</p>
        {this.props.newprop01(this.state.user)}
        {this.props.newprop02(this.state.count)}
      </div>
    );
  }
}

const Children01 = (props) => {
  return <p>{props.user}</p>;
};

const Children02 = (props) => {
  return <h1>{props.count}</h1>;
};

export { Parent, Children01, Children02 };
```
