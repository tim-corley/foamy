## Code Splitting

code splitting is the practice of only loading the JS you need the moment you need it. this improves:

- performance
- impact on battery (thus, battery on mobile)
- the download size

`React.lazy` & `Suspence` for the perfect was to lazily load a dependency and only load it when needed.

use `React.lazy` to import a component. the component will then be dynamically added to the output as soon as it's availble. Webpack will create a seperate bundle for it and will take care of loading it when necessary

a `Suspense` compponent is then needed to wrap an lazily loaded component. it takes care of handling the output while the lazy loaded component is fetched and rendered. can use it's `fallback` prop to output some jsx or a component output while loading.

```javascript
import React, { lazy, Suspense } from "react";
import "./styles.css";

const Todo = lazy(() => import("./Todo"));

export default function App() {
  return (
    <div className="App">
      <Suspense fallback={<p>loading...</p>}>
        <Todo />
      </Suspense>
    </div>
  );
}
```

- with react router:

```javascript
import React from "react";
import { BrowserRouter as Router, Route, Switch } from "react-router-dom";

const TodoList = React.lazy(() => import("./routes/TodoList"));
const NewTodo = React.lazy(() => import("./routes/NewTodo"));

const App = () => (
  <Router>
    <React.Suspense fallback={<p>Please wait</p>}>
      <Switch>
        <Route exact path="/" component={TodoList} />
        <Route path="/new" component={NewTodo} />
      </Switch>
    </React.Suspense>
  </Router>
);
```
