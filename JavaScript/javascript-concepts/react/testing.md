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

### mocking

mocking allows you to test functionality that depends on:

- database
- network requests
- access to files
- any external system

so that:

- tests run faster
- tests are independent
- tests do not populate any data storage

most importantly, when executing a **unit test**, it should test the functionality of a function in **isolation** - not with all the baggage of things it touches

using mocks, you can inspect if a module function has been called & which parameters were used, with:

- `expect().toHaveBeenCalled`: check if a spied function has been called
- `expect().toHaveBeenCalledTimes()`: count how many time a spied function has been called
- `expect().toHaveBeenCalledWith`: check if the function has been called with a specific set of parameters
- `expect().toHaveBeenLastCalledWith()`: check the parameters of the last time the function has been invoked

**spy packages without affecting the functions code**

when importing a package, you can tell Jest to "spy" on the execution of a particular function using `spyOn()`, without affecting how that method works

```javascript
import mathFuncs from "./math";

test(`The mathjs log function`, () => {
  const spy = jest.spyOn(mathjs, "log");
  const result = mathjs.log(10000, 10);

  expect(mathjs.log).toHaveBeenCalled();
  expect(mathjs.log).toHaveBeenLastCalledWith(10000, 10);
});
```

**mock an entire package**

you can mock an entire package by creating a `__mocks__` folder in the project root and, within this folder, create one file for each package.

say you import `mathjs` - create a `__mocks__/mathjs.js` file at project root and add:

```javascript
const testing = {
  log: jest.fn(() => "test"),
};

export default testing;
```

this will mock the log function of the package - add as many functions as you want to mock

```javascript
import testing from "../__mocks__/mathjs.js"

test(`The mathjs log function`, () => {
    const result = mathjs.log(10000, 10)
    expect(result).toBe('test)
    expect(mathjs.log).toHaveBeenCalled()
    expect(mathjs.log).toHaveBeenCalledWith(1000, 10)
})
```

**mock a single function**

mock a single function using `jest.fn()`

```
import mathFuncs from "./math"

math.log = jest.fn(() => 'test')
test(`The mathjs log function`, () => {
    const result = mathjs.log(10000, 10)
    expect(result).toBe('test)
    expect(mathjs.log).toHaveBeenCalled()
    expect(mathjs.log).toHaveBeenCalledWith(1000, 10)
})
```

you can also use `jest.fn().mockReturnValue('test')` to create a simple mock that does nothing except return a value.

**pre-build mocks**

mock `fetch()` calls and provide sample return values without interacting with the actual server in tests by using [jest-fetch-mock](https://github.com/jefflau/jest-fetch-mock) library

**snapshot testing**

snapshot testing memorizes how the UI components are rendered and compares it to the current test - raising an error if there is a mismatch.

[Code Sandbox](https://codesandbox.io/s/jest-snap-test-oywti)
[Code Sandbox](https://codesandbox.io/s/jest-snapshots-7928o)

be sure to pass update flag (`jest --updateSnapshot`)

**testing react components**

[Code Sandbox](https://codesandbox.io/s/testing01-85fwk?)

https://www.npmjs.com/package/@testing-library/react
