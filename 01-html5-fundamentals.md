# HTML5 Fundamentals

## 📋 Quick Cheat Sheet

### Basic HTML5 Structure
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Page Title</title>
</head>
<body>
    <!-- Content goes here -->
</body>
</html>
```

### Semantic HTML5 Elements
- `<header>` - Page or section header
- `<nav>` - Navigation links
- `<main>` - Main content
- `<article>` - Independent content (blog post, news)
- `<section>` - Thematic grouping
- `<aside>` - Sidebar/supplementary content
- `<footer>` - Footer content

### Important Meta Tags
```html
<meta charset="UTF-8">                          <!-- Character encoding -->
<meta name="viewport" content="width=device-width, initial-scale=1.0">  <!-- Responsive -->
<meta name="description" content="Page description">  <!-- SEO -->
```

---

## 📖 Detailed Explanation

### What is HTML5?
HTML5 is the latest version of Hypertext Markup Language, introducing:
- Semantic elements for better structure
- New form elements and validation
- Canvas and SVG for graphics
- Audio and video support
- Geolocation API
- Local storage capabilities

### Semantic HTML5 Elements

**Why use semantic elements?**
1. Better accessibility for screen readers
2. Improved SEO
3. Cleaner, more readable code
4. Better for responsive design

**Example of semantic structure:**
```html
<header>
    <nav>
        <ul>
            <li><a href="/">Home</a></li>
            <li><a href="/about">About</a></li>
        </ul>
    </nav>
</header>

<main>
    <article>
        <h1>Blog Post Title</h1>
        <p>Article content...</p>
    </article>
    
    <aside>
        <h3>Related Links</h3>
        <ul>
            <li><a href="#">Link 1</a></li>
        </ul>
    </aside>
</main>

<footer>
    <p>&copy; 2026 My Website</p>
</footer>
```

### HTML5 Form Elements

```html
<form>
    <!-- Text inputs -->
    <input type="text" placeholder="Regular text">
    <input type="email" placeholder="Email address" required>
    <input type="password" placeholder="Password">
    
    <!-- Number and range -->
    <input type="number" min="1" max="100">
    <input type="range" min="0" max="100">
    
    <!-- Date and time -->
    <input type="date">
    <input type="time">
    <input type="datetime-local">
    
    <!-- Color and file -->
    <input type="color">
    <input type="file" accept="image/*">
    
    <!-- Dropdown -->
    <select>
        <option>Choose option</option>
        <option>Option 1</option>
        <option>Option 2</option>
    </select>
    
    <!-- Textarea -->
    <textarea rows="4" cols="50"></textarea>
    
    <!-- Buttons -->
    <button type="submit">Submit</button>
    <button type="reset">Reset</button>
    <button type="button">Click Me</button>
</form>
```

### HTML5 Data Attributes

Store custom data in HTML elements:
```html
<div data-user-id="123" data-role="admin">User Info</div>
```

Access in JavaScript:
```javascript
const div = document.querySelector('div');
console.log(div.dataset.userId);  // "123"
console.log(div.dataset.role);    // "admin"
```

### HTML5 Graphics

**Canvas (pixel-based drawing):**
```html
<canvas id="myCanvas" width="400" height="300"></canvas>

<script>
const canvas = document.getElementById('myCanvas');
const ctx = canvas.getContext('2d');

// Draw rectangle
ctx.fillStyle = 'blue';
ctx.fillRect(50, 50, 150, 100);

// Draw circle
ctx.fillStyle = 'red';
ctx.beginPath();
ctx.arc(300, 150, 50, 0, Math.PI * 2);
ctx.fill();
</script>
```

**SVG (vector-based):**
```html
<svg width="200" height="200">
    <circle cx="100" cy="100" r="80" fill="blue"/>
    <rect x="20" y="20" width="160" height="160" fill="none" stroke="red" stroke-width="2"/>
</svg>
```

### HTML5 Media Elements

```html
<!-- Audio -->
<audio controls>
    <source src="audio.mp3" type="audio/mpeg">
    Your browser doesn't support audio
</audio>

<!-- Video -->
<video width="320" height="240" controls>
    <source src="video.mp4" type="video/mp4">
    Your browser doesn't support video
</video>
```

---

## 💡 Important Tips for CDAC Exam

✅ **Know semantic elements** - They're heavily tested
✅ **Remember DOCTYPE** - Always use `<!DOCTYPE html>` for HTML5
✅ **Meta viewport** - Essential for responsive design questions
✅ **Form validation** - HTML5 provides built-in validation
✅ **Accessibility** - Semantic HTML improves screen reader compatibility
✅ **Canvas vs SVG** - Canvas for animations, SVG for scalable graphics
