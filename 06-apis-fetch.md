# APIs & Fetch

## 📋 Quick Cheat Sheet

### REST API Principles
```
GET     - Retrieve data      (Safe, Idempotent)
POST    - Create data        (Not idempotent)
PUT     - Replace data       (Idempotent)
PATCH   - Partial update     (Idempotent)
DELETE  - Delete data        (Idempotent)
HEAD    - Like GET, no body  (Safe, Idempotent)
OPTIONS - Describe options   (Safe, Idempotent)
```

### HTTP Status Codes
```
1xx - Informational
2xx - Success
    200 OK, 201 Created, 204 No Content
3xx - Redirection
    301 Moved Permanently, 304 Not Modified
4xx - Client Error
    400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found
5xx - Server Error
    500 Internal Server Error, 503 Service Unavailable
```

### Fetch API Basics
```javascript
// GET request
fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));

// POST request
fetch('https://api.example.com/data', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ name: 'John', age: 30 })
})
    .then(response => response.json())
    .then(data => console.log(data));
```

---

## 📖 Detailed Explanation

### Fetch API Complete Guide

```javascript
// Basic GET request
fetch('https://api.example.com/users')
    .then(response => {
        console.log('Status:', response.status);
        console.log('OK:', response.ok);        // true if 200-299
        console.log('Headers:', response.headers);
        
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        
        return response.json();
    })
    .then(data => console.log('Data:', data))
    .catch(error => console.error('Fetch error:', error));
```

### All HTTP Methods with Fetch

```javascript
const API_URL = 'https://api.example.com';

// GET - Retrieve data
fetch(`${API_URL}/users/1`)
    .then(r => r.json())
    .then(data => console.log(data));

// POST - Create data
fetch(`${API_URL}/users`, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
        name: 'John',
        email: 'john@example.com',
        age: 30
    })
})
    .then(r => r.json())
    .then(data => console.log('Created:', data));

// PUT - Replace entire resource
fetch(`${API_URL}/users/1`, {
    method: 'PUT',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
        id: 1,
        name: 'Jane',
        email: 'jane@example.com',
        age: 28
    })
})
    .then(r => r.json())
    .then(data => console.log('Updated:', data));

// PATCH - Partial update
fetch(`${API_URL}/users/1`, {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ age: 31 })  // Only update age
})
    .then(r => r.json())
    .then(data => console.log('Patched:', data));

// DELETE - Remove resource
fetch(`${API_URL}/users/1`, {
    method: 'DELETE'
})
    .then(r => r.json())
    .then(data => console.log('Deleted:', data));
```

### Async/Await with Fetch

```javascript
async function fetchUserData(userId) {
    try {
        const response = await fetch(`https://api.example.com/users/${userId}`);
        
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        
        const data = await response.json();
        return data;
    } catch (error) {
        console.error('Error fetching data:', error);
        throw error;
    }
}

// Using the function
async function displayUserData() {
    try {
        const user = await fetchUserData(1);
        console.log(user);
    } catch (error) {
        console.error('Failed to display user:', error);
    }
}

displayUserData();
```

### Advanced Fetch Options

```javascript
const options = {
    method: 'POST',
    
    // Headers
    headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer token123',
        'X-Custom-Header': 'custom-value'
    },
    
    // Body
    body: JSON.stringify({ name: 'John' }),
    
    // Timeout (not built-in, need AbortController)
    signal: AbortSignal.timeout(5000),
    
    // Credentials (for CORS with cookies)
    credentials: 'include', // 'same-origin', 'omit'
    
    // CORS mode
    mode: 'cors', // 'no-cors', 'same-origin'
    
    // Cache
    cache: 'no-cache', // 'default', 'no-store', 'reload', 'force-cache'
    
    // Redirect
    redirect: 'follow' // 'error', 'manual'
};

fetch('https://api.example.com/data', options)
    .then(r => r.json())
    .then(data => console.log(data));
```

### Handling Different Response Types

```javascript
fetch('https://api.example.com/data')
    .then(response => {
        // Parse different content types
        const contentType = response.headers.get('content-type');
        
        if (contentType?.includes('application/json')) {
            return response.json();
        } else if (contentType?.includes('text/html')) {
            return response.text();
        } else if (contentType?.includes('image')) {
            return response.blob();
        } else if (contentType?.includes('application/pdf')) {
            return response.arrayBuffer();
        }
    })
    .then(data => console.log(data));
```

### Request Cancellation with AbortController

```javascript
const controller = new AbortController();

fetch('https://api.example.com/data', {
    signal: controller.signal
})
    .then(r => r.json())
    .then(data => console.log(data))
    .catch(error => {
        if (error.name === 'AbortError') {
            console.log('Request cancelled');
        }
    });

// Cancel request after 5 seconds
setTimeout(() => controller.abort(), 5000);
```

### CORS Handling

```javascript
// CORS error: "No 'Access-Control-Allow-Origin' header"
// Backend needs to send appropriate headers:
// Access-Control-Allow-Origin: *
// Access-Control-Allow-Methods: GET, POST, PUT, DELETE
// Access-Control-Allow-Headers: Content-Type, Authorization

// Client side: include credentials for cookies
fetch('https://api.example.com/data', {
    method: 'POST',
    credentials: 'include', // Include cookies
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({ data: 'test' })
})
    .then(r => r.json())
    .then(data => console.log(data));
```

---

## 💡 Important Tips for CDAC Exam

✅ **HTTP Methods** - Know when to use GET, POST, PUT, PATCH, DELETE
✅ **Status Codes** - Understand 2xx, 3xx, 4xx, 5xx
✅ **response.ok** - Check this instead of just status
✅ **Async/Await** - Preferred over .then() chains
✅ **CORS** - Know about credentials: 'include'
✅ **Content-Type header** - Essential for POST/PUT/PATCH
