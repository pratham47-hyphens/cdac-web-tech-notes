# JavaScript Advanced Concepts

## 📋 Quick Cheat Sheet

### Scope & Closures
```javascript
// Global scope
var globalVar = 'global';

function outerFunction() {
    var localVar = 'local';
    
    function innerFunction() {
        console.log(globalVar);  // 'global' (closure)
        console.log(localVar);   // 'local' (closure)
    }
    
    innerFunction();
}

// Closure example
function counter() {
    let count = 0;
    return function() {
        return ++count;
    };
}

const increment = counter();
increment(); // 1
increment(); // 2
increment(); // 3
```

### `this` Context
```javascript
// 1. Function call
function greet() { console.log(this); }
greet();  // window (or undefined in strict mode)

// 2. Method call
const obj = {
    name: 'John',
    greet() { console.log(this.name); }
};
obj.greet();  // obj

// 3. Constructor call
function Person(name) { this.name = name; }
new Person('John');

// 4. Explicit binding
greet.call(obj);              // obj (call)
greet.apply(obj, []);         // obj (apply)
const boundGreet = greet.bind(obj);  // bind
```

### Prototypes & Inheritance
```javascript
function Animal(name) {
    this.name = name;
}

Animal.prototype.speak = function() {
    console.log(`${this.name} makes a sound`);
};

function Dog(name, breed) {
    Animal.call(this, name);
    this.breed = breed;
}

Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

Dog.prototype.bark = function() {
    console.log(`${this.name} barks`);
};

const dog = new Dog('Max', 'Labrador');
dog.speak();  // 'Max makes a sound'
dog.bark();   // 'Max barks'
```

---

## 📖 Detailed Explanation

### Closure Deep Dive

```javascript
// Closure: A function with access to outer scope variables
function outer() {
    const outerVar = 'I am outer';
    
    function inner() {
        console.log(outerVar); // Can access outerVar
    }
    
    return inner;
}

const innerFunc = outer();
innerFunc(); // 'I am outer' - closure preserves outer scope

// Practical example: Data privacy
function createBankAccount(initialBalance) {
    let balance = initialBalance; // Private variable
    
    return {
        deposit(amount) {
            balance += amount;
            return balance;
        },
        withdraw(amount) {
            balance -= amount;
            return balance;
        },
        getBalance() {
            return balance;
        }
    };
}

const account = createBankAccount(1000);
account.deposit(500);   // 1500
account.withdraw(200);  // 1300
// balance is inaccessible from outside
```

### Higher-Order Functions

```javascript
// Function that returns a function
function makeMultiplier(multiplier) {
    return function(number) {
        return number * multiplier;
    };
}

const double = makeMultiplier(2);
const triple = makeMultiplier(3);

double(5);  // 10
triple(5);  // 15

// Function that takes a function as argument
function execute(func, value) {
    return func(value);
}

execute(x => x * 2, 5);  // 10

// Function composition
function compose(f, g) {
    return function(x) {
        return f(g(x));
    };
}

const add5 = x => x + 5;
const multiply2 = x => x * 2;

const addThenMultiply = compose(multiply2, add5);
addThenMultiply(3);  // (3 + 5) * 2 = 16
```

### Event Handling & Event Delegation

```javascript
// Basic event listener
const button = document.getElementById('myButton');
button.addEventListener('click', (event) => {
    console.log('Button clicked');
    event.preventDefault();  // Prevent default behavior
    event.stopPropagation(); // Stop event bubbling
});

// Event delegation (handling events on parent for children)
const list = document.getElementById('myList');

list.addEventListener('click', (event) => {
    if (event.target.tagName === 'LI') {
        console.log('Item clicked:', event.target.textContent);
    }
});

// Event types
element.addEventListener('click', handler);      // Mouse click
element.addEventListener('dblclick', handler);    // Double click
element.addEventListener('mouseenter', handler);  // Mouse enter
element.addEventListener('mouseleave', handler);  // Mouse leave
element.addEventListener('keydown', handler);     // Key pressed
element.addEventListener('change', handler);      // Input changed
element.addEventListener('submit', handler);      // Form submitted
```

### Event Object Properties

```javascript
document.addEventListener('click', (event) => {
    event.type;           // 'click'
    event.target;         // Element that triggered event
    event.currentTarget;   // Element with listener
    event.clientX;         // X coordinate relative to viewport
    event.clientY;         // Y coordinate relative to viewport
    event.pageX;           // X coordinate relative to page
    event.pageY;           // Y coordinate relative to page
    event.key;             // Key pressed (for keyboard events)
    event.code;            // Physical key (for keyboard events)
});
```

### Debounce & Throttle

```javascript
// Debounce: Execute function after user stops triggering it
function debounce(func, delay) {
    let timeoutId;
    return function(...args) {
        clearTimeout(timeoutId);
        timeoutId = setTimeout(() => func(...args), delay);
    };
}

const searchInput = document.getElementById('search');
const handleSearch = debounce((e) => {
    console.log('Searching for:', e.target.value);
}, 300);

searchInput.addEventListener('input', handleSearch);

// Throttle: Execute function at most once per time period
function throttle(func, limit) {
    let inThrottle;
    return function(...args) {
        if (!inThrottle) {
            func(...args);
            inThrottle = true;
            setTimeout(() => (inThrottle = false), limit);
        }
    };
}

const handleScroll = throttle(() => {
    console.log('User scrolling');
}, 1000);

window.addEventListener('scroll', handleScroll);
```

---

## 💡 Important Tips for CDAC Exam

✅ **Closure** - Understand how variables are captured
✅ **this binding** - Know call, apply, bind methods
✅ **Prototypal inheritance** - Know prototype chain
✅ **Event delegation** - More efficient than individual listeners
✅ **Debounce vs Throttle** - Know when to use each
✅ **Memory management** - Closures keep references in memory
