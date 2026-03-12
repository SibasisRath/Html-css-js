# CSS Advanced

## Topic 1: Flexbox & Grid Layout

### Deep-Dive Explanation

Flexbox and Grid are modern layout techniques. Flexbox handles one-dimensional layouts (rows OR columns), while Grid handles two-dimensional layouts (rows AND columns simultaneously). Together, they replace float layouts and make responsive design intuitive.

**Behind-the-Scenes:**
- Flexbox creates a flex container where children (flex items) are flexible
- Main axis and cross axis change based on flex-direction
- `justify-content` controls alignment along main axis
- `align-items` controls alignment along cross axis
- Grid creates template rows and columns
- Grid items automatically place themselves in grid cells
- Flexbox is best for components, Grid best for page layout
- Gap property controls spacing between items

### Code Examples

### Right Way ✅
```css
/* Flexbox for simple, flexible layouts */
.navbar {
    display: flex;
    justify-content: space-between;  /* Space between items */
    align-items: center;             /* Vertically centered */
    padding: 20px;
    gap: 10px;                       /* Space between children */
}

.navbar {
    flex-direction: row;             /* Left to right (default) */
    /* flex-direction: column;        /* Top to bottom */
}

/* Flex items grow/shrink to fill space */
.container {
    display: flex;
    gap: 20px;
}

.sidebar {
    flex: 0 0 200px;                 /* Don't grow/shrink, fixed 200px */
}

.content {
    flex: 1;                         /* Grow to fill remaining space */
}

/* Grid for complex 2D layouts */
.layout {
    display: grid;
    grid-template-columns: 200px 1fr 250px;  /* 3 columns: fixed, flexible, fixed */
    grid-template-rows: auto 1fr auto;       /* 3 rows: auto, fill, auto */
    gap: 20px;
    height: 100vh;
}

.header {
    grid-column: 1 / -1;             /* Span all columns */
    grid-row: 1;
}

.sidebar {
    grid-column: 1;
    grid-row: 2;
}

.content {
    grid-column: 2;
    grid-row: 2;
}

.aside {
    grid-column: 3;
    grid-row: 2;
}

.footer {
    grid-column: 1 / -1;
    grid-row: 3;
}

/* Responsive Grid with auto-fit */
.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
}
/* Creates responsive columns that minimum 250px, grow to available space */

/* Flex wrap for responsive rows */
.flex-wrap {
    display: flex;
    flex-wrap: wrap;         /* Wrap to next line if needed */
    gap: 20px;
}

.flex-item {
    flex: 1 1 300px;         /* Grow, shrink, base 300px */
    min-width: 0;            /* Allow content to shrink */
}

/* Aligning individual grid items */
.card {
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: start;      /* Align to top */
    justify-items: center;   /* Center horizontally */
}

/* Flexible aspect ratio boxes with grid */
.aspect-ratio {
    display: grid;
    grid-template-columns: 1fr;
    aspect-ratio: 16 / 9;
}

.aspect-ratio img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

/* Space-around vs space-between */
.space-between {
    display: flex;
    justify-content: space-between;  /* Items at edges, gap between */
}

.space-around {
    display: flex;
    justify-content: space-around;   /* Equal space around each item */
}

.space-evenly {
    display: flex;
    justify-content: space-evenly;   /* Equal space everywhere */
}

/* Centering with flexbox (the easy way!) */
.center-flex {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
}

/* Centering with grid (also works) */
.center-grid {
    display: grid;
    place-items: center;             /* Shorthand for align & justify */
    height: 100%;
}
```

### Common Mistake ❌
```css
/* Not using flexbox gap - using margin instead */
.flex {
    display: flex;
}

.flex > * {
    margin-right: 10px;  /* Works but last item has unwanted margin */
}

/* Confusing main axis and cross axis */
.flex {
    display: flex;
    flex-direction: column;
    justify-content: center;  /* Only centers horizontally, not vertically! */
    align-items: center;      /* This centers vertically */
}

/* Using flexbox when grid is better */
.layout {
    display: flex;
    flex-wrap: wrap;
}
/* Two-dimensional layouts are harder in flexbox */

/* Not setting min-width on flex items with content */
.flex-item {
    flex: 1;
    /* If item content too wide, it won't shrink properly */
    /* Solution: min-width: 0; */
}

/* Over-complex grid template */
.grid {
    grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
    gap: 10px;
}
/* Should use: repeat(5, 1fr) */

/* Incorrect grid spanning */
.grid-item {
    grid-column: 1 / 3;      /* Spans columns 1 and 2 */
    grid-row: 1 / 2;         /* Only in first row */
}

/* Not using auto-fit for responsive grids */
.grid {
    grid-template-columns: repeat(auto-fit, 300px);
    /* Doesn't grow items! Use minmax() */
    /* grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); */
}
```

**Why it matters:** Flexbox and Grid simplify layouts that historically required floats or positioning. They're essential for modern responsive design.

### Practical Tasks

**Task 1:** Create layouts with Flexbox
- Navigation bar with logo, menu items, and button
- Card component with image, title, content, button
- Hero section with centered content
- Sidebar + main content layout
- Responsive menu that switches to column on mobile

**Task 2:** Create layouts with CSS Grid
- Page layout with header, sidebar, content, footer
- Product grid that responds to screen size
- Dashboard with various widget sizes
- Card layout with specific positioning
- Gallery grid with overlaying text

**Task 3:** Compare Flexbox vs Grid
- Rebuild the same layout using both methods
- Document when to use each
- Measure browser support
- Test responsiveness on multiple screen sizes
- Choose which is better for each use case

### Revision Mind Map

```
Flexbox & Grid
├── Flexbox (1D Layout)
│   ├── display: flex
│   ├── flex-direction (row | column)
│   ├── Main axis (justify-content)
│   │   ├── flex-start, center, flex-end
│   │   ├── space-between, space-around, space-evenly
│   │   └── stretch
│   ├── Cross axis (align-items)
│   │   ├── flex-start, center, flex-end
│   │   ├── stretch
│   │   └── baseline
│   ├── Flex items
│   │   ├── flex: [grow] [shrink] [basis]
│   │   ├── flex-grow (0-∞)
│   │   ├── flex-shrink (0-∞)
│   │   └── flex-basis (width/height)
│   ├── flex-wrap (wrap items to next line)
│   └── gap (space between items)
├── Grid (2D Layout)
│   ├── display: grid
│   ├── Columns
│   │   ├── grid-template-columns: 200px 1fr 200px
│   │   ├── grid-auto-columns (implicit)
│   │   └── repeat(3, 1fr) - repeating pattern
│   ├── Rows
│   │   ├── grid-template-rows
│   │   └── grid-auto-rows
│   ├── Auto-fit for responsive
│   │   └── repeat(auto-fit, minmax(250px, 1fr))
│   ├── Grid items
│   │   ├── grid-column: 1 / 3 (span columns 1-2)
│   │   ├── grid-row: 1 / 2 (span rows)
│   │   └── grid-area: name (named grid areas)
│   ├── Alignment
│   │   ├── justify-items (horizontal alignment)
│   │   └── align-items (vertical alignment)
│   └── gap (space between cells)
└── When to Use
    ├── Flexbox: components, headers, navbars
    ├── Grid: page layouts, galleries
    └── Combine both: use grid for layout, flex for components
```

---

## Topic 2: Positioning & Stacking Context

### Deep-Dive Explanation

CSS Positioning changes how elements are positioned in the document flow. There are four main position values: static (default), relative, absolute, and fixed. Understanding z-index and stacking context prevents layering issues.

**Behind-the-Scenes:**
- Static positioning is the default - elements follow normal flow
- Relative positioning offsets element from its normal position without affecting other elements
- Absolute positioning removes element from flow, positioned relative to nearest positioned ancestor
- Fixed positioning removes element from flow, positioned relative to viewport
- z-index only works on positioned elements (not static)
- Stacking context is created by position values, opacity, transform, and more
- Each stacking context has its own z-index stack - z-index 999 in one context may be behind z-index 1 in another

### Code Examples

### Right Way ✅
```css
/* Static positioning (default) - no special behavior */
.normal {
    position: static;  /* Default, not needed to write */
}

/* Relative positioning - offset from normal position */
.tooltip-trigger {
    position: relative;
    cursor: help;
}

.tooltip {
    position: absolute;
    background-color: #333;
    color: white;
    padding: 10px;
    border-radius: 4px;
    
    /* Position relative to .tooltip-trigger (positioned ancestor) */
    bottom: 100%;
    left: 50%;
    transform: translateX(-50%);
    
    white-space: nowrap;
    pointer-events: none;  /* Don't interfere with mouse events */
}

/* Absolute positioning - removes from flow */
.card {
    position: relative;  /* Creates positioning context for children */
    overflow: hidden;
}

.card-image {
    width: 100%;
    height: 200px;
    object-fit: cover;
}

.card-overlay {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;  /* Fill entire card */
    background: rgba(0, 0, 0, 0.5);
    opacity: 0;
    transition: opacity 0.3s;
}

.card:hover .card-overlay {
    opacity: 1;
}

.card-badge {
    position: absolute;
    top: 10px;
    right: 10px;
    background-color: #e74c3c;
    color: white;
    padding: 5px 10px;
    border-radius: 3px;
}

/* Fixed positioning - relative to viewport */
.sticky-header {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    background-color: white;
    border-bottom: 1px solid #ddd;
    z-index: 100;  /* Above other content */
}

body {
    padding-top: 60px;  /* Space below fixed header */
}

.back-to-top {
    position: fixed;
    bottom: 20px;
    right: 20px;
    width: 50px;
    height: 50px;
    background-color: #3498db;
    color: white;
    cursor: pointer;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 99;  /* Below header */
}

/* Managing stacking context carefully */
.modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.8);
    z-index: 1000;  /* Very high - on top of everything */
    display: flex;
    align-items: center;
    justify-content: center;
}

.modal {
    background-color: white;
    padding: 30px;
    border-radius: 8px;
    max-width: 500px;
    z-index: 1001;  /* Slightly higher than overlay (unnecessary but clear) */
    /* Don't need high z-index - within same context */
}

/* Creating new stacking context explicitly */
.dropdown {
    position: relative;
}

.dropdown-menu {
    position: absolute;
    top: 100%;
    left: 0;
    background-color: white;
    border: 1px solid #ddd;
    border-radius: 4px;
}

/* Use transform to create stacking context without positioning */
.layered {
    position: relative;
    transform: translateZ(0);  /* Creates stacking context */
    z-index: 1;               /* Now z-index works predictably */
}

/* Sticky positioning (hybrid) */
.section-heading {
    position: sticky;
    top: 60px;  /* Stick 60px below viewport top (below fixed header) */
    background-color: white;
    z-index: 50;  /* Below fixed header, above content */
}
```

### Common Mistake ❌
```css
/* Using absolute positioning without parent being positioned */
.parent {
    /* No position: relative */
}

.child {
    position: absolute;
    /* Positions relative to nearest positioned ancestor (could be html!) */
    /* Solution: add position: relative; to parent */
}

/* Excessive z-index values */
.element1 {
    z-index: 9999;
}

.element2 {
    z-index: 99999;
}
/* Arms race! Use reasonable values (1-100 usually sufficient) */

/* z-index on unpositioned elements */
.box {
    z-index: 50;  /* Doesn't work! position: static by default */
    /* Solution: add position: relative; */
}

/* Conflicting stacking contexts */
.sidebar {
    position: relative;
    z-index: 50;
}

.sidebar-dropdown {
    z-index: 1;  /* High value in this context */
              /* But still behind everything else because sidebar only z-index: 50 */
}

/* Not managing overflow with positioning */
.container {
    position: relative;
}

.absolute-child {
    position: absolute;
    width: 200%;  /* Overflows parent */
}
/* Solution: set overflow: visible; or accept overflow behavior */

/* Forgetting to offset absolutely positioned elements */
.positioned {
    position: absolute;
    /* No top/left/right/bottom - element stays in normal flow position */
    /* Very confusing! */
}
```

**Why it matters:** Positioning allows precise control but can create confusing layering. Understanding stacking context prevents z-index frustrations.

### Practical Tasks

**Task 1:** Create positioning scenarios
- Tooltip component (relative + absolute)
- Image overlay on hover
- Fixed sticky header
- Back-to-top button
- Dropdown menu positioning

**Task 2:** Build a modal dialog
- Full-screen overlay with fixed positioning
- Modal centered on screen
- Overlay behind modal with lower z-index
- Close button in top-right corner
- Content scrolls if overflows (not overlay)

**Task 3:** Understand stacking context
- Create nested elements with various z-index values
- Document which elements appear on top
- Adjust z-index and observe results
- Identify where new stacking contexts are created
- Refactor to use consistent stacking context strategy

### Revision Mind Map

```
Positioning & Stacking
├── Position Values
│   ├── static (default, no special positioning)
│   ├── relative (offset from normal position)
│   ├── absolute (positioned to nearest positioned ancestor)
│   ├── fixed (positioned to viewport)
│   └── sticky (hybrid of relative and fixed)
├── Positioning Properties
│   ├── top, right, bottom, left (offset values)
│   ├── z-index (layering, only on positioned elements)
│   ├── transform (position without affecting document flow)
│   └── inset (shorthand for all four directions)
├── Stacking Context
│   ├── Created by position (non-static)
│   ├── Created by opacity < 1
│   ├── Created by transform
│   ├── Created by z-index with position
│   └── Each context has its own z-index stack
├── Best Practices
│   ├── Use relative for positioning container
│   ├── Use absolute for positioned children
│   ├── Use fixed for persistent UI (headers, modals)
│   ├── Keep z-index values reasonable (1-100)
│   ├── Document stacking strategy
│   └── Avoid excessive absolute positioning
└── Common Uses
    ├── Tooltips (relative + absolute)
    ├── Overlays (fixed positioning)
    ├── Dropdowns (absolute positioning)
    ├── Sticky headers (sticky/fixed)
    └── Image overlays (absolute in relative)
```

---

## Topic 3: Responsive Design & Media Queries

### Deep-Dive Explanation

Responsive design ensures your site works on all screen sizes. Media queries allow different CSS for different conditions (screen width, orientation, device type). Mobile-first design starts with mobile and enhances for larger screens.

**Behind-the-Scenes:**
- Media features include `min-width`, `max-width`, `orientation`, `device-pixel-ratio`
- Mobile-first uses `min-width` queries (base is mobile, enhance)
- Desktop-first uses `max-width` queries (base is desktop, degrade)
- CSS Grid and Flexbox are inherently responsive - no complex media queries needed
- `viewport` meta tag tells mobile browsers how to scale
- Touch targets should be 44x44px minimum
- Text should be readable without zooming

### Code Examples

### Right Way ✅
```css
/* Mobile-first approach: start simple for mobile, enhance for larger screens */

/* Base styles (mobile) */
.container {
    width: 100%;
    padding: 0 15px;
    margin: 0 auto;
}

.nav {
    display: flex;
    flex-direction: column;  /* Stack vertically on mobile */
    gap: 10px;
}

.grid {
    display: grid;
    grid-template-columns: 1fr;  /* Single column on mobile */
    gap: 15px;
}

/* Enhance for tablet screens */
@media (min-width: 768px) {
    .container {
        max-width: 750px;
    }
    
    .nav {
        flex-direction: row;  /* Horizontal on tablet */
        justify-content: space-between;
    }
    
    .grid {
        grid-template-columns: repeat(2, 1fr);  /* Two columns */
    }
}

/* Enhance for desktop screens */
@media (min-width: 1024px) {
    .container {
        max-width: 960px;
    }
    
    .grid {
        grid-template-columns: repeat(3, 1fr);  /* Three columns */
    }
}

/* Large desktop */
@media (min-width: 1280px) {
    .container {
        max-width: 1200px;
    }
}

/* Hide elements on mobile, show on desktop */
.desktop-only {
    display: none;
}

@media (min-width: 768px) {
    .desktop-only {
        display: block;
    }
}

/* Show on mobile, hide on desktop */
.mobile-menu {
    display: block;
}

@media (min-width: 768px) {
    .mobile-menu {
        display: none;
    }
}

/* Adjust font sizes for readability */
h1 {
    font-size: 1.5rem;
}

@media (min-width: 768px) {
    h1 {
        font-size: 2rem;
    }
}

@media (min-width: 1024px) {
    h1 {
        font-size: 2.5rem;
    }
}

/* Touch device optimization */
@media (hover: none) and (pointer: coarse) {
    /* Touch devices - buttons don't have hover state */
    button {
        padding: 12px 24px;  /* Larger touch target */
    }
    
    a {
        padding: 10px;  /* Larger tap area */
    }
}

/* High DPI screens */
@media (min-resolution: 300dpi) {
    .icon {
        background-image: url('icon-2x.png');
        background-size: 50%;
    }
}

/* Dark mode preference */
@media (prefers-color-scheme: dark) {
    :root {
        --bg-color: #1e1e1e;
        --text-color: #fff;
    }
}

/* Reduced motion preference */
@media (prefers-reduced-motion: reduce) {
    * {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
    }
}

/* Landscape orientation */
@media (orientation: landscape) {
    .hero {
        height: 60vh;  /* Less height in landscape */
    }
}

/* Combining conditions */
@media (min-width: 768px) and (max-width: 1023px) {
    /* Only tablet size */
}

@media (min-width: 1024px) or (orientation: landscape) {
    /* Desktop or landscape */
}
```

### Common Mistake ❌
```css
/* Desktop-first approach - harder to maintain */
.grid {
    grid-template-columns: repeat(3, 1fr);
}

@media (max-width: 1024px) {
    .grid {
        grid-template-columns: repeat(2, 1fr);
    }
}

@media (max-width: 768px) {
    .grid {
        grid-template-columns: 1fr;
    }
}

/* Fixed widths - not responsive */
.container {
    width: 1200px;  /* Doesn't adapt to screen */
}

/* Not including viewport meta tag */
/* <meta name="viewport" ...> REQUIRED in HTML head */

/* Touch targets too small */
button {
    padding: 3px 6px;  /* Only 9x6px effective size */
    /* Minimum should be 44x44px */
}

/* Confusing media query values */
@media (width: 768px) {
    /* Only applies at EXACTLY 768px, not a range */
    /* Use min-width and max-width instead */
}

/* Unit inconsistencies */
body {
    font-size: 16px;
}

h1 {
    font-size: 32em;  /* Based on body, so 32 * 16px = 512px! */
    /* Should use rem: font-size: 2rem; */
}

/* Not testing actual devices */
/* Responsive design tools in browser are helpful but test on real devices too */
```

**Why it matters:** Responsive design ensures usability across all devices. It's expected by users and improves SEO.

### Practical Tasks

**Task 1:** Build a responsive layout
- Create a layout that works on mobile (320px), tablet (768px), and desktop (1024px)
- Use media queries with mobile-first approach
- Test at each breakpoint with browser DevTools
- Ensure navigation is accessible on all sizes
- Check that text is readable without zooming

**Task 2:** Create responsive images
- Use srcset for different image resolutions
- Implement `<picture>` element for different crops
- Optimize images for each breakpoint
- Test loading performance on slow connections
- Verify images display correctly at all sizes

**Task 3:** Design media query strategy
- Define breakpoints for your design (mobile, tablet, desktop)
- Document which CSS changes at each breakpoint
- Ensure consistent spacing hierarchy
- Test touch targets are properly sized
- Create a responsive design checklist

### Revision Mind Map

```
Responsive Design & Media Queries
├── Media Queries
│   ├── min-width (mobile-first)
│   ├── max-width (desktop-first)
│   ├── orientation (portrait/landscape)
│   ├── (hover: none) (touch devices)
│   ├── prefers-reduced-motion
│   ├── prefers-color-scheme
│   └── min-resolution (DPI)
├── Viewport Meta Tag (HTML)
│   └── <meta name="viewport" content="width=device-width, initial-scale=1.0">
├── Breakpoints (Common)
│   ├── Mobile: 320px-767px
│   ├── Tablet: 768px-1023px
│   ├── Desktop: 1024px+
│   └── Extra large: 1280px+
├── Mobile-First Approach
│   ├── Base styles (mobile)
│   ├── @media (min-width: 768px) { }
│   ├── @media (min-width: 1024px) { }
│   └── Progressive enhancement
├── Design Principles
│   ├── Flexible grids (%, rem, em)
│   ├── Responsive images (srcset, <picture>)
│   ├── Touch targets: 44x44px minimum
│   ├── Readable text (no zoom needed)
│   └── Single column on mobile
└── Testing
    ├── Desktop browser (multiple widths)
    ├── Device inspector (Chrome DevTools)
    ├── Real devices (if possible)
    ├── Touch simulation
    └── Performance on mobile
```

---

## Quick Reference: Responsive Breakpoints

| Device | Width Range | CSS Target |
|--------|-------------|-----------|
| Mobile | 320px - 767px | `@media (max-width: 767px)` or base styles |
| Tablet | 768px - 1023px | `@media (min-width: 768px) and (max-width: 1023px)` |
| Desktop | 1024px+ | `@media (min-width: 1024px)` |
| Large Desktop | 1280px+ | `@media (min-width: 1280px)` |
| Extra Large | 1920px+ | `@media (min-width: 1920px)` |

---

## Helpful Resources

- [MDN: CSS Documentation](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [CSS Tricks: Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [CSS Tricks: Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [Web.dev: Responsive Design](https://web.dev/responsive-web-design-basics/)
- [Can I Use: Browser Support](https://caniuse.com/)
- [Google PageSpeed Insights](https://pagespeed.web.dev/)
