# DOM & Events

## 📋 Quick Cheat Sheet

### DOM Selectors
```javascript
// Single element
document.getElementById('myId');           // By ID
document.querySelector('.myClass');         // CSS selector
document.querySelector('#id > .class');     // Complex selector

// Multiple elements
document.getElementsByClassName('myClass'); // Returns HTMLCollection
document.getElementsByTagName('p');         // Returns HTMLCollection
document.querySelectorAll('.myClass');      // Returns NodeList (better)

// Difference: querySelector(All) returns NodeList, others return HTMLCollection
// NodeList has forEach, HTMLCollection doesn't
```

### DOM Traversal
```javascript
const element = document.getElementById('myElement');

// Parent
element.parentElement;      // Direct parent
element.parentNode;         // Parent (node)
element.closest('.class');  // Closest ancestor with class

// Children
element.children;           // HTMLCollection of child elements
element.childNodes;         // All child nodes (includes text nodes)
element.firstElementChild;  // First child element
element.lastElementChild;   // Last child element
element.firstChild;         // First node (may be text)

// Siblings
element.nextElementSibling;  // Next sibling element
element.previousElementSibling; // Previous sibling element
element.nextSibling;         // Next sibling node
```

### DOM Manipulation
```javascript
const div = document.createElement('div');
div.textContent = 'Hello';
div.innerHTML = '<p>Hello</p>';
div.className = 'my-class';
div.id = 'my-id';
div.style.color = 'red';
div.setAttribute('data-value', '123');

parent.appendChild(div);     // Add to end
parent.insertBefore(div, sibling); // Insert before
parent.replaceChild(newChild, oldChild); // Replace
element.remove();            // Remove element
parent.removeChild(element); // Remove child
```

---

## 📖 Detailed Explanation

### DOM Tree Structure

```
Document
└── html
    ├── head
    │   ├── meta
    │   ├── title
    │   └── link
    └── body
        ├── header
        │   └── nav
        │       └── ul
        │           ├── li
        │           └── li
        ├── main
        │   ├── article
        │   └── aside
        └── footer
```

### Event Flow

```
Event Capturing (top to bottom)
window → document → body → ... → target
↓
Target Phase (on element itself)
↓
Event Bubbling (bottom to top)
target → ... → body → document → window
```

**Controlling event flow:**
```javascript
element.addEventListener('click', handler, true);  // Capturing phase
element.addEventListener('click', handler, false); // Bubbling phase (default)
element.addEventListener('click', handler);        // Bubbling (default)
```

### Complete Event Example

```html
<html>
<body>
    <div class="container" id="container">
        <button id="btn">Click me</button>
    </div>
    
    <script>
        const btn = document.getElementById('btn');
        const container = document.getElementById('container');
        
        // Event on button (target)
        btn.addEventListener('click', (event) => {
            console.log('Button clicked');
            console.log('event.target:', event.target);      // <button>
            console.log('event.currentTarget:', event.currentTarget); // <button>
        });
        
        // Event on container (parent - capturing)
        container.addEventListener('click', (event) => {
            console.log('Container clicked (capturing)');
        }, true);
        
        // Event on container (parent - bubbling)
        container.addEventListener('click', (event) => {
            console.log('Container clicked (bubbling)');
        });
        
        // Event on window
        window.addEventListener('click', (event) => {
            console.log('Window clicked');
        });
        
        // Stop propagation
        btn.addEventListener('click', (event) => {
            event.stopPropagation(); // Prevent bubbling to container/window
        });
    </script>
</body>
</html>
```

### DOM Lifecycle Events

```javascript
// DOM Content Loaded
document.addEventListener('DOMContentLoaded', () => {
    console.log('DOM fully parsed');
    // Safe to manipulate DOM here
});

// Window Load (all resources loaded)
window.addEventListener('load', () => {
    console.log('All resources loaded (images, styles, etc)');
});

// Before Unload
window.addEventListener('beforeunload', (event) => {
    event.preventDefault();
    event.returnValue = ''; // Show confirmation dialog
});

// Unload
window.addEventListener('unload', () => {
    console.log('Page unloading');
});
```

### Keyboard Events

```javascript
document.addEventListener('keydown', (event) => {
    console.log('Key pressed:', event.key);     // Character typed
    console.log('Key code:', event.code);       // Physical key
    console.log('Shift pressed:', event.shiftKey);
    console.log('Ctrl pressed:', event.ctrlKey);
    console.log('Alt pressed:', event.altKey);
});

document.addEventListener('keyup', (event) => {
    console.log('Key released:', event.key);
});

// Example: Detect Enter key
input.addEventListener('keypress', (event) => {
    if (event.key === 'Enter') {
        console.log('Enter pressed');
    }
});
```

### Form Events

```javascript
const form = document.getElementById('myForm');
const input = document.getElementById('username');

// Form submission
form.addEventListener('submit', (event) => {
    event.preventDefault(); // Prevent default form submission
    const formData = new FormData(form);
    console.log(formData.get('username'));
});

// Input changes
input.addEventListener('change', (event) => {
    console.log('Changed to:', event.target.value);
});

input.addEventListener('input', (event) => {
    console.log('Input:', event.target.value); // Triggers on every keystroke
});

// Focus events
input.addEventListener('focus', (event) => {
    console.log('Input focused');
});

input.addEventListener('blur', (event) => {
    console.log('Input lost focus');
});
```

---

## 💡 Important Tips for CDAC Exam

✅ **Event Delegation** - Use for dynamic elements
✅ **Event Flow** - Know capturing vs bubbling
✅ **preventDefault vs stopPropagation** - Know the difference
✅ **Event Target** - Remember target vs currentTarget
✅ **DOM Methods** - QuerySelector is preferred over getElement*
✅ **DOMContentLoaded** - Use instead of load for faster execution
