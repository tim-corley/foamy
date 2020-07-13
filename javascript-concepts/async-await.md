## Async Await

[Code Sandbox](https://codesandbox.io/s/async-await-u6lqk)

async/await is built on promises - they are a higher level abstraction. goal is to reduce the required boilerplate around promises. end result is __async functions__ that look synchronous but are actually asychronous and non-blocking

an async function returns a promise, such as:

```javascript
const doSomethingAsync = () => {
    return new Promise(resolve => {
        setTimeout(() => resolve('i did something!'), 3000)
    })
}
```

when you want to __call__ this function you prepend `await` and the calling code will stop until the promise is resolved or rejected. For this to work though, the client function must be defined as `async`

```javascript
const doSomething = async () => {
    console.log(await doSomethingAsync())
}
```

 - retrieving data with Promises:
  ```javascript
  // retrieving & consuming json data with promises
const getFirstPostComments = () => {
    return fetch("https://jsonplaceholder.typicode.com/posts") // get all posts
      .then(res => res.json()) // parse JSON
      .then(posts => posts[0]) // pick first post
      .then(post =>
        fetch(`https://jsonplaceholder.typicode.com/posts/${post.id}/comments`)
      )
      .then(commentRes => commentRes.json())
      .then(commentRes =>
        commentRes.forEach((comment, idx) =>
          console.log(`comment data (${idx}):\n`, comment)
        )
      );
  };
  ```

   - retrieving data with Async/Await:
  ```javascript
// retrieving & consuming json data with async/await
const getSecondPostComments = async () => {
  const res = await fetch("https://jsonplaceholder.typicode.com/posts");
  const posts = await res.json();
  const post = posts[1];
  const commentRes = await fetch(
    `https://jsonplaceholder.typicode.com/posts/${post.id}/comments`
  );
  const commentData = await commentRes.json();
  commentData.forEach((comment, idx) =>
    console.log(
      `[via async/await] second post comment data (${idx}):\n`,
      comment
    )
  );
  return commentData;
};

getSecondPostComments();
  ```

