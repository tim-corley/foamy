## Components

[Code Sandbox](https://codesandbox.io/s/components-j59zo)

A component is one isolated piece of interface. in React everything is a component. even plain HTML tags are components on thier own and they are added by default. these pieces are equivalent - one with jsx, one without - both inject `<h1>Hello World</h1>` into an element w/ id of `app`

```javascript
import React from 'react'
import ReactDOM from 'react-dom'

// jsx
ReactDOM.render(<h1>Hello World!</h1>, document.getElementById('app'))

// vanilla 
ReactDOM.render(
    React.DOM.h1(null, 'Hello World!'),
    document.getElementById('app')
)
```

### custom components

 - functional component
```javascript
const BlogPostExcerpt = () => {
    return (
        <div>
            <h1>Title</h1>
            <p>Description</p>
        </div>
    )
}
```

 - class component
```javascript
import React, { Component } from 'react'

class BlogPostExcerpt extends Component {
    render() {
        return (
            <div>
                <h1>Title</h1>
                <p>Description</p>
            </div>
        )
    }
}
```

up until recently, class components were the only way to define a component that had its own state and could access the lifecycle methods (so things could be done when component was first rendered, updated, or removed)

__React Hooks__ changed this - so now functional components are now much more powerful, having access to state & lifecycle