# HTML5 Fundamentals

## 🎯 Quick Cheat Sheet

| Concept | Key Points |
|---------|-----------|
| **Semantic HTML** | Use `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<footer>` for better structure |
| **HTML5 DOCTYPE** | `<!DOCTYPE html>` - simple and standard for HTML5 |
| **Attributes** | `id`, `class`, `data-*`, `aria-*` for accessibility |
| **Forms** | Input types: `text`, `email`, `password`, `number`, `date`, `file`, `checkbox`, `radio` |
| **New Elements** | `<canvas>`, `<video>`, `<audio>`, `<svg>`, `<progress>`, `<meter>` |
| **Validation** | HTML5 provides built-in validation (required, pattern, min, max) |

---

## 📖 Detailed Explanation

### 1. HTML5 Document Structure

HTML5 introduces semantic elements that clearly define different parts of content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document Title</title>
    <meta name="description" content="Page description for SEO">
</head>
<body>
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
            <h1>Article Title</h1>
            <section>
                <h2>Section 1</h2>
                <p>Content here...</p>
            </section>
        </article>

        <aside>
            <h2>Related Links</h2>
        </aside>
    </main>

    <footer>
        <p>&copy; 2026 Company. All rights reserved.</p>
    </footer>
</body>
</html>
```

**Key Semantic Elements:**
- `<header>` - Introductory content or navigation
- `<nav>` - Navigation links
- `<main>` - Main content of the page (only one per page)
- `<article>` - Self-contained content
- `<section>` - Thematic grouping of content
- `<aside>` - Sidebar or related content
- `<footer>` - Footer information

### 2. HTML5 Forms

HTML5 provides built-in validation and new input types:

```html
<form action="/submit" method="POST">
    <!-- Text input -->
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required>

    <!-- Email input with validation -->
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>

    <!-- Number input with range -->
    <label for="age">Age:</label>
    <input type="number" id="age" name="age" min="1" max="120">

    <!-- Date input -->
    <label for="dob">Date of Birth:</label>
    <input type="date" id="dob" name="dob">

    <!-- Password input -->
    <label for="password">Password:</label>
    <input type="password" id="password" name="password" 
           pattern="(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{8,}" 
           title="Must contain uppercase, lowercase, and numbers">

    <!-- File input -->
    <label for="file">Upload:</label>
    <input type="file" id="file" name="file" accept=".pdf,.doc,.docx">

    <!-- Checkbox -->
    <input type="checkbox" id="terms" name="terms" required>
    <label for="terms">I agree to terms</label>

    <!-- Radio buttons -->
    <fieldset>
        <legend>Choose an option:</legend>
        <input type="radio" id="opt1" name="option" value="1">
        <label for="opt1">Option 1</label>
        <input type="radio" id="opt2" name="option" value="2">
        <label for="opt2">Option 2</label>
    </fieldset>

    <!-- Select dropdown -->
    <label for="country">Country:</label>
    <select id="country" name="country">
        <option value="">Select...</option>
        <option value="in">India</option>
        <option value="us">USA</option>
        <option value="uk">UK</option>
    </select>

    <!-- Textarea -->
    <label for="message">Message:</label>
    <textarea id="message" name="message" rows="5" cols="40"></textarea>

    <!-- Submit button -->
    <button type="submit">Submit</button>
    <button type="reset">Reset</button>
    <button type="button">Cancel</button>
</form>
```

**Form Input Types:**
- `text` - Single line text
- `email` - Email validation
- `password` - Masked input
- `number` - Numeric input
- `range` - Slider
- `date` - Date picker
- `time` - Time picker
- `file` - File upload
- `checkbox` - Multiple selections
- `radio` - Single selection
- `submit` - Submit button
- `reset` - Reset form
- `button` - Custom button

### 3. HTML5 Attributes

```html
<!-- Global attributes -->
<div id="unique-id" class="class1 class2" data-user-id="123">
    Content
</div>

<!-- Data attributes (accessible via JavaScript) -->
<button data-action="delete" data-id="42">Delete</button>

<!-- ARIA attributes for accessibility -->
<button aria-label="Close menu" aria-expanded="false">X</button>

<!-- Boolean attributes -->
<input type="checkbox" checked disabled>
<video controls autoplay muted loop></video>
```

### 4. HTML5 Media Elements

```html
<!-- Audio element -->
<audio controls>
    <source src="audio.mp3" type="audio/mpeg">
    <source src="audio.ogg" type="audio/ogg">
    Your browser does not support audio.
</audio>

<!-- Video element -->
<video width="640" height="480" controls poster="poster.jpg">
    <source src="video.mp4" type="video/mp4">
    <source src="video.webm" type="video/webm">
    Your browser does not support video.
</video>

<!-- Canvas for drawing -->
<canvas id="myCanvas" width="400" height="400"></canvas>

<!-- SVG for scalable graphics -->
<svg width="100" height="100">
    <circle cx="50" cy="50" r="40" fill="blue" />
</svg>
```

### 5. Progress and Meter Elements

```html
<!-- Progress bar -->
<label for="progress">Download:</label>
<progress id="progress" max="100" value="70"></progress>

<!-- Meter (gauge) -->
<label for="score">Score:</label>
<meter id="score" min="0" max="100" value="75" low="40" high="80"></meter>
```

---

## 💡 Important Tips for CDAC Exam

1. **Always use semantic HTML** - It improves SEO and accessibility
2. **Form validation** - HTML5 provides client-side validation; don't rely on it alone
3. **Accessibility** - Use proper labels, ARIA attributes, and semantic elements
4. **Responsive design** - Use `<meta name="viewport">` for mobile devices
5. **DOCTYPE declaration** - Always include `<!DOCTYPE html>` at the start
6. **Character encoding** - Always specify `<meta charset="UTF-8">`
7. **Data attributes** - Use `data-*` for storing custom data in HTML
8. **Form groups** - Use `<fieldset>` and `<legend>` for grouped form elements

---

## 🎓 Key Concepts to Remember

- **HTML5** is the current standard for markup
- **Semantic elements** improve structure and SEO
- **Form validation** is built-in but should also be validated server-side
- **Media elements** (`<video>`, `<audio>`, `<canvas>`) are native without plugins
- **Accessibility** is crucial - use ARIA attributes and semantic HTML
