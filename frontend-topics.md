# Frontend Learning Roadmap

This document provides a depth-first roadmap for mastering HTML5, CSS3, and Modern JavaScript (ES6+). The goal is to equip you with the foundational knowledge and practical skills to confidently approach any frontend framework.

---

## HTML5

### Core Concepts to Know
- **Document Structure**: `<!DOCTYPE html>`, `<html>`, `<head>`, `<body>`
- **Semantics**: proper use of `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`, `<aside>`
- **Forms**: `<form>`, input types, labels, validation attributes
- **Media**: `<img>`, `<picture>`, `<video>`, `<audio>`, `srcset`, `alt` text
- **Accessibility basics**: ARIA roles, `tabindex`, alt text, landmarks
- **Meta-tags**: `charset`, viewport settings for responsive design
- **Linking resources**: CSS, scripts, favicons

### Advanced Mechanics to Understand
- **Parsing and DOM construction**: how browsers parse HTML into the DOM tree
- **HTML5 parsing algorithm quirks**: handling malformed markup
- **Shadow DOM basics** and custom elements
- **Progressive enhancement & graceful degradation**
- **SEO fundamentals**: structured data, accessibility overlap

### Practical Skills to Practice
- Building forms with validation and custom controls
- Structuring an accessible page layout using semantic tags
- Managing media responsiveness and optimization strategies
- Using ARIA attributes and testing with screen readers

### Milestone Projects
1. **Personal blog template** with semantic markup and responsive images
2. **Custom survey form** with client-side validation and accessible widgets
3. **Media gallery** incorporating `<picture>` element and lazy loading

---

## CSS3

### Core Concepts to Know
- **Selectors & Specificity**: how rules apply, inheritance
- **Box Model**: margin, border, padding, content, `box-sizing`
- **Positioning**: static, relative, absolute, fixed, sticky
- **Display types**: `block`, `inline`, `inline-block`, `flex`, `grid`, `none`
- **Colors & Typography**: `rem`, `em`, custom properties, web fonts
- **Responsive design basics**: media queries, mobile-first
- **Accessibility considerations**: contrast, focus states, reduced-motion

### Advanced Mechanics to Understand
- **Rendering flow & layout process**: reflow vs repaint
- **CSS Cascade, specificity, and inheritance in depth**
- **Flexbox and Grid internals**: algorithmic layout behavior
- **Painting layers and GPU acceleration**
- **CSS Houdini fundamentals** (worklets, custom properties)
- **Performance best practices**: critical CSS, avoiding layout thrashing

### Practical Skills to Practice
- Creating fluid layouts with Flexbox and Grid
- Implementing responsive navigation and complex components
- Using custom properties for theming and maintainability
- Animations & transitions with `@keyframes`, `transform`, `opacity`
- Debugging layout issues using browser devtools

### Milestone Projects
1. **Responsive landing page** with grid-based hero section
2. **Dashboard UI** featuring card layout, sidebar, and responsive breakpoints
3. **Animated UI component library** (accordion, tabs, modals)

---

## Modern JavaScript (ES6+)

### Core Concepts to Know
- **Syntax enhancements**: `let`, `const`, arrow functions, template literals
- **Modules**: `import`/`export`, bundling concepts
- **Data structures**: `Map`, `Set`, `WeakMap`, `WeakSet`
- **Promises & async/await**
- **Closures and lexical scope**
- **Prototypes and inheritance**
- **Event Loop & concurrency model**
- **Strict mode**

### Advanced Mechanics to Understand
- **Memory management and garbage collection**
- **The Event Loop in depth**: microtasks, macrotasks
- **Compilation steps**: parsing, AST, bytecode (V8 specifics)
- **Module resolution and bundler behavior**
- **Advanced prototypal inheritance patterns**
- **Decorators, proxies, and reflect API**
- **Web APIs**: `fetch`, `WebSocket`, `IndexedDB`, `Service Worker`

### Practical Skills to Practice
- Writing asynchronous code with fetch/async-await
- Manipulating the DOM and handling events efficiently
- Using localStorage/sessionStorage and working with JSON
- Implementing a simple state container (pub/sub or observer)
- Debugging with breakpoints, console, and performance profiling

### Milestone Projects
1. **To-do list app** with add/edit/delete and localStorage persistence
2. **Real-time chat front end** using WebSocket or polling
3. **Single-page application (SPA)** with manual routing and dynamic imports

---

## Prerequisites for Frameworks
- **Component thinking**: breaking UI into reusable pieces, props/slots
- **State management concepts**: uni-directional data flow, immutability, reducers, context
- **Routing fundamentals**: client-side routing, history API
- **Build tools & package management**: NPM/Yarn, Vite, Webpack, Babel
- **Tooling**: linters (ESLint), formatters (Prettier), TypeScript basics
- **Testing basics**: unit tests with Jest/RTL, end-to-end with Cypress
- **Accessibility** as a constant concern in component design
- **Debugging frameworks**: using React DevTools, Vue Devtools, etc.
- **Performance optimization**: code splitting, lazy loading, tree shaking
- **Version control workflow**: commits, branching, PRs

> By mastering these foundational areas and building real projects, you'll be well-prepared to learn and use any modern frontend framework.
