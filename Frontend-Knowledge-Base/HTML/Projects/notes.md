# HTML Projects

## Project 1: Personal Portfolio Website

### Project Overview
Build a professional portfolio website showcasing your skills, projects, and contact information. This project covers semantic HTML structure, form creation, and accessibility.

### Requirements

#### Structure & Sections
- **Header/Navigation**: Logo and navigation menu with links to all sections
- **Hero Section**: Eye-catching introduction with your name and tagline
- **About Section**: Brief bio, skills list, and professional summary
- **Projects Section**: 4-6 project cards with descriptions and links
- **Contact Section**: Contact form with validation attributes
- **Footer**: Copyright, social links, and secondary navigation
- **Responsive Layout**: Single column on mobile, 2+ columns on desktop (HTML structure supports this)

#### Requirements Checklist
- [ ] Use semantic HTML (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`)
- [ ] All navigation links work and point to correct sections
- [ ] Create a proper contact form with email, name, subject, and message fields
- [ ] Use `<picture>` element for responsive hero image
- [ ] Include proper alt text for all images
- [ ] Add meta tags (title, description, OpenGraph tags)
- [ ] Implement mobile viewport meta tag
- [ ] Validate HTML with W3C Validator
- [ ] Make navigation accessible with keyboard (Tab)
- [ ] Include focus indicators visible on interactive elements
- [ ] Labels properly associated with form inputs

### Step-by-Step Guidance

1. **Create the HTML skeleton**
   - Start with proper DOCTYPE and meta tags
   - Structure major sections
   - Use semantic elements throughout

2. **Build the header and navigation**
   - Logo/site title in header
   - Navigation list with links to each section
   - Make it accessible with proper link semantics

3. **Develop the hero section**
   - Large headline and subheadline
   - Call-to-action button
   - Background image using `<picture>` for responsiveness

4. **Create project cards**
   - Use consistent HTML structure for reusability
   - Include image, title, description, and link
   - Use `data-*` attributes to store project metadata

5. **Build the contact form**
   - Proper form structure with `<fieldset>` for grouping
   - Email field with type="email"
   - Text area for message
   - Submit button

6. **Add footer**
   - Social media links
   - Copyright info
   - Back-to-top link

7. **Optimize and validate**
   - Run through W3C Validator
   - Test with screen reader
   - Test keyboard navigation

### Deliverables
- `index.html` - Main portfolio page
- Valid HTML (0 errors from W3C Validator)
- At least 4-6 project items
- Fully functional contact form
- All accessibility requirements met

---

## Project 2: E-Commerce Product Listing Page

### Project Overview
Create an e-commerce product page with filters, search, and product catalog. This project emphasizes proper form structure, accessibility, and data organization.

### Requirements

#### Structure & Sections
- **Header**: Logo, search bar, shopping cart icon, navigation
- **Filter Sidebar**: 
  - Category checkboxes
  - Price range input
  - Rating filter
  - Sort dropdown
- **Product Grid**: Display 12+ products in a responsive grid
- **Search Results**: Show product count and allow "clear filters" button
- **Footer**: Company info, help links, newsletter signup

#### Product Card Elements
- Product image (thumbnail)
- Product name
- Price (with currency)
- Star rating (☆☆☆★★)
- Add to cart button
- "View details" link

#### Requirements Checklist
- [ ] Search form with proper input and submit button
- [ ] Multiple filter types (checkboxes, range slider, dropdown)
- [ ] All form inputs have `name` and `id` attributes
- [ ] Labels properly associated with form elements
- [ ] Product cards structured with `<article>` elements
- [ ] Images have descriptive alt text
- [ ] Price displayed in a `<span>` with currency symbol
- [ ] Rating displayed accessibly (not just stars)
- [ ] "Add to cart" buttons use proper `<button>` element
- [ ] Form doesn't require JavaScript for basic submission
- [ ] Meta tags optimized for product page SEO
- [ ] Product grid is responsive (3 cols desktop, 2 cols tablet, 1 col mobile)

### Step-by-Step Guidance

1. **Create the page structure**
   - Implement header with search form
   - Create main content area with sidebar and grid section
   - Plan footer layout

2. **Build the search form**
   - Input field for search query
   - Submit button
   - Use proper form semantics

3. **Create the filter sidebar**
   - Categories: Use checkboxes with labels
   - Price range: Input type range or number inputs
   - Rating: Radio buttons or dropdown
   - Sort: Select dropdown with options

4. **Design product cards**
   - Use `<article>` for each product
   - Include image, name, price, rating
   - Add quantity selector (input type="number")
   - Action buttons (cart, wishlist, details)

5. **Add accessibility**
   - Use `<fieldset>` and `<legend>` for filter groups
   - Aria-labels for icon-only buttons
   - Color contrast for price and ratings
   - Keyboard navigable buttons

6. **Meta tags and SEO**
   - Product category in title
   - Description mentioning benefits
   - OpenGraph image of featured product

### Deliverables
- `products.html` - Product listing page
- Valid HTML structure
- 12+ product items (can be hardcoded for this project)
- Fully functional filter system (HTML only, no JS required)
- Search form
- Accessible product cards

---

## Project 3: Multi-Page Documentation Website

### Project Overview
Create a documentation/blog website with multiple pages, navigation, and a table of contents. This project emphasizes proper heading hierarchy, semantic articles, and cross-page navigation.

### Requirements

#### Site Structure
- **Home page**: Overview and featured articles
- **3-5 Documentation pages**: Each covering a different topic
  - Example: "Getting Started", "API Reference", "Tutorials", "FAQ"
- **Navigation**: Header nav that works on all pages
- **Sidebar**: Table of contents for current page
- **Breadcrumbs**: Show current location (Home > Docs > Getting Started)
- **Page footer**: Previous/Next navigation links

#### Content Structure
- Main heading (h1) - only one per page
- Section headings (h2) at top level
- Subsection headings (h3) within section
- Code examples in `<pre>` and `<code>` blocks
- Callout boxes for important information
- Internal cross-links between pages
- External references and citations

#### Requirements Checklist
- [ ] Single h1 per page
- [ ] Proper heading hierarchy (don't skip levels: h1 → h2 → h3)
- [ ] Navigation works on every page (no broken links)
- [ ] Breadcrumb navigation on content pages
- [ ] Table of contents auto-generated from page headings
- [ ] Code blocks properly marked as `<pre><code>`
- [ ] Tables used for structured data (not layout)
- [ ] Images have alt text (include captions in `<figcaption>`)
- [ ] Internal links use relative paths (/docs/api)
- [ ] External links open in new tab (target="_blank")
- [ ] Mobile-responsive HTML structure
- [ ] Consistent meta tags on each page (unique titles/descriptions)
- [ ] Breadcrumbs use semantic list structure

### Step-by-Step Guidance

1. **Create a common header/footer template**
   - Logo and main navigation
   - Used on all pages
   - Links point to all page sections

2. **Design the home page**
   - Hero section
   - Featured content/articles
   - Quick navigation to main docs

3. **Create documentation page template**
   - Sidebar with table of contents
   - Main content area with article
   - Breadcrumbs at top
   - Previous/Next navigation at bottom

4. **Develop individual documentation pages**
   - Follow consistent heading structure
   - Use proper semantic HTML for content
   - Include code examples and callouts
   - Cross-link to related pages

5. **Build table of contents**
   - List of page headings as links (anchor tags with #)
   - Update for each page

6. **Meta tags per page**
   - Unique title (page topic)
   - Description mentioning content
   - Canonical URL

### Deliverables
- `index.html` - Home page
- `docs/` folder with 3-5 documentation pages
- Consistent navigation across all pages
- Valid HTML structure
- Table of contents that works properly
- Responsive structure (adapts to mobile)
- All cross-links working

---

## Project Submission Checklist

For each project, before considering it complete:

### Code Quality
- [ ] Uses semantic HTML elements appropriately
- [ ] No warning/errors from W3C Validator
- [ ] Consistent indentation (2 or 4 spaces)
- [ ] Meaningful class names (aligned with BEM or similar)
- [ ] Unique, descriptive IDs where needed
- [ ] Proper use of `data-*` attributes for custom data

### Accessibility
- [ ] Keyboard navigation works (Tab, Enter, Escape)
- [ ] Focus indicators are visible
- [ ] All interactive elements reachable with Tab key
- [ ] Images have proper alt text
- [ ] Links have descriptive text (not "click here")
- [ ] Forms have labels associated with inputs
- [ ] Color not used alone to convey information
- [ ] Tested with screen reader simulation

### Mobile Responsiveness
- [ ] HTML structure supports mobile layout (CSS handles responsiveness)
- [ ] No horizontal scrolling on mobile
- [ ] Touch targets are large enough (44x44px minimum)
- [ ] Meta viewport tag present

### Performance
- [ ] Images are optimized
- [ ] No duplicate resources
- [ ] Script tags are deferred or async
- [ ] CSS is organized

### Testing
- [ ] Tested in Chrome, Firefox, Safari
- [ ] Works with JavaScript disabled
- [ ] All forms submit properly
- [ ] Links navigate correctly
- [ ] Page loads completely (no 404 errors)

---

## Tips for Project Success

1. **Start with HTML first** - Don't worry about CSS initially. Get structure right.
2. **Use semantic elements** - They provide meaning and improve accessibility.
3. **Test frequently** - Validate HTML as you build, don't wait until the end.
4. **Plan before coding** - Sketch the page structure on paper first.
5. **Think about users** - Keyboard users, screen reader users, slow connections.
6. **Reuse patterns** - Create consistent components (card, button, form group).
7. **Document your code** - Comments explain complex structures.
8. **Get feedback** - Have someone else test your site.

---

## Learning Resources

- [MDN: HTML](https://developer.mozilla.org/en-US/docs/Web/HTML)
- [Web.dev: HTML Best Practices](https://web.dev/articles/)
- [W3C Validator](https://validator.w3.org/)
- [WebAIM Accessibility](https://webaim.org/)
- [Can I Use](https://caniuse.com/) - Browser support checking
