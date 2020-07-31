## Testing

### Jest

[Code Sandbox](https://codesandbox.io/s/jest-testing-1mbfm)

jest is a library for testing JS (opensource, maintained by Facebook), well suited for React testing:

- fast
- can perform **snapshot testing**
- opinionated & provides everything out of the box (limits choices)

```bash
npm i jest --save-dev
```

Note: jest comes included when using `create-react-app`

```javascript
// math.js
const sum = (a, b) => a + b;
const mul = (a, b) => a * b;
const sub = (a, b) => a - b;
const div = (a, b) => a / b;

export { sum, mul, sub, div };

// const mathFuncs = {
//   sum: (a, b) => a + b,
//   mul: (a, b) => a * b,
//   sub: (a, b) => a - b,
//   div: (a, b) => a / b
// };

// export default mathFuncs;

// ------------------------
// math.test.js
import { sum, mul, sub, div } from "./math";

test("Adding 1 + 1 equals 2", () => {
  expect(sum(1, 1)).toBe(2);
});
test("Multiplying 1 * 1 equals 1", () => {
  expect(mul(1, 1)).toBe(1);
});
test("Subtracting 1 - 1 equals 0", () => {
  expect(sub(1, 1)).toBe(0);
});
test("Dividing 1 / 1 equals 1", () => {
  expect(div(1, 1)).toBe(1);
});

// import mathFuncs from "./math";

// test("Adding 1 + 1 equals 2", () => {
//   expect(mathFuncs.sum(1, 1)).toBe(2);
// });
// test("Multiplying 1 * 1 equals 1", () => {
//   expect(mathFuncs.mul(1, 1)).toBe(1);
// });
// test("Subtracting 1 - 1 equals 0", () => {
//   expect(mathFuncs.sub(1, 1)).toBe(0);
// });
// test("Dividing 1 / 1 equals 1", () => {
//   expect(mathFuncs.div(1, 1)).toBe(1);
// });
```

### matchers

most commonly used matchers, comparing the value of the result of `expect()` with the value passed in as argument, are:

- `toBe` compares strict equality, using ===
- `toEqual` compares the values of two variables. If it’s an object or array, it checks the equality of all the properties or elements
- `toBeNull` is true when passing a null value
- `toBeDefined` is true when passing a defined value (opposite to the above)
- `toBeUndefined` is true when passing an undefined value
- `toBeCloseTo` is used to compare floating values, avoiding rounding errors
- `toBeTruthy` true if the value is considered true (like an if does)
- `toBeFalsy` true if the value is considered false (like an if does)
- `toBeGreaterThan` true if the result of expect() is higher than the argument
- `toBeGreaterThanOrEqual` true if the result of expect() is equal to the argument, or higher than the argument
- `toBeLessThan` true if the result of expect() is lower than the argument
- `toBeLessThanOrEqual` true if the result of expect() is equal to the argument, or lower than the argument
- `toMatch` is used to compare strings with regular expression pattern matching
- `toContain` is used in arrays, true if the expected array contains the argument in its elements set
- `toHaveLength(number)`: checks the length of an array
- `toHaveProperty(key, value)`: checks if an object has a property, and optionally checks its value
- `toThrow` checks if a function you pass throws an exception (in general) or a specific exception
- `toBeInstanceOf()`: checks if an object is an instance of a class

all those matchers can be negated using `.not.` inside the statement, for example:

```javascript
test("Adding 1 + 1 does not equal 3", () => {
  expect(sum(1, 1)).not.toBe(3);
});
```

for use with promises, you can use `.resolvers` and `.rejects`:

```javascript
expect(Promise.resolve('lemon)).resolves.toBe('lemon')
expect(Promise.reject(new Error('octopus'))).rejects.toThrow('octopus')
```

### setup

before running tests, you'll want to perform some initialization

- to do something **once** before **all** of the tests, use the `beforeAll()` function:

```javascript
beforeAll(() => {
  // do somthing once...
});
```

- to do something before **each** test runs, use `beforeEach()`:

```javascript
beforeEach(() => {
  // do somthing once...
});
```

### teardown

just as you can do something before with setup, you can perform something after with teardown

- to do something **once** after **all** of the tests, use the `afterAll()` function:

```javascript
afterAll(() => {
  // do somthing once...
});
```

- to do something after **each** test runs, use `afterEach()`:

```javascript
afterEach(() => {
  // do somthing once...
});
```

### group tests with `describe()`

you can create groups of tests, in a single file, that isolate the setup and teardown functions:

```javascript
describe("first set", () => {
  beforeEach(() => {
    //do something
  });
  afterAll(() => {
    //do something
  });
  test(/*...*/);
  test(/*...*/);
});

describe("second set", () => {
  beforeEach(() => {
    //do something
  });
  beforeAll(() => {
    //do something
  });
  test(/*...*/);
  test(/*...*/);
});
```

### testing asynchronous code

asynchronous code in modern JS can have basically two forms: **callbacks** and **promises**. on top of promises we can use **async/await**.

**callbacks**

you can't have a test in a callback b/c jest won't execute it - the execution of the test file ends before the callback is called. to fix this, pass a parameter to the test function which you can call `done`. jest will then wait until you call `done()` before ending that math.test.js

```javascript
//uppercase.js
function uppercase(str, callback) {
  callback(str.toUpperCase())
}
export default uppercase

//uppercase.test.js
import uppercase from "./uppercase"

test(`uppercase 'test' to equal 'TEST'`, (done) => {
  uppercase('test', (str) => {
    expect(str).toBe('TEST')
    done()
  }
})
```

[code sandbox](https://codesandbox.io/s/jest-testing-1mbfm?file=/src/uppercase.test.js)

**promises**

with functions that return promises, we simply **return a promise** from the test:

```javascript
//uppercase02.js
const uppercase = (str) => {
  return new Promise((resolve, reject) => {
    if (!str) {
      reject("Empty string");
      return;
    }
    resolve(str.toUpperCase());
  });
};

export default uppercase;

//uppercase02.test.js
import uppercase from "./uppercase02";

test(`uppercase 'test' to equal 'TEST'`, () => {
  return uppercase("test").then((str) => {
    expect(str).toBe("TEST");
  });
});

// rejected promise test...
test(`uppercase 'test' to equal 'TEST'`, () => {
  return uppercase("").catch((e) => {
    expect(e).toMatch("Empty string");
  });
});
```

**async/await**

```javascript
test(`uppercase 'test' to equal 'TEST'`, async () => {
  const str = await uppercase("test");
  expect(str).toBe("TEST");
});
```
