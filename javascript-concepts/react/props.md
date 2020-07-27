## Props

props is how compenents get thier properties. every child component gets its props from the parent. a component either holds data (has state) or recieves data through its props

### functional component

- must pass a `props` argument
```javascript
const BlogPostExcerpt = props => {
    return (
        <div>
            <h1>{props.title}</h1>
            <p>{props.description}</p>
        </div>
    )
}
```

### class component

- props are passed by default & are accessible via `this.props`
```javascript
import React, { Component } from 'react'

class BlogPostExcerpt extends Component {
    render() {
        return (
            <div>
                <h1>{this.props.title}</h1>
                <p>{this.props.description}</p>
            </div>
        )
    }
}
```

### prop types and default values

```javascript
BlogPostExcerpt.propTypes = {
    title: PropTypes.string,
    description: PropTypes.string
}

BlogPostExcerpt.defaultProps = {
    title: '',
    description: ''
}
```

### passing props

- similar to passing HTML attributes
```javascript
const desc = 'a simple description'
// ...
<BlogPostExcerpt title="My Post" description={desc} />
```

### children

a special prop is `children`. that contains the value of anything that is passed in the __body__ of the component. example:

```javascript
<BlogPostExcerpt title="My Post" description={desc} >
    Something
</BlogPostExcerpt>
```

in this case, inside of `BlogPostExcerpt` we could access "Something" by looking up `this.props.children`

### presentational vs. container components

react components are often divided into two buckets: __presentational__ & __container__

__presentational components__ are mostly concerned with generating some markup to be outputted. they do _not_ manage any kind of state (except for state related to the presentation).

__container components__ are mostly concerned with the "backend" operations. they might handle the state of various sub-components or they might wrap several presentational components or they might interface with Redux. 

- presentational = the look
- container = making things work

```javascript
/// presentational
const Users = props => (
    <ul>
        {props.users.map(user => (
            <li>{user}</li>
        ))}
    </ul>
)
```

```javascript
/// container
class UserContainer exends React.Component {
    constuctor() {
        this.state = {
            users: []
        }
    }

    componentDidMount() {
        axios.get('/users').then(users => this.setState({ users: users}))
    }

    render() {
        return <Users users={this.state.users} />
    }
}
```
