# JSON & Data Handling

## 📋 Quick Cheat Sheet

### JSON Format
```json
{
  "name": "John",
  "age": 30,
  "active": true,
  "salary": null,
  "skills": ["JavaScript", "Python", "SQL"],
  "address": {
    "street": "123 Main St",
    "city": "NYC"
  }
}
```

### JSON Methods
```javascript
const obj = { name: 'John', age: 30 };

// Convert to JSON string
const json = JSON.stringify(obj);
// '{"name":"John","age":30}'

// Parse JSON string to object
const parsed = JSON.parse(json);
// { name: 'John', age: 30 }

// Pretty print
const pretty = JSON.stringify(obj, null, 2);
/*
{
  "name": "John",
  "age": 30
}
*/
```

---

## 📖 Detailed Explanation

### JSON Data Types

```javascript
// Valid JSON types
const validJSON = `
{
  "string": "hello",           // String
  "number": 42,                // Number (integer or float)
  "boolean": true,             // Boolean (true/false)
  "null": null,                // Null
  "array": [1, 2, 3],          // Array
  "object": { "key": "value" } // Object
}
`;

// Invalid in JSON (valid in JavaScript)
const invalidJSON = `
{
  "function": function() {},   // Functions not allowed
  "undefined": undefined,      // undefined not allowed
  "date": new Date(),          // Objects not allowed
  "bigint": 123n,              // BigInt not allowed
  "symbol": Symbol('s')        // Symbol not allowed
}
`;
```

### JSON.stringify() Advanced

```javascript
const person = {
    name: 'John',
    age: 30,
    password: 'secret',
    email: 'john@example.com'
};

// Basic stringify
JSON.stringify(person);
// '{"name":"John","age":30,"password":"secret","email":"john@example.com"}'

// With replacer function (filter out password)
const json = JSON.stringify(person, (key, value) => {
    if (key === 'password') {
        return undefined; // Exclude password
    }
    return value;
});
// '{"name":"John","age":30,"email":"john@example.com"}'

// With specific keys
const json2 = JSON.stringify(person, ['name', 'email']);
// '{"name":"John","email":"john@example.com"}'

// With formatting (indentation)
const json3 = JSON.stringify(person, null, 2);
/*
{
  "name": "John",
  "age": 30,
  "password": "secret",
  "email": "john@example.com"
}
*/
```

### JSON.parse() Advanced

```javascript
const jsonString = '{"name":"John","age":30,"birthDate":"1993-05-15"}';

// Basic parse
const person = JSON.parse(jsonString);
// { name: 'John', age: 30, birthDate: '1993-05-15' }

// With reviver function (convert string to Date)
const personWithDate = JSON.parse(jsonString, (key, value) => {
    if (key === 'birthDate') {
        return new Date(value); // Convert to Date object
    }
    return value;
});
// { name: 'John', age: 30, birthDate: Date object }

// Safe parsing (catch JSON errors)
function safeJsonParse(jsonString) {
    try {
        return JSON.parse(jsonString);
    } catch (error) {
        console.error('Invalid JSON:', error);
        return null;
    }
}
```

### Serialization & Deserialization Example

```javascript
// API Response Example
const apiResponse = `
[
  {
    "id": 1,
    "username": "john_doe",
    "email": "john@example.com",
    "registeredAt": "2023-01-15T10:30:00Z",
    "isActive": true
  },
  {
    "id": 2,
    "username": "jane_smith",
    "email": "jane@example.com",
    "registeredAt": "2023-02-20T14:45:00Z",
    "isActive": false
  }
]
`;

// Parse with reviver to convert dates
const users = JSON.parse(apiResponse, (key, value) => {
    if (key === 'registeredAt' && typeof value === 'string') {
        return new Date(value);
    }
    return value;
});

console.log(users[0].registeredAt instanceof Date); // true

// Send back to server (stringify)
const userUpdate = {
    id: 1,
    username: 'john_doe',
    lastUpdated: new Date()
};

const jsonToSend = JSON.stringify(userUpdate, (key, value) => {
    if (value instanceof Date) {
        return value.toISOString(); // Convert Date to ISO string
    }
    return value;
});

console.log(jsonToSend);
// '{"id":1,"username":"john_doe","lastUpdated":"2026-05-08T...Z"}'
```

### Working with Complex Data Structures

```javascript
// Nested data structure
const company = {
    name: 'Tech Corp',
    departments: [
        {
            id: 1,
            name: 'Engineering',
            employees: [
                { id: 101, name: 'John', role: 'Developer' },
                { id: 102, name: 'Jane', role: 'Architect' }
            ]
        },
        {
            id: 2,
            name: 'Sales',
            employees: [
                { id: 201, name: 'Bob', role: 'Manager' }
            ]
        }
    ]
};

// Stringify with indentation for readability
const jsonCompany = JSON.stringify(company, null, 2);

// Access nested data
const parsedCompany = JSON.parse(jsonCompany);
const firstEmployee = parsedCompany.departments[0].employees[0];
console.log(firstEmployee.name); // 'John'
```

### JSON Schema Validation

```javascript
// Simple validation function
function validateUserData(data) {
    const required = ['name', 'email', 'age'];
    
    for (const field of required) {
        if (!(field in data)) {
            throw new Error(`Missing required field: ${field}`);
        }
    }
    
    if (typeof data.age !== 'number' || data.age < 0) {
        throw new Error('Age must be a positive number');
    }
    
    if (!data.email.includes('@')) {
        throw new Error('Invalid email format');
    }
    
    return true;
}

const user = { name: 'John', email: 'john@example.com', age: 30 };

try {
    validateUserData(user);
    console.log('Valid user data');
} catch (error) {
    console.error('Validation error:', error.message);
}
```

---

## 💡 Important Tips for CDAC Exam

✅ **JSON is text** - It's a string representation of data
✅ **Only 6 data types** - String, Number, Boolean, Null, Array, Object
✅ **No functions in JSON** - Cannot serialize functions
✅ **stringify() vs parse()** - Always paired for serialization
✅ **Reviver/Replacer** - Use for custom serialization/deserialization
✅ **Error handling** - Always wrap parse() in try-catch
