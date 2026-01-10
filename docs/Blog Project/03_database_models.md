# Blog Project: Database Models

In this tutorial, we'll design and create the database models for our blog. We'll use Django's ORM (Object-Relational Mapping) to define our data structure, which will automatically create SQL tables.

## Understanding Models

Django models are Python classes that represent database tables. Each model class corresponds to a table, and each attribute represents a column.

## Model Design

We'll create three main models:

1. **Category** - Organize posts by topic
2. **Post** - The main blog post content
3. **Comment** - Allow readers to comment on posts

## Step 1: Category Model

Open `blog/models.py` and add the Category model:

```python
from django.db import models
from django.urls import reverse

class Category(models.Model):
    name = models.CharField(max_length=100, unique=True)
    slug = models.SlugField(max_length=100, unique=True)
    description = models.TextField(blank=True)
    created_at = models.DateTimeField(auto_now_add=True)

    class Meta:
        verbose_name_plural = "Categories"
        ordering = ['name']

    def __str__(self):
        return self.name

    def get_absolute_url(self):
        return reverse('category_posts', kwargs={'slug': self.slug})
```

### Field Explanations

- **`name`:** Category name (e.g., "Web Development", "Python")
- **`slug`:** URL-friendly version of the name (e.g., "web-development")
- **`description`:** Optional description of the category
- **`created_at`:** Automatically set when category is created

## Step 2: Post Model

Add the Post model:

```python
class Post(models.Model):
    title = models.CharField(max_length=200)
    slug = models.SlugField(max_length=200, unique=True)
    author = models.ForeignKey(
        'auth.User',
        on_delete=models.CASCADE,
        related_name='blog_posts'
    )
    category = models.ForeignKey(
        Category,
        on_delete=models.SET_NULL,
        null=True,
        related_name='posts'
    )
    content = models.TextField()
    excerpt = models.TextField(max_length=300, blank=True)
    featured_image = models.ImageField(upload_to='posts/', blank=True, null=True)
    status = models.CharField(
        max_length=10,
        choices=[
            ('draft', 'Draft'),
            ('published', 'Published'),
        ],
        default='draft'
    )
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    published_at = models.DateTimeField(null=True, blank=True)

    class Meta:
        ordering = ['-created_at']
        indexes = [
            models.Index(fields=['-created_at']),
            models.Index(fields=['status']),
        ]

    def __str__(self):
        return self.title

    def get_absolute_url(self):
        return reverse('post_detail', kwargs={'slug': self.slug})
```

### Field Explanations

- **`title`:** Post title
- **`slug`:** URL-friendly version of title
- **`author`:** Foreign key to User model (who wrote the post)
- **`category`:** Foreign key to Category (optional)
- **`content`:** Main post content (HTML/text)
- **`excerpt`:** Short summary for previews
- **`featured_image`:** Optional header image
- **`status`:** Draft or Published
- **`created_at`:** When post was created
- **`updated_at`:** Last modification time
- **`published_at`:** When post was published

### Relationships Explained

- **ForeignKey:** Creates a many-to-one relationship
  - Many posts can belong to one category
  - Many posts can be written by one author
- **`on_delete=models.CASCADE`:** If author is deleted, delete their posts
- **`on_delete=models.SET_NULL`:** If category is deleted, set post category to NULL

## Step 3: Comment Model

Add the Comment model:

```python
class Comment(models.Model):
    post = models.ForeignKey(
        Post,
        on_delete=models.CASCADE,
        related_name='comments'
    )
    author = models.CharField(max_length=100)
    email = models.EmailField()
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    approved = models.BooleanField(default=False)

    class Meta:
        ordering = ['-created_at']

    def __str__(self):
        return f'Comment by {self.author} on {self.post.title}'
```

### Field Explanations

- **`post`:** Foreign key to Post (which post this comment belongs to)
- **`author`:** Commenter's name
- **`email`:** Commenter's email
- **`content`:** Comment text
- **`created_at`:** When comment was created
- **`approved`:** Whether comment is approved (moderation)

## Step 4: Complete models.py

Your complete `blog/models.py` should look like this:

```python
from django.db import models
from django.urls import reverse

class Category(models.Model):
    name = models.CharField(max_length=100, unique=True)
    slug = models.SlugField(max_length=100, unique=True)
    description = models.TextField(blank=True)
    created_at = models.DateTimeField(auto_now_add=True)

    class Meta:
        verbose_name_plural = "Categories"
        ordering = ['name']

    def __str__(self):
        return self.name

    def get_absolute_url(self):
        return reverse('category_posts', kwargs={'slug': self.slug})


class Post(models.Model):
    title = models.CharField(max_length=200)
    slug = models.SlugField(max_length=200, unique=True)
    author = models.ForeignKey(
        'auth.User',
        on_delete=models.CASCADE,
        related_name='blog_posts'
    )
    category = models.ForeignKey(
        Category,
        on_delete=models.SET_NULL,
        null=True,
        related_name='posts'
    )
    content = models.TextField()
    excerpt = models.TextField(max_length=300, blank=True)
    featured_image = models.ImageField(upload_to='posts/', blank=True, null=True)
    status = models.CharField(
        max_length=10,
        choices=[
            ('draft', 'Draft'),
            ('published', 'Published'),
        ],
        default='draft'
    )
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    published_at = models.DateTimeField(null=True, blank=True)

    class Meta:
        ordering = ['-created_at']
        indexes = [
            models.Index(fields=['-created_at']),
            models.Index(fields=['status']),
        ]

    def __str__(self):
        return self.title

    def get_absolute_url(self):
        return reverse('post_detail', kwargs={'slug': self.slug})


class Comment(models.Model):
    post = models.ForeignKey(
        Post,
        on_delete=models.CASCADE,
        related_name='comments'
    )
    author = models.CharField(max_length=100)
    email = models.EmailField()
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    approved = models.BooleanField(default=False)

    class Meta:
        ordering = ['-created_at']

    def __str__(self):
        return f'Comment by {self.author} on {self.post.title}'
```

## Step 5: Create and Run Migrations

Now we need to create migration files and apply them to the database:

```bash
# Create migration files
python manage.py makemigrations

# Apply migrations to database
python manage.py migrate
```

## Step 6: Register Models in Admin

Open `blog/admin.py` and register the models:

```python
from django.contrib import admin
from .models import Category, Post, Comment

@admin.register(Category)
class CategoryAdmin(admin.ModelAdmin):
    list_display = ['name', 'slug', 'created_at']
    prepopulated_fields = {'slug': ('name',)}

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'author', 'category', 'status', 'created_at']
    list_filter = ['status', 'created_at', 'category']
    search_fields = ['title', 'content']
    prepopulated_fields = {'slug': ('title',)}
    date_hierarchy = 'created_at'

@admin.register(Comment)
class CommentAdmin(admin.ModelAdmin):
    list_display = ['author', 'post', 'created_at', 'approved']
    list_filter = ['approved', 'created_at']
    search_fields = ['author', 'content']
```

## Step 7: Test in Admin Panel

1. Start the server: `python manage.py runserver`
2. Visit http://127.0.0.1:8000/admin/
3. Log in with your superuser credentials
4. Try creating a category and a post

## Understanding SQL Behind the Scenes

Django's ORM automatically generates SQL. When you run `makemigrations`, Django creates SQL CREATE TABLE statements. For example, the Post model creates:

```sql
CREATE TABLE blog_post (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    title VARCHAR(200) NOT NULL,
    slug VARCHAR(200) NOT NULL UNIQUE,
    author_id INTEGER NOT NULL,
    category_id INTEGER,
    content TEXT NOT NULL,
    excerpt TEXT,
    featured_image VARCHAR(100),
    status VARCHAR(10) NOT NULL,
    created_at DATETIME NOT NULL,
    updated_at DATETIME NOT NULL,
    published_at DATETIME,
    FOREIGN KEY (author_id) REFERENCES auth_user(id),
    FOREIGN KEY (category_id) REFERENCES blog_category(id)
);
```

## Best Practices

### Use Slugs for URLs

Slugs create clean, SEO-friendly URLs:
- Instead of: `/post/1/`
- Use: `/post/my-awesome-blog-post/`

### Add Indexes for Performance

We added indexes on `created_at` and `status` for faster queries.

### Use Related Names

`related_name='posts'` allows us to access all posts in a category:
```python
category.posts.all()  # All posts in this category
```

## What's Next?

Now that we have our database models, we'll create views and URLs to display our blog posts.

!!! success "Models Created!"
    Your database structure is ready. In the next tutorial, we'll create views to display the blog content.

---

**Previous Tutorial:** [Project Setup](02_project_setup.md)  
**Next Tutorial:** [Views and URLs](04_views_urls.md)
