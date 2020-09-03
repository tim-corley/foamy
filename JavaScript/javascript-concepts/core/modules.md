## Modules

[Code Sandbox](https://codesandbox.io/s/modules-bjqqo)

the synax to import a module:

```javascript
import package from 'module-name'
```
 - note that when working in _node.js_, you'll see it as:

```javascript
const package = require('module-name')
```

a module is a javascript file that __exports__ one or more values (objects, functions, variables), using the `export` keyword. for example:

> _uppercase.js_
```javascript
export default str => str.toUpperCase()
```

here, the module defines a single __default export__ (so it can be an anonymous function). now any other javascript module (i.e. file) can import the functionality offered by uppercase.js 

 - within html:
  ```html
  <script type="module" src="uppercase.js"></script>
  ```

 - within javascript:
```javascript
import toUpperCase from './uppercase.js'
```

export more than one thing:
```javascript
const a = 1
const b = 2
const c = 3

export { a, b, c }
```

import more than one thing (all things):
```javascript
import * from 'module'
```

use destructuring to import a filtered selection:
```javascript
import { a, b } from 'module'
```

rename an import by using `as`:
```javascript
import { a, b as two } from 'module'
```

import the default export and any non-default export by name (common in React)
```javascript
import React, { Component } from 'react'
```


