# Blog Project: Views and URLs

In this tutorial, we'll create views to handle displaying blog posts and set up URL routing. Views are the logic that processes requests and returns responses.

## Understanding Views

Django views are Python functions or classes that:
- Receive HTTP requests
- Process data (query database, validate forms)
- Return HTTP responses (HTML pages, JSON, redirects)

## Step 1: Create Blog URLs

First, create `blog/urls.py`:

```python
from django.urls import path
from . import views

app_name = 'blog'

urlpatterns = [
    path('', views.PostListView.as_view(), name='post_list'),
    path('post/<slug:slug>/', views.PostDetailView.as_view(), name='post_detail'),
    path('category/<slug:slug>/', views.CategoryPostView.as_view(), name='category_posts'),
    path('search/', views.SearchView.as_view(), name='search'),
]
```

## Step 2: Create Views

Open `blog/views.py` and add the following views:

### Import Required Modules

```python
from django.shortcuts import render, get_object_or_404
from django.views.generic import ListView, DetailView
from django.db.models import Q
from .models import Post, Category, Comment
from .forms import CommentForm
```

### Post List View (Homepage)

This view displays all published posts:

```python
class PostListView(ListView):
    model = Post
    template_name = 'blog/index.html'
    context_object_name = 'posts'
    paginate_by = 6

    def get_queryset(self):
        return Post.objects.filter(status='published').select_related('author', 'category')
```

**Explanation:**
- **`ListView`:** Generic view for displaying a list of objects
- **`model = Post`:** Model to display
- **`template_name`:** HTML template to render
- **`context_object_name`:** Variable name in template (default is `object_list`)
- **`paginate_by`:** Number of posts per page
- **`get_queryset()`:** Customize which posts to show (only published)
- **`select_related()`:** Optimize database queries

### Post Detail View

This view displays a single post with comments:

```python
class PostDetailView(DetailView):
    model = Post
    template_name = 'blog/post_detail.html'
    context_object_name = 'post'

    def get_queryset(self):
        return Post.objects.filter(status='published').select_related('author', 'category')

    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        post = self.get_object()
        context['comments'] = post.comments.filter(approved=True)
        context['comment_form'] = CommentForm()
        context['related_posts'] = Post.objects.filter(
            category=post.category,
            status='published'
        ).exclude(id=post.id)[:3]
        return context
```

**Explanation:**
- **`DetailView`:** Generic view for displaying a single object
- **`get_context_data()`:** Add extra data to template context
- **`comments`:** Approved comments for this post
- **`comment_form`:** Form for submitting new comments
- **`related_posts`:** Posts in the same category

### Category Posts View

Display all posts in a specific category:

```python
class CategoryPostView(ListView):
    model = Post
    template_name = 'blog/category_posts.html'
    context_object_name = 'posts'
    paginate_by = 6

    def get_queryset(self):
        category = get_object_or_404(Category, slug=self.kwargs['slug'])
        return Post.objects.filter(
            category=category,
            status='published'
        ).select_related('author', 'category')

    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        context['category'] = get_object_or_404(Category, slug=self.kwargs['slug'])
        return context
```

### Search View

Handle search functionality:

```python
class SearchView(ListView):
    model = Post
    template_name = 'blog/search_results.html'
    context_object_name = 'posts'
    paginate_by = 6

    def get_queryset(self):
        query = self.request.GET.get('q')
        if query:
            return Post.objects.filter(
                Q(title__icontains=query) | Q(content__icontains=query),
                status='published'
            ).select_related('author', 'category')
        return Post.objects.none()

    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        context['query'] = self.request.GET.get('q', '')
        return context
```

**Explanation:**
- **`Q` objects:** Allow complex database queries (OR conditions)
- **`icontains`:** Case-insensitive search
- **`objects.none()`:** Return empty queryset if no query

## Step 3: Create Comment Form

Create `blog/forms.py`:

```python
from django import forms
from .models import Comment

class CommentForm(forms.ModelForm):
    class Meta:
        model = Comment
        fields = ['author', 'email', 'content']
        widgets = {
            'author': forms.TextInput(attrs={
                'class': 'form-control',
                'placeholder': 'Your Name'
            }),
            'email': forms.EmailInput(attrs={
                'class': 'form-control',
                'placeholder': 'Your Email'
            }),
            'content': forms.Textarea(attrs={
                'class': 'form-control',
                'placeholder': 'Your Comment',
                'rows': 4
            }),
        }
```

## Step 4: Handle Comment Submission

Add a function view to handle comment submissions:

```python
from django.shortcuts import redirect
from django.contrib import messages

def add_comment(request, slug):
    post = get_object_or_404(Post, slug=slug, status='published')
    if request.method == 'POST':
        form = CommentForm(request.POST)
        if form.is_valid():
            comment = form.save(commit=False)
            comment.post = post
            comment.save()
            messages.success(request, 'Your comment is awaiting moderation.')
            return redirect('blog:post_detail', slug=slug)
    return redirect('blog:post_detail', slug=slug)
```

Update `blog/urls.py` to include the comment URL:

```python
urlpatterns = [
    # ... existing patterns
    path('post/<slug:slug>/comment/', views.add_comment, name='add_comment'),
]
```

## Step 5: Complete views.py

Your complete `blog/views.py`:

```python
from django.shortcuts import render, get_object_or_404, redirect
from django.views.generic import ListView, DetailView
from django.db.models import Q
from django.contrib import messages
from .models import Post, Category, Comment
from .forms import CommentForm

class PostListView(ListView):
    model = Post
    template_name = 'blog/index.html'
    context_object_name = 'posts'
    paginate_by = 6

    def get_queryset(self):
        return Post.objects.filter(status='published').select_related('author', 'category')

class PostDetailView(DetailView):
    model = Post
    template_name = 'blog/post_detail.html'
    context_object_name = 'post'

    def get_queryset(self):
        return Post.objects.filter(status='published').select_related('author', 'category')

    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        post = self.get_object()
        context['comments'] = post.comments.filter(approved=True)
        context['comment_form'] = CommentForm()
        context['related_posts'] = Post.objects.filter(
            category=post.category,
            status='published'
        ).exclude(id=post.id)[:3]
        return context

class CategoryPostView(ListView):
    model = Post
    template_name = 'blog/category_posts.html'
    context_object_name = 'posts'
    paginate_by = 6

    def get_queryset(self):
        category = get_object_or_404(Category, slug=self.kwargs['slug'])
        return Post.objects.filter(
            category=category,
            status='published'
        ).select_related('author', 'category')

    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        context['category'] = get_object_or_404(Category, slug=self.kwargs['slug'])
        return context

class SearchView(ListView):
    model = Post
    template_name = 'blog/search_results.html'
    context_object_name = 'posts'
    paginate_by = 6

    def get_queryset(self):
        query = self.request.GET.get('q')
        if query:
            return Post.objects.filter(
                Q(title__icontains=query) | Q(content__icontains=query),
                status='published'
            ).select_related('author', 'category')
        return Post.objects.none()

    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        context['query'] = self.request.GET.get('q', '')
        return context

def add_comment(request, slug):
    post = get_object_or_404(Post, slug=slug, status='published')
    if request.method == 'POST':
        form = CommentForm(request.POST)
        if form.is_valid():
            comment = form.save(commit=False)
            comment.post = post
            comment.save()
            messages.success(request, 'Your comment is awaiting moderation.')
            return redirect('blog:post_detail', slug=slug)
    return redirect('blog:post_detail', slug=slug)
```

## Step 6: Test the Views

1. Create some test data in the admin panel
2. Visit http://127.0.0.1:8000/ to see the post list
3. Click on a post to see the detail view

## URL Patterns Explained

- **`path('', ...)`** - Homepage (empty string matches root URL)
- **`path('post/<slug:slug>/', ...)`** - Post detail page
  - `<slug:slug>` captures the slug from the URL
  - Example: `/post/my-first-post/` → `slug='my-first-post'`
- **`path('category/<slug:slug>/', ...)`** - Category page
- **`app_name = 'blog'`** - Namespace for URLs (prevents conflicts)

## Best Practices

### Use Generic Views

Django's generic views (ListView, DetailView) reduce boilerplate code.

### Optimize Queries

Use `select_related()` and `prefetch_related()` to reduce database queries.

### Filter Published Posts

Always filter by `status='published'` to hide drafts.

## What's Next?

Now that we have views and URLs, we'll create HTML templates to display our blog content.

!!! success "Views Created!"
    Your blog views are ready. In the next tutorial, we'll create HTML templates.

---

**Previous Tutorial:** [Database Models](03_database_models.md)  
**Next Tutorial:** [HTML Templates](05_html_templates.md)
