# JavaScript Foundations

## Topic 1: Variables, Data Types & JavaScript Basics

### Deep-Dive Explanation

JavaScript is the programmable glue of web pages. Variables store data, data types define what kind of data, and understanding the difference between `var`, `let`, and `const` is fundamental. JavaScript is dynamically typed - variables can hold any type and change types at runtime.

**Behind-the-Scenes:**
- `var` is function-scoped (old, avoid in modern code)
- `let` is block-scoped (preferred for mutable values)
- `const` is block-scoped, cannot be reassigned (preferred for constants)
- All values are either primitives (immutable) or objects (mutable)
- Primitive types: string, number, boolean, null, undefined, symbol, bigint
- Primitive values are copied by value, objects by reference
- Type coercion happens automatically (can cause bugs)
- `===` is strict equality (no coercion), `==` is loose equality (coerces types)

### Code Examples

### Right Way ✅
```javascript
// Use const by default, let if reassignment needed
const PI = 3.14159;        // Won't change
let count = 0;             // Will change
const name = 'Alice';      // Won't change

// Primitive types
const age = 25;            // number
const name = 'Bob';        // string
const isStudent = true;    // boolean
const nothingHere = null;  // intentional absence
let undefinedVar;          // undefined (not assigned)

// Objects (arrays, functions, plain objects)
const user = {             // object literal
    name: 'Charlie',
    age: 30,
    email: 'charlie@example.com'
};

const colors = ['red', 'green', 'blue'];  // array (special object)

// Template literals for string interpolation
const greeting = `Hello, ${name}! You are ${age} years old.`;
// Instead of: 'Hello, ' + name + '! You are ' + age + ' years old.'

// Strict equality (preferred)
5 === '5'    // false (different types)
5 === 5      // true (same type, same value)

// Loose equality (avoid - coerces types)
5 == '5'     // true (converts string to number)
5 == 5       // true

// Destructuring (extract values)
const { name, age } = user;        // From object
const [first, second] = colors;    // From array
console.log(name, age, first);     // Charlie, 30, red

// Spread operator (expand arrays/objects)
const moreColors = [...colors, 'yellow', 'purple'];
const newUser = { ...user, age: 31 };  // Copy and update

// Nullish coalescing (use right side if left is null/undefined)
const displayName = name ?? 'Guest';   // Safe

// Optional chaining (safely access nested properties)
const userEmail = user?.email ?? 'no-email';  // Safe navigation
```

### Common Mistake ❌
```javascript
// Using var (function-scoped, hoisted)
for (var i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 1000);
    // Prints 3, 3, 3 (i is function-scoped)
}

// Loose equality causes unexpected results
if ('0' == false) {
    console.log('true');  // Prints 'true' (unexpected!)
}

0 == false     // true (weird!)
'' == false    // true (weird!)
null == undefined  // true (but null === undefined is false!)

// Forgetting const/let, creates global variable
function setup() {
    statusMessage = 'Ready';  // Global! Bad!
}

// Confusing null and undefined
const x = null;        // Intentional absence
const y = undefined;   // Missing value
x == y;                // true (loose equality)
x === y;               // false (strict equality)

// Mutating const doesn't prevent property changes
const user = { name: 'Alice' };
user.name = 'Bob';     // OK! (const prevents reassignment, not mutation)
user = {};             // Error! (can't reassign)

// Forgetting to declare variables (accidentally global)
function getData() {
    data = fetchData();  // No let/const - creates global!
}

// Type coercion confusion
'5' + 3              // '53' (string concatenation)
'5' - 3              // 2 (numeric subtraction, coerces)
'5' * 3              // 15 (numeric multiplication)
true + 1             // 2 (boolean coerced to 1)
```

**Why it matters:** Variables and types are the foundation. Using const/let and strict equality prevents many bugs.

### Practical Tasks

**Task 1:** Data types exploration
- Create variables of each primitive type
- Create objects and arrays
- Use template literals with variables
- Practice destructuring from objects and arrays
- Use spread operator with arrays and objects

**Task 2:** Equality practice
- Compare primitives with === and ==
- Observe coercion behavior
- Write conditional logic using strict equality
- Understand why === is preferred
- Identify situations where coercion causes bugs

**Task 3:** Scope investigation
- Compare var, let, and const behavior
- Test block scope with let/const
- Observe variable hoisting
- Write code that relies on proper scoping
- Refactor old var code to use const/let

### Revision Mind Map

```
JavaScript Basics
├── Variables
│   ├── const (preferred, block-scoped, no reassign)
│   ├── let (block-scoped, can reassign)
│   └── var (avoid: function-scoped, hoisted)
├── Primitive Types
│   ├── string ('text', "text", `template`)
│   ├── number (5, 3.14, NaN, Infinity)
│   ├── boolean (true, false)
│   ├── null (intentional absence)
│   ├── undefined (uninitialized)
│   ├── symbol (unique identifier)
│   └── bigint (large integers)
├── Objects
│   ├── {} (plain object, mutable)
│   ├── [] (array, ordered mutable)
│   ├── function () {} (functions)
│   └── new Date(), new Map(), etc.
├── Type Coercion
│   ├── === (strict, no coercion)
│   ├── == (loose, coerces types)
│   └── Avoid == (unpredictable)
├── Modern Syntax
│   ├── Template literals: `text ${var}`
│   ├── Destructuring: const { x, y } = obj
│   ├── Spread: [...array], { ...obj }
│   ├── Optional chaining: obj?.prop
│   └── Nullish coalescing: x ?? 'default'
└── Best Practices
    ├── Use const by default
    ├── Use let if reassign needed
    ├── Never use var
    ├── Use === for comparison
    ├── Destructure when possible
```

---

## Topic 2: Understanding the DOM (Document Object Model)

### Deep-Dive Explanation

The DOM is a live, tree-structured representation of your HTML. JavaScript can read from and write to the DOM, creating dynamic, interactive web pages. The DOM is the bridge between HTML and JavaScript.

**Behind-the-Scenes:**
- The browser parses HTML and creates the DOM tree
- Each HTML element becomes a DOM Node
- Document is the root of the DOM tree
- Element nodes have properties (id, className, innerHTML, etc.) and methods
- The DOM is live - changes to DOM appear immediately in browser
- Accessing DOM elements is slow (compared to JavaScript operations) - minimize queries
- Modifying DOM causes layout recalculation (reflow) - expensive operation
- CSS selectors work in JavaScript (querySelector)

### Code Examples

### Right Way ✅
```javascript
// 1. SELECTING ELEMENTS

// querySelector (modern, flexible)
const button = document.querySelector('#submit-button');      // by ID
const input = document.querySelector('.search-input');        // by class
const firstPara = document.querySelector('p');               // by tag
const link = document.querySelector('a[href="#contact"]');  // complex selector

// querySelectorAll (returns all matches)
const paragraphs = document.querySelectorAll('p');
const items = document.querySelectorAll('.list-item');

// getElementById (only by ID, specific)
const header = document.getElementById('main-header');

// For repeated access, cache the element
const form = document.querySelector('#contact-form');
form.addEventListener('submit', handleSubmit);
form.reset();  // Access saved element, no new query

// 2. READING PROPERTIES

const element = document.querySelector('.card');

// Content
console.log(element.textContent);      // Only text, ignores HTML
console.log(element.innerHTML);        // HTML and text (be careful!)

// Attributes
console.log(element.id);               // Element ID
console.log(element.className);        // CSS classes (string)
console.log(element.getAttribute('data-card-id'));  // Custom attributes

// Styling
console.log(element.style.color);      // Inline styles (limited)
console.log(element.classList);        // DOMTokenList, easier than className

// Size/position
console.log(element.offsetWidth);      // Width including border
console.log(element.offsetHeight);     // Height including border
console.log(element.getBoundingClientRect());  // Position + size relative to viewport

// 3. MODIFYING CONTENT

const target = document.querySelector('.status');

// Safe: text content only
target.textContent = 'Loading...';

// Use innerHTML only if you MUST include HTML
const html = '<strong>Important:</strong> Read this!';
target.innerHTML = html;  // Only if HTML is under your control!

// Creating and inserting elements
const newParagraph = document.createElement('p');
newParagraph.textContent = 'New paragraph';
document.body.appendChild(newParagraph);

// Create from template (safer for HTML)
const template = document.querySelector('#item-template');
const clone = template.content.cloneNode(true);
document.querySelector('.list').appendChild(clone);

// 4. MODIFYING ATTRIBUTES & CLASSES

const button = document.querySelector('button');

// Attributes
button.setAttribute('disabled', '');    // Add disabled
button.removeAttribute('disabled');     // Remove disabled
button.hasAttribute('disabled');        // Check existence

// Classes (preferred over className)
button.classList.add('active');         // Add class
button.classList.remove('active');      // Remove class
button.classList.toggle('active');      // Add if missing, remove if present
button.classList.contains('active');    // Check class

// 5. SAFE DOM UPDATES

// Bad: modifying one at a time (slow, causes reflows)
for (let i = 0; i < 1000; i++) {
    document.body.appendChild(document.createElement('div'));
}

// Good: batch updates
const fragment = document.createDocumentFragment();
for (let i = 0; i < 1000; i++) {
    fragment.appendChild(document.createElement('div'));
}
document.body.appendChild(fragment);  // Single reflow

// 6. EVENT DELEGATION (listening from parent)

// Bad: attach listener to each item (memory intensive)
document.querySelectorAll('.button').forEach(button => {
    button.addEventListener('click', handleClick);
});

// Good: listen on parent, handle bubbled events
document.querySelector('.button-container').addEventListener('click', (event) => {
    if (event.target.classList.contains('button')) {
        handleClick.call(event.target);
    }
});

// 7. DATA ATTRIBUTES

const card = document.querySelector('.card');
console.log(card.dataset.cardId);      // Reads data-card-id
console.log(card.dataset.type);        // Reads data-type

card.dataset.status = 'active';        // Sets data-status="active"
```

### Common Mistake ❌
```javascript
// Querying repeatedly (inefficient)
for (let i = 0; i < 10; i++) {
    document.querySelector('.counter').textContent = i;  // Queries 10 times
}

// Using innerHTML with untrusted data (XSS vulnerability)
const userInput = getUserInput();  // Could be malicious
element.innerHTML = userInput;     // UNSAFE!

// Modifying className as string (error-prone)
element.className = element.className + ' active';  // String manipulation

// Using single quotes in CSS selector
const element = document.querySelector('#id-with-dash');  // Works
const element = document.querySelector('.class-name');    // Works

// Not handling missing elements
const missing = document.querySelector('.nonexistent');
missing.addEventListener('click', handler);  // Error! missing is null

// Inefficient event handlers on many elements
document.querySelectorAll('button').forEach(btn => {
    btn.addEventListener('click', handler);  // Many listeners
});
// Better: use event delegation

// Directly accessing element properties that might not exist
const value = document.querySelector('input').value;  // What if input doesn't exist?
const value = document.querySelector('input')?.value ?? '';  // Safe

// Confusion between textContent and innerText
element.textContent;   // Always works, ignores styling
element.innerText;     // Considers CSS (visibility, display), slower
```

**Why it matters:** The DOM is where JavaScript interacts with the page. Efficient DOM manipulation is critical for performance.

### Practical Tasks

**Task 1:** DOM selection and querying practice
- Select elements by ID, class, tag, and complex selectors
- Use querySelector vs querySelectorAll appropriately
- Cache element references to avoid repeated queries
- Test your selectors in browser console

**Task 2:** Modify DOM content and attributes
- Change text content of elements
- Add/remove HTML elements
- Modify CSS classes dynamically
- Update data attributes
- Create new elements and insert them

**Task 3:** Build an interactive to-do list
- Display a list of items from HTML
- Add remove buttons to each item
- Implement add new item functionality
- Toggle completed state with classes
- Use event delegation for efficiency

### Revision Mind Map

```
DOM (Document Object Model)
├── Selection
│   ├── querySelector (any CSS selector)
│   ├── querySelectorAll (all matches)
│   ├── getElementById (by ID only)
│   ├── getElementsByClassName (by class)
│   └── getElementsByTagName (by tag)
├── Reading
│   ├── element.textContent (text only)
│   ├── element.innerHTML (HTML + text)
│   ├── element.getAttribute('attr')
│   ├── element.className (string)
│   ├── element.classList (easier classes)
│   └── element.dataset (data-* attributes)
├── Writing
│   ├── element.textContent = 'text'
│   ├── element.innerHTML = '<html>'
│   ├── element.setAttribute('attr', 'value')
│   ├── element.classList.add/remove/toggle
│   └── element.removeAttribute('attr')
├── Creating/Inserting
│   ├── document.createElement('tag')
│   ├── parent.appendChild(child)
│   ├── parent.insertBefore(child, ref)
│   ├── parent.removeChild(child)
│   └── element.remove()
├── Layout Properties
│   ├── element.offsetWidth/Height
│   ├── element.getBoundingClientRect()
│   └── element.scrollHeight/Width
└── Performance
    ├── Cache element references
    ├── Use classList (not className)
    ├── Batch DOM updates
    ├── Event delegation
    └── Minimize reflows
```

---

## Topic 3: JavaScript Events & Listeners

### Deep-Dive Explanation

Events are how users interact with web pages (clicks, typing, scrolling, etc.). Event listeners respond to these interactions. Understanding event flow (capturing, bubbling, delegation) is essential for interactive JavaScript.

**Behind-the-Scenes:**
- Every interaction on a page triggers events
- Events bubble up the DOM tree (child to parent)
- Capturing phase goes down (parent to child), bubbling goes up
- Event listeners can be added with `addEventListener`
- `this` in event handler refers to the target element
- `event.target` is the element that triggered the event
- `event.currentTarget` is the element the handler is attached to
- `preventDefault()` stops default browser behavior
- `stopPropagation()` prevents event from bubbling to parent

### Code Examples

### Right Way ✅
```javascript
// 1. BASIC EVENT LISTENING

const button = document.querySelector('button');

// Modern approach: addEventListener
button.addEventListener('click', (event) => {
    console.log('Button clicked!');
    console.log('Target:', event.target);
});

// Function can be named (easier to remove)
function handleClick(event) {
    console.log('Clicked:', event.target);
}

button.addEventListener('click', handleClick);
button.removeEventListener('click', handleClick);  // Remove specific listener

// 2. COMMON EVENTS

const input = document.querySelector('input');
const form = document.querySelector('form');

// Typing
input.addEventListener('input', (event) => {
    console.log('Value changed:', event.target.value);
});

// Change (when input loses focus)
input.addEventListener('change', (event) => {
    console.log('Input changed and blurred:', event.target.value);
});

// Form submission
form.addEventListener('submit', (event) => {
    event.preventDefault();  // Stop page reload
    const formData = new FormData(form);
    console.log('Form submitted:', Object.fromEntries(formData));
});

// 3. MOUSE EVENTS

const element = document.querySelector('.interactive');

element.addEventListener('mouseenter', () => {
    element.classList.add('hover');  // Mouse entered
});

element.addEventListener('mouseleave', () => {
    element.classList.remove('hover');  // Mouse left
});

element.addEventListener('mousedown', () => {
    console.log('Mouse button pressed');
});

element.addEventListener('mouseup', () => {
    console.log('Mouse button released');
});

// 4. KEYBOARD EVENTS

document.addEventListener('keydown', (event) => {
    console.log('Key pressed:', event.key);
    
    if (event.key === 'Enter') {
        console.log('Enter pressed');
    }
    
    if (event.ctrlKey && event.key === 's') {
        event.preventDefault();  // Prevent browser save
        saveLocally();
    }
});

// 5. EVENT FLOW & DELEGATION

const list = document.querySelector('.list');

// Single listener on parent (efficient)
list.addEventListener('click', (event) => {
    const item = event.target.closest('.list-item');  // Find closest list-item
    
    if (item) {
        console.log('Item clicked:', item.textContent);
        item.classList.toggle('selected');
    }
});

// 6. EVENT DELEGATION FOR DYNAMIC CONTENT

const container = document.querySelector('.dynamic-items');

// Listener works for items added after page load
container.addEventListener('click', (event) => {
    if (event.target.matches('button.delete')) {  // Match selector
        console.log('Delete button clicked');
        event.target.closest('.item').remove();
    }
});

// 7. PREVENTING DEFAULTS AND PROPAGATION

const form = document.querySelector('form');
const submitButton = form.querySelector('button');

form.addEventListener('submit', (event) => {
    event.preventDefault();  // Prevent form submission (reload)
    console.log('Form prevented from submitting');
});

submitButton.addEventListener('click', (event) => {
    event.stopPropagation();  // Prevent bubbling to form
    console.log('Click handled, won\'t bubble to form');
});

// 8. CAPTURING VS BUBBLING

const parent = document.querySelector('.parent');
const child = document.querySelector('.child');

// Bubbling (default, most common)
parent.addEventListener('click', (event) => {
    console.log('Parent clicked (bubbling)');
}, false);  // false = bubbling phase (default)

child.addEventListener('click', (event) => {
    console.log('Child clicked (bubbling)');
}, false);

// Capturing (rare)
parent.addEventListener('click', (event) => {
    console.log('Parent clicked (capturing)');
}, true);  // true = capturing phase

// Click child: "Parent clicked (capturing)", "Child clicked (bubbling)", "Parent clicked (bubbling)"

// 9. ONCE OPTION

const loginButton = document.querySelector('.login');

loginButton.addEventListener('click', handleFirstLogin, { once: true });
// Handler fires only once, then removes itself

function handleFirstLogin() {
    console.log('First login!');
}
```

### Common Mistake ❌
```javascript
// Using onclick attribute (old, single handler)
// <button onclick="handleClick()">Click</button>
// Better: addEventListener (multiple handlers possible)

// Inline event handlers (poor separation)
button.onclick = handleClick;
button.onclick = handleOtherClick;  // Overwrites first!

// Not preventing default behavior
link.addEventListener('click', (event) => {
    // event.preventDefault();  // Missing!
    doSomething();
});  // Link still navigates away!

// Confusing event.target and event.currentTarget
button.addEventListener('click', (event) => {
    console.log(event.target);    // The clicked element
    console.log(event.currentTarget);  // The element handler attached to
});  // If button clicked, both are button. If child of button clicked, target is child!

// Not handling event delegation properly
document.querySelectorAll('.item').forEach(item => {
    item.addEventListener('click', handler);
});
// Breaks if items are added dynamically!

// Using event.stopPropagation() unnecessarily
// It prevents parent listeners from firing - usually want that to happen

// Not using preventDefault() when needed
form.addEventListener('submit', (event) => {
    validateAndSubmit();
});  // Form still submits to server!

// Memory leak with many listeners
for (let i = 0; i < 1000; i++) {
    const element = document.createElement('div');
    element.addEventListener('click', () => {
        console.log('Clicked', i);
    });
    document.body.appendChild(element);
}
// Better: use event delegation on parent
```

**Why it matters:** Events are how users interact with pages. Proper event handling makes sites responsive and efficient.

### Practical Tasks

**Task 1:** Create an interactive form
- Text input that updates display in real-time
- Form submission that prevents page reload
- Button clicks that toggle states
- Input validation on change event
- Display error messages

**Task 2:** Build a dynamic list manager
- Add items to list (from input + button)
- Delete items (event delegation)
- Check off completed items
- All without page reload
- Test that new items work correctly

**Task 3:** Keyboard shortcuts implementation
- Detect specific key presses
- Prevent browser defaults (Ctrl+S, Ctrl+A)
- Create keyboard navigation (arrows for menu)
- Implement Escape to close modals
- Document all shortcuts

### Revision Mind Map

```
JavaScript Events
├── Adding Listeners
│   ├── addEventListener('event', handler)
│   ├── addEventListener with options ({ once, capture })
│   ├── removeEventListener('event', handler)
│   └── Not: onclick attribute or .onclick property
├── Common Events
│   ├── Mouse: click, mouseenter, mouseleave, mousedown
│   ├── Keyboard: keydown, keyup, keypress
│   ├── Form: submit, change, input, focus, blur
│   ├── Document: DOMContentLoaded, load, scroll
│   └── Window: resize, (load), beforeunload
├── Event Object
│   ├── event.target (element that triggered)
│   ├── event.currentTarget (element handler attached to)
│   ├── event.key (which key pressed)
│   ├── event.ctrlKey, event.shiftKey (modifiers)
│   └── event.preventDefault() (block default)
├── Event Flow
│   ├── Capturing: parent → child
│   ├── Bubbling: child → parent (default)
│   ├── stopPropagation() (prevent bubbling)
│   └── stopImmediatePropagation() (prevent other handlers)
├── Event Delegation
│   ├── Listen on parent for child events
│   ├── Use event.target or event.closest()
│   ├── Efficient for many items
│   └── Works for dynamically added elements
└── Best Practices
    ├── Use addEventListener (not onclick)
    ├── Cache element references
    ├── Remove listeners if no longer needed
    ├── Use delegation for dynamic content
    └── preventDefault() only when needed
```

---

## Quick Reference: DOM & Event Cheat Sheet

| Method | Purpose | Example |
|--------|---------|---------|
| `document.querySelector(selector)` | Find one element | `querySelector('.card')` |
| `document.querySelectorAll(selector)` | Find all matching | `querySelectorAll('.item')` |
| `element.textContent` | Read/set text | `element.textContent = 'Hi'` |
| `element.innerHTML` | Read/set HTML | `element.innerHTML = '<p>Hi</p>'` |
| `element.classList.add(class)` | Add CSS class | `classList.add('active')` |
| `element.classList.remove(class)` | Remove CSS class | `classList.remove('active')` |
| `element.addEventListener(event, handler)` | Add listener | `addEventListener('click', fn)` |
| `event.preventDefault()` | Stop default behavior | `event.preventDefault()` |
| `event.stopPropagation()` | Stop bubbling | `event.stopPropagation()` |
| `element.appendChild(child)` | Add child | `parent.appendChild(child)` |
| `element.removeChild(child)` | Remove child | `parent.removeChild(child)` |

---

## Helpful Resources

- [MDN: JavaScript Basics](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps)
- [MDN: DOM Documentation](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)
- [MDN: Events Guide](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)
- [JavaScript.info: JavaScript Tutorial](https://javascript.info/)
- [Web.dev: JavaScript Fundamentals](https://web.dev/javascript/)
