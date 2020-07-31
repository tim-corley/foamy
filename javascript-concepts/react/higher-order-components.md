## Higher Order Components

[Code Sandbox](https://codesandbox.io/s/higher-order-comps-4xcsd?)

[Code Sandbox](https://codesandbox.io/s/hoc02-j6ujr?)

- https://github.com/gopinav/React-Tutorials/tree/master/React%20Fundamentals/advanced-guide-demo/src/components
- https://www.youtube.com/watch?v=rsBQj6X7UK8

References:

- https://levelup.gitconnected.com/understanding-react-higher-order-components-by-example-95e8c47c8006
- https://www.youtube.com/watch?v=hKvV0euP3mY

use to "super charge" a component by add / modifying props or use to share functionality across components

when a component accepts a component as input and returns a component as its output

allows for code that is composable, reusable, and more encapsulated. can use a HOC to add methods or proporties to the state of a component. could use HOC to enhance existng component, operate on the state or props, or alter its rendered markup.

there is a convention of prepending a HOC with the `with` string - so if there is a `Button` component, its HOC counterpart should be `withButton`

simplest example of a HOC is one that simply returns the component unaltered

```javascript
const withElement = Element => () => &lt;Element />
```

to make more useful, add a property to the button (in addition to all the other props it came with)

```javascript
const withColor = (Element) => (props) => <Element {...props} color="red" />;
```

then use the HOC in a component jsx

```javascript
const Button = () => {
  return <button>test</button>;
};

const ColorButton = withColor(Button);
```

and render the ColorButton component to the app jsx

```javascript
function App() {
  return (
    <div className="App">
      <h1>Hello</h1>
      <ColorButton />
    </div>
  );
}
```

### example

```javascript
// App.js
import React from "react";
import ClickCounter from "./comps/ClickCounter";
import HoverCounter from "./comps/HoverCounter";
import "./styles.css";

export default function App() {
  return (
    <div className="App">
      <h1>Welcome!</h1>
      <ClickCounter demoProp="Demo String" />
      <HoverCounter />
    </div>
  );
}

// comps/ClickCounter.js
import React, { Component } from "react";
import withCounter from "./withCounter";

class ClickCounter extends Component {
  render() {
    const { count, incrementCount } = this.props;
    return (
      <button onClick={incrementCount}>
        {" "}
        {this.props.demoProp} CLICK COUNT: {count}
      </button>
    );
  }
}

export default withCounter(ClickCounter, 3);

// comps/HoverCounter.js
import React, { Component } from "react";
import withCounter from "./withCounter";

class HoverCounter extends Component {
  render() {
    const { count, incrementCount } = this.props;
    return <h3 onMouseOver={incrementCount}> HOVER COUNT: {count}</h3>;
  }
}

export default withCounter(HoverCounter, 5);

// comps/withCounter.js
import React from "react";

const withCounter = (WrappedComponent, incrementNum) => {
  class withCounter extends React.Component {
    constructor(props) {
      super(props);
      this.state = {
        count: 0,
      };
    }

    incrementCount = () => {
      this.setState((prevState) => {
        return { count: prevState.count + incrementNum };
      });
    };

    render() {
      return (
        <WrappedComponent
          count={this.state.count}
          incrementCount={this.incrementCount}
          {...this.props}
        />
      );
    }
  }
  return withCounter;
};

export default withCounter;
```
