# Week 7: Interactive Portfolio
## From Static to Dynamic - Adding JavaScript Interactivity

### Learning Objectives
By completing this project, you will:
- Master DOM manipulation using querySelector and querySelectorAll
- Implement event listeners for clicks, form submissions, and scrolling
- Create dynamic, data-driven user interfaces
- Build real-time form validation with error handling
- Animate elements based on user interactions and scroll position
- Filter and show/hide content dynamically
- Build upon your Week 5 portfolio to create a professional, interactive website

### Prerequisites
Before starting, you should have:
- Completed Week 7 lecture on DOM Manipulation & Events
- Reviewed prep work chapters:
  - **Modern JavaScript Chapter 7**: DOM Manipulation
  - **Modern JavaScript Chapter 8**: Events
  - **(Optional) Chapter 9**: LocalStorage
- **(Recommended)** Your code from Week 5 - Modern Layout Portfolio

### Project Overview
This week, you'll transform your static Week 5 portfolio into a fully interactive web application! You'll add JavaScript functionality to make navigation smooth, projects filterable, skills animated, forms validated, and mobile menus functional - all without changing your beautiful HTML/CSS foundation.

**Why This Matters**: This project demonstrates how JavaScript brings static designs to life, creating engaging user experiences while maintaining clean separation of concerns. Plus, it sets the perfect foundation for Week 8 when we convert everything to React!

---

## Getting Started

### First: Accept the GitHub Classroom Assignment
Your instructor will provide a GitHub Classroom assignment link. Accepting it will create a new repository with the Week 7 starter code.

1. **Clone your new repository:**
   ```bash
   git clone [your-github-classroom-repo-url]
   cd [your-repo-name]
   ```

2. **Choose Your Path:**

---

## Path A: Continue from Week 5 (Recommended)

If you completed the Week 5 Modern Layout Portfolio project and want to build upon it:

### Step 1: Prepare Your Repository
1. **Delete the starter files** in your cloned repository (but **keep the .git folder!**)
   ```bash
   # In your cloned Week 7 repository
   rm index.html styles.css script.js
   # DO NOT delete the .git folder
   ```

2. **Copy your Week 5 files** into the cloned repository folder:
   ```bash
   # Copy your Week 5 files
   cp /path/to/your/week5/index.html .
   cp /path/to/your/week5/styles.css .
   # Copy any assets if you have them
   ```

### Step 2: Add JavaScript Setup
1. **Create the script.js file:**
   ```bash
   touch script.js
   ```

2. **Link the script in your HTML** (add before closing `</body>` tag):
   ```html
   <script src="script.js"></script>
   </body>
   </html>
   ```

### Step 3: Add Interactive Elements to HTML

#### 3.1: Add Filter Buttons for Projects
In your Projects section, add these filter buttons **before** the projects grid:

```html
<section id="projects" class="section">
    <div class="container">
        <h2>Featured Projects</h2>

        <!-- ADD THIS: Filter Buttons -->
        <div class="filter-buttons">
            <button class="filter-btn active" data-filter="all">All Projects</button>
            <button class="filter-btn" data-filter="frontend">Frontend</button>
            <button class="filter-btn" data-filter="fullstack">Full-Stack</button>
            <button class="filter-btn" data-filter="design">Design</button>
            <button class="filter-btn" data-filter="webapp">Web App</button>
        </div>

        <div class="projects-grid">
            <!-- Your existing project cards -->
        </div>
    </div>
</section>
```

#### 3.2: Add Data Attributes to Project Cards
Add `data-category` attribute to each project card to match the filter buttons:

```html
<div class="project-card" data-category="frontend">
    <!-- project content -->
</div>

<div class="project-card" data-category="fullstack">
    <!-- project content -->
</div>

<!-- And so on for each project -->
```

#### 3.3: Add ID to Contact Form
Make sure your contact form has an ID:

```html
<form id="contact-form" class="contact-form">
    <!-- form fields -->
</form>
```

#### 3.4: Add CSS for New Elements
Add this CSS to your `styles.css`:

```css
/* Filter Buttons */
.filter-buttons {
    display: flex;
    justify-content: center;
    gap: 1rem;
    margin: 2rem 0;
    flex-wrap: wrap;
}

.filter-btn {
    padding: 0.5rem 1.5rem;
    border: 2px solid #667eea;
    background: transparent;
    color: #667eea;
    border-radius: 25px;
    cursor: pointer;
    transition: all 0.3s ease;
    font-size: 1rem;
    font-weight: 500;
}

.filter-btn:hover {
    background: #667eea;
    color: white;
    transform: translateY(-2px);
}

.filter-btn.active {
    background: #667eea;
    color: white;
}

/* Form Validation Styles */
.error-message {
    color: #dc2626;
    font-size: 0.875rem;
    margin-top: 0.25rem;
    display: block;
}

.form-group input.error,
.form-group textarea.error {
    border-color: #dc2626;
}

.success-message {
    background: #d1fae5;
    color: #059669;
    padding: 1rem;
    border-radius: 8px;
    margin-top: 1rem;
    text-align: center;
    font-weight: 500;
}
```

### Step 4: Follow the JavaScript Instructions Below
Jump to the "Step-by-Step JavaScript Implementation" section to add interactivity!

---

## Path B: Fresh Start

If you didn't complete Week 5 or want to start fresh, use the provided starter files:

### Step 1: Review the Starter Files
Your cloned repository includes:
- `index.html` - Complete portfolio structure (based on Week 5)
- `styles.css` - Modern CSS with Flexbox/Grid layouts
- `script.js` - JavaScript file with TODO comments

### Step 2: Customize the Content
1. **Open `index.html`** in your code editor
2. **Replace "Alex Johnson"** with your name
3. **Update the about section** with your information
4. **Customize the skills** to match your skill set
5. **Update the projects** with your own work (or keep examples)
6. **Update contact information** with your email/phone

### Step 3: Follow the JavaScript Instructions Below
Continue to the "Step-by-Step JavaScript Implementation" section!

---

## Step-by-Step JavaScript Implementation

### Part 1: Smooth Scroll Navigation (15 minutes)

**Goal**: Make navigation links smoothly scroll to their target sections.

#### Step 1.1: Select Navigation Links
In `script.js`, add:

```javascript
// Select all navigation links
const navLinks = document.querySelectorAll('.nav-link');
```

#### Step 1.2: Add Click Event Listeners
```javascript
// Add smooth scroll to each nav link
navLinks.forEach(link => {
    link.addEventListener('click', (e) => {
        e.preventDefault(); // Prevent default jump

        // Get the target section ID from href
        const targetId = link.getAttribute('href');
        const targetSection = document.querySelector(targetId);

        // Smooth scroll to target
        targetSection.scrollIntoView({
            behavior: 'smooth',
            block: 'start'
        });
    });
});
```

**What's Happening**:
- `querySelectorAll` gets all elements with class `nav-link`
- `forEach` loops through each link
- `preventDefault()` stops the default jump behavior
- `scrollIntoView()` smoothly scrolls to the target section

**Test It**: Click your navigation links - they should smoothly scroll!

#### Step 1.3: BONUS - Highlight Active Nav on Scroll
```javascript
// Update active nav link on scroll
window.addEventListener('scroll', () => {
    const sections = document.querySelectorAll('section');
    const scrollPos = window.scrollY + 100;

    sections.forEach(section => {
        const sectionTop = section.offsetTop;
        const sectionHeight = section.offsetHeight;
        const sectionId = section.getAttribute('id');

        if (scrollPos >= sectionTop && scrollPos < sectionTop + sectionHeight) {
            // Remove active from all links
            navLinks.forEach(link => link.classList.remove('active'));

            // Add active to current section's link
            const activeLink = document.querySelector(`.nav-link[href="#${sectionId}"]`);
            if (activeLink) {
                activeLink.classList.add('active');
            }
        }
    });
});
```

---

### Part 2: Project Filtering (20 minutes)

**Goal**: Filter projects by category when filter buttons are clicked.

#### Step 2.1: Select Elements
```javascript
// Select filter buttons and project cards
const filterButtons = document.querySelectorAll('.filter-btn');
const projectCards = document.querySelectorAll('.project-card');
```

#### Step 2.2: Create Filter Function
```javascript
// Function to filter projects
function filterProjects(category) {
    projectCards.forEach(card => {
        const cardCategory = card.getAttribute('data-category');

        if (category === 'all' || cardCategory === category) {
            card.style.display = 'block'; // Show matching cards
        } else {
            card.style.display = 'none'; // Hide non-matching cards
        }
    });
}
```

#### Step 2.3: Add Click Listeners to Filter Buttons
```javascript
// Add event listeners to filter buttons
filterButtons.forEach(button => {
    button.addEventListener('click', () => {
        // Remove active class from all buttons
        filterButtons.forEach(btn => btn.classList.remove('active'));

        // Add active class to clicked button
        button.classList.add('active');

        // Get filter value and filter projects
        const filterValue = button.getAttribute('data-filter');
        filterProjects(filterValue);
    });
});
```

**What's Happening**:
- Each button has a `data-filter` attribute (e.g., "frontend")
- Each project card has a `data-category` attribute matching the filters
- When a button is clicked, we show/hide cards based on matching categories

**Test It**: Click filter buttons - projects should show/hide!

---

### Part 3: Mobile Menu Toggle (10 minutes)

**Goal**: Toggle mobile navigation menu on/off.

#### Step 3.1: Select Elements
```javascript
// Select mobile menu elements
const navToggle = document.querySelector('.nav-toggle');
const navMenu = document.querySelector('.nav-menu');
```

#### Step 3.2: Add Toggle Functionality
```javascript
// Toggle mobile menu
navToggle.addEventListener('click', () => {
    navMenu.classList.toggle('active');
    navToggle.classList.toggle('active');
});

// Close menu when nav link is clicked
navLinks.forEach(link => {
    link.addEventListener('click', () => {
        navMenu.classList.remove('active');
        navToggle.classList.remove('active');
    });
});
```

**Note**: You'll need to add mobile menu CSS if not already present:

```css
@media (max-width: 768px) {
    .nav-menu {
        position: fixed;
        left: -100%;
        top: 70px;
        flex-direction: column;
        background-color: #fff;
        width: 100%;
        text-align: center;
        transition: 0.3s;
        box-shadow: 0 10px 27px rgba(0,0,0,0.05);
    }

    .nav-menu.active {
        left: 0;
    }

    .nav-toggle {
        display: block;
        cursor: pointer;
    }
}
```

---

### Part 4: Skill Animations (15 minutes)

**Goal**: Animate skill bars when they come into view.

#### Step 4.1: Select Skill Bars
```javascript
// Select all skill progress bars
const skillBars = document.querySelectorAll('.skill-progress');
```

#### Step 4.2: Create Animation Function
```javascript
// Animate skills on scroll
function animateSkills() {
    const skillsSection = document.querySelector('#skills');
    const skillsPosition = skillsSection.getBoundingClientRect().top;
    const screenPosition = window.innerHeight;

    if (skillsPosition < screenPosition) {
        skillBars.forEach(bar => {
            const skillLevel = bar.style.getPropertyValue('--skill-level');
            bar.style.width = skillLevel;
        });
    }
}

// Add scroll listener
window.addEventListener('scroll', animateSkills);

// Run once on load in case skills are already visible
animateSkills();
```

**What's Happening**:
- We check if skills section is in viewport
- When visible, we animate each bar to its `--skill-level` width
- CSS transition handles the smooth animation

**Test It**: Scroll to skills section - bars should animate in!

---

### Part 5: Form Validation (20 minutes)

**Goal**: Validate contact form in real-time and on submission.

#### Step 5.1: Select Form Elements
```javascript
// Select form and inputs
const contactForm = document.querySelector('#contact-form');
const nameInput = document.querySelector('#name');
const emailInput = document.querySelector('#email');
const messageInput = document.querySelector('#message');
```

#### Step 5.2: Create Validation Functions
```javascript
// Email validation function
function isValidEmail(email) {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return emailRegex.test(email);
}

// Show error message
function showError(input, message) {
    // Remove any existing error
    clearError(input);

    // Create error element
    const error = document.createElement('span');
    error.className = 'error-message';
    error.textContent = message;

    // Add error class to input
    input.classList.add('error');
    input.classList.remove('success');

    // Append error after input
    input.parentElement.appendChild(error);
}

// Clear error message
function clearError(input) {
    const error = input.parentElement.querySelector('.error-message');
    if (error) {
        error.remove();
    }
    input.classList.remove('error');
}

// Show success state
function showSuccess(input) {
    clearError(input);
    input.classList.add('success');
    input.classList.remove('error');
}
```

#### Step 5.3: Real-Time Validation
```javascript
// Validate name input
nameInput.addEventListener('input', () => {
    if (nameInput.value.trim().length < 2) {
        showError(nameInput, 'Name must be at least 2 characters');
    } else {
        showSuccess(nameInput);
    }
});

// Validate email input
emailInput.addEventListener('input', () => {
    if (!isValidEmail(emailInput.value)) {
        showError(emailInput, 'Please enter a valid email address');
    } else {
        showSuccess(emailInput);
    }
});

// Validate message input
messageInput.addEventListener('input', () => {
    if (messageInput.value.trim().length < 10) {
        showError(messageInput, 'Message must be at least 10 characters');
    } else {
        showSuccess(messageInput);
    }
});
```

#### Step 5.4: Form Submission
```javascript
// Handle form submission
contactForm.addEventListener('submit', (e) => {
    e.preventDefault(); // Prevent actual submission

    // Validate all fields
    let isValid = true;

    if (nameInput.value.trim().length < 2) {
        showError(nameInput, 'Name must be at least 2 characters');
        isValid = false;
    }

    if (!isValidEmail(emailInput.value)) {
        showError(emailInput, 'Please enter a valid email address');
        isValid = false;
    }

    if (messageInput.value.trim().length < 10) {
        showError(messageInput, 'Message must be at least 10 characters');
        isValid = false;
    }

    // If valid, show success
    if (isValid) {
        // Create success message
        const successMsg = document.createElement('div');
        successMsg.className = 'success-message';
        successMsg.textContent = 'Thank you! Your message has been sent successfully.';

        // Append after form
        contactForm.appendChild(successMsg);

        // Clear form after 2 seconds
        setTimeout(() => {
            contactForm.reset();
            successMsg.remove();
            document.querySelectorAll('.success').forEach(input => {
                input.classList.remove('success');
            });
        }, 3000);
    }
});
```

**Test It**: Try submitting with invalid data - errors should appear in real-time!

---

## Challenge Extensions

### Extension 1: Theme Switcher with LocalStorage
Add a dark mode toggle that persists across page refreshes:

```javascript
// Add theme toggle button to your HTML navbar:
// <button class="theme-toggle"><</button>

const themeToggle = document.querySelector('.theme-toggle');

// Load saved theme
const savedTheme = localStorage.getItem('theme');
if (savedTheme === 'dark') {
    document.body.classList.add('dark-theme');
    themeToggle.textContent = ' ';
}

// Toggle theme
themeToggle.addEventListener('click', () => {
    document.body.classList.toggle('dark-theme');

    if (document.body.classList.contains('dark-theme')) {
        localStorage.setItem('theme', 'dark');
        themeToggle.textContent = ' ';
    } else {
        localStorage.setItem('theme', 'light');
        themeToggle.textContent = '<';
    }
});
```

### Extension 2: Project Sorting
Add sorting functionality for projects:

```javascript
// Add sort dropdown to HTML:
// <select id="sort-projects">
//     <option value="date">Sort by Date</option>
//     <option value="title">Sort by Title</option>
// </select>

const sortSelect = document.querySelector('#sort-projects');

sortSelect.addEventListener('change', () => {
    const projectsGrid = document.querySelector('.projects-grid');
    const projects = Array.from(projectsGrid.querySelectorAll('.project-card'));

    projects.sort((a, b) => {
        if (sortSelect.value === 'title') {
            const titleA = a.querySelector('.project-title').textContent;
            const titleB = b.querySelector('.project-title').textContent;
            return titleA.localeCompare(titleB);
        }
        // Add other sort criteria as needed
    });

    // Re-append in sorted order
    projects.forEach(project => projectsGrid.appendChild(project));
});
```

---

## Troubleshooting Guide

### Issue: Navigation links don't scroll smoothly
**Solution**:
- Check that each link's `href` matches a section's `id`
- Ensure `scrollIntoView({behavior: 'smooth'})` is used
- Some browsers may need a polyfill for smooth scroll

### Issue: Filter buttons don't work
**Solution**:
- Verify each project card has a `data-category` attribute
- Check that `data-filter` values on buttons match category values
- Use DevTools to confirm elements are selected correctly

### Issue: Form validation not working
**Solution**:
- Confirm form has `id="contact-form"`
- Check input IDs match your selectors (#name, #email, #message)
- Look for console errors - they'll tell you what's missing

### Issue: Skill bars don't animate
**Solution**:
- Verify CSS transition is set on `.skill-progress`
- Ensure `--skill-level` CSS variable is set on each bar
- Check that scroll event listener is added

### Issue: Mobile menu not toggling
**Solution**:
- Add the mobile menu CSS provided
- Confirm `.nav-toggle` and `.nav-menu` elements exist
- Check that `active` class is being toggled correctly

---

## Testing Checklist

Before submitting, verify:

- [ ] All navigation links scroll smoothly to sections
- [ ] Active nav link updates as you scroll
- [ ] Filter buttons show/hide projects correctly
- [ ] All filter buttons update their active state
- [ ] Mobile menu opens and closes
- [ ] Mobile menu closes when a link is clicked
- [ ] Skill bars animate when scrolled into view
- [ ] Form shows errors for invalid inputs
- [ ] Form shows success message when valid
- [ ] Form clears after successful submission
- [ ] No console errors
- [ ] Site works on mobile screen sizes
- [ ] All interactions feel smooth and responsive

---

## Resources & References

- [MDN: Document.querySelector()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)
- [MDN: EventTarget.addEventListener()](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
- [MDN: Element.classList](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList)
- [MDN: Using data attributes](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Use_data_attributes)
- [MDN: Form validation](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation)
- [JavaScript.info: Introduction to Events](https://javascript.info/introduction-browser-events)

---

## Tips for Success

1. **Test Frequently**: After each section, test in the browser to ensure it works
2. **Use Console.log**: Debug by logging values: `console.log(variable)`
3. **DevTools Are Your Friend**: Use the Elements tab to inspect DOM changes
4. **One Feature at a Time**: Complete one part fully before moving to the next
5. **Comment Your Code**: Add comments explaining what each section does
6. **Ask Questions**: If stuck, ask in class or office hours!

---

## What's Next?

**Week 8: React Introduction**
- We'll convert this portfolio to React components
- You'll see how React simplifies DOM manipulation
- Understanding vanilla JavaScript makes React much easier to learn!

**Why This Matters**: Mastering DOM manipulation and events in vanilla JavaScript gives you a deep understanding of how web applications work. When you learn React next week, you'll appreciate how it abstracts these concepts and makes them easier to manage!

---

Remember: This is a portfolio piece! Make it yours, be creative, and showcase your skills. You're not just learning concepts - you're building something you can deploy and share with the world.

Good luck, and happy coding!