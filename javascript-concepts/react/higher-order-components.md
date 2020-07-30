## Higher Order Components 

[Code Sandbox](https://codesandbox.io/s/higher-order-comps-4xcsd?)

References:
 - https://levelup.gitconnected.com/understanding-react-higher-order-components-by-example-95e8c47c8006

when a component accepts a component as input and returns a component as its output

allows for code that is composable, reusable, and more encapsulated. can use a HOC to add methods or proporties to the state of a component. could use HOC to enhance existng component, operate on the state or props, or alter its rendered markup.

there is a convention of prepending a HOC with the `with` string - so if there is a `Button` component, its HOC counterpart should be `withButton`

simplest example of a HOC is one that simply returns the component unaltered

```javascript
const withElement = Element => () => &lt;Element />
```

to make more useful, add a property to the button (in addition to all the other props it came with)

```javascript
const withColor = Element => props => <Element {...props} color="red" />
```

then use the HOC in a component jsx

```javascript
const Button = () => {
    return <button>test</button>
}

const ColorButton = withColor(Button)
```

and render the ColorButton component to the app jsx
```javascript
function App() {
    return (
        <div className="App">
            <h1>Hello</h1>
            <ColorButton />
        </div>
    )
}
```