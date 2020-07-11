## Variables 

[Code Sandbox](https://codesandbox.io/s/variables-dl9ge)

JavaScript can be referred to as __"untyped"__ because once a specific literal type has been assigned to a variables, it can later be reassigned to host any other type

A variable must be __declared__ before use. Three options:
- `var`
- `let`
- `const`

### var

an unitialized variable, when declared, will have a value of undefined
```javascript
var a // typeof a === 'undefined' 
```

declare multiple variables in same statement
```javascript
var a = 50, b = 'foo'
```

### scope

the __scope__ is the portion of the code where the variable is visible

 - __global scope__: a variable initialized w/ `var` _outside_ of any function. it is assigned to the global object and is visible everwhere
 - __local scope__: a variable initialized w/ `var` _inside_ of a function and is only visible (i.e. useable) within the function 
 - any variable defined within a function with the same name as a global variable takes precedence over the global variable - _"shadowing"_ it 
 - a new scope is only created when a function is created

### hoisting

inside of a function, any variable defined within it is visible in the function code - even if the variable is declared at the end of the function it can still be referenced in the beginning. This is beacuase JavaScript, before executing any code, actually _moves all variables on top_

### let 

`let` is essentially a blocked version of `var` - it's scope is limited to the block (i.e. content within curly braces), statement, or expression where it is defined

 - defining `let` outside of a function does _not_ create a global variable

```javascript
let c = 'foo'
```

### const

variables declared with `var` & `let` can be changed/reassigned later on in the program. However, variables declared with `const` - once intialized - can never be changed again

 - `const` has blocked scope (same as `let`)
 - is preferred way to declare a variable if it is known that it will not change later in the program

```javascript
const d = ['alpha', 'bravo']
```