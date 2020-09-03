## React Router

[Code Sandbox](https://codesandbox.io/s/routing-3w5do)

routing in a single page application is the way to introduce some features to navigating the app through links, which are expected in normal web aplications.

1. the browser should change the url when navigating to a different screen
2. deep linking should work (pointing the browser to a url, the application should reconstruct the same view that was presented when the url was generated)
3. the browser back (and forward) button should work as expected

react router offers a way to write your code so that it will show certain components of your app only iff the route matches what you define

```bash
npm i react-router-dom --save-dev
```

**types of routes**

- `BrowserRouter`
- `HashRouter`

One builds classic URLs, the other builds URLs with the hash:

```
https://application.com/dashboard   /* BrowserRouter */
https://application.com/#/dashboard /* HashRouter    */
```

recommended to use `BrowserRouter` since it uses the History API (recent feature)

**components**

the 3 components you'll interact with the most when working with React Router are:

- `BrowserRouter` (usually aliased as 'Router') - wraps all the Route components
- `Link` - used to generate links to your routes
- `Route` - responsible for showing - or hiding - the components that they contain

```javascript
import React from "react";
import { BrowserRouter as Router, Link, Route } from "react-router-dom";
import "./styles.css";

const Dashboard = () => (
  <div>
    <h2>Dashboard Page</h2>
  </div>
);

const About = () => (
  <div>
    <h2>About Page</h2>
  </div>
);

export default function App() {
  return (
    <Router>
      <div className="App">
        <h3>Welcome, have a look around...</h3>
        <aside>
          <Link to={"/"}>Dashboard</Link> <Link to={"/about"}>About</Link>
        </aside>

        <main>
          <Route exact path="/" component={Dashboard} />
          <Route path="/about" component={About} />
        </main>
      </div>
    </Router>
  );
}
```
