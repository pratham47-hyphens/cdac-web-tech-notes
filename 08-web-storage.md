# Web Storage

## 📋 Quick Cheat Sheet

### Storage Types Comparison
```
LocalStorage vs SessionStorage vs Cookies

┌─────────────────┬──────────────┬────────────────┬──────────────┐
│ Feature         │ LocalStorage │ SessionStorage │ Cookies      │
├─────────────────┼──────────────┼────────────────┼──────────────┤
│ Lifetime        │ Persistent   │ Until tab close│ Expirable    │
│ Domain/Path     │ Domain       │ Domain         │ Path-specific│
│ Size Limit      │ 5-10 MB      │ 5-10 MB        │ 4 KB         │
│ Server Access   │ No           │ No             │ Yes          │
│ Sync            │ Same domain  │ Same tab       │ Auto         │
└─────────────────┴──────────────┴────────────────┴──────────────┘
```

### LocalStorage API
```javascript
// Set item
localStorage.setItem('name', 'John');
localStorage.setItem('preferences', JSON.stringify({ theme: 'dark' }));

// Get item
const name = localStorage.getItem('name');        // 'John'
const prefs = JSON.parse(localStorage.getItem('preferences'));

// Remove item
localStorage.removeItem('name');

// Clear all
localStorage.clear();

// Get length
console.log(localStorage.length);

// Iterate
for (let i = 0; i < localStorage.length; i++) {
    const key = localStorage.key(i);
    const value = localStorage.getItem(key);
}
```

---

## 📖 Detailed Explanation

### LocalStorage

```javascript
// Storing user preferences
const userPreferences = {
    theme: 'dark',
    language: 'en',
    fontSize: 14,
    autoSave: true
};

localStorage.setItem('userPrefs', JSON.stringify(userPreferences));

// Retrieving and parsing
const savedPrefs = JSON.parse(localStorage.getItem('userPrefs'));
if (savedPrefs) {
    applyTheme(savedPrefs.theme);
    setLanguage(savedPrefs.language);
}

// Updating preferences
const currentPrefs = JSON.parse(localStorage.getItem('userPrefs')) || {};
currentPrefs.theme = 'light';
localStorage.setItem('userPrefs', JSON.stringify(currentPrefs));

// Removing
localStorage.removeItem('userPrefs');
```

### SessionStorage

```javascript
// Session storage is cleared when tab closes
// Useful for temporary data within a session

// Store temporary form data
sessionStorage.setItem('formDraft', JSON.stringify({
    title: 'My Article',
    content: 'Some content...',
    savedAt: new Date().toISOString()
}));

// Retrieve on page reload
window.addEventListener('beforeunload', () => {
    const draft = JSON.parse(sessionStorage.getItem('formDraft'));
    if (draft) {
        // Save to server before leaving
        fetch('/api/save-draft', {
            method: 'POST',
            body: JSON.stringify(draft)
        });
    }
});
```

### Cookies

```javascript
// Set cookie
function setCookie(name, value, days = 7) {
    const date = new Date();
    date.setTime(date.getTime() + (days * 24 * 60 * 60 * 1000));
    const expires = `expires=${date.toUTCString()}`;
    document.cookie = `${name}=${value}; ${expires}; path=/`;
}

// Get cookie
function getCookie(name) {
    const nameEQ = `${name}=`;
    const cookies = document.cookie.split(';');
    for (let cookie of cookies) {
        cookie = cookie.trim();
        if (cookie.indexOf(nameEQ) === 0) {
            return cookie.substring(nameEQ.length);
        }
    }
    return null;
}

// Delete cookie
function deleteCookie(name) {
    setCookie(name, '', -1);
}

// Usage
setCookie('sessionId', 'abc123', 1);  // 1 day
const sessionId = getCookie('sessionId');
deleteCookie('sessionId');

// Cookie attributes
function setSecureCookie(name, value) {
    const cookie = `${name}=${value}; path=/; domain=example.com; Secure; SameSite=Strict`;
    document.cookie = cookie;
}
```

### Storage Events

```javascript
// Listen for storage changes (other tabs/windows)
window.addEventListener('storage', (event) => {
    console.log('Storage changed in another tab');
    console.log('Key:', event.key);         // Changed key
    console.log('Old value:', event.oldValue);
    console.log('New value:', event.newValue);
    console.log('URL:', event.url);         // Page that triggered change
    
    // Update UI if data changed
    if (event.key === 'userPrefs') {
        const newPrefs = JSON.parse(event.newValue);
        applyTheme(newPrefs.theme);
    }
});
```

### IndexedDB

```javascript
// Open/Create database
const dbRequest = indexedDB.open('myDatabase', 1);

dbRequest.onerror = () => console.error('DB error');

dbRequest.onsuccess = () => {
    const db = dbRequest.result;
    console.log('DB opened successfully');
};

// Create object store (table)
dbRequest.onupgradeneeded = (event) => {
    const db = event.target.result;
    
    if (!db.objectStoreNames.contains('users')) {
        const store = db.createObjectStore('users', { keyPath: 'id' });
        store.createIndex('email', 'email', { unique: true });
    }
};

// Add data
const addRequest = db.transaction(['users'], 'readwrite')
    .objectStore('users')
    .add({ id: 1, name: 'John', email: 'john@example.com' });

// Get data
const getRequest = db.transaction(['users'], 'readonly')
    .objectStore('users')
    .get(1);

getRequest.onsuccess = () => {
    console.log('User:', getRequest.result);
};

// Query by index
const emailIndex = db.transaction(['users'], 'readonly')
    .objectStore('users')
    .index('email')
    .get('john@example.com');
```

### Practical Examples

**Shopping Cart:**
```javascript
class ShoppingCart {
    constructor() {
        this.storageKey = 'shoppingCart';
        this.items = this.loadCart();
    }
    
    addItem(product) {
        const existing = this.items.find(p => p.id === product.id);
        if (existing) {
            existing.quantity += product.quantity || 1;
        } else {
            this.items.push({ ...product, quantity: product.quantity || 1 });
        }
        this.saveCart();
    }
    
    removeItem(productId) {
        this.items = this.items.filter(p => p.id !== productId);
        this.saveCart();
    }
    
    saveCart() {
        localStorage.setItem(this.storageKey, JSON.stringify(this.items));
    }
    
    loadCart() {
        const stored = localStorage.getItem(this.storageKey);
        return stored ? JSON.parse(stored) : [];
    }
    
    clear() {
        this.items = [];
        localStorage.removeItem(this.storageKey);
    }
}

const cart = new ShoppingCart();
cart.addItem({ id: 1, name: 'Product A', price: 50, quantity: 1 });
console.log(cart.items);
```

---

## 💡 Important Tips for CDAC Exam

✅ **LocalStorage persists** - Data survives page reload and browser restart
✅ **SessionStorage clears** - Data cleared when tab closes
✅ **JSON serialization** - Always stringify objects before storing
✅ **Storage limit** - 5-10MB per domain (varies by browser)
✅ **Storage events** - Listen across tabs/windows
✅ **Cookies security** - Use Secure and SameSite attributes
✅ **IndexedDB** - For large structured data (like offline databases)
