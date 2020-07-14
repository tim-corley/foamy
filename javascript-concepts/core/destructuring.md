## Destructuring

[Code Sandox](https://codesandbox.io/s/destructuring-vohsz)

#### References:
 - https://www.youtube.com/watch?v=_ApRMRGI-6g


### objects
 - arrays
```javascript
const arr = [1, 2, 3, 4, 5]
const [one, two] = arr
console.log(one);
```

 - objects
```javascript
const actor = {
    firstName: 'Tom',
    lastName: 'Hanks',
    oscarWinner: true,
    age: 64
}

// map firstName to new variable
const { firstName: name, age } = actor
console.log(`${name} is ${age} years old!`);
```

 - nested object
```javascript
const makeItem = () => {
    return {
        data: {
            item: {
                name: 'Shoes',
                size: {
                    US: 10,
                    EU: 44
                }
            }
        },
        status: 'live'
    }
}

// const { data, status } = makeItem();
// console.log(data, status);

const { data: { item: { name, size: { US, EU }}}, status } = makeItem();
console.log(name, US, EU);
```


### arrays