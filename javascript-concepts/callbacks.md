## Callbacks

[Code Sandbox](https://codesandbox.io/s/callbacks-5ti3r)

you can't know when a user will click at button (or perform any range of actions - ex.: `onClick`, `onMouseOver`, `onChange`, or `onSubmit`) so, in JavaScript, you must define an __event handler__ for the click event.

```javascript
document.getElementById('button').addEventListener('click', () => {
    console.log('Button was clicked!')
})
```

this is the __callback__. a callback is a simple function that is passed as a value to another function and will only be executed when the event happens. a function that accepts another function as an argument is called a __higher order function__

a common callback usecase is to wrap all clinet code in a `load` event listener (on the window object) so that code is only run once the page is ready

```javascript
window.addEventListener('load', () => {
    // window is now loaded
    // execute some code...
})
```

### handling errors

implement __error-first callbacks__ - meaning that the first parameter in the callback function is the error object

```javascript
fs.readFile('/file.json', (err, data) => {
    if (err !== null) {
        //handle error
        console.log(err)
        return
    }

    // no errors, process data
    console.log(data)
})
```

### problem with callbacks 

can get quickly complicated due to amount of nesting

```javascript
window.addEventListener('load', () => {
    document.getElementById('button').addEventListener('click', () => {
        setTimeout(() => {
            items.forEach(item => {
                // do something
            })
        }, 2000);
    })
})
```

### alternatives 

in order to solve "callback hell" features where introduced that help with asynchronous code that do not involve using callbacks.

 - promises (ES6) [[promises.md]]
 - async/await (ES8) [[async-await.md]]