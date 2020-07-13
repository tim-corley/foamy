## Classes

[Code Sandox](https://codesandbox.io/s/classes-5mssx)

### class definition

```javascript
class Person {
    constructor(name) {
        this.name = name
    }

    hello() {
        return`Hello, I am ${this.name}. What's your name?`;
    }
}

// initalize
const charlie = new Person('Charlie')
const logHello = charlie.hello()
console.log(logHello);
```

### inheritance

```javascript
class Developer extends Person {
    hey() {
        return super.hello() + ' I am a developer.'
        
    }
}

const dennis = new Developer('Dennis')
const logHey = dennis.hey()
console.log(logHey);
```

### static methods

usually methods are called on the instance but __static methods__ are executed on the class

```javascript
class Docs {
    static genericName() {
        return 'document-00'
    }
}

console.log(Docs.genericName());
```

### getters & setters

control access to values within a class
 - getters: accessing a variable
 - setters: modifying a variable's value

```javascript
class Movie {
    constructor(title, year) {
        this.title = title
        this.year = year
    }

    set newTitle(_val) {
        this.title = _val
    }

    get getTitle() {
        return this.title
    }
}

const newRelease = new Movie('Tenet', 2020)
console.log(newRelease.getTitle);

newRelease.newTitle = 'tenet 2'
console.log(newRelease.getTitle);
```
