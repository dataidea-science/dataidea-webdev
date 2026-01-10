# Blog Project: HTML Templates

In this tutorial, we'll create HTML templates using Django's template language. Templates combine HTML structure with dynamic data from our views.

## Understanding Django Templates

Django templates use:
- **HTML** for structure
- **Template tags** `{% %}` for logic
- **Template variables** `{{ }}` for data
- **Template inheritance** for reusable layouts

## Step 1: Create Base Template

Create `templates/base.html` - this will be the foundation for all pages:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}My Blog{% endblock %}</title>
    {% load static %}
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
</head>
<body>
    <!-- Navigation -->
    <nav class="navbar">
        <div class="container">
            <a href="{% url 'blog:post_list' %}" class="logo">My Blog</a>
            <ul class="nav-menu">
                <li><a href="{% url 'blog:post_list' %}">Home</a></li>
                <li><a href="#categories">Categories</a></li>
                <li><a href="#about">About</a></li>
            </ul>
            <!-- Search Form -->
            <form class="search-form" method="get" action="{% url 'blog:search' %}">
                <input type="search" name="q" placeholder="Search posts..." class="search-input">
                <button type="submit" class="search-btn">Search</button>
            </form>
        </div>
    </nav>

    <!-- Main Content -->
    <main class="main-content">
        <div class="container">
            <!-- Messages -->
            {% if messages %}
                <div class="messages">
                    {% for message in messages %}
                        <div class="alert alert-{{ message.tags }}">
                            {{ message }}
                        </div>
                    {% endfor %}
                </div>
            {% endif %}

            <!-- Page Content -->
            {% block content %}
            {% endblock %}
        </div>
    </main>

    <!-- Footer -->
    <footer class="footer">
        <div class="container">
            <p>&copy; 2024 My Blog. All rights reserved.</p>
        </div>
    </footer>

    <script src="{% static 'js/main.js' %}"></script>
</body>
</html>
```

### Key Template Features

- **`{% load static %}`** - Load static files (CSS, JS, images)
- **`{% static 'css/style.css' %}`** - Generate correct path to static file
- **`{% url 'blog:post_list' %}`** - Generate URL from name
- **`{% block title %}`** - Define sections that child templates can override
- **`{{ message }}`** - Display variable content

## Step 2: Create Post List Template

Create `templates/blog/index.html` - displays all posts:

```html
{% extends 'base.html' %}

{% block title %}Home - My Blog{% endblock %}

{% block content %}
<section class="hero">
    <h1>Welcome to My Blog</h1>
    <p>Discover amazing articles about web development, programming, and more.</p>
</section>

<section class="posts-section">
    <h2>Latest Posts</h2>
    
    {% if posts %}
        <div class="posts-grid">
            {% for post in posts %}
                <article class="post-card">
                    {% if post.featured_image %}
                        <img src="{{ post.featured_image.url }}" alt="{{ post.title }}" class="post-image">
                    {% endif %}
                    
                    <div class="post-content">
                        <div class="post-meta">
                            <span class="post-date">{{ post.created_at|date:"F d, Y" }}</span>
                            {% if post.category %}
                                <a href="{% url 'blog:category_posts' post.category.slug %}" class="post-category">
                                    {{ post.category.name }}
                                </a>
                            {% endif %}
                        </div>
                        
                        <h3 class="post-title">
                            <a href="{% url 'blog:post_detail' post.slug %}">{{ post.title }}</a>
                        </h3>
                        
                        {% if post.excerpt %}
                            <p class="post-excerpt">{{ post.excerpt }}</p>
                        {% else %}
                            <p class="post-excerpt">{{ post.content|truncatewords:30 }}</p>
                        {% endif %}
                        
                        <div class="post-footer">
                            <span class="post-author">By {{ post.author.get_full_name|default:post.author.username }}</span>
                            <a href="{% url 'blog:post_detail' post.slug %}" class="read-more">Read More →</a>
                        </div>
                    </div>
                </article>
            {% endfor %}
        </div>

        <!-- Pagination -->
        {% if is_paginated %}
            <div class="pagination">
                {% if page_obj.has_previous %}
                    <a href="?page={{ page_obj.previous_page_number }}" class="pagination-link">Previous</a>
                {% endif %}
                
                <span class="pagination-info">
                    Page {{ page_obj.number }} of {{ page_obj.paginator.num_pages }}
                </span>
                
                {% if page_obj.has_next %}
                    <a href="?page={{ page_obj.next_page_number }}" class="pagination-link">Next</a>
                {% endif %}
            </div>
        {% endif %}
    {% else %}
        <p class="no-posts">No posts available yet. Check back soon!</p>
    {% endif %}
</section>
{% endblock %}
```

### Template Tags Used

- **`{% extends 'base.html' %}`** - Inherit from base template
- **`{% for post in posts %}`** - Loop through posts
- **`{{ post.title }}`** - Display post title
- **`{{ post.created_at|date:"F d, Y" }}`** - Format date (filter)
- **`{{ post.content|truncatewords:30 }}`** - Truncate to 30 words
- **`{% if post.featured_image %}`** - Conditional display

## Step 3: Create Post Detail Template

Create `templates/blog/post_detail.html`:

```html
{% extends 'base.html' %}

{% block title %}{{ post.title }} - My Blog{% endblock %}

{% block content %}
<article class="post-detail">
    <!-- Post Header -->
    <header class="post-header">
        <div class="post-meta">
            <span class="post-date">{{ post.created_at|date:"F d, Y" }}</span>
            {% if post.category %}
                <a href="{% url 'blog:category_posts' post.category.slug %}" class="post-category">
                    {{ post.category.name }}
                </a>
            {% endif %}
        </div>
        
        <h1 class="post-title">{{ post.title }}</h1>
        
        <div class="post-author">
            <span>By {{ post.author.get_full_name|default:post.author.username }}</span>
        </div>
    </header>

    <!-- Featured Image -->
    {% if post.featured_image %}
        <img src="{{ post.featured_image.url }}" alt="{{ post.title }}" class="featured-image">
    {% endif %}

    <!-- Post Content -->
    <div class="post-body">
        {{ post.content|linebreaks }}
    </div>

    <!-- Related Posts -->
    {% if related_posts %}
        <section class="related-posts">
            <h3>Related Posts</h3>
            <div class="related-posts-grid">
                {% for related_post in related_posts %}
                    <a href="{% url 'blog:post_detail' related_post.slug %}" class="related-post-card">
                        <h4>{{ related_post.title }}</h4>
                        <span>{{ related_post.created_at|date:"M d, Y" }}</span>
                    </a>
                {% endfor %}
            </div>
        </section>
    {% endif %}
</article>

<!-- Comments Section -->
<section class="comments-section">
    <h3>Comments ({{ comments.count }})</h3>
    
    <!-- Display Comments -->
    {% if comments %}
        <div class="comments-list">
            {% for comment in comments %}
                <div class="comment">
                    <div class="comment-header">
                        <strong class="comment-author">{{ comment.author }}</strong>
                        <span class="comment-date">{{ comment.created_at|date:"F d, Y" }}</span>
                    </div>
                    <div class="comment-content">
                        {{ comment.content|linebreaks }}
                    </div>
                </div>
            {% endfor %}
        </div>
    {% else %}
        <p class="no-comments">No comments yet. Be the first to comment!</p>
    {% endif %}

    <!-- Comment Form -->
    <div class="comment-form-container">
        <h4>Leave a Comment</h4>
        <form method="post" action="{% url 'blog:add_comment' post.slug %}" class="comment-form">
            {% csrf_token %}
            <div class="form-group">
                <label for="{{ comment_form.author.id_for_label }}">Name</label>
                {{ comment_form.author }}
            </div>
            <div class="form-group">
                <label for="{{ comment_form.email.id_for_label }}">Email</label>
                {{ comment_form.email }}
            </div>
            <div class="form-group">
                <label for="{{ comment_form.content.id_for_label }}">Comment</label>
                {{ comment_form.content }}
            </div>
            <button type="submit" class="submit-btn">Submit Comment</button>
        </form>
    </div>
</section>
{% endblock %}
```

### Important Template Features

- **`{% csrf_token %}`** - Required for POST forms (security)
- **`{{ post.content|linebreaks }}`** - Convert line breaks to `<br>` tags
- **`{{ comments.count }}`** - Count related objects

## Step 4: Create Category Posts Template

Create `templates/blog/category_posts.html`:

```html
{% extends 'base.html' %}

{% block title %}{{ category.name }} - My Blog{% endblock %}

{% block content %}
<section class="category-header">
    <h1>{{ category.name }}</h1>
    {% if category.description %}
        <p class="category-description">{{ category.description }}</p>
    {% endif %}
</section>

<section class="posts-section">
    {% if posts %}
        <div class="posts-grid">
            {% for post in posts %}
                <article class="post-card">
                    <!-- Same structure as index.html -->
                    {% include 'blog/post_card.html' %}
                </article>
            {% endfor %}
        </div>

        <!-- Pagination -->
        {% if is_paginated %}
            <div class="pagination">
                {% if page_obj.has_previous %}
                    <a href="?page={{ page_obj.previous_page_number }}">Previous</a>
                {% endif %}
                <span>Page {{ page_obj.number }} of {{ page_obj.paginator.num_pages }}</span>
                {% if page_obj.has_next %}
                    <a href="?page={{ page_obj.next_page_number }}">Next</a>
                {% endif %}
            </div>
        {% endif %}
    {% else %}
        <p>No posts in this category yet.</p>
    {% endif %}
</section>
{% endblock %}
```

## Step 5: Create Search Results Template

Create `templates/blog/search_results.html`:

```html
{% extends 'base.html' %}

{% block title %}Search Results{% endblock %}

{% block content %}
<section class="search-header">
    <h1>Search Results</h1>
    {% if query %}
        <p>Searching for: "<strong>{{ query }}</strong>"</p>
    {% endif %}
</section>

<section class="posts-section">
    {% if posts %}
        <p class="results-count">Found {{ posts.count }} result(s)</p>
        <div class="posts-grid">
            {% for post in posts %}
                <article class="post-card">
                    <!-- Post card content -->
                </article>
            {% endfor %}
        </div>
    {% else %}
        <p class="no-results">No results found. Try a different search term.</p>
    {% endif %}
</section>
{% endblock %}
```

## Template Best Practices

### Use Semantic HTML

- `<article>` for blog posts
- `<section>` for content sections
- `<header>`, `<footer>` for page structure
- `<nav>` for navigation

### Template Inheritance

- Create a base template with common elements
- Use `{% extends %}` to inherit
- Override blocks with `{% block %}`

### Reusable Components

Create partial templates for repeated elements:

```html
<!-- templates/blog/post_card.html -->
<article class="post-card">
    <!-- Post card content -->
</article>
```

Then include it:
```html
{% include 'blog/post_card.html' %}
```

## What's Next?

Now that we have HTML templates, we'll style them with CSS to create a beautiful, modern design.

!!! success "Templates Created!"
    Your HTML templates are ready. In the next tutorial, we'll add CSS styling.

---

**Previous Tutorial:** [Views and URLs](04_views_urls.md)  
**Next Tutorial:** [CSS Styling](06_css_styling.md)
