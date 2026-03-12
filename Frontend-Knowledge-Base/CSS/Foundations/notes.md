# CSS Foundations

## Topic 1: CSS Box Model & Layout Fundamentals

### Deep-Dive Explanation

The CSS Box Model is the foundation of all layouts. Every element is a box with content, padding, border, and margin. Understanding how these layers interact is essential for controlling spacing and sizing.

**Behind-the-Scenes:**
- Content box is where text/images live
- Padding is inside the border, creates space inside the element
- Border surrounds the padding
- Margin is outside the border, creates space between elements
- `box-sizing: border-box` includes padding + border in the element's width/height (more intuitive)
- By default (`box-sizing: content-box`), padding and border are added to width
- Vertical margins collapse - only the largest margin is used (confuses many)
- Horizontal margins never collapse

### Code Examples

### Right Way ✅
```css
/* Use border-box for intuitive sizing */
* {
    box-sizing: border-box;
}

/* Clear spacing model - easy to predict */
.card {
    width: 300px;
    padding: 20px;        /* Internal spacing */
    border: 1px solid #ccc;
    margin: 10px;         /* External spacing */
    /* Total width is 300px, not 300 + 20 + 1 + 20 + 1 */
}

/* Padding: T R B L shorthand */
.box {
    padding: 20px;              /* All sides 20px */
    padding: 20px 10px;         /* Top/Bottom 20px, Left/Right 10px */
    padding: 10px 20px 30px;    /* Top 10px, L/R 20px, Bottom 30px */
    padding: 10px 20px 30px 40px; /* Top, Right, Bottom, Left */
}

/* Margin auto centers block elements */
.centered {
    width: 80%;
    margin: 0 auto;  /* 0 top/bottom, auto left/right */
}

/* Handle margin collapse deliberately */
.container > * + * {
    margin-top: 20px;  /* Space between items (not first item) */
}

/* Understand the visual box */
.element {
    width: 200px;
    padding: 10px;    /* 20px total (T+B) */
    border: 2px solid;/* 4px total (T+B) */
    margin: 15px;     /* 30px total (T+B) */
    /* Total height in document flow: 200 + 20 + 4 = 224px (margin separate) */
}
```

### Common Mistake ❌
```css
/* Not using border-box - confusing math */
.card {
    width: 300px;
    padding: 20px;  /* Adds 40px to actual width! */
    border: 1px;    /* Adds 2px */
    /* Actual width becomes 300 + 40 + 2 = 342px */
}

/* Unpredictable margins due to collapse */
.title {
    margin-bottom: 20px;
}
.subtitle {
    margin-top: 30px;  /* Only 30px gap, not 50px! */
}

/* Confusing padding shorthand */
.box {
    padding: 10px 20px 30px;  /* Many forget it's Top, Right, Bottom */
}

/* Trying to margin elements with no width set */
.box {
    margin: 0 auto;  /* Doesn't work without width! */
}

/* Negative margins (usually confusion) */
.overlap {
    margin: -10px;  /* Hard to reason about */
}
```

**Why it matters:** Box Model miscalculations cause layout issues, misaligned elements, and unexpected overflow.

### Practical Tasks

**Task 1:** Build a spacing system
- Create margin/padding utilities for common values (5px, 10px, 15px, 20px, etc.)
- Create classes like `.m-20` (margin 20px), `.p-10` (padding 10px)
- Test that elements with these utilities align predictably
- Create a visual reference showing Box Model layers

**Task 2:** Create a card layout using Box Model
- Card container with padding and border
- Image that bleeds to edges (negative margin)
- Content area with proper spacing
- Button with padding and margin
- Test alignment with multiple cards

**Task 3:** Build a centered section layout
- Hero section centered on page
- Hero content centered within section
- Multiple nested centered elements
- Use `margin: 0 auto` properly
- Ensure margins work as expected

### Revision Mind Map

```
CSS Box Model
├── Layers (Inside to Outside)
│   ├── Content (text, images)
│   ├── Padding (space inside border)
│   ├── Border (line around element)
│   └── Margin (space outside border)
├── box-sizing Property
│   ├── content-box (default, padding/border added to size)
│   ├── border-box (padding/border included in size)
│   └── * { box-sizing: border-box } (recommended)
├── Width/Height
│   ├── Affects content box only
│   ├── Padding/border added if content-box
│   └── Set explicitly for predictability
├── Padding (space inside)
│   ├── Never collapses
│   ├── Shorthand: T R B L
│   └── Proportional: padding: 10% (of width)
├── Margin (space outside)
│   ├── Collapses vertically (use larger value)
│   ├── Never collapses horizontally
│   ├── Can be negative
│   └── margin: 0 auto (horizontal centering)
└── Visual Layout
    ├── Block elements stack vertically
    ├── Margin collapse affects vertical spacing
    ├── Padding doesn't collapse
    └── Total space = content + padding + border + margin
```

---

## Topic 2: Selectors & Specificity

### Deep-Dive Explanation

CSS selectors are how you target HTML elements to style. Specificity determines which styles win when multiple rules apply to the same element. Mastering selectors and specificity prevents frustration and overuse of `!important`.

**Behind-the-Scenes:**
- Specificity is calculated: (inline, IDs, classes/attributes/pseudo, elements)
- Higher specificity always wins over lower specificity
- `!important` has highest specificity - avoid using
- Order matters when specificity is equal (last rule wins)
- Selector combining (descendant, child, adjacent sibling) allows precise targeting
- Pseudo-selectors (`:hover`, `:focus`, `:nth-child`) provide dynamic styling

### Code Examples

### Right Way ✅
```css
/* Element selector - low specificity, reusable */
p {
    color: #333;
    line-height: 1.6;
}

/* Class selector - medium specificity, reusable */
.highlight {
    background-color: yellow;
    font-weight: bold;
}

/* Combining selectors - more specific but still reusable */
.card {
    padding: 20px;
    border-radius: 8px;
}

.card .title {
    font-size: 1.5em;
    margin-bottom: 10px;
}

.card .description {
    color: #666;
}

/* Adjacent sibling selector */
h2 + p {
    margin-top: 0;  /* Remove space between heading and first para */
}

/* Child selector - direct children only */
ul > li {
    list-style: none;
}

/* Pseudo-classes for state */
.button {
    padding: 10px 20px;
    cursor: pointer;
    transition: background 0.2s;
}

.button:hover {
    background-color: #e0e0e0;
}

.button:active {
    transform: scale(0.98);
}

.button:focus {
    outline: 2px solid blue;
}

.button:disabled {
    opacity: 0.5;
    cursor: not-allowed;
}

/* :nth-child for pattern selection */
li:nth-child(2n) {
    background-color: #f5f5f5;  /* Zebra striping */
}

/* :first-child, :last-child */
.list li:first-child {
    border-top: 1px solid #ddd;
}

.list li:last-child {
    border-bottom: 1px solid #ddd;
}

/* Attribute selectors - specific yet reusable */
input[type="email"] {
    border: 1px solid #ccc;
}

input[placeholder*="required"] {
    border-color: orange;
}

a[href$=".pdf"] {
    background-image: url(pdf-icon.png);
    padding-right: 20px;
}

/* Descendant combinator - all nested elements */
.sidebar p {
    font-size: 0.9em;
}

/* Child combinator - only direct children */
.list > .item {
    margin-bottom: 5px;
}

/* Groups with comma */
h1, h2, h3 {
    line-height: 1.2;
    margin-top: 1em;
}
```

### Common Mistake ❌
```css
/* Using IDs for styling - too specific, can't reuse */
#header-title {
    font-size: 2em;
}

#sidebar-title {
    font-size: 2em;
}
/* Should be one .title class! */

/* Over-specific selectors - fragile to HTML changes */
.page-container .main-content div.article-section h2.article-title {
    color: blue;
}
/* If HTML structure changes slightly, styles break */

/* Using !important excessively */
.button {
    background-color: blue !important;
}

.button:hover {
    background-color: darkblue !important;  /* Fighting with !important */
}

/* Confusing pseudo-elements with pseudo-classes */
.hover a:before {  /* Pseudo-elements use :: not : */
    content: "→";
}

/* Wrong selector combinations */
.card .title, .description {  /* description not necessarily in .card */
    color: blue;
}

/* Not considering cascade order */
.active {
    color: blue;
}

.card {
    color: red;  /* This wins if .card.active - order doesn't matter! Only specificity. */
}
```

**Why it matters:** High specificity creates fragile stylesheets. Low specificity with good selectors is maintainable.

### Practical Tasks

**Task 1:** Create a reusable selector system  
- Component class selectors (.card, .button, .input)
- Modifier classes (.button--primary, .card--large)
- Avoid element selectors in component CSS
- Test that styles follow cascade properly

**Task 2:** Write a CSS selector playbook
- Document 20+ different selector patterns
- Show specificity calculation for each
- Explain when to use each type
- Examples: descendant, child, adjacent, attribute, pseudo-class, pseudo-element

**Task 3:** Refactor CSS to lower specificity
- Start with existing CSS with high specificity
- Identify IDs and overly-specific selectors
- Rewrite using classes and simpler selectors
- Verify styles still apply correctly
- Document specificity of before/after

### Revision Mind Map

```
CSS Selectors & Specificity
├── Selector Types (Low to High Specificity)
│   ├── Element: p, div, a (1 point)
│   ├── Class: .highlight, [type="text"] (10 points)
│   ├── ID: #header (100 points)
│   └── Inline: style="" (1000 points)
│   └── !important (highest, avoid!)
├── Basic Selectors
│   ├── Element: p, div
│   ├── Class: .name
│   ├── ID: #name
│   ├── Attribute: [type="text"]
│   └── Universal: *
├── Combinators
│   ├── Descendant: .container p (any p inside)
│   ├── Child: .container > p (direct p child)
│   ├── Adjacent: h2 + p (p after h2)
│   └── General sibling: h2 ~ p (any p after h2)
├── Pseudo-Classes (element state)
│   ├── :hover, :focus, :active
│   ├── :nth-child(n), :first-child, :last-child
│   ├── :not(.class) (negation)
│   └── :disabled, :checked, :visited
├── Pseudo-Elements (create virtual elements)
│   ├── ::before (content before)
│   ├── ::after (content after)
│   ├── ::first-line
│   └── ::selection
├── Specificity Calculation
│   ├── Count IDs (#)
│   ├── Count classes and attributes (., [])
│   ├── Count elements (tag names)
│   └── Higher number wins
└── Best Practices
    ├── Keep specificity low
    ├── Use classes, not IDs
    ├── Avoid !important
    ├── Shorter selectors are better
    └── Be specific when needed
```

---

## Topic 3: Colors, Fonts & Typography

### Deep-Dive Explanation

Colors and typography carry emotional weight and affect readability. Proper color contrast and font sizing ensure your site is accessible and visually appealing. CSS provides multiple ways to specify colors and control text rendering.

**Behind-the-Scenes:**
- RGB colors are additive (0 = black, 255 = white)
- HSL is more intuitive (Hue = color wheel, Saturation = intensity, Lightness = brightness)
- Color contrast ratio must be 4.5:1 for normal text (WCAG AA)
- Font files must be loaded before text renders (affects First Contentful Paint)
- Line-height affects vertical rhythm and readability
- Font-weight affects visual hierarchy and can vary from 100-900
- System fonts load instantly, web fonts take time

### Code Examples

### Right Way ✅
```css
/* Define custom properties for colors - easier maintenance */
:root {
    --color-primary: #3498db;
    --color-secondary: #2c3e50;
    --color-text: #333;
    --color-text-light: #666;
    --color-bg: #fff;
    --color-border: #ddd;
    --color-success: #27ae60;
    --color-error: #e74c3c;
    --color-warning: #f39c12;
}

/* Proper contrast for readability (4.5:1 WCAG AA) */
body {
    color: var(--color-text);      /* #333 on white = 12.6:1 contrast */
    background-color: var(--color-bg);
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    font-size: 16px;               /* Base size for responsive scaling */
    line-height: 1.6;              /* Ample line spacing for readability */
    letter-spacing: 0.5px;         /* Slight spacing for clarity */
}

/* Type scale - consistent hierarchy */
h1 {
    font-size: 2.5rem;     /* 40px at 16px base */
    font-weight: 700;      /* Bold for headings */
    line-height: 1.2;      /* Tighter for headings */
    margin-bottom: 0.5em;  /* Space to next content */
    color: var(--color-secondary);
}

h2 {
    font-size: 1.875rem;
    font-weight: 700;
    line-height: 1.2;
    margin-top: 1em;
    margin-bottom: 0.5em;
}

h3 {
    font-size: 1.25rem;
    font-weight: 600;
}

p {
    margin-bottom: 1em;
    color: var(--color-text);
}

/* Web fonts - optimize loading */
@font-face {
    font-family: 'Open Sans';
    src: url('opensans.woff2') format('woff2'),
         url('opensans.woff') format('woff');
    font-weight: normal;
    font-display: swap;  /* Show fallback while loading */
}

.serif {
    font-family: 'Georgia', serif;  /* Fallback to system serif */
}

.monospace {
    font-family: 'Courier New', monospace;
    background-color: #f5f5f5;
    padding: 2px 6px;
    border-radius: 3px;
}

/* Color with context */
.button-primary {
    background-color: var(--color-primary);
    color: white;          /* Good contrast with blue bg */
}

.button-secondary {
    background-color: transparent;
    color: var(--color-primary);
    border: 1px solid var(--color-primary);
}

.error {
    color: var(--color-error);
    /* Error color (#e74c3c) on white has 3.93:1 contrast - borderline
       Add icon or background to improve accessibility */
    background-color: #fee;
}

.success {
    color: var(--color-success);
    background-color: #efe;
}

/* Emphasis without just color */
.important {
    color: var(--color-error);
    font-weight: 600;      /* Not just red, also bold */
}

strong, .weight-bold {
    font-weight: 600;
}

em, .style-italic {
    font-style: italic;
}

/* Responsive font sizing */
@media (max-width: 768px) {
    h1 { font-size: 2rem; }
    h2 { font-size: 1.5rem; }
    body { font-size: 15px; }
}

/* Links should be visible and accessible */
a {
    color: var(--color-primary);
    text-decoration: underline;
    cursor: pointer;
}

a:visited {
    color: #8e44ad;  /* Visited state */
}

a:hover {
    text-decoration: none;
    opacity: 0.8;
}

a:focus {
    outline: 2px solid var(--color-primary);
}
```

### Common Mistake ❌
```css
/* Low contrast - unreadable */
.text {
    color: #999;           /* Gray on white = only 3.6:1 */
    background-color: #f0f0f0;  /* Too light */
}

/* Color alone for meaning */
.error {
    color: red;            /* Colorblind users won't know it's an error */
}

/* No line-height - cramped text */
p {
    line-height: 1;        /* Too tight, hard to read */
}

/* Mismatched font fallbacks */
body {
    font-family: 'Fancy Web Font' Georgia, serif;
    /* Fallback is serif, but Fancy is sans-serif - styles differ greatly */
}

/* No web font optimization */
@font-face {
    font-family: 'Big Font';
    src: url('hugefile.ttf');  /* 400KB TTF file, blocks rendering */
    /* Should be woff2 (smaller) and use font-display */
}

/* Bad color contrast */
input {
    background-color: #f9f9f9;
    color: #fafafa;        /* Nearly invisible */
}

/* Fixed sizes that don't scale */
h1 {
    font-size: 32px;       /* Doesn't scale with viewport or user zoom */
}

/* Over-styled text */
.fancy {
    font-style: italic;
    text-decoration: underline;
    color: red;
    text-transform: uppercase;
    letter-spacing: 0.5em;
    /* Too much at once - distracting */
}
```

**Why it matters:** Poor typography and contrast harm accessibility and readability. Good typography makes content approachable.

### Practical Tasks

**Task 1:** Create a typography system
- Define a color palette (5-10 colors with contrast ratios)
- Create heading hierarchy (h1-h6) with consistent sizing
- Document line-height recommendations
- Choose readable base font size and font family
- Create a style guide with examples

**Task 2:** Optimize web fonts
- Select 2-3 web fonts (avoid overloading)
- Use woff2 format for modern browsers
- Implement `font-display: swap` for fallback
- Test loading performance
- Measure impact on First Contentful Paint

**Task 3:** Ensure color contrast compliance
- Audit existing colors against WCAG AA threshold (4.5:1)
- Identify text/background combinations below threshold
- Adjust colors to meet compliance
- Test with colorblindness simulator
- Document all color combinations used

### Revision Mind Map

```
Colors, Fonts & Typography
├── Color Formats
│   ├── Hex: #3498db (6 digits = RGB)
│   ├── RGB: rgb(52, 152, 219) (0-255)
│   ├── RGBA: rgba(52, 152, 219, 0.5) (with transparency)
│   ├── HSL: hsl(204, 70%, 53%) (more intuitive)
│   └── Color names: blue, red (limited)
├── Color Best Practices
│   ├── Define with CSS variables (--color-primary)
│   ├── Check contrast ratios (4.5:1 minimum)
│   ├── Never use color alone for meaning
│   ├── Test with colorblindness simulator
│   └── Use limited palette (5-10 colors)
├── Fonts
│   ├── System fonts (instant, no cache)
│   ├── Web fonts (prettier, requires request)
│   ├── Google Fonts (free, popular)
│   ├── Font weights (100-900)
│   └── Font formats: woff2 (modern), woff (fallback)
├── Typography
│   ├── Font-size: rem or em (scalable)
│   ├── Line-height: 1.5-1.7 (readable spacing)
│   ├── Letter-spacing: subtle (0.5-1px)
│   ├── Type scale: consistent hierarchy
│   └── Font-weight: varies importance
├── Heading Hierarchy
│   ├── h1: largest, most important (one per page)
│   ├── h2: section headings
│   ├── h3: subsections
│   ├── h4-h6: rare, only if needed
│   └── Outline should be logical
└── Accessibility
    ├── Minimum size: 16px for body text
    ├── Contrast ratio: 4.5:1 normal, 3:1 large
    ├── Readable fonts (avoid fancy for body)
    ├── Sufficient line-height (1.5+)
    └── Color + text for emphasis
```

---

## Quick Reference: Common CSS Properties

| Property | Purpose | Example |
|----------|---------|---------|
| `color` | Text color | `color: #333;` |
| `background-color` | Element background | `background-color: #f5f5f5;` |
| `font-size` | Text size | `font-size: 16px;` |
| `font-weight` | Text boldness | `font-weight: 600;` |
| `line-height` | Vertical text spacing | `line-height: 1.6;` |
| `padding` | Internal spacing | `padding: 20px;` |
| `margin` | External spacing | `margin: 10px;` |
| `border` | Element border | `border: 1px solid #ccc;` |
| `border-radius` | Rounded corners | `border-radius: 8px;` |
| `width` | Element width | `width: 100%;` |
| `height` | Element height | `height: auto;` |
| `display` | How element renders | `display: flex;` |
| `position` | Positioning method | `position: relative;` |
| `opacity` | Transparency | `opacity: 0.8;` |
| `transform` | 2D/3D transformations | `transform: rotate(45deg);` |

---

## Helpful Resources

- [MDN: CSS Documentation](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [CSS Tricks: A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [WebAIM: Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [Google Fonts](https://fonts.google.com/)
- [Can I Use: Browser Support](https://caniuse.com/)
