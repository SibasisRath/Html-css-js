# HTML Advanced

## Topic 1: Accessibility (a11y) & ARIA

### Deep-Dive Explanation

Accessibility ensures your website works for everyone, including people with disabilities. ARIA (Accessible Rich Internet Applications) attributes help assistive technologies like screen readers understand complex interfaces. Semantic HTML is the foundation - ARIA enhances it.

**Behind-the-Scenes:**
- Screen readers announce elements based on their semantic meaning and ARIA roles
- The accessibility tree is built from HTML elements and ARIA attributes
- Every interactive component needs a way for users to activate it (keyboard + mouse)
- Color alone should never convey information (add text/icons)
- Focus management helps keyboard-only users navigate your site
- Alt text for images is metadata, not a "nice-to-have"

### Code Examples

### Right Way ✅
```html
<!-- Semantic HTML + ARIA for complex interactive elements -->
<div role="search">
    <label for="search-input">Search articles:</label>
    <input 
        id="search-input" 
        type="search" 
        placeholder="Type keyword..."
        aria-describedby="search-help"
    >
    <small id="search-help">Press Enter to search or Tab to filter</small>
</div>

<!-- Accessible dropdown menu using ARIA -->
<nav>
    <button 
        id="menu-button"
        aria-expanded="false" 
        aria-controls="menu-list"
        aria-label="Toggle navigation menu"
    >
        Menu ▼
    </button>
    
    <ul id="menu-list" role="menu" aria-labelledby="menu-button" hidden>
        <li role="none">
            <a href="/" role="menuitem">Home</a>
        </li>
        <li role="none">
            <a href="/products" role="menuitem">Products</a>
        </li>
    </ul>
</nav>

<!-- Image with proper alt text -->
<figure>
    <!-- Alt text describes the image content, not "image of" -->
    <img 
        src="chart.png" 
        alt="Sales increased 30% from Q1 to Q2 2026"
    >
    <figcaption>Quarterly sales comparison</figcaption>
</figure>

<!-- Video with captions and transcripts -->
<video controls aria-labelledby="video-title">
    <source src="tutorial.mp4" type="video/mp4">
    <track kind="captions" src="captions-en.vtt" srclang="en" label="English">
    <!-- This text displays if video format unsupported -->
    Your browser doesn't support HTML5 video. 
    <a href="transcript.txt">Read the transcript</a>
</video>

<!-- Live region for dynamic content updates -->
<div 
    role="status" 
    aria-live="polite" 
    aria-atomic="true"
    id="notifications"
>
    <!-- Screen reader announces changes here -->
</div>

<!-- Landmark regions help keyboard users navigate -->
<header role="banner">
    <h1>Site Title</h1>
</header>

<nav role="navigation" aria-label="Main navigation">
    <!-- Navigation content -->
</nav>

<main role="main">
    <!-- Main content -->
</main>

<aside role="complementary" aria-label="Sidebar">
    <!-- Sidebar content -->
</aside>

<footer role="contentinfo">
    <!-- Footer content -->
</footer>
```

### Common Mistake ❌
```html
<!-- No semantic structure, images with no alt text -->
<div id="header">
    <div id="navigation">
        <span onclick="toggleMenu()">Menu</span>
        <div id="menu" style="display:none;">
            <span onclick="navigate('/')">Home</span>
            <span onclick="navigate('/about')">About</span>
        </div>
    </div>
</div>

<!-- No alt text, not accessible -->
<img src="chart.png">

<!-- Color alone conveys information -->
<p>
    <span style="color: red;">Error</span>: Password is weak
    <!-- No text or icon, just color -->
</p>

<!-- Dynamic content updated with no screen reader announcement -->
<div id="notifications"></div>

<!-- Click-only interactive element, no keyboard support -->
<div id="button" onclick="submitForm()">Submit</div>

<!-- Video with no captions -->
<video src="tutorial.mp4" controls></video>
```

**Why it matters:** Accessibility is both ethical and legally required (ADA, WCAG). It benefits everyone - captions help in noisy environments, large text helps with readability, etc.

### Practical Tasks

**Task 1:** Make an existing website accessible
- Add proper alt text to all images (describe content, not "image of")
- Add semantic HTML elements where divs exist
- Identify interactive elements and ensure they're keyboard accessible
- Test with Tab key navigation
- Test with a screen reader (like NVDA on Windows)

**Task 2:** Create an accessibly hidden menu
- Build a hamburger menu that works with keyboard (Enter/Space to open)
- Manage focus properly (trap focus inside menu when open)
- Use ARIA attributes (`aria-expanded`, `aria-controls`)
- Close when user presses Escape key

**Task 3:** Build a data table with proper accessibility
- Use `<table>`, `<thead>`, `<tbody>`, `<th>`, `<td>` semantic elements
- Use `scope` attribute on headers (row/col)
- Add a `<caption>` describing the table
- Use `aria-colcount` and `aria-rowcount` for large tables
- Make sortable columns keyboard accessible

### Revision Mind Map

```
Accessibility (a11y)
├── Foundation: Semantic HTML
│   ├── <header>, <nav>, <main>, <footer>
│   ├── <article>, <section>, <aside>
│   └── <img alt="description">
├── ARIA Attributes
│   ├── role (defines element purpose)
│   ├── aria-label (text for screen readers)
│   ├── aria-expanded (collapsible state)
│   ├── aria-controls (links button to element)
│   ├── aria-live (announces dynamic changes)
│   ├── aria-describedby (detailed description)
│   └── aria-hidden (hides from screen readers)
├── Keyboard Navigation
│   ├── All interactive elements keyboard accessible
│   ├── Logical focus order (Tab key)
│   ├── Focus indicators visible
│   └── Escape key closes menus
├── Visual Design
│   ├── Color + text (never color alone)
│   ├── Sufficient contrast ratios (4.5:1)
│   ├── Resizable text
│   └── No flashing (3+ times/second)
└── Media
    ├── Captions for video
    ├── Transcripts for audio
    ├── Descriptions for images
    └── Controls for playback
```

---

## Topic 2: Meta Tags & SEO Fundamentals

### Deep-Dive Explanation

Meta tags provide metadata about your HTML document. They don't display on the page but inform browsers, search engines, and social media platforms how to handle your content. Search engines use meta tags to understand your page's content and rank it appropriately.

**Behind-the-Scenes:**
- The `<title>` tag is your first impression in search results and browser tabs
- `description` meta tag appears below the title in search results
- `keywords` meta tag has lost importance but some systems use it
- OpenGraph tags control how your content appears when shared on social media
- `viewport` meta tag tells mobile browsers how to scale content
- robots meta tag instructs search engines on crawling/indexing

### Code Examples

### Right Way ✅
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Character encoding must be first -->
    <meta charset="UTF-8">
    
    <!-- Essential for mobile devices -->
    <meta 
        name="viewport" 
        content="width=device-width, initial-scale=1.0"
    >
    
    <!-- Concise, keyword-rich title (50-60 chars) -->
    <title>Professional Web Design | XYZ Company</title>
    
    <!-- Compelling description (150-160 chars) for search results -->
    <meta 
        name="description" 
        content="Stunning websites that convert. Expert web design services for small businesses. 10+ years experience."
    >
    
    <!-- Keywords (less important, but helpful) -->
    <meta 
        name="keywords" 
        content="web design, web development, responsive design, small business"
    >
    
    <!-- Prevent indexing of sample/test pages -->
    <meta name="robots" content="noindex, nofollow">
    <!-- Or for public pages: index, follow -->
    
    <!-- Social media sharing (OpenGraph) -->
    <meta property="og:type" content="website">
    <meta property="og:url" content="https://example.com/article">
    <meta property="og:title" content="How to Build Fast Websites">
    <meta property="og:description" content="Learn the secrets to 100% Google Lighthouse scores...">
    <meta property="og:image" content="https://example.com/image.jpg">
    
    <!-- Twitter Card -->
    <meta name="twitter:card" content="summary_large_image">
    <meta name="twitter:site" content="@yourhandle">
    <meta name="twitter:title" content="How to Build Fast Websites">
    <meta name="twitter:description" content="Learn the secrets...">
    <meta name="twitter:image" content="https://example.com/image.jpg">
    
    <!-- Author and copyright -->
    <meta name="author" content="Jane Doe">
    <meta name="copyright" content="2026 XYZ Company">
    
    <!-- Canonical URL (for duplicate content on multiple URLs) -->
    <link rel="canonical" href="https://example.com/main-article">
    
    <!-- Favicon -->
    <link rel="icon" type="image/x-icon" href="/favicon.ico">
    
    <!-- Stylesheets -->
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <!-- Content -->
</body>
</html>
```

### Common Mistake ❌
```html
<head>
    <!-- Meta tags in wrong order -->
    <title>Untitled Document</title>
    <!-- No description, search engines create a generic one -->
    
    <!-- No viewport - mobile users see zoomed-out desktop view -->
    
    <!-- Title too long and keyword-stuffed -->
    <title>Web Design Services | Web Development | Responsive Design | Small Business | Best Price</title>
    
    <!-- Description too short or missing keywords -->
    <meta name="description" content="My website">
    
    <!-- No OpenGraph tags - sharing on social media looks terrible -->
    
    <!-- Duplicate content not marked with canonical -->
    
    <!-- Missing favicon -->
    
    <!-- Random meta tags that provide no value -->
    <meta name="foo" content="bar">
</head>
```

**Why it matters:** Good meta tags improve SEO rankings, social sharing appearance, and phone storage of your site (favicon).

### Practical Tasks

**Task 1:** Optimize a website's meta tags
- Write a compelling title (50-60 chars)
- Create a description (150-160 chars) with primary keyword
- Add OpenGraph tags for social sharing
- Add Twitter Card tags
- Set a canonical URL if applicable
- Test sharing on Facebook, LinkedIn, Twitter

**Task 2:** Create SEO-optimized pages for a portfolio site
- Home page with company overview
- Services page describing what you offer
- Blog post page with article content
- Contact page
- Ensure unique, compelling titles and descriptions for each

**Task 3:** Audit a website's meta tags
- Collect all pages from a site (10+)
- Record their titles and descriptions
- Check if they're unique and keyword-focused
- Identify pages missing descriptions
- Create a list of improvements

### Revision Mind Map

```
Meta Tags & SEO
├── Essential Tags
│   ├── <meta charset="UTF-8">
│   ├── <meta name="viewport" ...>
│   ├── <title> (50-60 chars)
│   └── <meta name="description"> (150-160 chars)
├── Search Engine Tags
│   ├── <meta name="robots"> (index/noindex)
│   ├── <link rel="canonical"> (prevent duplicates)
│   └── <meta name="keywords"> (less important)
├── Social Media (OpenGraph)
│   ├── og:type, og:url, og:title
│   ├── og:description, og:image
│   └── Twitter Card (twitter:card, twitter:title, ...)
├── Author & Branding
│   ├── <meta name="author">
│   ├── <link rel="icon"> (favicon)
│   └── <meta name="theme-color">
└── Best Practices
    ├── Unique title per page
    ├── Keyword-rich description
    ├── Use canonical URLs
    ├── High-quality OpenGraph images
    └── Mobile-optimized viewport
```

---

## Topic 3: Performance & Web Vitals

### Deep-Dive Explanation

HTML doesn't just structure content - it affects how fast your site loads. Code splitting, lazy loading, and resource hints tell the browser how to prioritize data. Optimizing HTML improves Core Web Vitals scores, which Google uses for ranking.

**Behind-the-Scenes:**
- Images are often the biggest asset - lazy loading delays loading until they're needed
- Render-blocking resources (CSS, JavaScript) delay First Contentful Paint
- DNS prefetch and preconnect reduce latency for cross-origin requests
- `async` and `defer` attributes control JavaScript loading timing
- Viewport size and DPR affect image resolution needed
- Compression (gzip, brotli) reduces file size dramatically

### Code Examples

### Right Way ✅
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fast Loading Website</title>
    
    <!-- DNS prefetch for external services -->
    <link rel="dns-prefetch" href="https://cdn.example.com">
    <link rel="dns-prefetch" href="https://api.thirdparty.com">
    
    <!-- Preconnect for critical cross-origin resources -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    
    <!-- Critical CSS (above the fold) -->
    <style>
        /* Minimal critical CSS for hero section */
        body { margin: 0; font-family: system-ui; }
        .hero { background: blue; color: white; padding: 20px; }
    </style>
    
    <!-- Load non-critical CSS asynchronously -->
    <link rel="stylesheet" href="styles.css" media="print" onload="this.media='all'">
    <noscript><link rel="stylesheet" href="styles.css"></noscript>
</head>
<body>
    <header class="hero">
        <h1>Welcome</h1>
    </header>
    
    <main>
        <!-- Lazy load images - don't load until user scrolls near them -->
        <img 
            src="placeholder.jpg" 
            data-src="real-image.jpg"
            alt="Product photo"
            loading="lazy"
            width="400"
            height="300"
        >
        
        <!-- Responsive images for different screen sizes -->
        <picture>
            <source srcset="image-mobile.jpg" media="(max-width: 600px)">
            <source srcset="image-tablet.jpg" media="(max-width: 1200px)">
            <img src="image-desktop.jpg" alt="Responsive image">
        </picture>
        
        <!-- WebP modern format with fallback -->
        <picture>
            <source srcset="image.webp" type="image/webp">
            <img src="image.jpg" alt="Image with modern format">
        </picture>
    </main>
    
    <!-- Defer non-critical JavaScript to not block rendering -->
    <script src="tracking.js" defer></script>
    
    <!-- Load critical JavaScript synchronously only if needed -->
    <script src="critical.js"></script>
    
    <!-- Async for independent scripts that can load anytime -->
    <script src="analytics.js" async></script>
</body>
</html>
```

### Common Mistake ❌
```html
<head>
    <title>Slow Website</title>
    
    <!-- Multiple unoptimized images -->
    <link rel="stylesheet" href="styles1.css">
    <link rel="stylesheet" href="styles2.css">
    <link rel="stylesheet" href="styles3.css">
    
    <!-- Heavy JavaScript in head blocks rendering -->
    <script src="jquery.js"></script>
    <script src="bootstrap.js"></script>
    <script src="analytics.js"></script>
    <script src="ads.js"></script>
</head>
<body>
    <!-- Massive images with no optimization -->
    <img src="huge-image.png" width="5000" height="3000" alt="Big image">
    <img src="huge-image2.png" alt="Another big image">
    
    <!-- More render-blocking JavaScript at end -->
    <script src="more-scripts.js"></script>
</body>
```

**Why it matters:** Fast sites have better SEO ranking, lower bounce rates, and higher conversion. Every 100ms delay costs users.

### Practical Tasks

**Task 1:** Optimize images for web  
- Find non-optimized images (>200KB each)
- Convert to modern formats (WebP with JPEG fallback)
- Implement responsive images using `<picture>` and `srcset`
- Add `loading="lazy"` to below-the-fold images
- Measure file size reduction

**Task 2:** Improve HTML loading performance
- Identify render-blocking resources
- Move non-critical CSS to `media="print"` and async-load
- Defer or async JavaScript where possible
- Add DNS prefetch and preconnect for external resources
- Measure First Contentful Paint improvement

**Task 3:** Implement a resource loading strategy
- Critical content loads first and synchronously
- Above-the-fold images use responsive images
- Below-the-fold images lazy load
- Analytics scripts load async
- Ads load deferred
- Create a checklist for future projects

### Revision Mind Map

```
HTML Performance
├── Loading Strategy
│   ├── Critical path resources (sync)
│   ├── Important resources (preload/prefetch)
│   ├── Nice-to-have (defer/async)
│   └── Non-essential (lazy load)
├── Images
│   ├── Responsive images (srcset, <picture>)
│   ├── Modern formats (WebP + fallback)
│   ├── Lazy loading (loading="lazy")
│   ├── Proper dimensions (width/height)
│   └── Descriptive alt text
├── CSS
│   ├── Critical CSS inline in <style>
│   ├── Non-critical async (media="print" trick)
│   └── No @import (slower)
├── JavaScript
│   ├── Async (independent scripts)
│   ├── Defer (dependent on DOM)
│   ├── No <script> in <head>
│   └── Minimize render-blocking JS
├── Cross-Origin Resources
│   ├── dns-prefetch (resolve domain early)
│   ├── preconnect (resolve + TLS handshake)
│   ├── prefetch (low-priority resource)
│   └── preload (high-priority resource)
└── Web Vitals (Google Metrics)
    ├── LCP: Largest Contentful Paint
    ├── FID: First Input Delay
    └── CLS: Cumulative Layout Shift
```

---

## Quick Reference: Common Advanced Patterns

### Progressive Enhancement
```html
<!-- JavaScript enhances user experience, not required for functionality -->
<button onclick="optimized()" id="form-submit">
    Submit
</button>
<noscript>
    <form method="POST" action="/submit">
        <!-- Fallback form for users without JS -->
        <button type="submit">Submit</button>
    </form>
</noscript>
```

### Graceful Degradation
```html
<!-- Modern browser features with fallbacks -->
<video controls poster="poster.jpg">
    <source src="video.webm" type="video/webm">
    <source src="video.mp4" type="video/mp4">
    <p>Your browser doesn't support HTML5 video</p>
</video>
```

### Testing Accessibility
- WAVE Browser Extension
- Axe DevTools
- Screen reader testing (NVDA, JAWS)
- Lighthouse (built into Chrome DevTools)
- WebAIM contrast checker

---

## Helpful Resources

- [MDN: HTML Documentation](https://developer.mozilla.org/en-US/docs/Web/HTML)
- [Web.dev: Core Web Vitals](https://web.dev/vitals/)
- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [WebAIM: Accessibility Articles](https://webaim.org/)
- [PageSpeed Insights](https://pagespeed.web.dev/)
