## Promises

[Code Sandbox](https://codesandbox.io/s/promises-51hpc)

#### References:
 - https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API

once a promise has been called, it will start a __pending state__. Meaning that the caller function continues the execution while it waits for the promise to do its own processing and give the caller function some feedback. 

at this point, the caller function waits for the promise to either return a __resolved state__ or a __rejected state__. Since JavaScript is _asynchronous_, the function continues its execution while the promise does it's work.

APIs such as Fetch use Promises

### creating a promise

The Promise API exposes a Promise constructor - intialized by using: `new Promise()`

```javascript
let done = true

const isItDoneYet = new Promise((resolve, reject) => {
    if (done) {
        const workDone = 'Here is the thing I built'
        resolve(workDone)
    } else {
        const why = 'Still working on something else'
        reject(why)
    }
})
```

### consuming a promise

```javascript
const checkIfItsDone = () => {
    isItDoneYet
        .then(ok => {
            console.log('OK')
        })
        .catch(err => {
            console.error(err)
        })
}
```

running `checkIfItsDone` will execute the `isItDoneYet()` promise and will wait fot it to resolve, using the `then` callback and, if there is an error, it will handle it in the `catch` callback

### chaining promises

a promise can be returned to another promise - creating a chain of promises

calling `fetch()` (a promise-based mechanism/layer on top of the XMLHttpRequest API) is equivalent to defining your own promise using the `new Promise()` syntax

```javascript
const status = res => {
    if (res.status >= 200 && res.status < 300) {
        return Promise.resolve(res)
    }
    return Promise.reject(new Error(res.statusText))
}

const json = res => res.json()

fetch('/todos.json')
    .then(status)
    .then(json)
    .then(data => {
        console.log('Request succeeded with JSON response', data)
    })
    .catch(error => {
        console.log('Request Failed', error)
    })
```
 
 ### orchestrating promises

 use `Promise.all()` to define a list of promises and only execute subsequent code once they are _all_ resolved

 ```javascript
 const f01 = fetch('https://jsonplaceholder.typicode.com/users/3')
 const f02 = fetch('https://jsonplaceholder.typicode.com/posts/5')

 Promise.all([f01, f02])
    .then(res => {
        console.log('Array of results', res)
    })
    .catch(err => {
        console.log(err)
    })
 ```

 use `Promise.race()` to execute the ballback attached to first promise that is resolved

 ```javascript
 const promiseOne = new Promise((resolve, reject) => {
     setTimeout(resolve, 500, 'ONE')
 })

  const promiseTwo = new Promise((resolve, reject) => {
     setTimeout(resolve, 200, 'TWO')
 })

 Promise.race([promiseOne, promiseTwo]).then(result => {
     console.log(result) // 'TWO'
 })
 ```