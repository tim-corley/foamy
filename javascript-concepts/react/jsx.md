## JSX

JSX is a technology that was introduced by React. Can use JSX syntax to declaritively write syntax of what a component UI should be. And not using strings here to descripe the UI but rather using JavaScript.

This is just JavaScript:
```javascript
const element = <h1>Hello, world!</h1>
```

Inside of a JSX expression, attributes can be easily inserted:
```javascript
const myId = 'test'
const newElement = <h1 id={myId}>Hello, world!</h1>
```

Make sure, within JSX, attributes are converted from using a dash (`-`) to using camelCase. Also, these two special cases because they are reserved keywords in JavaScript:
 - `class` --> `className`
 - `for` --> `htmlFor` 

Since __the render() function can only return a single node__, returning 2+ sibling components requires a parent wrapper - often a `div` but can be any tag.

```javascript
<div>
    <BlogPostList />
    <Sidebar />
</div>
```

### transpiling

A browser cannot execute JavaScript files containing JSX code - they must first be transoformed to regular JS. This is done via a process called __transpiling__.

 - these bits of code are equivalent:
> _vanilla js_
```javascript
ReactDOM.render(
    React.DOM.div(
        { id: 'test },
        React.DOM.h1(null, 'A Title'),
        React.DOM.p(null, 'a paragraph')
    ),
    document.getElementById('myApp')
)
```
> _jsx_
```javascript
ReactDOM.render(
    <div id="test">
        <h1>A Title</h1>
        <p>a paragraph</p>
    </div>,
    document.getElementById('myApp')
)
```
__Babel__ is a commong transpiling tool (used by `create-react-app`)

### js in jsx 

use `{}` to encapsulate javascript within jsx code

```javascript
const myParagraph = 'a simple paragraph.'
ReactDOM.render(
    <div id="test">
        <h1>A Title</h1>
        <p>{myParagraph}</p>
    </div>,
    document.getElementById('myApp')
)
```
 - nesting:
```javascript
const myParagraph = 'a simple paragraph.'
ReactDOM.render(
    <table>
        {rows.map((row, i) => {
            return <tr>{row.text}</tr>
        })}
    </table>,
    document.getElementById('myApp')
)
```

### html in jsx

jsx resembles HTML but it is actually XML syntax so there are a few quirks to be aware of.
 - all tags need to be closed, can use self-closing tags (`<br>` --> `<br />`)
 - camelCase is used (`onclick` --> `onClick`)
 - `class` --> `className`

### css in react
- inline styling - good for simple styling 

### forms in jsx




