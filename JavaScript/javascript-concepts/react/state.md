## State

[Code Sandbox](https://codesandbox.io/s/state-gknfv)

### setting default state (of a component)

 - class 
```javascript
import React, { Component } from "react";

class BlogPostExcerpt extends Component {
    constructor(props) {
        super(props)
        this.state = { clicked: false }
    }

    render() {
        return (
            <div>
                <h1>Title</h1>
                <p>is it selected? {this.state.clicked.toString()}</p>
            </div>
        )
    }
}
```
 - functional 
```javascript
import React, { useState } from "react";

const BlogPostExcerpt = () => {
    const [clicked, setClicked] = useState(false)

    return (
        <div>
            <h1>Title</h1>
            <p>is it selected? {clicked.toString()}</p>
        </div>
    )
}
```

### mutating state

a state should __never__ be mutated by using:
```javascript
this.state.clicked = true
```

instead, __always__ use `setState()` and pass it an object:
```javascript
this.setState({ clicked: true })
```

the object can contain a subset or superset of the state. only the properties you pass will be mutated and the ones omitted will be left in their current state

it is important to always use `setState()` because this method lets React know that the state was changed and this triggers a series of events that lead to the component being re-rendered (along with any DOM updates is needed)

beasue of __unidirectional data flow__, changing the state on a component will never affect it's parent or it's siblings - just it's children. this is why state is often moved up in the component tree

### moving the state up the tree

if two+ components need to share state, the state needs to be moved up to a common ancestor. the state - once hosted in a common ancestor - is passed down to the components that need that value via props.

```javascript
import React from "react"

export default class Converter extends React.Component {
    constructor(props) {
        super(props)
        this.state = { currency: '€' }
    }

    render() {
        return (
            <div>
                <Display currency={this.state.currency} />
                <CurrencySwitcher currency={this.state.currency} />
            </div>
        )
    }
}
```

the state can be mutated by a child component by passing a muating function down as a prop:

```javascript
import React from "react"

export default class Converter extends React.Component {
    constructor(props) {
        super(props)
        this.state = { currency: '€' }
    }

    handleChangeCurrency = event => {
        this.setState({ currency: this.state.currency === '€' ? '$' : '€'})
    }

    render() {
        return (
            <div>
                <Display currency={this.state.currency} />
                <CurrencySwitcher currency={this.state.currency} handleChangeCurrency={this.handleChangeCurrency} />
            </div>
        )
    }
}

const CurrencySwitcher = props => {
    return (
        <button onClick={props.handleChangeCurrency}>
            Currently using: {props.currency}. Click to change.
        </button>
    )
}

const Display = props => {
    return <p>The current currency being used is: {props.currency}.</p>
}
```