## Rest & Spread

[Code Sandox](https://codesandbox.io/s/rest-spread-4o3jc)

#### References:
 - https://scotch.io/bar-talk/javascripts-three-dots-spread-vs-rest-operators543

### basic destructuring

 - arrays
  ```javascript
  const myList = ['alpha','bravo','charlie','delta','echo']
  // leave space between commas to skip
  const [first,,third] = myList
  console.log(first) // alpha
  console.log(third) // charlie
  ```

 - function returns
  ```javascript
  const sumAndMult = (x, y) => [x + y, x * y]

  const noDestruct = sumAndMult(4, 5)
  const [sum, mult, div = 'No Division'] = sumAndMult(4, 5)

  console.log(noDestruct)
  console.log(sum)
  console.log(mult)
  console.log(div)
  ```

  - objects
  ```javascript
  const personOne = {
      name: 'Mac',
      age: 38,
      location: {
          city: 'Los Angeles',
          state: 'California'
      }
  }
  const personTwo = {
      name: 'Dee',
      age: 36,
      location: {
          city: 'New York City',
          state: 'New York'
      }
  }

  // not using position (like arrays) so inputs must match property name
  const { name, age } = personOne

  console.log(name)
  console.log(age)

  // map value to a new variable
  const { name: firstName } = personTwo
  console.log(firstName)

  const personA = {
    name: 'Frank',
    age: 60,
    owner: true
  }

  const personB = {
    age: 45,
    location: {
        city: 'Boston',
        state: 'Massachusetts'
    }
  }

  const personC = { ...personA, ...personB }
  // with common/shared properties, last value is applied
  console.log(personC);

  // passing objects into functions

  // without destructuring
  const printUser01 = (user) => console.log(`name is: ${user.name} & age is: ${user.age}`);
  printUser01(personOne)

  // with destructuring
  const printUser02 = ({ name, age }) => console.log(`name is: ${name} & age is: ${age}`);
  printUser02(personTwo)

  // with destructuring & default value
  const printUser03 = ({ name, age, isDefault = true }) => console.log(`name is: ${name} & age is: ${age}. Are we using a default value: ${isDefault}`);
  printUser03(personOne)
  ```

### `...`
the `...` is a feature released in ECMA6 that can be used in two different ways:
 - spread operator
 - rest parameter

### spread
allows iterables (arrays / objects / strings) to be expanded into single arguments/ elements

```javascript
const myArr = ['bravo', 'charlie', 'delta']
const newArr = ['alpha', ...myArr, 'echo']
```

 - arrays
  ```javascript
  const a = [3, 6, 9]
  // create a new array
  const b = [...a, 7, 10, 11]
  // create a copy of an array
  const c = [...a]
  ```

  - objects
  ```javascript
  // clone an object
  const newObj = { ...oldObj }
  ```

  - strings
  ```javascript
  const h = 'Hello'
  // create array from strong, each char is an item
  const arrayized = [...h]
  ```

importantly, the spread operator enables ability to easily use an array as a function argument

  ```javascript
  const f = (foo, bar, par) => {}
  const test = ['alpha', 'bravo', 'charlie']
  f(...test)

  const add = (a, b, c) => {
      return a + b + c
  }
  const args = [2, 4, 8]
  add(...args)
  ```

unlike the rest parameter (which needs to be last arg), the spread operator can be used/placed at any position in the args

  ### rest
collects all __remaining__ elements into an array

  ```javascript
// without rest (only first two args are taken)
const add = (x, y) => x + y;
const noRest = add(2, 3, 5) // 5

// with rest (gather all args into an array)
const addAgain = (...args) => {
    let result = 0;
    for (let a of args ) result += a;
    return result
}

const withRest = addAgain(2, 3, 5) // 10
```

rest parameters _have to be the last argument_ becuase it collects remaining / excess args in an array. this will __not__ work:

```javascript
const badRest = (a, ...b, c) => {
    ...
    return
}
```
