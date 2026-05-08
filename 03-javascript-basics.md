# JavaScript Basics

## 📋 Quick Cheat Sheet

### Variables & Data Types
```javascript
// Variable declaration
var x = 10;           // Function-scoped (avoid)
let y = 20;           // Block-scoped
const z = 30;         // Block-scoped, immutable

// Data types
typeof 42;            // "number"
typeof "hello";       // "string"
typeof true;          // "boolean"
typeof undefined;     // "undefined"
typeof null;          // "object" (quirk!)
typeof {};            // "object"
typeof [];            // "object"
typeof Symbol('id');  // "symbol"
```

### Operators
```javascript
// Arithmetic
10 + 5, 10 - 5, 10 * 5, 10 / 5, 10 % 3, 2 ** 8

// Comparison
5 == "5"      // true (type coercion)
5 === "5"     // false (strict equality)
5 != "5"      // false
5 !== "5"     // true

// Logical
true && false // false
true || false // true
!true         // false

// Ternary
condition ? valueIfTrue : valueIfFalse
```

### String Methods
```javascript
const str = "Hello World";
str.length                    // 11
str.toUpperCase()             // "HELLO WORLD"
str.toLowerCase()             // "hello world"
str.charAt(0)                 // "H"
str.indexOf("World")          // 6
str.slice(0, 5)               // "Hello"
str.substring(0, 5)           // "Hello"
str.trim()                    // Remove whitespace
str.split(" ")                // ["Hello", "World"]
str.replace("World", "JS")   // "Hello JS"
str.includes("World")         // true
str.startsWith("Hello")       // true
```

### Array Methods
```javascript
const arr = [1, 2, 3, 4, 5];

// Add/Remove
arr.push(6)              // Add to end
arr.pop()                // Remove from end
arr.unshift(0)           // Add to start
arr.shift()              // Remove from start
arr.splice(2, 1, 9)      // Remove 1 at index 2, insert 9

// Search
arr.indexOf(3)           // 2
arr.includes(3)          // true
arr.find(x => x > 3)     // 4 (first match)
arr.findIndex(x => x > 3) // 3

// Transform
arr.map(x => x * 2)      // [2, 4, 6, 8, 10]
arr.filter(x => x > 2)   // [3, 4, 5]
arr.reduce((a, b) => a + b) // 15 (sum)
arr.reverse()            // [5, 4, 3, 2, 1]
arr.sort((a, b) => a - b) // Ascending order

// Check
arr.every(x => x > 0)    // true (all positive)
arr.some(x => x > 4)     // true (at least one > 4)

// Join
arr.join(", ")           // "1, 2, 3, 4, 5"
```

---

## 📖 Detailed Explanation

### ES6+ Features

**Arrow Functions:**
```javascript
// Traditional function
function add(a, b) {
    return a + b;
}

// Arrow function
const add = (a, b) => a + b;

// Arrow function with single parameter
const square = x => x * x;

// Arrow function with no parameters
const greet = () => "Hello";

// Arrow function with multiple statements
const calculate = (x, y) => {
    const sum = x + y;
    return sum * 2;
};
```

**Destructuring:**
```javascript
// Array destructuring
const [a, b, c] = [1, 2, 3];
const [first, ...rest] = [1, 2, 3, 4]; // first=1, rest=[2,3,4]

// Object destructuring
const person = { name: "John", age: 30, city: "NYC" };
const { name, age } = person;
const { name: personName } = person; // Rename
const { name, ...others } = person; // Rest operator
```

**Template Literals:**
```javascript
const name = "John";
const age = 30;

// Old way
const message = "Hello, " + name + ". You are " + age + " years old.";

// Template literals
const message = `Hello, ${name}. You are ${age} years old.`;

// Multi-line
const html = `
    <div>
        <h1>${name}</h1>
        <p>Age: ${age}</p>
    </div>
`;
```

**Spread Operator:**
```javascript
// Array spreading
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const combined = [...arr1, ...arr2]; // [1, 2, 3, 4, 5, 6]

// Object spreading
const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3 };
const merged = { ...obj1, ...obj2 }; // { a: 1, b: 2, c: 3 }

// Function arguments
function sum(a, b, c) { return a + b + c; }
const nums = [1, 2, 3];
sum(...nums); // 6
```

### Async/Await

```javascript
// Promise approach
function fetchData() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve({ id: 1, name: "John" });
        }, 1000);
    });
}

fetchData()
    .then(data => console.log(data))
    .catch(error => console.log(error));

// Async/Await approach
async function getData() {
    try {
        const response = await fetch('https://api.example.com/data');
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.log('Error:', error);
    }
}

getData();
```

### Map & Set

```javascript
// Map (key-value pairs with any type as key)
const map = new Map();
map.set('name', 'John');
map.set(1, 'one');
map.set({ id: 1 }, 'object key');

map.get('name');          // 'John'
map.has('name');          // true
map.size;                 // 3
map.delete('name');
map.clear();

// Iterate
for (const [key, value] of map) {
    console.log(key, value);
}

// Set (unique values)
const set = new Set([1, 2, 2, 3, 3, 3]);
set.size;                 // 3
set.add(4);
set.has(2);               // true
set.delete(2);
set.clear();
```

### Class Basics

```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    
    greet() {
        return `Hello, I'm ${this.name}`;
    }
    
    static info() {
        return "This is the Person class";
    }
    
    get year() {
        return new Date().getFullYear() - this.age;
    }
    
    set year(value) {
        this.age = new Date().getFullYear() - value;
    }
}

const person = new Person("John", 30);
person.greet();           // "Hello, I'm John"
Person.info();            // Static method
```

---

## 💡 Important Tips for CDAC Exam

✅ **let vs const** - Use const by default, let when needed
✅ **Arrow functions** - Don't have their own `this`
✅ **Async/Await** - Preferred over Promise chains
✅ **Destructuring** - Very common in modern JS
✅ **Spread operator** - Essential for copying arrays/objects
✅ **Template literals** - Always use over string concatenation
