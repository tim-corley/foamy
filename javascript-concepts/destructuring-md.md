## Destructuring

[Code Sandox](https://codesandbox.io/s/destructuring-vohsz)

#### References:
 - https://www.youtube.com/watch?v=_ApRMRGI-6g


### objects

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