# Hamburger Menu JavaScript Documentation

This document explains how the JavaScript works for the hamburger menu toggle functionality.

---

## The JavaScript Code

```javascript
// Hamburger menu toggle
const hamburger = document.querySelector('.hamburger');
const navLinks = document.querySelector('.nav-links');

hamburger.addEventListener('click', () => {
    hamburger.classList.toggle('active');
    navLinks.classList.toggle('active');
});

// Close dropdown when clicking outside
document.addEventListener('click', (e) => {
    if (!hamburger.contains(e.target) && !navLinks.contains(e.target)) {
        hamburger.classList.remove('active');
        navLinks.classList.remove('active');
    }
});
```

---

## Line-by-Line Explanation

### 1. Selecting Elements

```javascript
const hamburger = document.querySelector('.hamburger');
const navLinks = document.querySelector('.nav-links');
```

**What it does:**
- `document.querySelector('.hamburger')` finds the hamburger button element in the HTML and stores it in the variable `hamburger`
- `document.querySelector('.nav-links')` finds the navigation links container and stores it in `navLinks`
- `const` means these variables cannot be reassigned later
- `querySelector` returns the first matching element (there's only one of each)

**What are these elements?**
- `.hamburger` = The button with three lines (≡) that appears on mobile
- `.nav-links` = The `<ul>` containing all navigation links and dropdown

---

### 2. Adding Click Event Listener

```javascript
hamburger.addEventListener('click', () => {
    hamburger.classList.toggle('active');
    navLinks.classList.toggle('active');
});
```

**What it does:**
- `addEventListener('click', ...)` waits for the user to click on the hamburger button
- When clicked, it executes the function inside the `{}` brackets
- `() => { ... }` is an arrow function (shorthand for a function)

**What is `.toggle('active')`?**
- `.classList.toggle()` adds a CSS class if it doesn't exist, or removes it if it does
- This switches the `active` class on/off each time you click

**What happens with the CSS classes?**

| Click # | hamburger.classList | navLinks.classList | Visual Result |
|---------|---------------------|--------------------|---------------|
| 0 (start) | no 'active' | no 'active' | Hamburger shown, menu hidden |
| 1 | has 'active' | has 'active' | Hamburger becomes X, menu shown |
| 2 | no 'active' | no 'active' | Hamburger shown, menu hidden |
| 3 | has 'active' | has 'active' | Hamburger becomes X, menu shown |

---

### 3. Closing Menu When Clicking Outside

```javascript
document.addEventListener('click', (e) => {
    if (!hamburger.contains(e.target) && !navLinks.contains(e.target)) {
        hamburger.classList.remove('active');
        navLinks.classList.remove('active');
    }
});
```

**What it does:**
- Listens for clicks ANYWHERE on the document (the whole page)
- `e` = the event object containing information about the click
- `e.target` = the specific element that was clicked

**The `if` condition explained:**
```javascript
if (!hamburger.contains(e.target) && !navLinks.contains(e.target))
```

Translates to:
> "If the clicked element is NOT the hamburger AND is NOT inside the navLinks..."

Breaking it down:
- `hamburger.contains(e.target)` = "Was the hamburger or its children clicked?"
- `!hamburger.contains(...)` = "Was it NOT the hamburger?" (clicked elsewhere)
- `&&` = "AND" (both conditions must be true)
- `!navLinks.contains(e.target)` = "Was it NOT inside the navLinks?"

**The action:**
```javascript
hamburger.classList.remove('active');
navLinks.classList.remove('active');
```

If the click was outside both elements, remove the `active` class from both, which:
- Transforms the hamburger back to three lines
- Hides the navigation menu

**Why is this useful?**
- When user opens the menu, then clicks somewhere else on the page, the menu closes
- Provides better user experience

---

## Complete Flow Diagram

```
User opens page (desktop)
        ↓
   Hamburger is hidden (display: none)
   Menu is visible
        ↓
   Resize to mobile (< 768px)
        ↓
   Hamburger appears
   Menu stays visible
        ↓
   ┌─────────────────────┐
   │  User clicks [≡]    │
   └─────────────────────┘
        ↓
   toggle('active') called
        ↓
   ┌─────────────────────┐
   │ Hamburger: [x]      │
   │ Menu: opens         │
   └─────────────────────┘
        ↓
   ┌─────────────────────┐
   │ User clicks link    │
   │ OR User clicks [x]  │
   └─────────────────────┘
        ↓
   toggle('active') called
        ↓
   ┌─────────────────────┐
   │ Hamburger: [≡]      │
   │ Menu: closes        │
   └─────────────────────┘
        ↓
   ┌─────────────────────┐
   │ User clicks outside │
   │ (on page content)   │
   └─────────────────────┘
        ↓
   remove('active') called
        ↓
   Menu closes (if not already)
```

---

## CSS Classes Toggled

### `.hamburger.active` Applied

```css
.hamburger.active .hamburger-line:nth-child(1) {
    transform: rotate(45deg) translate(5px, 5px);
}

.hamburger.active .hamburger-line:nth-child(2) {
    opacity: 0;
}

.hamburger.active .hamburger-line:nth-child(3) {
    transform: rotate(-45deg) translate(7px, -6px);
}
```

**What this does:**
- Line 1: Rotates 45 degrees and moves slightly right/down
- Line 2: Fades out completely (becomes invisible)
- Line 3: Rotates -45 degrees and moves slightly right/up
- Result: The three lines form an "X" (close button)

**Before (hamburger):**
```
   ─
   ─
   ─
```

**After (active/X):**
```
    ╲
     ╳
    ╱
```

### `.nav-links.active` Applied

```css
.nav-links.active {
    display: flex;
}
```

**What this does:**
- The menu is normally `display: none` on mobile
- When `active` class is added, it becomes `display: flex`
- Menu items stack vertically due to `flex-direction: column`

---

## Event Listener Concepts

### What is an Event Listener?

An event listener is like a "watcher" that waits for something to happen:

```javascript
element.addEventListener('event', function)
```

Common events:
- `'click'` - when user clicks
- `'hover'` - when mouse goes over (not for all elements)
- `'keydown'` - when a key is pressed
- `'submit'` - when a form is submitted
- `'load'` - when a page finishes loading

### What is `this` in an Event Listener?

In the arrow function `() => { ... }`, `this` refers to the surrounding scope (not the clicked element).

We use `e.target` instead to know what was clicked.

---

## Alternative Ways to Write This Code

### Using function() instead of arrow function:

```javascript
hamburger.addEventListener('click', function() {
    hamburger.classList.toggle('active');
    navLinks.classList.toggle('active');
});
```

### Using more specific class names:

```javascript
const menuToggle = document.querySelector('.hamburger');
const menuContent = document.querySelector('.nav-links');

menuToggle.addEventListener('click', function() {
    menuToggle.classList.toggle('is-open');
    menuContent.classList.toggle('is-open');
});
```

### Using forEach for multiple elements (if you had multiple menus):

```javascript
document.querySelectorAll('.hamburger').forEach(hamburger => {
    hamburger.addEventListener('click', () => {
        hamburger.classList.toggle('active');
        const navLinks = hamburger.nextElementSibling;
        navLinks.classList.toggle('active');
    });
});
```

---

## Common Issues and Solutions

### Issue: Menu doesn't open

**Possible causes:**
1. JavaScript is loading before the HTML elements exist
2. CSS has `display: none` with no way to override

**Solution:** Make sure `<script>` tag is at the end of `<body>` or use `DOMContentLoaded` event

```javascript
document.addEventListener('DOMContentLoaded', () => {
    const hamburger = document.querySelector('.hamburger');
    const navLinks = document.querySelector('.nav-links');
    
    hamburger.addEventListener('click', () => {
        hamburger.classList.toggle('active');
        navLinks.classList.toggle('active');
    });
});
```

### Issue: Menu closes immediately after opening

**Possible cause:** Click event is bubbling up and triggering the outside-click listener

**Solution:** Use `event.stopPropagation()`

```javascript
hamburger.addEventListener('click', (e) => {
    e.stopPropagation(); // Prevent event from reaching document
    hamburger.classList.toggle('active');
    navLinks.classList.toggle('active');
});
```

### Issue: Hamburger animation doesn't work

**Possible causes:**
1. Missing CSS transitions
2. Wrong selector in CSS
3. Transform properties not set correctly

**Check CSS:**
```css
.hamburger-line {
    transition: 0.3s; /* Must have this */
}
```

---

## Accessibility Considerations

### Adding ARIA attributes for screen readers:

```html
<button class="hamburger" aria-label="Toggle menu" aria-expanded="false">
    <span class="hamburger-line"></span>
    <span class="hamburger-line"></span>
    <span class="hamburger-line"></span>
</button>
```

**What they mean:**
- `aria-label`: Text description for screen readers
- `aria-expanded`: Indicates if the menu is open or closed

**JavaScript update:**

```javascript
hamburger.addEventListener('click', () => {
    const isExpanded = hamburger.getAttribute('aria-expanded') === 'true';
    hamburger.classList.toggle('active');
    navLinks.classList.toggle('active');
    hamburger.setAttribute('aria-expanded', !isExpanded);
});
```

---

## Summary

| Part | Purpose |
|------|---------|
| `querySelector` | Find HTML elements |
| `addEventListener` | Listen for clicks |
| `classList.toggle` | Switch CSS classes on/off |
| `contains()` | Check if element is inside another |
| `classList.remove` | Remove CSS classes |

The hamburger menu works by:
1. Finding the hamburger button and menu
2. Adding a click listener to the button
3. Toggling an `active` class when clicked
4. CSS shows/hides menu based on that class
5. Optional: Close menu when clicking outside

