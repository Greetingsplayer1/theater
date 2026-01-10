# CSS Documentation for Navbar

This document explains each CSS rule and how they work together to create a responsive navbar with dropdown functionality.

---

## 1. Body Styles

```css
body {
  font-family: Arial, Helvetica, sans-serif;
  margin: 0;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}
```

### What it does:
- **font-family**: Sets the default font to Arial or Helvetica
- **margin: 0**: Removes default browser margin around the page
- **min-height: 100vh**: Makes the body at least the full viewport height
- **display: flex + flex-direction: column**: Creates a flex container that stacks children vertically, which helps keep the footer at the bottom

---

## 2. Grid Container

```css
.grid-container {
  display: grid;
  grid-template-areas: 
    "head"
    "main";
  width: 100%;
}
```

### What it does:
- **display: grid**: Creates a CSS grid layout
- **grid-template-areas**: Defines named areas for different sections
  - "head" is the navbar area at the top
  - "main" is the content area below
- **width: 100%**: Makes the grid span the full width

---

## 3. Navbar Styles

```css
.navbar {
  background-color: #333;
  grid-area: head;
  position: relative;
}
```

### What it does:
- **background-color: #333**: Sets dark gray background
- **grid-area: head**: Places this element in the "head" area of the grid
- **position: relative**: Establishes positioning context for absolutely positioned children (like the dropdown)

---

## 4. Hamburger Menu

```css
.hamburger {
  display: none;
  cursor: pointer;
  background: none;
  border: none;
}

.hamburger-line {
  display: block;
  width: 20px;
  height: 2px;
  margin: 3px 0;
  background-color: white;
  transition: 0.3s;
}
```

### What it does:
- **display: none**: Hides the hamburger by default (only shows on mobile)
- **cursor: pointer**: Changes cursor to hand on hover
- **background: none + border: none**: Removes default button styling
- **transition: 0.3s**: Smooth animation when lines transform

### Hamburger Animation (on click):
- First line rotates 45 degrees and moves
- Middle line fades out (opacity: 0)
- Third line rotates -45 degrees and moves
- Creates an "X" close button effect

---

## 5. Navigation Links Container

```css
.nav-links {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-links li {
  display: inline-block;
}
```

### What it does:
- **display: flex**: Aligns links horizontally in a row
- **list-style: none**: Removes bullet points from list
- **margin/padding: 0**: Removes default list spacing
- **inline-block**: List items sit side by side

---

## 6. Navigation Links

```css
.navbar a {
  font-size: 14px;
  color: white;
  text-align: center;
  padding: 8px 12px;
  text-decoration: none;
  display: inline-block;
  transition: background-color 0.3s;
}
```

### What it does:
- **font-size: 14px**: Text size for links
- **color: white**: White text color
- **padding: 8px 12px**: Clickable area around each link
- **text-decoration: none**: Removes underline from links
- **transition: 0.3s**: Smooth color transition on hover

### Hover Effect:
```css
.navbar a:hover, .dropdown:hover .dropbtn, .dropdown .dropbtn:hover {
  background-color: red;
}
```
Changes background to red when hovering over links or dropdown buttons.

---

## 7. Dropdown Styles

```css
.dropdown {
  position: relative;
  display: inline-block;
}
```

### What it does:
- **position: relative**: Establishes positioning context for the dropdown content
- **display: inline-block**: Allows dropdown to sit inline with other links

---

## 8. Dropdown Button

```css
.dropdown .dropbtn {
  font-size: 14px;
  border: none;
  outline: none;
  color: white;
  padding: 8px 12px;
  background-color: inherit;
  font-family: inherit;
  margin: 0;
  cursor: pointer;
  transition: background-color 0.3s;
}
```

### What it does:
- **background-color: inherit**: Inherits parent's background color
- **font-family: inherit**: Uses the same font as parent
- **border/outline: none**: Removes default button borders
- All other properties match the navigation links styling

---

## 9. Dropdown Content (Hidden Menu)

```css
.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f9f9f9;
  min-width: 140px;
  box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
  z-index: 1000;
  top: 100%;
  left: 0;
}

.dropdown-content a {
  float: none;
  color: black;
  padding: 10px 12px;
  text-decoration: none;
  display: block;
  text-align: left;
}

.dropdown-content a:hover {
  background-color: #ddd;
}
```

### What it does:
- **display: none**: Hidden by default
- **position: absolute**: Positioned relative to the dropdown button
- **top: 100% + left: 0**: Positions directly below the button
- **min-width: 140px**: Ensures consistent width
- **box-shadow**: Adds drop shadow for depth
- **z-index: 1000**: Ensures it appears above other content
- **display: block + float: none**: Stacks links vertically
- **text-align: left**: Left-aligns dropdown links

---

## 10. Show Dropdown on Hover

```css
.dropdown:hover .dropdown-content,
.dropdown:focus-within .dropdown-content {
  display: block;
}
```

### What it does:
- When hovering over the dropdown container, show the content
- **focus-within**: Also shows when any element inside has keyboard focus (accessibility)

---

## 11. Main Content Area

```css
.main-content {
  grid-area: main;
  padding: 1rem;
  flex: 1;
}

.main-content h1 {
  text-align: center;
}
```

### What it does:
- **grid-area: main**: Places in the "main" grid area
- **padding: 1rem**: Space around content
- **flex: 1**: Takes up remaining vertical space
- **text-align: center**: Centers heading text

---

## 12. Footer

```css
.footer {
  background-color: #333;
  color: white;
  text-align: center;
  padding: 1rem;
  margin-top: auto;
}
```

### What it does:
- **margin-top: auto**: In a flex column layout, pushes footer to the bottom
- Dark background matching the navbar
- Centered text content

---

## 13. Mobile Styles (Media Query)

```css
@media screen and (max-width: 768px) {
  /* Show hamburger menu */
  .hamburger {
    display: block;
  }

  /* Change nav-links to vertical stack */
  .nav-links {
    display: none;
    flex-direction: column;
    position: absolute;
    top: 100%;
    left: 0;
    width: 100%;
    background-color: #333;
  }

  /* Show menu when active class is added */
  .nav-links.active {
    display: flex;
  }

  /* Make each link full width */
  .navbar a {
    display: block;
    width: 100%;
    text-align: left;
    padding: 10px 15px;
  }

  /* Style dropdown for mobile */
  .dropdown .dropbtn {
    display: block;
    width: 100%;
    text-align: left;
    padding: 10px 15px;
    background-color: #444;
  }

  /* Dropdown content always visible on mobile */
  .dropdown-content {
    position: static;
    background-color: #444;
    box-shadow: none;
  }

  /* Indent dropdown links */
  .dropdown-content a {
    padding-left: 30px;
  }
}
```

### What it does:
- **@media screen and (max-width: 768px)**: Only applies these styles on screens 768px or narrower (tablets and phones)

- **Hamburger**: Changes from `display: none` to `display: block`

- **Nav-links**: 
  - Hidden by default
  - Stacks vertically (`flex-direction: column`)
  - Full width below navbar
  - Shows when JavaScript adds `active` class

- **Links and dropdowns**:
  - Full width (`width: 100%`)
  - Left-aligned text
  - Larger padding for touch targets
  - Darker background for dropdown items

---

## Summary of Layout Structure

```
Desktop Layout:
┌─────────────────────────┐
│       NAVBAR            │  ← grid-area: head
├─────────────────────────┤
│                         │
│      MAIN CONTENT       │  ← grid-area: main
│                         │
├─────────────────────────┤
│        FOOTER           │  ← margin-top: auto
└─────────────────────────┘

Mobile Layout (≤768px):
┌─────────────────────────┐
│ [≡]    NAVBAR LINKS     │  ← Hamburger + horizontal or hamburger menu
├─────────────────────────┤
│      MAIN CONTENT       │
├─────────────────────────┤
│        FOOTER           │
└─────────────────────────┘

When hamburger is clicked:
┌─────────────────────────┐
│ [x]                     │
│ ─────────────────────── │
│ Home                    │
│ About                   │
│ Services                │
│ Dropdown ▾              │  ← Shows submenu
│   ├── Link 1            │
│   ├── Link 2            │
│   └── Link 3            │
│ Contact                 │
└─────────────────────────┘
```

---

## Key Concepts Used

1. **CSS Grid**: For page layout with named areas
2. **CSS Flexbox**: For navbar horizontal layout and mobile menu vertical stacking
3. **Position Absolute/Relative**: For dropdown menu positioning
4. **CSS Transitions**: For smooth hover animations
5. **Media Queries**: For responsive design (mobile vs desktop)
6. **Z-Index**: For ensuring dropdown appears above other content
7. **Box Shadow**: For visual depth on dropdown menu

