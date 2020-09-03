## Server Side Rendering (SSR)

SSR is the ability for JavaScript to render on the server rather than in the browser. 

Why?
 - fast first page load time
 - SEO 
 - sharing via social media (allows for metadata)

Usefult to get to "sweet spot" where page is first loaded via server-side and then all subsuquent interactions are handled client-side 

### SSR Demo App

 - tim-corley/javascript-concepts/React/ssr-demo-app
 - reference: https://www.freecodecamp.org/news/the-react-handbook-b71c27b0a795/#server-side-rendering

```bash
npx create-react-app ssr-demo-app 
cd ssr-demo-app
npm install express
mkdir server
cd server
touch server.js
touch index.js 
npm install @babel/register @babel/preset-env @babel/preset-react ignore-styles express
```

### public/index.html

replace: `<div id="root"></div>` with: `<div id="root">\${ReactDOMServer.renderToString(<App />)}</div>`

### src/index.js

replace `ReactDOM.render(...)` with: `ReactDOM.hydrate(...)` 

### server/server.js

```javascript
import path from 'path'
import fs from 'fs'

import express from 'express'
import React from 'react'
import ReactDOMServer from 'react-dom/server'

import App from '../src/App'

const PORT = 8080
const app = express()

const router = express.Router()

const serverRenderer = (req, res, next) => {
  fs.readFile(path.resolve('./build/index.html'), 'utf8', (err, data) => {
    if (err) {
      console.error(err)
      return res.status(500).send('An error occurred')
    }
    return res.send(
      data.replace(
        '<div id="root"></div>',
        `<div id="root">${ReactDOMServer.renderToString(<App />)}</div>`
      )
    )
  })
}
router.use('^/$', serverRenderer)

router.use(
  express.static(path.resolve(__dirname, '..', 'build'), { maxAge: '30d' })
)

// tell the app to use the above rules
app.use(router)

// app.use(express.static('./build'))
app.listen(PORT, () => {
  console.log(`SSR running on port ${PORT}`)
})
```

### server/index/js
```javascript
require('ignore-styles')

require('@babel/register')({
  ignore: [/(node_modules)/],
  presets: ['@babel/preset-env', '@babel/preset-react']
})

require('./server')
```

```bash
npm run build
node server/index.js
```

Server-Side Rendering can get pretty tricky, will likely want to lean on tools like Next.js & GatsbyJS to help out. 