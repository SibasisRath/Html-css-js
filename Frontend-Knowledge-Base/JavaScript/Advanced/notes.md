# JavaScript Advanced

## Topic 1: Advanced DOM Manipulation & Performance

### Deep-Dive Explanation

DOM manipulation is how JavaScript creates interactive experiences. Advanced techniques prevent performance issues when dealing with large numbers of elements or frequent updates. Understanding the DOM's performance characteristics is crucial for fast, responsive applications.

**Behind-the-Scenes:**
- Every DOM change triggers reflow (layout calculation) and repaint (drawing)
- Reflow is expensive - minimize changes to avoid cascading reflows
- Reading properties that trigger reflow (offsetWidth, getBoundingClientRect) forces synchronous calculation
- Using DocumentFragment batches changes into a single reflow
- Virtual DOM concepts (used in React) avoid many reflows
- CSS transforms and changes to opacity don't trigger reflow (GPU-accelerated)
- `requestAnimationFrame` syncs with browser's repaint cycle (60fps)

### Code Examples

### Right Way ✅
```javascript
// 1. EFFICIENT DOM UPDATES - batch changes

// Bad: multiple reflows
for (let i = 0; i < 100; i++) {
    const div = document.createElement('div');
    div.textContent = `Item ${i}`;
    document.body.appendChild(div);  // Reflow each time!
}

// Good: batch with DocumentFragment
const fragment = document.createDocumentFragment();
for (let i = 0; i < 100; i++) {
    const div = document.createElement('div');
    div.textContent = `Item ${i}`;
    fragment.appendChild(div);  // No reflow yet
}
document.body.appendChild(fragment);  // Single reflow!

// 2. HTML TEMPLATES (for complex structures)

// Define reusable structure
const template = document.querySelector('#card-template');

function createCard(data) {
    const clone = template.content.cloneNode(true);  // Deep clone
    clone.querySelector('.title').textContent = data.title;
    clone.querySelector('.description').textContent = data.description;
    clone.querySelector('img').src = data.image;
    return clone;
}

const cards = [
    { title: 'Card 1', description: 'Desc 1', image: 'img1.jpg' },
    { title: 'Card 2', description: 'Desc 2', image: 'img2.jpg' }
];

const fragment = document.createDocumentFragment();
cards.forEach(card => {
    fragment.appendChild(createCard(card));
});
document.querySelector('.container').appendChild(fragment);

// 3. MINIMIZING REFLOWS - read then write

// Bad: alternating reads and writes (triggers reflows)
for (let i = 0; i < elements.length; i++) {
    elements[i].style.width = elements[i].offsetWidth + 10 + 'px';
}

// Good: read all, then write all
const widths = elements.map(el => el.offsetWidth + 10);  // Read all
widths.forEach((width, i) => {
    elements[i].style.width = width + 'px';  // Write all
});

// 4. EFFICIENT DOM TRAVERSAL

const item = document.querySelector('.list-item');

// Bad: querying from document each time
const parent = document.querySelector('.parent');
const siblings = document.querySelectorAll('.parent > .item');

// Good: use element methods
const parent = item.parentElement;
const siblings = parent.children;  // Direct access, no query
const prevSibling = item.previousElementSibling;
const nextSibling = item.nextElementSibling;

// 5. BULK STYLE CHANGES

const items = document.querySelectorAll('.item');

// Bad: modifying inline styles (triggers reflow per item)
items.forEach(item => {
    item.style.color = 'red';
    item.style.backgroundColor = 'yellow';
    item.style.padding = '10px';
});

// Good: add/remove classes
items.forEach(item => {
    item.classList.add('highlighted');  // Single reflow
});

// Or use cssText for multiple properties
items.forEach(item => {
    item.style.cssText = 'color: red; background: yellow; padding: 10px;';
});

// 6. ANIMATIONS WITH requestAnimationFrame

// Syncs with browser repaint cycle (60fps)
function smoothScroll(element, targetScroll) {
    let currentScroll = element.scrollTop;
    const step = (targetScroll - currentScroll) / 20;  // 20 frames
    let frame = 0;
    
    function animate() {
        currentScroll += step;
        element.scrollTop = currentScroll;
        frame++;
        
        if (frame < 20) {
            requestAnimationFrame(animate);  // Schedule next frame
        }
    }
    
    requestAnimationFrame(animate);
}

// 7. CLONING ELEMENTS (efficient for repetition)

const original = document.querySelector('.card-template');

// Clone and modify (faster than createElement + building)
for (let i = 0; i < 100; i++) {
    const clone = original.cloneNode(true);
    clone.querySelector('.id').textContent = i;
    document.querySelector('.container').appendChild(clone);
}

// 8. VISIBILITY TOGGLE (vs remove/add)

const element = document.querySelector('.modal');

// Hide without removing from DOM
element.style.display = 'none';  // or visibility: hidden

// Show again
element.style.display = 'block';

// Or use CSS class
element.classList.add('hidden');  // CSS: .hidden { display: none; }
element.classList.remove('hidden');

// 9. EVENT DELEGATION (central pattern)

const list = document.querySelector('.list');

// Instead of adding listener to 100 items, add to parent
list.addEventListener('click', (event) => {
    const item = event.target.closest('.list-item');
    if (item) {
        handleItemClick(item);
    }
});

// 10. LAZY RENDERING (load on scroll)

const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            // Element entered viewport
            entry.target.classList.add('loaded');
            observer.unobserve(entry.target);
        }
    });
});

document.querySelectorAll('[data-lazy]').forEach(el => {
    observer.observe(el);
});
```

### Common Mistake ❌
```javascript
// Checking offsetWidth inside loop (forces reflow each time)
for (let i = 0; i < items.length; i++) {
    items[i].style.width = (items[i].offsetWidth * 1.1) + 'px';
}

// Modifying innerHTML with concatenation (loses event listeners)
let html = element.innerHTML;
html += '<p>New paragraph</p>';
element.innerHTML = html;  // Rebuilds entire element!

// Creating elements with string concatenation (inefficient)
let str = '<div><span>Item</span></div>';
const container = document.createElement('div');
container.innerHTML = str;  // Parses HTML string

// Not caching element references
for (let i = 0; i < 1000; i++) {
    document.querySelector('.counter').textContent = i;  // Query 1000 times!
}

// Forgetting to cleanup event listeners (memory leak)
function setupListener() {
    const element = document.querySelector('.button');
    element.addEventListener('click', heavyFunction);
    // If element is removed and setupListener called again,
    // multiple listeners stack up!
}

// Synchronous rendering loops (blocks main thread)
while (scrollPos < targetScroll) {
    scrollPos += 10;
    element.scrollTop = scrollPos;
}  // Blocks everything until done

// Not using requestAnimationFrame (janky animations)
// Use setTimeout instead - doesn't sync with browser refresh
```

**Why it matters:** Large, slow DOM operations block user interaction. Efficient manipulation is essential for smooth, responsive sites.

### Practical Tasks

**Task 1:** Optimize DOM-heavy page
- Start with 500+ DOM elements being manipulated inefficiently
- Identify reflow triggers
- Refactor to batch updates, use fragments
- Measure performance improvements with DevTools
- Document bottlenecks and solutions

**Task 2:** Build an infinite scroll feature
- Load items as user scrolls down
- Use IntersectionObserver for efficiency
- Add loading indicator
- Prevent duplicate requests
- Handle end of list

**Task 3:** Create smooth animations
- Implement scroll animation using requestAnimationFrame
- Create element hover animations
- Measure FPS with DevTools
- Ensure 60fps performance
- Compare with CSS animations

---

## Topic 2: Fetch API & Async/Await (Data Communication)

### Deep-Dive Explanation

The Fetch API allows JavaScript to communicate with servers. It replaces XMLHttpRequest with a modern, promise-based interface. Async/await syntax makes asynchronous code readable and maintainable. This is your bridge to frameworks and backend integration.

**Behind-the-Scenes:**
- Fetch is async - returns a Promise that resolves with Response object
- Response is a stream - must call `.json()` or `.text()` to read data
- HTTP errors (404, 500) don't reject Promise - check response.ok
- CORS (Cross-Origin Resource Sharing) may block requests from browser
- Request headers tell server what format you're sending/expecting
- Response headers tell you what format data is in
- Async/await is syntactic sugar for Promise chains
- Error handling with try/catch is cleaner than .catch()

### Code Examples

### Right Way ✅
```javascript
// 1. BASIC FETCH

// GET request
async function fetchData() {
    try {
        const response = await fetch('/api/data');
        
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        
        const data = await response.json();
        console.log('Data:', data);
        return data;
    } catch (error) {
        console.error('Fetch failed:', error);
    }
}

// 2. POST REQUEST (sending data)

async function createUser(userData) {
    try {
        const response = await fetch('/api/users', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify(userData)  // Convert object to JSON
        });
        
        if (!response.ok) {
            throw new Error(`Failed to create user: ${response.status}`);
        }
        
        const newUser = await response.json();
        console.log('Created:', newUser);
        return newUser;
    } catch (error) {
        console.error('Creation failed:', error);
        throw error;  // Re-throw for caller to handle
    }
}

// 3. PUT/PATCH REQUEST (updating)

async function updateUser(userId, updates) {
    try {
        const response = await fetch(`/api/users/${userId}`, {
            method: 'PUT',  // Or PATCH for partial updates
            headers: {
                'Content-Type': 'application/json',
                'Authorization': `Bearer ${token}`  // Auth token
            },
            body: JSON.stringify(updates)
        });
        
        if (!response.ok) {
            throw new Error(`Update failed: ${response.status}`);
        }
        
        const updated = await response.json();
        return updated;
    } catch (error) {
        console.error('Update error:', error);
    }
}

// 4. DELETE REQUEST

async function deleteUser(userId) {
    try {
        const response = await fetch(`/api/users/${userId}`, {
            method: 'DELETE',
            headers: {
                'Authorization': `Bearer ${token}`
            }
        });
        
        if (!response.ok) {
            throw new Error(`Delete failed: ${response.status}`);
        }
        
        console.log('User deleted');
        return true;
    } catch (error) {
        console.error('Delete error:', error);
    }
}

// 5. HANDLING DIFFERENT CONTENT TYPES

async function fetchData(url) {
    try {
        const response = await fetch(url);
        
        // Check content type
        const contentType = response.headers.get('content-type');
        
        if (contentType.includes('application/json')) {
            return await response.json();
        } else if (contentType.includes('text')) {
            return await response.text();
        } else if (contentType.includes('blob')) {
            return await response.blob();  // File/image
        }
    } catch (error) {
        console.error('Fetch error:', error);
    }
}

// 6. UPLOAD FILE

async function uploadFile(file) {
    const formData = new FormData();
    formData.append('file', file);
    formData.append('type', 'profile-photo');
    
    try {
        const response = await fetch('/api/upload', {
            method: 'POST',
            headers: {
                'Authorization': `Bearer ${token}`
                // Don't set Content-Type - browser does it!
            },
            body: formData  // FormData object
        });
        
        if (!response.ok) {
            throw new Error('Upload failed');
        }
        
        const result = await response.json();
        return result;
    } catch (error) {
        console.error('Upload error:', error);
    }
}

// 7. FETCH WITH TIMEOUT

async function fetchWithTimeout(url, timeout = 5000) {
    const controller = new AbortController();
    const timeoutId = setTimeout(() => controller.abort(), timeout);
    
    try {
        const response = await fetch(url, {
            signal: controller.signal
        });
        
        clearTimeout(timeoutId);
        
        if (!response.ok) {
            throw new Error(`HTTP ${response.status}`);
        }
        
        return await response.json();
    } catch (error) {
        if (error.name === 'AbortError') {
            console.error('Request timed out');
        } else {
            console.error('Fetch error:', error);
        }
    }
}

// 8. SEQUENTIAL REQUESTS (wait for first, then second)

async function getUserWithPosts(userId) {
    try {
        // First request
        const userResponse = await fetch(`/api/users/${userId}`);
        const user = await userResponse.json();
        
        // Second request (depends on first)
        const postsResponse = await fetch(`/api/users/${userId}/posts`);
        const posts = await postsResponse.json();
        
        return { user, posts };
    } catch (error) {
        console.error('Error:', error);
    }
}

// 9. PARALLEL REQUESTS (multiple independent requests)

async function getMultipleData() {
    try {
        // All three requests start simultaneously
        const [usersRes, postsRes, commentsRes] = await Promise.all([
            fetch('/api/users'),
            fetch('/api/posts'),
            fetch('/api/comments')
        ]);
        
        const [users, posts, comments] = await Promise.all([
            usersRes.json(),
            postsRes.json(),
            commentsRes.json()
        ]);
        
        return { users, posts, comments };
    } catch (error) {
        console.error('Error fetching data:', error);
    }
}

// 10. USING FETCH TO UPDATE PAGE CONTENT

async function loadPostsIntoPage() {
    const container = document.querySelector('.posts-container');
    
    // Show loading state
    container.innerHTML = '<p>Loading...</p>';
    
    try {
        const response = await fetch('/api/posts');
        const posts = await response.json();
        
        // Clear loading
        container.innerHTML = '';
        
        // Render posts
        posts.forEach(post => {
            const article = document.createElement('article');
            article.className = 'post';
            article.innerHTML = `
                <h2>${post.title}</h2>
                <p>${post.content}</p>
                <button data-post-id="${post.id}">Delete</button>
            `;
            container.appendChild(article);
        });
        
        // Attach event listeners with delegation
        container.addEventListener('click', (event) => {
            if (event.target.matches('button')) {
                const postId = event.target.dataset.postId;
                deletePost(postId);
            }
        });
    } catch (error) {
        container.innerHTML = '<p>Error loading posts</p>';
        console.error('Error:', error);
    }
}

// 11. FORM SUBMISSION VIA FETCH

const form = document.querySelector('#contact-form');

form.addEventListener('submit', async (event) => {
    event.preventDefault();
    
    const formData = new FormData(form);
    
    try {
        const response = await fetch('/api/contact', {
            method: 'POST',
            body: formData
        });
        
        if (!response.ok) {
            throw new Error('Submission failed');
        }
        
        const result = await response.json();
        alert('Message sent!');
        form.reset();
    } catch (error) {
        alert('Error: ' + error.message);
    }
});
```

### Common Mistake ❌
```javascript
// Ignoring HTTP error status codes
const response = await fetch('/api/data');
const data = await response.json();  // May be error response!

// Should check:
if (!response.ok) {
    throw new Error(`HTTP ${response.status}`);
}

// Assuming JSON response without checking header
const data = await response.json();
// What if server returned HTML error page?

// Not handling network errors
await fetch('/api/data');  // Network error (timeout, no connection)
// Crashes if no try/catch!

// Blocking on sequential requests that could be parallel
const users = await fetch('/api/users').then(r => r.json());
const posts = await fetch('/api/posts').then(r => r.json());
// Better: use Promise.all() for both to happen simultaneously

// Forgetting async keyword
function fetchData() {  // Missing async
    const data = await fetch('/api/data');  // Syntax error!
}

// Not sending/parsing JSON correctly
const response = await fetch(url, {
    body: userData  // Should be JSON.stringify(userData)
});

// Memory leak with event listeners
async function loadData() {
    container.addEventListener('click', handler);
    // If loadData called multiple times, handlers stack up!
}

// Assuming fetch works like synchronous code
console.log('Fetching...');
fetch('/api/data').then(r => r.json()).then(d => {
    console.log('Got data:', d);  // This is second!
});
console.log('Done');  // This is first!
// Order: "Fetching...", "Done", "Got data..."
```

**Why it matters:** Fetch API is how you connect frontend to backend. It's essential for dynamic, data-driven applications.

### Practical Tasks

**Task 1:** Build a data-driven page with Fetch
- Display list of items from API
- Add ability to create new item
- Delete items from list
- Update item details
- Show loading/error states

**Task 2:** Create a weather app
- Fetch weather data from public API (OpenWeatherMap, WeatherAPI)
- Display current weather
- Show forecast
- Allow location search
- Refresh data periodically

**Task 3:** Build an image gallery from API
- Fetch images from API (Unsplash, Pexels, or custom)
- Display in grid
- Infinite scroll loading
- Search functionality
- Download/share buttons

### Revision Mind Map

```
Fetch API & Async/Await
├── Fetch Basics
│   ├── fetch(url, options) - returns Promise<Response>
│   ├── Method: GET, POST, PUT, PATCH, DELETE
│   ├── Headers: Content-Type, Authorization, etc.
│   └── Body: JSON.stringify(data), FormData, string
├── Response Object
│   ├── response.ok (true if 200-299 status)
│   ├── response.status (HTTP status code)
│   ├── response.headers (response headers)
│   ├── response.json() (parse as JSON)
│   ├── response.text() (parse as text)
│   └── response.blob() (parse as binary)
├── Async/Await
│   ├── async function (marks async)
│   ├── await expression (wait for Promise)
│   ├── try/catch (error handling)
│   └── Must use async before await
├── Request Types
│   ├── GET (retrieve data)
│   ├── POST (create data)
│   ├── PUT (replace data)
│   ├── PATCH (update data)
│   └── DELETE (remove data)
├── Advanced
│   ├── Promise.all() (parallel requests)
│   ├── Promise.race() (fastest request)
│   ├── AbortController (cancel requests)
│   └── FormData (file uploads)
└── Best Practices
    ├── Always check response.ok
    ├── Use try/catch for errors
    ├── Show loading state
    ├── Timeout long requests
    └── Use Promise.all for parallel
```

---

## Topic 3: Advanced JavaScript Patterns & Optimization

### Deep-Dive Explanation

As JavaScript becomes more complex, patterns and optimization techniques become essential. Closures, callbacks, promises, modules, and data caching are patterns that enable scalable applications. Performance optimization ensures responsive user experiences.

**Behind-the-Scenes:**
- Closure is a function that has access to variables from its parent scope
- Callback hell occurs when callbacks nest deeply - promises and async/await fix this
- Promises represent eventual completion/failure of async operation
- Module pattern (or ES modules) encapsulates code and prevents global pollution
- Debouncing and throttling prevent excessive function calls
- Memoization caches function results for reuse
- Generator functions can pause/resume execution
- WeakMap/WeakSet allow garbage collection of objects

### Code Examples

### Right Way ✅
```javascript
// 1. CLOSURES (functions with access to parent scope)

function createCounter(start = 0) {
    let count = start;  // Private variable
    
    return {
        increment() {
            return ++count;
        },
        decrement() {
            return --count;
        },
        get() {
            return count;
        }
    };
}

const counter = createCounter(10);
console.log(counter.increment());  // 11
console.log(counter.increment());  // 12
console.log(counter.get());        // 12
// count is private - can't access directly

// 2. DEBOUNCING (prevent excessive function calls)

function debounce(func, delay) {
    let timeoutId;
    
    return function(...args) {
        clearTimeout(timeoutId);
        timeoutId = setTimeout(() => {
            func(...args);
        }, delay);
    };
}

const searchInput = document.querySelector('input');
const debouncedSearch = debounce((query) => {
    console.log('Searching for:', query);
    fetch(`/api/search?q=${query}`);
}, 300);

searchInput.addEventListener('input', (event) => {
    debouncedSearch(event.target.value);
});
// Only searches 300ms after user stops typing

// 3. THROTTLING (limit function call frequency)

function throttle(func, limit) {
    let inThrottle;
    
    return function(...args) {
        if (!inThrottle) {
            func(...args);
            inThrottle = true;
            setTimeout(() => {
                inThrottle = false;
            }, limit);
        }
    };
}

window.addEventListener('scroll', throttle(() => {
    console.log('Scrolled!');
}, 1000));
// Only logs once per second, even if scrolling fast

// 4. MEMOIZATION (cache function results)

function memoize(func) {
    const cache = {};
    
    return function(...args) {
        const key = JSON.stringify(args);
        
        if (key in cache) {
            console.log('Returning cached result');
            return cache[key];
        }
        
        const result = func(...args);
        cache[key] = result;
        return result;
    };
}

const expensiveCalculation = memoize((n) => {
    console.log('Calculating...');
    return n * n;
});

console.log(expensiveCalculation(5));  // Calculates: 25
console.log(expensiveCalculation(5));  // Cached: 25 (no calculation)
console.log(expensiveCalculation(10)); // Calculates: 100

// 5. PROMISES (handling async operations)

function fetchUserWithPromise(userId) {
    return fetch(`/api/users/${userId}`)
        .then(response => {
            if (!response.ok) {
                throw new Error('User not found');
            }
            return response.json();
        })
        .then(user => {
            console.log('User loaded:', user);
            return user;
        })
        .catch(error => {
            console.error('Error:', error);
        });
}

// Much cleaner with async/await:
async function fetchUserWithAsync(userId) {
    try {
        const response = await fetch(`/api/users/${userId}`);
        
        if (!response.ok) {
            throw new Error('User not found');
        }
        
        const user = await response.json();
        console.log('User loaded:', user);
        return user;
    } catch (error) {
        console.error('Error:', error);
    }
}

// 6. ES MODULES (encapsulation)

// math.js
export function add(a, b) {
    return a + b;
}

export function multiply(a, b) {
    return a * b;
}

// app.js
import { add, multiply } from './math.js';

console.log(add(2, 3));        // 5
console.log(multiply(2, 3));   // 6

// 7. SINGLETON PATTERN (single instance)

const ConfigManager = (() => {
    let instance;
    
    function createInstance() {
        return {
            apiUrl: 'https://api.example.com',
            timeout: 5000,
            getConfig() {
                return this;
            }
        };
    }
    
    return {
        getInstance() {
            if (!instance) {
                instance = createInstance();
            }
            return instance;
        }
    };
})();

const config1 = ConfigManager.getInstance();
const config2 = ConfigManager.getInstance();
console.log(config1 === config2);  // true (same instance)

// 8. OBSERVER PATTERN (pub/sub)

class EventEmitter {
    constructor() {
        this.events = {};
    }
    
    on(event, callback) {
        if (!this.events[event]) {
            this.events[event] = [];
        }
        this.events[event].push(callback);
    }
    
    emit(event, data) {
        if (this.events[event]) {
            this.events[event].forEach(callback => {
                callback(data);
            });
        }
    }
}

const emitter = new EventEmitter();

emitter.on('user-login', (user) => {
    console.log('User logged in:', user.name);
});

emitter.emit('user-login', { name: 'Alice' });

// 9. GENERATOR FUNCTIONS (pausable functions)

function* countdown(n) {
    while (n > 0) {
        yield n;
        n--;
    }
}

const gen = countdown(3);
console.log(gen.next().value);  // 3
console.log(gen.next().value);  // 2
console.log(gen.next().value);  // 1

// 10. PERFORMANCE OPTIMIZATION

// Use const/let (faster than var)
const obj = { x: 1, y: 2 };  // Should not change

// Minimize object property access
const x = obj.deeply.nested.property.value;  // Cache it
// vs
function getValue() {
    return obj.deeply.nested.property.value;  // Repeated lookups slower
}

// Avoid global variables
// Good: use modules or IIFE
const app = (() => {
    const privateVar = 'private';
    return {
        publicMethod() {}
    };
})();
```

### Common Mistake ❌
```javascript
// Callback hell (deeply nested callbacks)
function loadData(callback) {
    fetch('/api/users').then(response => {
        response.json().then(users => {
            users.forEach(user => {
                fetch(`/api/users/${user.id}`).then(resp => {
                    resp.json().then(fullUser => {
                        callback(fullUser);  // Deeply nested!
                    });
                });
            });
        });
    });
}

// Better: use async/await

// Not debouncing search input (too many requests)
searchInput.addEventListener('input', (event) => {
    fetch(`/api/search?q=${event.target.value}`);
    // Requests fired on every keystroke!
});

// Mutating closure variables unexpectedly
for (var i = 0; i < 3; i++) {
    setTimeout(() => {
        console.log(i);  // Logs 3, 3, 3 (i is global)
    }, 1000);
}

// Forgetting 'new' with constructor
function User(name) {
    this.name = name;
}

const user = User('Alice');  // Missing 'new'!
// this.name is now a global variable!

// Memory leaks with closures
function setup() {
    const largeData = new Array(1000000);
    button.addEventListener('click', () => {
        console.log(largeData);  // Closure keeps largeData in memory!
    });
}

// Not removing event listeners
function setupPage() {
    button.addEventListener('click', handler);
}
setupPage();  // 1 listener
setupPage();  // 2 listeners (leaks!)
```

**Why it matters:** Good patterns make code maintainable. Performance optimization provides better user experience.

### Practical Tasks

**Task 1:** Implement search with debouncing
- Create search input
- Implement debounce function
- Fetch results from API (simulated)
- Display results
- Measure reduction in API calls

**Task 2:** Build a simple pub/sub event system
- Create EventEmitter class
- Subscribe to events
- Emit events with data
- Test with multiple listeners
- Use it in application

**Task 3:** Optimize script with profiling
- Identify performance bottlenecks
- Apply memoization
- Implement debouncing/throttling
- Measure improvements
- Document optimizations made

### Revision Mind Map

```
Advanced JavaScript
├── Closures & Scope
│   ├── Closure: function + parent variables
│   ├── Private variables with closures
│   ├── Module pattern
│   └── IIFE (Immediately Invoked Function Expression)
├── Performance Patterns
│   ├── Debouncing (after delay)
│   ├── Throttling (at intervals)
│   ├── Memoization (cache results)
│   └── Lazy loading (load on demand)
├── Async Patterns
│   ├── Callbacks (old, avoid deep nesting)
│   ├── Promises (.then().catch())
│   ├── Async/await (modern, preferred)
│   └── Promise.all/race (multiple operations)
├── Design Patterns
│   ├── Singleton (single instance)
│   ├── Observer/Pub-Sub (event system)
│   ├── Factory (create objects)
│   └── Module (encapsulation)
├── Advanced Features
│   ├── Generator functions (pausable)
│   ├── Symbols (unique values)
│   ├── Proxy (intercept operations)
│   └── Reflect (introspection)
└── Optimization
    ├── Minimize re-renders
    ├── Cache results
    ├── Reduce DOM queries
    ├── Event delegation
    └── Lazy load resources
```

---

## Quick Reference: Common Patterns

| Pattern | Use Case | Example |
|---------|----------|---------|
| Debounce | Search input, resize handlers | Fires after user stops typing |
| Throttle | Scroll events, window resize | Fires at most once per 100ms |
| Memoize | Expensive calculations | Cache results of function |
| Promise.all | Multiple independent async tasks | Load multiple API endpoints at once |
| Generator | Large datasets, pausable loops | Memory-efficient processing |
| WeakMap | Object-specific metadata | Don't prevent garbage collection |

---

## Helpful Resources

- [MDN: JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- [JavaScript.info: Advanced Topics](https://javascript.info/advanced)
- [Web.dev: JavaScript Performance](https://web.dev/javascript/)
- [Eloquent JavaScript (book)](https://eloquentjavascript.net/)
- [You Don't Know JS (book series)](https://github.com/getify/You-Dont-Know-JS)
