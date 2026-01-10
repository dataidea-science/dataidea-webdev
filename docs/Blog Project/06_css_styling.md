# Blog Project: CSS Styling

In this tutorial, we'll create modern, responsive CSS styles for our blog. We'll use CSS Grid, Flexbox, and modern design principles to create a professional, beautiful interface.

## Step 1: Create Main Stylesheet

Create `static/css/style.css` with the following structure:

```css
/* ========================================
   CSS Variables (Custom Properties)
   ======================================== */
:root {
    --primary-color: #2563eb;
    --secondary-color: #64748b;
    --text-color: #1e293b;
    --text-light: #64748b;
    --bg-color: #ffffff;
    --bg-light: #f8fafc;
    --border-color: #e2e8f0;
    --shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
    --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
    --shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);
    --radius: 8px;
    --transition: all 0.3s ease;
}

/* Dark mode support */
@media (prefers-color-scheme: dark) {
    :root {
        --text-color: #f1f5f9;
        --text-light: #94a3b8;
        --bg-color: #0f172a;
        --bg-light: #1e293b;
        --border-color: #334155;
    }
}

/* ========================================
   Reset & Base Styles
   ======================================== */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
    line-height: 1.6;
    color: var(--text-color);
    background-color: var(--bg-color);
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

/* ========================================
   Navigation
   ======================================== */
.navbar {
    background-color: var(--bg-color);
    border-bottom: 1px solid var(--border-color);
    padding: 1rem 0;
    position: sticky;
    top: 0;
    z-index: 1000;
    box-shadow: var(--shadow);
}

.navbar .container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 1rem;
}

.logo {
    font-size: 1.5rem;
    font-weight: 700;
    color: var(--primary-color);
    text-decoration: none;
    transition: var(--transition);
}

.logo:hover {
    opacity: 0.8;
}

.nav-menu {
    display: flex;
    list-style: none;
    gap: 2rem;
}

.nav-menu a {
    color: var(--text-color);
    text-decoration: none;
    font-weight: 500;
    transition: var(--transition);
}

.nav-menu a:hover {
    color: var(--primary-color);
}

.search-form {
    display: flex;
    gap: 0.5rem;
}

.search-input {
    padding: 0.5rem 1rem;
    border: 1px solid var(--border-color);
    border-radius: var(--radius);
    font-size: 0.9rem;
    min-width: 200px;
}

.search-btn {
    padding: 0.5rem 1.5rem;
    background-color: var(--primary-color);
    color: white;
    border: none;
    border-radius: var(--radius);
    cursor: pointer;
    font-weight: 500;
    transition: var(--transition);
}

.search-btn:hover {
    opacity: 0.9;
    transform: translateY(-1px);
}

/* ========================================
   Hero Section
   ======================================== */
.hero {
    text-align: center;
    padding: 4rem 0;
    background: linear-gradient(135deg, var(--primary-color) 0%, #1e40af 100%);
    color: white;
    margin-bottom: 3rem;
    border-radius: var(--radius);
}

.hero h1 {
    font-size: 2.5rem;
    margin-bottom: 1rem;
}

.hero p {
    font-size: 1.2rem;
    opacity: 0.9;
}

/* ========================================
   Posts Grid
   ======================================== */
.posts-section {
    margin: 3rem 0;
}

.posts-section h2 {
    font-size: 2rem;
    margin-bottom: 2rem;
    color: var(--text-color);
}

.posts-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
    gap: 2rem;
    margin-bottom: 3rem;
}

/* ========================================
   Post Card
   ======================================== */
.post-card {
    background: var(--bg-color);
    border: 1px solid var(--border-color);
    border-radius: var(--radius);
    overflow: hidden;
    transition: var(--transition);
    box-shadow: var(--shadow);
    display: flex;
    flex-direction: column;
}

.post-card:hover {
    transform: translateY(-4px);
    box-shadow: var(--shadow-lg);
    border-color: var(--primary-color);
}

.post-image {
    width: 100%;
    height: 200px;
    object-fit: cover;
}

.post-content {
    padding: 1.5rem;
    flex-grow: 1;
    display: flex;
    flex-direction: column;
}

.post-meta {
    display: flex;
    gap: 1rem;
    margin-bottom: 1rem;
    font-size: 0.875rem;
    color: var(--text-light);
}

.post-category {
    color: var(--primary-color);
    text-decoration: none;
    font-weight: 500;
}

.post-category:hover {
    text-decoration: underline;
}

.post-title {
    font-size: 1.5rem;
    margin-bottom: 0.75rem;
}

.post-title a {
    color: var(--text-color);
    text-decoration: none;
    transition: var(--transition);
}

.post-title a:hover {
    color: var(--primary-color);
}

.post-excerpt {
    color: var(--text-light);
    margin-bottom: 1rem;
    flex-grow: 1;
}

.post-footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: auto;
    padding-top: 1rem;
    border-top: 1px solid var(--border-color);
}

.post-author {
    font-size: 0.875rem;
    color: var(--text-light);
}

.read-more {
    color: var(--primary-color);
    text-decoration: none;
    font-weight: 500;
    transition: var(--transition);
}

.read-more:hover {
    text-decoration: underline;
}

/* ========================================
   Post Detail
   ======================================== */
.post-detail {
    max-width: 800px;
    margin: 0 auto;
}

.post-header {
    margin-bottom: 2rem;
}

.post-header .post-title {
    font-size: 2.5rem;
    margin: 1rem 0;
}

.featured-image {
    width: 100%;
    height: 400px;
    object-fit: cover;
    border-radius: var(--radius);
    margin-bottom: 2rem;
}

.post-body {
    font-size: 1.1rem;
    line-height: 1.8;
    margin-bottom: 3rem;
}

.post-body p {
    margin-bottom: 1.5rem;
}

/* ========================================
   Comments
   ======================================== */
.comments-section {
    margin-top: 4rem;
    padding-top: 2rem;
    border-top: 2px solid var(--border-color);
}

.comments-list {
    margin-bottom: 3rem;
}

.comment {
    background: var(--bg-light);
    padding: 1.5rem;
    border-radius: var(--radius);
    margin-bottom: 1rem;
}

.comment-header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 0.5rem;
}

.comment-author {
    color: var(--text-color);
}

.comment-date {
    color: var(--text-light);
    font-size: 0.875rem;
}

.comment-content {
    color: var(--text-color);
    line-height: 1.6;
}

.comment-form-container {
    background: var(--bg-light);
    padding: 2rem;
    border-radius: var(--radius);
}

.form-group {
    margin-bottom: 1.5rem;
}

.form-group label {
    display: block;
    margin-bottom: 0.5rem;
    font-weight: 500;
    color: var(--text-color);
}

.form-control {
    width: 100%;
    padding: 0.75rem;
    border: 1px solid var(--border-color);
    border-radius: var(--radius);
    font-size: 1rem;
    transition: var(--transition);
}

.form-control:focus {
    outline: none;
    border-color: var(--primary-color);
    box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
}

.submit-btn {
    background-color: var(--primary-color);
    color: white;
    padding: 0.75rem 2rem;
    border: none;
    border-radius: var(--radius);
    font-size: 1rem;
    font-weight: 500;
    cursor: pointer;
    transition: var(--transition);
}

.submit-btn:hover {
    opacity: 0.9;
    transform: translateY(-1px);
}

/* ========================================
   Pagination
   ======================================== */
.pagination {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 1rem;
    margin: 3rem 0;
}

.pagination-link {
    padding: 0.5rem 1rem;
    background: var(--bg-light);
    color: var(--text-color);
    text-decoration: none;
    border-radius: var(--radius);
    transition: var(--transition);
}

.pagination-link:hover {
    background: var(--primary-color);
    color: white;
}

.pagination-info {
    color: var(--text-light);
}

/* ========================================
   Messages/Alerts
   ======================================== */
.messages {
    margin: 1rem 0;
}

.alert {
    padding: 1rem;
    border-radius: var(--radius);
    margin-bottom: 1rem;
}

.alert-success {
    background-color: #d1fae5;
    color: #065f46;
    border: 1px solid #6ee7b7;
}

/* ========================================
   Responsive Design
   ======================================== */
@media (max-width: 768px) {
    .navbar .container {
        flex-direction: column;
    }

    .nav-menu {
        flex-direction: column;
        gap: 1rem;
    }

    .search-form {
        width: 100%;
    }

    .search-input {
        flex: 1;
    }

    .posts-grid {
        grid-template-columns: 1fr;
    }

    .hero h1 {
        font-size: 2rem;
    }

    .post-header .post-title {
        font-size: 2rem;
    }

    .featured-image {
        height: 250px;
    }
}
```

## Step 2: Add Custom Styles

You can customize colors, spacing, and other design elements by modifying the CSS variables at the top of the file.

## CSS Best Practices

### Use CSS Variables

CSS variables make it easy to maintain consistent colors and spacing throughout your site.

### Mobile-First Design

Start with mobile styles, then add media queries for larger screens.

### Use Flexbox and Grid

Modern layout tools make responsive design easier:
- **Flexbox:** For one-dimensional layouts (rows or columns)
- **Grid:** For two-dimensional layouts (rows and columns)

### Semantic Class Names

Use descriptive class names:
- ✅ `.post-card` (good)
- ❌ `.box1` (bad)

## What's Next?

Now that we have beautiful styling, we'll add JavaScript to make the blog interactive and dynamic.

!!! success "Styling Complete!"
    Your blog now has a modern, responsive design. In the next tutorial, we'll add JavaScript interactivity.

---

**Previous Tutorial:** [HTML Templates](05_html_templates.md)  
**Next Tutorial:** [JavaScript Interactivity](07_javascript.md)
