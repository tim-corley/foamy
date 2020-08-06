## React-Firebase Todo App

https://www.freecodecamp.org/news/how-to-build-a-todo-application-using-reactjs-and-firebase/

https://console.firebase.google.com/project/react-todo-ac8c2/overview

### install firebase tools

```bash
 sudo npm install -g firebase-tools
```

### configure project

```bash
➜  React npx nano-react-app firebase-todo
```

- run through config options

### add styling (tailwind)

see: [[styling.md]]

### add test function & deploy

```javascript
//functions/index.js
const functions = require("firebase-functions");

// // Create and Deploy Your First Cloud Functions
// // https://firebase.google.com/docs/functions/write-firebase-functions

exports.helloWorld = functions.https.onRequest((request, response) => {
  functions.logger.info("Hello logs!", { structuredData: true });
  response.send("Hello from Firebase!");
});
```

```bash
firebase deploy
```

should see "Hello from Firebase!" at: https://us-central1-react-todo-ac8c2.cloudfunctions.net/helloWorld

### backend

```bash
npm i express
```

```javascript
// functions/index.js
const functions = require("firebase-functions");
const app = require("express")();

const { getAllTodos } = require("./apis/todos");

app.get("/todos", getAllTodos);
exports.api = functions.https.onRequest(app);
```

Parcel (for bundling) does not allow for proxy (see: https://chaseohlson.com/proxy-api-requests-parcel). Attempted to find a workaround but no luck. Going to rebuild project with create-react-app (i.e. webpack) in order to use proxy

/home/tim/Projects/React/todo-app

npx create-react-app todo-app

TAILWIND
https://blog.logrocket.com/create-react-app-and-tailwindcss/
npm install tailwindcss

npx tailwind init tailwind.js --full

npm install postcss-cli autoprefixer --save-dev

```javascript
//postcss.config.js
const tailwindcss = require("tailwindcss");
module.exports = {
  plugins: [tailwindcss("./tailwind.js"), require("autoprefixer")],
};
```

```json
// package.json
  "scripts": {
    "build:style": "tailwind build src/styles/index.css -o src/styles/tailwind.css",
    "start": "npm run build:style && react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
```

Firebase

- functions

  ```
  ➜  todo-app git:(master) ✗ firebase init
  ```
