## Add Stlying to React Projects

### tailwind

https://blog.logrocket.com/create-react-app-and-tailwindcss/

```bash
➜  React npx nano-react-app firebase-todo && cd firebase-todo
➜  firebase-todo npm install tailwindcss --save-dev
➜  firebase-todo npx tailwind init tailwind.js --full
➜  firebase-todo npm install postcss-cli autoprefixer --save-dev
➜  firebase-todo touch postcss.config.js
```

```javascript
// postcss.config.js
const tailwindcss = require("tailwindcss");
module.exports = {
  plugins: [tailwindcss("./tailwind.js"), require("autoprefixer")],
};
```

create a `stlyes` directory (in `src/`) and add `tailwind.css` & `index.css`

```bash
➜  firebase-todo cd src && mkdir styles
➜  src cd styles && touch tailwind.css index.css
```

```css
/*index.css*/
@tailwind base;

@tailwind components;

@tailwind utilities;
```

```json
// package.json
  "scripts": {
    "build:style": "tailwind build src/styles/index.css -o src/styles/tailwind.css",
    "start": "npm run build:style && parcel index.html",
    "build": "parcel build index.html"
  },
```

```javascript
//src/index.js
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";
import "./styles/tailwind.css";

ReactDOM.render(<App />, document.getElementById("root"));
```

```javascript
// App.js
import React from "react";

export default () => (
  <>
    <div className="flex">
      <div className="m-auto w-full max-w-md bg-gray-800 my-10">
        <form action="" className=" bg-white shadow-md rounded px-8 py-8 pt-8">
          <div className="px-4 pb-4">
            <label htmlFor="email" className="text-sm block font-bold  pb-2">
              EMAIL ADDRESS
            </label>
            <input
              type="email"
              name="email"
              id=""
              className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline border-blue-300 "
              placeholder="Johnbull@example.com"
            />
          </div>
          <div className="px-4 pb-4">
            <label htmlFor="password" className="text-sm block font-bold pb-2">
              PASSWORD
            </label>
            <input
              type="password"
              name="email"
              id=""
              className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline border-blue-300"
              placeholder="Enter your password"
            />
          </div>
          <div>
            <button
              className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
              type="button"
            >
              Sign In
            </button>
          </div>
        </form>
      </div>
    </div>
  </>
);
```
