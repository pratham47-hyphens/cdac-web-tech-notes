# CSS3 & Styling

## 📋 Quick Cheat Sheet

### CSS Selectors
```css
/* Basic selectors */
p { }                    /* Element */
.class { }               /* Class */
#id { }                  /* ID */
[attr] { }               /* Attribute */

/* Combinators */
div p { }                /* Descendant */
div > p { }              /* Child */
div + p { }              /* Adjacent sibling */
div ~ p { }              /* General sibling */

/* Pseudo-classes */
a:hover { }              /* Hover state */
input:focus { }          /* Focus state */
li:first-child { }       /* First child */
li:nth-child(2n) { }     /* Even children */
```

### Box Model
```
┌─────────────────────────────┐
│        Margin               │
│  ┌─────────────────────────┐│
│  │    Border               ││
│  │  ┌─────────────────────┐││
│  │  │   Padding           │││
│  │  │ ┌─────────────────┐ │││
│  │  │ │   Content       │ │││
│  │  │ └─────────────────┘ │││
│  │  └─────────────────────┘││
│  └─────────────────────────┘│
└─────────────────────────────┘
```

---

## 📖 Detailed Explanation

### Flexbox (Flexible Box Layout)

**Container Properties:**
```css
.container {
    display: flex;                      /* Enable flexbox */
    flex-direction: row;                /* row, row-reverse, column, column-reverse */
    justify-content: center;            /* Horizontal alignment (flex-start, center, space-between, space-around) */
    align-items: center;                /* Vertical alignment */
    gap: 20px;                          /* Space between items */
    flex-wrap: wrap;                    /* Allow wrapping */
}
```

**Item Properties:**
```css
.item {
    flex: 1;                            /* Shorthand: flex-grow flex-shrink flex-basis */
    flex-grow: 1;                       /* Growth factor */
    flex-shrink: 1;                     /* Shrink factor */
    flex-basis: 200px;                  /* Base width/height */
    align-self: flex-end;               /* Override container alignment */
}
```

**Flexbox Layout Example:**
```html
<style>
    .navbar {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 1rem;
        background: #333;
    }
    
    .nav-brand { color: white; font-weight: bold; }
    
    .nav-links {
        display: flex;
        gap: 2rem;
        list-style: none;
        margin: 0;
    }
    
    .nav-links a {
        color: white;
        text-decoration: none;
    }
</style>

<nav class="navbar">
    <div class="nav-brand">MyApp</div>
    <ul class="nav-links">
        <li><a href="#">Home</a></li>
        <li><a href="#">About</a></li>
        <li><a href="#">Contact</a></li>
    </ul>
</nav>
```

### CSS Grid

**Container Properties:**
```css
.grid-container {
    display: grid;
    grid-template-columns: 1fr 2fr 1fr;  /* 3 columns with ratios */
    grid-template-rows: 100px 200px;     /* 2 rows with heights */
    gap: 20px;                           /* Space between items */
    grid-auto-flow: dense;               /* Auto placement */
}
```

**Grid Placement:**
```css
.grid-item {
    grid-column: 1 / 3;                 /* Span columns 1-3 */
    grid-row: 1 / 2;                    /* Span row 1 */
}
```

**Grid Template Areas:**
```css
.grid-layout {
    display: grid;
    grid-template-areas:
        "header header header"
        "sidebar main main"
        "footer footer footer";
    grid-template-columns: 200px 1fr 1fr;
    gap: 10px;
}

header { grid-area: header; }
main { grid-area: main; }
sidebar { grid-area: sidebar; }
footer { grid-area: footer; }
```

### CSS Animations & Transitions

**Transitions (smooth property changes):**
```css
.button {
    background: blue;
    transition: background 0.3s ease-in-out;  /* property duration timing-function */
}

.button:hover {
    background: red;
}
```

**Animations:**
```css
@keyframes slideIn {
    from {
        opacity: 0;
        transform: translateX(-100px);
    }
    to {
        opacity: 1;
        transform: translateX(0);
    }
}

.animated-box {
    animation: slideIn 1s ease-in-out forwards;
    animation-delay: 0.5s;              /* Delay before animation starts */
    animation-iteration-count: infinite; /* How many times to repeat */
}
```

**Transform Examples:**
```css
.box {
    /* 2D Transforms */
    transform: rotate(45deg);
    transform: scale(1.5);
    transform: translate(50px, 100px);
    transform: skew(10deg, 20deg);
    
    /* 3D Transforms */
    transform: rotateX(45deg);
    transform: rotateY(45deg);
    transform: perspective(1000px) rotateX(45deg);
}
```

### Responsive Design

**Mobile-First Approach:**
```css
/* Base styles (mobile) */
.container {
    font-size: 14px;
    padding: 10px;
}

/* Tablet */
@media (min-width: 768px) {
    .container {
        font-size: 16px;
        padding: 20px;
    }
}

/* Desktop */
@media (min-width: 1024px) {
    .container {
        font-size: 18px;
        padding: 30px;
        max-width: 1200px;
    }
}
```

**Media Query Features:**
```css
/* Device width */
@media (max-width: 600px) { }

/* Orientation */
@media (orientation: landscape) { }

/* Multiple conditions */
@media (min-width: 768px) and (max-width: 1024px) { }

/* Print styles */
@media print { }
```

### CSS Variables (Custom Properties)

```css
:root {
    --primary-color: #3498db;
    --secondary-color: #2ecc71;
    --spacing: 1rem;
}

.button {
    background: var(--primary-color);
    padding: var(--spacing);
}

.success {
    color: var(--secondary-color);
}
```

---

## 💡 Important Tips for CDAC Exam

✅ **Flexbox vs Grid** - Flexbox for 1D layouts, Grid for 2D layouts
✅ **Box-sizing** - Use `border-box` for predictable sizing
✅ **Responsive Design** - Always use media queries
✅ **Transform 3D** - Know perspective property for 3D effects
✅ **Animation Performance** - Use `transform` and `opacity` for smooth animations
✅ **Specificity** - ID > Class > Element (higher number wins)
