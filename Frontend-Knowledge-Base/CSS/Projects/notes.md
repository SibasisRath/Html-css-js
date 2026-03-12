# CSS Projects

## Project 1: Responsive E-Commerce Product Card

### Project Overview
Create a reusable product card component that looks great on mobile, tablet, and desktop. This project focuses on responsive CSS, flexbox, hover effects, and accessibility.

### Requirements

#### Visual Features
- **Product Image**: Responsive, high-quality image with overlay on hover
- **Product Info**: Name, price, rating, description
- **Color Options**: Clickable color swatches
- **Quantity Selector**: Input field with increment/decrement buttons
- **Action Buttons**: "Add to Cart" and "Favorite" buttons
- **Badge**: "New" or "Sale" badge in top-right corner
- **Responsive Layout**: Stacks appropriately on different screen sizes

#### CSS Requirements Checklist
- [ ] Uses Flexbox for component layout
- [ ] Images are responsive (width: 100%, height: auto)
- [ ] Hover effects on image (overlay, scale, or brightness)
- [ ] Smooth transitions on all interactive elements
- [ ] Color swatches use CSS for selection state
- [ ] Buttons accessible with keyboard (tab navigation)
- [ ] Touch targets 44x44px minimum
- [ ] Dark mode support using `prefers-color-scheme`
- [ ] Proper spacing using gap property
- [ ] WCAG color contrast compliance
- [ ] Mobile-first responsive approach
- [ ] Uses CSS variables for colors and spacing

### Step-by-Step Guidance

1. **Set up HTML structure**
   - Semantic card container
   - Image section with badge
   - Info section with product details
   - Action buttons in footer

2. **Create base mobile styles**
   - Single column layout
   - Full-width image
   - Readable text sizes
   - Proper spacing with padding/gap

3. **Add color system**
   - Define CSS variables (--primary, --secondary, etc.)
   - Create swatches that respond to :checked state
   - Show proper feedback on hover/selection

4. **Implement hover states**
   - Image overlay on desktop
   - Button hover effects
   - Color swatch selection feedback
   - Smooth transitions (0.2-0.3s)

5. **Make responsive**
   - Adjust font sizes with media queries
   - Modify layout at tablet/desktop
   - Ensure touch targets remain adequate
   - Test on actual mobile devices

6. **Optimize for accessibility**
   - Clear focus indicators
   - ARIA labels for icon buttons
   - Sufficient color contrast
   - No color-only indicators

### Deliverables
- `product-card.html` - HTML structure
- `product-card.css` - Complete styling
- Responsive at mobile, tablet, desktop
- Fully accessible (keyboard navigation, screen reader)
- Dark mode support

---

## Project 2: Responsive Navigation Menu

### Project Overview
Build a responsive navigation menu that switches from hamburger menu on mobile to horizontal menu on desktop. This project emphasizes responsive design, flexbox, and smooth transitions.

### Requirements

#### Features
- **Header**: Logo on left, navigation on right
- **Desktop Navigation**: Horizontal menu with hover effects
- **Mobile Menu**: Hamburger icon that reveals vertical menu
- **Dropdown Menus**: Submenus that appear on hover (desktop) or click (mobile)
- **Active States**: Current page highlighted
- **Sticky Header**: Stays at top while scrolling
- **Responsive**: Transforms between mobile and desktop layouts

#### CSS Requirements Checklist
- [ ] Uses Flexbox for horizontal/vertical layout
- [ ] Hamburger icon is CSS-only (no SVG required)
- [ ] Smooth hamburger animation (transform)
- [ ] Mobile menu slides in from side
- [ ] Dropdown menus appear with opacity/transform
- [ ] Touch targets 44x44px minimum
- [ ] Sticky positioning with fixed fallback
- [ ] Hover effects on desktop only (not mobile)
- [ ] Keyboard navigation (Tab, Enter, Escape)
- [ ] Mobile viewport required
- [ ] Proper z-index for menu layers
- [ ] Color contrast meets WCAG AA

### Step-by-Step Guidance

1. **Create header structure**
   - Logo/brand
   - Navigation list
   - Hamburger button (hidden on desktop)

2. **Style desktop navigation**
   - Flexbox layout (flex-direction: row)
   - Hover effects on menu items
   - Dropdown positioning

3. **Hide mobile menu on desktop**
   - nav { display: none; }
   - Show on mobile only
   - Use media queries (min-width)

4. **Create hamburger styles**
   - Three lines (CSS borders or ::before/::after)
   - Animation (rotate, skew) on click
   - Smooth transition (0.3s)

5. **Implement dropdown menus**
   - Position: absolute
   - Hide by default (opacity: 0, pointer-events: none)
   - Show on hover/focus
   - Arrow indicator

6. **Add responsive behavior**
   - Mobile: vertical, hamburger icon visible
   - Tablet/Desktop: horizontal, hamburger hidden
   - Test at actual breakpoints

### Deliverables
- `navigation.html` - HTML structure
- `navigation.css` - Complete responsive styling
- Works with JavaScript (or CSS-only with :checked hack)
- Fully keyboard accessible
- Mobile and desktop optimized

---

## Project 3: Multi-Page Website with Consistent Styling

### Project Overview
Create a multi-page website (minimum 4 pages) with consistent CSS across all pages. This project requires maintainable CSS architecture and responsive design at scale.

### Site Structure
- **Home Page**: Hero section, featured content, CTA
- **About Page**: Team members, company story, values
- **Services/Products Page**: Grid layout, cards, descriptions
- **Contact Page**: Contact form, map, contact information
- **Header/Footer**: Consistent across all pages

#### CSS Requirements Checklist
- [ ] CSS variables for colors and spacing (global theme)
- [ ] No inline styles (all CSS in stylesheet)
- [ ] Reusable component classes (.card, .button, .section)
- [ ] Consistent typography (heading sizes, line-height)
- [ ] Mobile-first responsive approach
- [ ] Dark mode support throughout
- [ ] 2+ custom fonts from Google Fonts
- [ ] Smooth page transitions
- [ ] Proper grid/flexbox layouts (no floats)
- [ ] Organized CSS file (commented sections)
- [ ] All WCAG AA accessibility requirements
- [ ] Performance optimized (CSS minification considered)

### Site Design Notes

**Color System**
- Primary color (main brand color)
- Secondary color (accent)
- Success/Error colors (feedback)
- Neutral grays (text, backgrounds)
- Dark mode variants

**Typography**
- Clear heading hierarchy (h1-h6)
- Readable body text (16px+, 1.5-1.7 line-height)
- Consistent spacing (margins/padding)

**Components**
- Card component (reusable)
- Button styles (primary, secondary, disabled)
- Form groups (labels, inputs, validation states)
- Section templates (hero, feature grid, testimonials)

**Responsive Breakpoints**
- Mobile: 320px-767px (base styles)
- Tablet: 768px-1023px (medium adjustments)
- Desktop: 1024px+ (full layout)

### Step-by-Step Guidance

1. **Plan CSS architecture**
   - Define color variables
   - Define spacing scale
   - List reusable components
   - Create component CSS (media queries per component, not page-by-page)

2. **Create global styles**
   - Reset/normalize (margin, padding)
   - Body font family, size, line-height
   - Link styles
   - Form input styles

3. **Build components**
   - Button component (multiple variants)
   - Card component (image, text, actions)
   - Form group component (label, input, error)
   - Section component (padding, max-width)

4. **Build page layouts**
   - Home page hero + content
   - About page team grid
   - Services/products grid
   - Contact page form + info

5. **Optimize responsive design**
   - Test mobile experience (actual device if possible)
   - Adjust font sizes with media queries
   - Ensure navigation works on all sizes
   - Verify touch targets

6. **Add refinements**
   - Smooth transitions/animations
   - Hover states
   - Loading states
   - Accessibility testing

### Deliverables
- 4+ page HTML files
- Single `styles.css` file (maintainable, organized)
- Fully responsive (mobile, tablet, desktop)
- Dark mode support
- All pages consistent
- Valid HTML on all pages
- WCAG AA accessibility compliance

---

## CSS Best Practices Checklist

### Code Organization
- [ ] CSS file is organized (grouped by component, responsive at bottom)
- [ ] Comments explain complex selectors
- [ ] Consistent indentation (2-4 spaces)
- [ ] No duplicate rules
- [ ] Reusable component classes used
- [ ] CSS variables for colors, spacing, fonts

### Responsive Design
- [ ] Mobile-first approach (base = mobile)
- [ ] Media queries with min-width (not max-width)
- [ ] Tested on multiple screen sizes
- [ ] Touch targets are 44x44px minimum
- [ ] Text readable without zoom
- [ ] Images responsive (100% width)

### Accessibility
- [ ] Color contrast meets WCAG AA (4.5:1)
- [ ] Link text is descriptive (not "click here")
- [ ] Focus indicators visible
- [ ] Keyboard navigation works
- [ ] No flashing content (>3x/second)
- [ ] Color not used alone for meaning
- [ ] Form labels associated with inputs

### Performance
- [ ] CSS file minified (or planned for)
- [ ] Critical CSS inlined in `<style>` (if needed)
- [ ] No @import (slower than `<link>`)
- [ ] No unused CSS/selectors
- [ ] Web fonts optimized (woff2, fewer weights)

### Browser Support
- [ ] Tested in Chrome, Firefox, Safari
- [ ] Fallbacks for older browsers (if needed)
- [ ] Vendor prefixes where necessary (-webkit-, -moz-)
- [ ] Graceful degradation for unsupported features

---

## CSS Debugging Tips

1. **Border all elements to see layout**
   ```css
   * { border: 1px solid red !important; }
   ```

2. **Check specificity**
   - Fewer selectors =better
   - Use inspector to see which rules apply

3. **Test responsive breakpoints**
   - Use Chrome DevTools responsive mode
   - Test at exact breakpoints (768px, 1024px)

4. **Accessibility testing**
   - Disable CSS to verify HTML structure
   - Tab through interactive elements
   - Test color contrast with tools

5. **Performance optimization**
   - Measure CSS file size
   - Check for unused CSS (Coverage tab in DevTools)
   - Lazy-load web fonts

---

## Project Submission Checklist

For each project, before considering complete:

### Code Quality
- [ ] Valid CSS (no syntax errors)
- [ ] No inline styles
- [ ] Consistent naming convention
- [ ] Proper indentation
- [ ] Comments for complex sections
- [ ] No duplicate rules

### Responsive Design
- [ ] Works on mobile (320px)
- [ ] Works on tablet (768px)
- [ ] Works on desktop (1024px+)
- [ ] Touch targets adequate (44x44px)
- [ ] No horizontal scrolling

### Accessibility
- [ ] Keyboard navigation works
- [ ] Focus indicators visible
- [ ] Color contrast compliant (4.5:1)
- [ ] ARIA labels where needed
- [ ] Images have alt text

### Visual Design
- [ ] Consistent spacing
- [ ] Proper typography hierarchy
- [ ] Smooth transitions/animations
- [ ] Hover states clear
- [ ] Professional appearance

### Browser Testing
- [ ] Chrome latest
- [ ] Firefox latest
- [ ] Safari latest
- [ ] Mobile Safari

---

## Helpful Resources

- [MDN: CSS Documentation](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [CSS Tricks: Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [CSS Tricks: Grid Guide](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [Web.dev: Responsive Design](https://web.dev/responsive-web-design-basics/)
- [WebAIM: Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [Can I Use: Browser Support](https://caniuse.com/)
- [Google Fonts](https://fonts.google.com/)
