# Blog Project: Setup

In this tutorial, we'll set up the Django project structure and configure everything needed to start building our blog.

## Step 1: Create Virtual Environment

First, let's create a virtual environment to isolate our project dependencies:

```bash
# Create virtual environment
python -m venv blog_env

# Activate virtual environment
# On Windows:
blog_env\Scripts\activate
# On macOS/Linux:
source blog_env/bin/activate
```

## Step 2: Install Django

Install Django and other required packages:

```bash
pip install django
pip install pillow  # For image handling
```

## Step 3: Create Django Project

Create a new Django project called `blog_project`:

```bash
django-admin startproject blog_project .
```

The `.` at the end creates the project in the current directory. Your structure should look like:

```
blog_project/
├── manage.py
├── blog_project/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
└── blog_env/
```

## Step 4: Create Blog App

Create the main blog application:

```bash
python manage.py startapp blog
```

Create the accounts app for user authentication:

```bash
python manage.py startapp accounts
```

## Step 5: Configure Settings

Open `blog_project/settings.py` and make the following changes:

### Add Apps to INSTALLED_APPS

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    # Our apps
    'blog',
    'accounts',
]
```

### Configure Static Files

Add these settings for static files (CSS, JavaScript, images):

```python
# Static files (CSS, JavaScript, Images)
STATIC_URL = '/static/'
STATICFILES_DIRS = [
    BASE_DIR / 'static',
]
STATIC_ROOT = BASE_DIR / 'staticfiles'

# Media files (user uploads)
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

### Set Time Zone

```python
TIME_ZONE = 'UTC'
USE_TZ = True
```

### Configure Templates

Update the `TEMPLATES` setting to include the `BASE_DIR`:

```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'],
        'APP_DIRS': True,
        # ... rest of settings
    },
]
```

## Step 6: Create Directory Structure

Create the necessary directories:

```bash
# Create directories
mkdir templates
mkdir static
mkdir static/css
mkdir static/js
mkdir static/images
mkdir media
```

Your project structure should now look like:

```
blog_project/
├── manage.py
├── blog_project/
│   ├── settings.py
│   ├── urls.py
│   └── ...
├── blog/
│   ├── models.py
│   ├── views.py
│   ├── urls.py
│   └── ...
├── accounts/
│   ├── models.py
│   ├── views.py
│   └── ...
├── templates/
├── static/
│   ├── css/
│   ├── js/
│   └── images/
└── media/
```

## Step 7: Configure Main URLs

Update `blog_project/urls.py` to include media files in development:

```python
from django.contrib import admin
from django.urls import path, include
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('blog.urls')),
    path('accounts/', include('accounts.urls')),
]

# Serve media files in development
if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
    urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```

## Step 8: Run Initial Migrations

Django comes with built-in apps that need database tables. Run migrations:

```bash
python manage.py migrate
```

## Step 9: Create Superuser

Create an admin user to access the Django admin panel:

```bash
python manage.py createsuperuser
```

Follow the prompts to create your admin account.

## Step 10: Test the Setup

Start the development server:

```bash
python manage.py runserver
```

Visit:
- **Homepage:** http://127.0.0.1:8000/
- **Admin Panel:** http://127.0.0.1:8000/admin/

You should see Django's default welcome page and be able to log into the admin panel.

## Project Checklist

✅ Virtual environment created and activated  
✅ Django installed  
✅ Project and apps created  
✅ Settings configured  
✅ Directory structure created  
✅ URLs configured  
✅ Migrations run  
✅ Superuser created  
✅ Server running  

## Common Issues

### Issue: ModuleNotFoundError

**Solution:** Make sure your virtual environment is activated and Django is installed.

### Issue: Port Already in Use

**Solution:** Use a different port:
```bash
python manage.py runserver 8001
```

### Issue: Static Files Not Loading

**Solution:** Make sure `STATICFILES_DIRS` is configured correctly in `settings.py`.

## What's Next?

Now that our project is set up, we'll create the database models for our blog posts, categories, and comments.

!!! success "Setup Complete!"
    Your Django project is ready. In the next tutorial, we'll design and create the database models.

---

**Previous Tutorial:** [Project Overview](01_project_overview.md)  
**Next Tutorial:** [Database Models](03_database_models.md)
