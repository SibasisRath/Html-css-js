# JavaScript Projects

## Project 1: Dynamic To-Do List Application

### Project Overview
Build a fully functional to-do list that persists data locally. This project focuses on DOM manipulation, event handling, and local storage. It's a realistic example of how to build interactive web applications.

### Requirements

#### Core Features
- **Add todos**: Input field + button to create new todos
- **Display todos**: List with all todos
- **Mark complete**: Check/uncheck completion status
- **Delete todos**: Remove specific todos
- **Edit todos**: Inline editing of todo text
- **Local storage**: Todos persist across page reloads
- **Filters**: Show all/active/completed todos
- **Clear completed**: Bulk delete completed items

#### Technical Requirements Checklist
- [ ] DOM selection using querySelector/querySelectorAll
- [ ] Event listeners on buttons, inputs, form
- [ ] Event delegation for dynamic list items
- [ ] localStorage API (save/load/remove)
- [ ] Enter key submission for inputs
- [ ] Real-time updates of todo count
- [ ] Proper element creation (createElement, appendChild)
- [ ] Class toggling for UI state (completed, active)
- [ ] Data attributes for storing todo IDs
- [ ] Smooth transitions/animations
- [ ] No jQuery or frameworks (vanilla JavaScript)
- [ ] Clean, organized code

### HTML Structure (provided)
```html
<div class="todo-app">
    <header>
        <h1>My To-Do List</h1>
    </header>
    
    <div class="input-section">
        <input type="text" id="todo-input" placeholder="Add a new todo...">
        <button id="add-btn">Add Todo</button>
    </div>
    
    <div class="filters">
        <button class="filter-btn active" data-filter="all">All</button>
        <button class="filter-btn" data-filter="active">Active</button>
        <button class="filter-btn" data-filter="completed">Completed</button>
    </div>
    
    <ul id="todo-list"></ul>
    
    <div class="footer">
        <span id="todo-count">0 items</span>
        <button id="clear-completed">Clear Completed</button>
    </div>
</div>
```

### Step-by-Step Implementation

1. **Create data structure**
   - Array of todos: `[{ id, text, completed, createdAt }, ...]`
   - Load from localStorage on startup
   - Save to localStorage after each change

2. **DOM elements caching**
   - Cache frequently accessed elements (input, list, buttons)
   - Reduces repeated querySelector calls

3. **Implement add todo**
   - Get input value on button click
   - Validate input (not empty)
   - Create todo object with unique ID
   - Add to todos array
   - Save to localStorage
   - Clear input
   - Render list

4. **Render todos**
   - Create function that builds list HTML
   - Handle empty state
   - Show appropriate todos based on filter
   - Attach event listeners to each todo

5. **Implement todo interactions**
   - Toggle completion on checkbox
   - Delete button removes item
   - Double-click to edit (inline editing)
   - Escape to cancel edit, Enter to save

6. **Add filtering**
   - Show/hide todos based on filter button clicked
   - Highlight active filter
   - Update todo count accordingly

7. **Implement persistence**
   - Save todos array to localStorage
   - Load todos on page load
   - Update localStorage after each modification

### Deliverables
- Complete HTML, CSS, JavaScript files
- Working to-do list with all features
- Data persists across page reloads
- Smooth animations/transitions
- Responsive layout (mobile to desktop)
- Clean, commented code

---

## Project 2: Weather Dashboard with Fetch API

### Project Overview
Build a weather application that fetches real-time data from the OpenWeatherMap API (free tier). This project emphasizes Fetch API, async/await, DOM manipulation, and error handling.

### Requirements

#### Features
- **Search by city**: Input field to search weather for any city
- **Display current weather**: Temperature, description, humidity, wind speed
- **Weather icon**: Display appropriate weather icon
- **Temperature unit**: Toggle between Celsius and Fahrenheit
- **Recent searches**: Show last 5 searched cities
- **Forecast**: 5-day weather forecast (daily)
- **Loading state**: Show spinner while fetching
- **Error handling**: Display friendly error messages
- **Geolocation**: Option to use current location

#### Technical Requirements Checklist
- [ ] Fetch API with async/await
- [ ] HTTP error handling (check response.ok)
- [ ] API key management (not in code)
- [ ] DOM manipulation (create/update elements)
- [ ] Event listeners (search input, buttons)
- [ ] Loading state display/hide
- [ ] localStorage for recent searches
- [ ] Temperature conversion function
- [ ] Proper formatting of data (dates, temperatures)
- [ ] CORS handling if needed
- [ ] Responsive grid layout
- [ ] No hardcoded API keys in code

### Step-by-Step Implementation

1. **Setup API integration**
   - Get free API key from OpenWeatherMap
   - Store in environment variable or config
   - Create function to build API URLs

2. **Create search functionality**
   - Text input for city name
   - Search button + Enter key submission
   - Disable button while fetching
   - Clear previous errors

3. **Fetch current weather**
   - Make Fetch request to API
   - Parse response JSON
   - Handle errors gracefully
   - Handle not found responses

4. **Display weather data**
   - Create DOM elements for each data point
   - Format temperature (with degree symbol)
   - Show appropriate weather icon
   - Display last updated time

5. **Implement forecast**
   - Fetch 5-day forecast from API
   - Display daily cards with weather
   - Filter to one forecast per day
   - Make cards clickable to show details

6. **Add temperature unit toggle**
   - Button to switch C/F
   - Convert and re-display all temperatures
   - Save preference to localStorage
   - Persist across visits

7. **Track recent searches**
   - Store last N city searches in localStorage
   - Display as clickable buttons
   - Clicking loads that city's weather
   - Remove duplicates (most recent first)

8. **Geolocation feature**
   - Button to "Use my location"
   - Request browser geolocation permission
   - Convert coords to city name (reverse geocoding)
   - Fetch weather for that location

### Sample API Calls
```
Current weather:
https://api.openweathermap.org/data/2.5/weather?q=London&appid=KEY&units=metric

Forecast:
https://api.openweathermap.org/data/2.5/forecast?q=London&appid=KEY&units=metric
```

### Deliverables
- Working weather dashboard
- Real API integration
- All features functional
- Error states handled
- Responsive design
- localStorage persistence
- Clean, documented code

---

## Project 3: E-Commerce Product Browser with API

### Project Overview
Build a product browsing interface that fetches from a mock/real API. Focus on pagination, filtering, sorting, dynamic content loading, and Fetch API integration.

### Requirements

#### Features
- **Product gallery**: Grid of product cards
- **Pagination**: Navigate between pages of products
- **Filters**: Category, price range, rating
- **Sort options**: Price low/high, newest, bestselling
- **Product details**: Modal with full information
- **Add to cart**: Track cart count in header
- **Search**: Search products by name
- **Infinite scroll**: Alternative to pagination (load more button)
- **Loading states**: Show skeletons while fetching
- **Responsive**: Works on mobile, tablet, desktop

#### Technical Requirements Checklist
- [ ] Fetch API with async/await
- [ ] Multiple filter types working together
- [ ] URL parameters for state (filter, page, sort)
- [ ] DOM manipulation for grid rendering
- [ ] Modal for product details
- [ ] Event delegation for dynamic content
- [ ] Debouncing search input
- [ ] localStorage for cart
- [ ] Loading skeleton UI
- [ ] Error boundaries for failed loads
- [ ] Responsive grid layout
- [ ] Performance optimization (image lazy loading)

### Step-by-Step Implementation

1. **Setup API mock or integration**
   - Use public API (e.g., FakeStore API) or create mock JSON
   - Define API endpoints for products, filters, categories

2. **Create product grid**
   - Fetch products on load
   - Display as responsive grid (CSS Grid or Flexbox)
   - Create reusable product card component
   - Handle loading state

3. **Implement pagination**
   - Add next/previous buttons
   - Update URL with page parameter
   - Fetch new products on page change
   - Show current page/total pages

4. **Add filtering**
   - Create filter UI (dropdowns, checkboxes, sliders)
   - Update products when filters change
   - Calculate available filters from dataset
   - Reset filters button

5. **Implement sorting**
   - Dropdown for sort order
   - Re-fetch with sort parameter
   - Remember selected sort order

6. **Create product detail modal**
   - Click product card to open modal
   - Display images carousel
   - Show full description, specs
   - Add to cart from modal
   - Close with close button or Escape key

7. **Add cart functionality**
   - Add to cart button increases count
   - Show cart count in header
   - Store cart in localStorage
   - Simple cart display (just count is OK for this project)

8. **Search implementation**
   - Search input with debounce
   - Filter products by name
   - Show no results message
   - Highlight search term in results

9. **UI Polish**
   - Skeleton loading placeholders
   - Smooth transitions between states
   - Hover effects on cards
   - Loading spinner on fetch

### Sample API (FakeStore)
```
Products: https://fakestoreapi.com/products
Categories: https://fakestoreapi.com/products/categories
Single product: https://fakestoreapi.com/products/1
Products in category: https://fakestoreapi.com/products/category/electronics
```

### Deliverables
- Working product browser
- API integration functional
- Filters and sorting working
- Modal product details
- Cart functionality
- Responsive design
- Smooth loading states
- Clean, scalable code

---

## DOM Manipulation Best Practices for Projects

### Efficient DOM Updates
1. **Cache element references**
   ```javascript
   const container = document.querySelector('.container');
   const items = container.querySelectorAll('.item');
   // Reuse container and items instead of querying each time
   ```

2. **Batch DOM changes**
   ```javascript
   const fragment = document.createDocumentFragment();
   items.forEach(item => {
       fragment.appendChild(createElement(item));
   });
   container.appendChild(fragment);  // Single reflow
   ```

3. **Use event delegation**
   ```javascript
   container.addEventListener('click', (event) => {
       if (event.target.matches('.delete-btn')) {
           deleteItem(event.target.closest('.item'));
       }
   });
   ```

4. **Minimize reflows**
   - Read dimensions/positions in a batch
   - Apply style changes in a batch
   - Use CSS classes instead of inline styles

### Rendering Large Lists
1. **Virtual scrolling**: Only render visible items
2. **Pagination**: Show limited items per page
3. **Lazy loading**: Load images on scroll
4. **Skeleton screens**: Show placeholders while loading

### Memory Management
1. **Remove listeners when not needed**
   ```javascript
   element.removeEventListener('click', handler);
   ```

2. **Clean up timers**
   ```javascript
   clearTimeout(timeoutId);
   clearInterval(intervalId);
   ```

3. **Avoid closure memory leaks**
   - Don't store large objects in closures unnecessarily

---

## Fetch API Best Practices for Projects

### Error Handling
1. **Always check response.ok**
2. **Handle network errors** with try/catch
3. **Show user-friendly errors** (not technical messages)
4. **Graceful degradation** if API unavailable

### Performance
1. **Use async/await** (cleaner than .then())
2. **Batch requests** with Promise.all()
3. **Cache responses** to avoid repeated requests
4. **Debounce search** to reduce API calls
5. **Add request timeout** to prevent hanging

### State Management
1. **Track loading state** (show spinner)
2. **Handle errors** gracefully
3. **Persist to localStorage** for offline access
4. **Manage API keys** securely

---

## Testing Your Projects

### Manual Testing Checklist
- [ ] Test on mobile device (actual device, not just DevTools)
- [ ] Test on slow 3G network (Chrome DevTools throttling)
- [ ] Test with JavaScript disabled (basic functionality)
- [ ] Test form inputs (empty, invalid, valid)
- [ ] Test edge cases (0 results, network error, timeout)
- [ ] Test keyboard navigation (Tab through inputs)
- [ ] Test accessibility (zoom, screen reader if possible)

### Browser Testing
- [ ] Chrome (latest)
- [ ] Firefox (latest)
- [ ] Safari (if available)
- [ ] Mobile browsers

---

## Project Submission Checklist

### Code Quality
- [ ] No console errors
- [ ] No console warnings
- [ ] Clean, readable code
- [ ] Comments on complex logic
- [ ] Consistent naming conventions
- [ ] DRY (Don't Repeat Yourself)

### Functionality
- [ ] All features working
- [ ] Handles errors gracefully
- [ ] No infinite loops
- [ ] No memory leaks

### Performance
- [ ] Page loads quickly
- [ ] No lag on interactions
- [ ] Images optimized
- [ ] No unnecessary API calls

### UX/Design
- [ ] Professional appearance
- [ ] Clear user feedback
- [ ] Loading states visible
- [ ] Mobile responsive

---

## Learning Path

1. **Start with To-Do List**
   - Solidify DOM manipulation fundamentals
   - Learn event handling patterns
   - Understand localStorage

2. **Move to Weather App**
   - Practice async/await and Fetch
   - Learn API integration
   - Handle real-world data

3. **Build E-Commerce**
   - Combine all previous knowledge
   - Handle complex state management
   - Optimize performance

---

## Helpful Resources

- [MDN: Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- [MDN: DOM Manipulation](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Manipulating_documents)
- [FakeStore API](https://fakestoreapi.com/)
- [OpenWeatherMap API](https://openweathermap.org/api)
- [Google Fonts](https://fonts.google.com/) (for nice typography)
- [Unsplash API](https://unsplash.com/developers) (free images)
- [Chrome DevTools](https://developer.chrome.com/docs/devtools/) (debugging)
