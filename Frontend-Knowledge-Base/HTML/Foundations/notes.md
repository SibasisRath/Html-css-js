# HTML Foundations

## Topic 1: HTML Structure & Document Semantics

### Deep-Dive Explanation

HTML (HyperText Markup Language) is the foundation of web pages. It uses a hierarchical structure with semantic elements that tell browsers and assistive technologies what content means, not just how it looks.

**Behind-the-Scenes:**
- The browser parses HTML top-to-bottom, building the DOM (Document Object Model) tree
- Semantic HTML elements (`<header>`, `<nav>`, `<section>`, `<article>`, `<footer>`) provide meaning to search engines, screen readers, and other assistive technologies
- The doctype declaration tells the browser which HTML version to expect
- Proper nesting prevents rendering issues and improves accessibility
- The DOM is a live object representation of your HTML that JavaScript can manipulate

### Code Examples

### Right Way ✅
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- Semantic structure guides users and machines -->
    <title>My Blog Post</title>
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
            <p>Content here</p>
        </article>
        <aside>
            <h2>Related Links</h2>
        </aside>
    </main>
    
    <footer>
        <p>&copy; 2026 My Site</p>
    </footer>
</body>
</html>
```

### Common Mistake ❌
```html
<!-- No doctype, improper semantic structure, divs everywhere -->
<html>
<head>
    <title>My Page</title>
</head>
<body>
    <div class="header">
        <div class="nav">
            <div>Navigation</div>
        </div>
    </div>
    
    <div class="content">
        <div class="article">
            <div class="title">Title</div>
            <div>Content</div>
        </div>
    </div>
    
    <div class="footer">Footer</div>
</body>
</html>
```

**Why it matters:** Semantic HTML is essential for accessibility, SEO, and maintainability. Screen readers rely on semantic elements to understand page structure.

### Practical Tasks

**Task 1:** Create a blog post page with proper semantic structure
- Include header with navigation
- Create a main article with a title, multiple paragraphs, and an aside
- Add a footer with author information
- Ensure all elements are properly nested

**Task 2:** Convert the "Common Mistake" example to proper semantic HTML
- Replace all unnecessary divs with semantic elements
- Add a doctype and proper head metadata
- Validate your HTML using the W3C Validator

**Task 3:** Build a restaurant website homepage
- Header with logo and navigation
- Hero section
- Menu section with semantic structure
- Testimonials section
- Footer with contact info

### Revision Mind Map

```
HTML Structure & Semantics
├── Document Setup
│   ├── <!DOCTYPE html>
│   ├── <html lang="en">
│   ├── <head> (metadata)
│   │   ├── <meta charset="UTF-8">
│   │   ├── <meta viewport>
│   │   └── <title>
│   └── <body>
├── Semantic Elements
│   ├── <header> - Top of page/section
│   ├── <nav> - Navigation links
│   ├── <main> - Main content
│   ├── <article> - Self-contained content
│   ├── <section> - Thematic grouping
│   ├── <aside> - Side content
│   └── <footer> - Bottom of page/section
└── Benefits
    ├── Better accessibility
    ├── Improved SEO
    └── Easier maintenance
```

---

## Topic 2: Forms & Input Elements

### Deep-Dive Explanation

Forms are how users interact with your application. HTML provides built-in form elements (`<input>`, `<select>`, `<textarea>`, etc.) that have native validation, accessibility features, and touch-optimized keyboards on mobile devices.

**Behind-the-Scenes:**
- Form submission sends data as `application/x-www-form-urlencoded` by default (key=value pairs)
- Each input needs a unique `name` attribute to be submitted (not the `id`)
- The `type` attribute determines how the input behaves and what keyboard appears on mobile
- Labels connected via `for` attribute improve accessibility and expand clickable area
- The browser can validate inputs before JavaScript gets involved using HTML5 validation attributes

### Code Examples

### Right Way ✅
```html
<form action="/submit" method="POST">
    <!-- Each form group wrapped with proper label -->
    <div class="form-group">
        <label for="username">Username:</label>
        <input 
            type="text" 
            id="username" 
            name="username" 
            required 
            minlength="3"
            aria-describedby="username-hint"
        >
        <small id="username-hint">3+ characters, alphanumeric only</small>
    </div>
    
    <div class="form-group">
        <label for="email">Email:</label>
        <input 
            type="email" 
            id="email" 
            name="email" 
            required
        >
        <!-- Browser validates email format automatically -->
    </div>
    
    <div class="form-group">
        <label for="password">Password:</label>
        <input 
            type="password" 
            id="password" 
            name="password" 
            required 
            minlength="8"
        >
    </div>
    
    <div class="form-group">
        <label for="country">Country:</label>
        <select id="country" name="country" required>
            <option value="">Select a country</option>
            <option value="us">United States</option>
            <option value="uk">United Kingdom</option>
            <option value="ca">Canada</option>
        </select>
    </div>
    
    <div class="form-group">
        <label for="bio">Bio:</label>
        <textarea 
            id="bio" 
            name="bio" 
            rows="4" 
            placeholder="Tell us about yourself"
        ></textarea>
    </div>
    
    <div class="form-group">
        <input 
            type="checkbox" 
            id="terms" 
            name="terms" 
            required
        >
        <label for="terms">I agree to the terms</label>
    </div>
    
    <button type="submit">Register</button>
    <button type="reset">Clear Form</button>
</form>
```

### Common Mistake ❌
```html
<!-- Missing labels, no validation, poor naming -->
<form>
    <input type="text" placeholder="Username">
    <input type="text" placeholder="Email">
    <input type="text" placeholder="Password">
    
    <!-- No label for checkboxes - small clickable area -->
    <input type="checkbox"> I agree
    
    <!-- No name attribute - won't submit -->
    <select id="country">
        <option>Pick one</option>
        <option value="us">USA</option>
    </select>
    
    <!-- Uses id instead of name for form data -->
    <textarea id="bio"></textarea>
    
    <!-- No submit type specified -->
    <button>Go</button>
</form>
```

**Why it matters:** Proper form structure enables browser validation, improves accessibility, and ensures data submission works correctly.

### Practical Tasks

**Task 1:** Create a contact form
- Include email, name, subject, and message fields
- Add form validation attributes (required, email type)
- Style the form with CSS
- Test that form submission works

**Task 2:** Build a user registration form
- Password and confirm password fields
- Email verification
- Dropdown for country selection
- Radio buttons for role selection (student/teacher)
- Terms checkbox
- Both submit and reset buttons

**Task 3:** Create a product filter form
- Search input
- Price range slider
- Category checkboxes (select multiple)
- Sort dropdown
- Filter button

### Revision Mind Map

```
HTML Forms
├── Form Element
│   ├── action="/path"
│   ├── method="GET|POST"
│   └── enctype="application/x-www-form-urlencoded"
├── Input Types
│   ├── text
│   ├── email (validates format)
│   ├── password (hides input)
│   ├── number (numeric keyboard)
│   ├── date (date picker)
│   ├── checkbox (multiple selections)
│   ├── radio (single selection)
│   └── file (file upload)
├── Input Attributes
│   ├── name (essential for data submission)
│   ├── id (for label connection)
│   ├── required (mandatory field)
│   ├── minlength/maxlength
│   ├── min/max (for number/date)
│   └── placeholder (hint text)
├── Other Elements
│   ├── <label for="id"> (improves accessibility)
│   ├── <select> (dropdown)
│   ├── <textarea> (multiline text)
│   ├── <button type="submit|reset|button">
│   └── <fieldset> (group related inputs)
└── Best Practices
    ├── Always use labels
    ├── Use proper input types
    ├── Include validation attributes
    ├── Add helpful hints with <small>
    └── Use fieldset for groups
```

---

## Topic 3: Attributes, IDs & Classes

### Deep-Dive Explanation

HTML attributes provide additional information about elements. The most important are `id` (unique identifier) and `class` (reusable classifier). Understanding when and how to use them is crucial for connecting HTML to CSS and JavaScript.

**Behind-the-Scenes:**
- `id` should be unique within a page - used for specific targeting in CSS and JavaScript
- `class` can be reused on many elements - used for styling groups of similar elements
- The `data-*` attribute stores custom data that JavaScript can access
- Global attributes like `title`, `aria-label` improve accessibility
- Attributes modify element behavior and provide metadata

### Code Examples

### Right Way ✅
```html
<!-- Clear, semantic naming conventions -->
<header id="main-header">
    <nav class="navigation">
        <ul class="nav-list">
            <li class="nav-item"><a href="/" class="nav-link">Home</a></li>
            <li class="nav-item"><a href="/about" class="nav-link">About</a></li>
        </ul>
    </nav>
</header>

<main>
    <!-- Use data-* for storing custom information -->
    <article class="post" data-post-id="123" data-category="tutorial">
        <h1 class="post-title">Learning HTML</h1>
        <p class="post-content">...</p>
        <!-- Multiple classes for flexible styling -->
        <button class="btn btn-primary btn-lg" aria-label="Read full article">
            Read More
        </button>
    </article>
    
    <!-- Card component reused with same class -->
    <div class="card">
        <img src="image.jpg" alt="Card image">
        <h2 class="card-title">Card Title</h2>
    </div>
    
    <div class="card">
        <img src="image2.jpg" alt="Card image">
        <h2 class="card-title">Another Card</h2>
    </div>
</main>
```

### Common Mistake ❌
```html
<!-- Vague naming, id for styling multiple elements, no semantic class names -->
<header id="header">
    <nav id="nav">
        <ul id="list">
            <li id="item1"><a id="link1">Home</a></li>
            <li id="item2"><a id="link2">About</a></li>
        </ul>
    </nav>
</header>

<main>
    <!-- Using id for multiple elements (non-unique) -->
    <article id="post">
        <h1 id="title">Learning HTML</h1>
        <p id="content">...</p>
        <!-- Unclear what this button does -->
        <button id="btn">Click</button>
    </article>
    
    <article id="post"><!-- Duplicate id! -->
        <h1 id="title">Another post</h1>
        <p id="content">...</p>
        <button id="btn">Click</button>
    </article>
</main>

<!-- No context for custom data -->
<div id="item" data-value="123"></div>
```

**Why it matters:** Proper naming makes code maintainable, prevents JavaScript conflicts, and allows CSS to efficiently target elements.

### Practical Tasks

**Task 1:** Refactor an existing HTML document
- Replace all single-letter or vague ids with descriptive ones
- Convert id-based styling to class-based
- Add semantic class names following BEM or similar convention
- Identify opportunities to use `data-*` attributes

**Task 2:** Create a product card component
- Use a class for reusable styling
- Include data attributes for product ID, price, and category
- Use proper semantic elements
- Create 3 instances of the same card with different data

**Task 3:** Build a navigation menu
- Use class names for styling different nav items
- Add an id to the main navigation for JavaScript targeting
- Include data attributes for tracking which is the active page
- Use aria-label for accessibility

### Revision Mind Map

```
HTML Attributes
├── id (unique)
│   ├── One per element
│   ├── Used in CSS (#id selector)
│   ├── Used in JavaScript (getElementById)
│   ├── Creates anchor links (#id)
│   └── Naming: kebab-case (main-header)
├── class (reusable)
│   ├── Multiple per element
│   ├── Used in CSS (.class selector)
│   └── Naming: kebab-case (nav-link)
├── data-* (custom data)
│   ├── Stores element-specific data
│   ├── Accessed via dataset in JavaScript
│   ├── Not visible to users
│   └── Example: data-post-id="123"
├── Global Attributes
│   ├── title (hover tooltip)
│   ├── aria-label (screen reader)
│   ├── role (accessibility role)
│   └── lang (language code)
└── Best Practices
    ├── Use id for unique elements
    ├── Use class for reusable styles
    ├── Use data-* for custom data
    └── Use aria-* for accessibility
```

---

## Quick Reference: Common HTML Elements

| Element | Purpose | Example |
|---------|---------|---------|
| `<h1>` to `<h6>` | Headings (h1 = most important) | `<h1>Main Title</h1>` |
| `<p>` | Paragraph | `<p>Text content</p>` |
| `<a>` | Link | `<a href="url">Link text</a>` |
| `<img>` | Image | `<img src="file.jpg" alt="description">` |
| `<ul>`, `<li>` | Unordered list | `<ul><li>Item</li></ul>` |
| `<ol>`, `<li>` | Ordered list | `<ol><li>Step 1</li></ol>` |
| `<button>` | Interactive button | `<button type="submit">Click</button>` |
| `<div>` | Generic container | `<div class="container">Content</div>` |
| `<span>` | Inline container | `<span class="highlight">text</span>` |
| `<strong>` | Important text | `<strong>Important</strong>` |
| `<em>` | Emphasized text | `<em>Emphasized</em>` |

---

## Helpful Resources

- [MDN: HTML Documentation](https://developer.mozilla.org/en-US/docs/Web/HTML)
- [W3C HTML Validator](https://validator.w3.org/)
- [WCAG Accessibility Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
