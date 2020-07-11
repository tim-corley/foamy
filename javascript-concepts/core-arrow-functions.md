## Arrow Functions 

[Code Sandox](https://codesandbox.io/s/arrow-functions-ihotb)

Enables creation of functions without using the `function` keyword

- old:
  ```javascript
  const myFunction = function() {
      //...
  }
  ```

- new:
  ```javascript
  const myFunction = () => {
      //...
  }
  ```

if the function body contains just a single statement, the brackets can be omitted and everything written on a single line 

```javascript
const myFunction = () => doSomething()
```

parameters can be passed

```javascript
const myFunction = (param01, param02) => doSomething(param01, param02)
```

no parentheses need if a single parameter is being passed 
```javascript
const myFunction = param => doSomething(param)
```

arrow functions are designed to encourage the use of small functions (due to it's simple syntax)

### implicit return

abilty to return value(s) without using the `return` keyword - only works with one-line statments in function body.

```javascript
const myFunction = () => 'foo'
myFunction() // 'foo'
```

```javascript
const myFunction = () => ({ value: 'foo' })
myFunction() // {value: 'foo'}
```

### using `this` in arrow functions

using a regular function to define a method of an object, `this` refers to the object. Example:

```javascript
const team = {
    name: 'Celtics',
    city: 'Boston',
    wins: 32,
    losses: 9,
    teamRecord: function() {
        return `The ${this.city} ${this.name} have a record of: ${this.wins} - ${this.losses}.`
    }
}

console.log(team.teamRecord()) 
```

using an arrow function like this will not work because the `this` scope is __inherited__ from the execution context. An arrow function does not _bind_ `this` at all - so it's value will be looked up in the call stack. Due to this, arrow functions are not suited as object methods.

- using arrow functions as object methods (with `this` keyword) won't work
  ```javascript
  const team = {
    name: 'Celtics',
    city: 'Boston',
    wins: 32,
    losses: 9,
    teamRecord: () => {
        return `The ${this.city} ${this.name} have a record of: ${this.wins} - ${this.losses}.`
    }
}

console.log(team.teamRecord()) // The undefined undefined have a...
  ```

nor can arrow functions be used as constructors - will raise a `TypeError`

when _dynamic context_ is not needed, use regular functions

also, DOM Event listeners set `this` to be the target element. so, if you rely on `this` in the event handler, must use a regaular function

```javascript
const link = document.querySelector('#link')
link.addEventListener('click', () => {
    // this === window
} )

const link = document.querySelector('#link')
link.addEventListener('click', function() {
    // this === link
})
```