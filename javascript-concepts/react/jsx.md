## JSX

[Code Sandbox](https://codesandbox.io/s/jsx-ulqbv)

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
- differences between regular css and css in jsx:
  - keys property names are camelCase
  - values are strings
  - seperate each tuple with a comma
- inline styling not good with:
  - media queries
  - animation
  - pseudo classes
  - pseudo elements 

### forms in jsx

the `value` attribute always holds the current value of the field

the `defaultValue` attribute holds the default value that was set when the field was created. also applies to the `textarea` field.

```javascript
// instead of:
<textarea>Some text here</textarea>
// use:
<textarea defaultValue={'Some text here'}/>
```
for `select` fields:
```javascript
// instead of:
<select>
    <option value="x" selected>
    ...
    </option>
</select>
// use:
<select defaultValue="x">
    <option value="x">...</option>
</select>
```

### onChange

by passing a function to the `onChange` attribute, you can subscribe to events on the form field. even works with:
 - `radio` 
 - `select`
 - `checkbox`
`onChange` also fires when typing a character into an `input` or `textarea`

### whitespace

need to explicitly add whitespace by adding a space expression
```javascript
<p>Something 
    {' '}needs
    {' '}space
</p>
```

### comments 
```javascript
<p>
    {/* a comment here */}
    {
        // another comment there
    }
</p>
```

### spread attributes

in JSX, a common operation is assigning values to attributes 

```javascript
// instead of doin it manually...
<div>
    <BlogPost title={data.title} date={data.date} />
</div>
// you can pass...
<div>
    <BlogPost {...data} />
</div>
```

here the properties of the `data` object will be used as attributes automatically thanks to the ES6 spread operator.

### looping

```javascript
// for loop
const elements = []
cosnt items = []

for (const [index, value] of elements.entries()) {
    items.push(<Element key={index}>)
}
```

```javascript
// for loop
const elements = ['alpha', 'bravo', 'charlie']
cosnt items = []

for (const [index, value] of elements.entries()) {
    items.push(<li key={index}>{value}</li>)
}

return (
    <div>
        {items}
    </div>
)
```

```javascript
// map 
const elements = ['alpha', 'bravo', 'charlie']
return (
    <ul>
        {elements.map((val, idx) => {
            return <li key={idx}>{val}</li>
        })}
    </ul>
)
```


