## Forms

[Code Sandbox](https://codesandbox.io/s/forms-s2ybv)

there are __two__ main ways of handling forms in react which differ on a fundamental level: how data is managed
 - if the data is __handled by the DOM__, they are called __uncontrolled components__
 - if the data is __handled by the component__, they are called __controlled components__

controlled components are used most of the time. the component state is the single source of truth (rather than the DOM). the `onChange` attribute is used to track a controlled component's element state change. 

```javascript
import React from "react";

export default class MyForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = { username: "" };
    this.handleChange = this.handleChange.bind(this);
  }

  handleChange(e) {
    this.setState({ username: e.target.value });
  }

  render() {
    return (
      <form>
        Username:{" "}
        <input
          type="text"
          value={this.state.username}
          onChange={this.handleChange}
        />
      </form>
    );
  }
}
```

 - with `onSubmit`:
```javascript
import React from "react";

export default class Submit extends React.Component {
  constructor(props) {
    super(props);
    this.state = { username: "" };
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(e) {
    this.setState({ username: e.target.value });
  }

  handleSubmit(e) {
    alert(this.state.username);
    e.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        Username:{" "}
        <input
          type="text"
          value={this.state.username}
          onChange={this.handleChange}
        />
        <input type="submit" value="SUBMIT" />
      </form>
    );
  }
}
```
 - using the ref attribute:
```javascript
import React from "react";

export default class Ref extends React.Component {
  constructor(props) {
    super(props);
    this.curriculum = React.createRef();
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleSubmit(e) {
    alert(this.curriculum.current.files[0].name);
    e.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <input type="file" ref={this.curriculum} />
        <input type="submit" value="SUBMIT" />
      </form>
    );
  }
}
```



