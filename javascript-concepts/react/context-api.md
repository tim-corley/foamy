## Context API

[Code Sandbox](https://codesandbox.io/s/context-emwfh)
[Code Sandbox](https://codesandbox.io/s/context-02-q29r9)

__Demo App__: javascript-concepts/React/context-api-app
* trying out [nano-react-app](https://github.com/nano-react-app/nano-react-app)
```bash
➜  React git:(master) npx nano-react-app context-api-app
npx: installed 130 in 6.137s
  NANO REACT APP  
  Creating directory... DONE
  Downloading template project... DONE

  SUCCESS!  

  Created project context-api-app at /home/tim/GitHub/tim-corley/javascript-concepts/React/context-api-app
  Navigate to that directory and run the following commands:

    1. npm install or yarn to install dependencies

    2. npm start or yarn start to start developing

  Enjoy!

➜  React git:(master) ✗ cd context-api-app 
➜  context-api-app git:(master) ✗ npm install
```

the Context API is used to pass state across the app without having to use props. when an app grows to more than a few levels of components, this helps reduce complexity.

start by creating a new context (returns a Context object):

```javascript
const { Provider, Consumer } = React.createContext()
```

then create a wrapper component that returns a __Provider__ component and add, as children, all the components from which you want access to context

```javascript
class Container extends React.Component {
    constructor(props) {
        super(props)
        this.state = {
            something: "hey"
        }
    }

    render() {
        return (
            <Provider value={{ state: this.state }}>{this.props.children}</Provider>
        )
    }
}

class HelloWorld extends React.Component {
    render() {
        return (
            <Container>
                <Button />
            </Container>
        )
    }
}
```

inside a component that is wrapped in a Provider, you can use a __Consumer__ component to make use of the context

```javascript
class Button extends React.Component {
    render() {
        return (
            <Consumer>
                {context => <button>{context.state.something}</button>}
            </Consumer>
        )
    }
}
```

