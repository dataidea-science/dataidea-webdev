# Blog Project: Search & Deployment

In this final tutorial, we'll enhance the search functionality and prepare your blog for deployment to production.

## Part 1: Enhanced Search

We already created a basic search view. Let's enhance it with better features.

### Improve Search View

Update `blog/views.py` SearchView:

```python
class SearchView(ListView):
    model = Post
    template_name = 'blog/search_results.html'
    context_object_name = 'posts'
    paginate_by = 6

    def get_queryset(self):
        query = self.request.GET.get('q', '').strip()
        if query:
            # Search in title, content, and excerpt
            return Post.objects.filter(
                Q(title__icontains=query) |
                Q(content__icontains=query) |
                Q(excerpt__icontains=query),
                status='published'
            ).select_related('author', 'category').distinct()
        return Post.objects.none()

    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        context['query'] = self.request.GET.get('q', '')
        context['results_count'] = self.get_queryset().count()
        return context
```

### Add Search Highlighting

Add to `static/js/main.js`:

```javascript
function highlightSearchTerms() {
    const urlParams = new URLSearchParams(window.location.search);
    const query = urlParams.get('q');
    
    if (query) {
        const posts = document.querySelectorAll('.post-card, .post-detail');
        const searchTerms = query.split(' ').filter(term => term.length > 2);
        
        posts.forEach(post => {
            searchTerms.forEach(term => {
                const regex = new RegExp(`(${term})`, 'gi');
                const walker = document.createTreeWalker(
                    post,
                    NodeFilter.SHOW_TEXT,
                    null,
                    false
                );
                
                const textNodes = [];
                let node;
                while (node = walker.nextNode()) {
                    if (node.parentElement.tagName !== 'SCRIPT' && 
                        node.parentElement.tagName !== 'STYLE') {
                        textNodes.push(node);
                    }
                }
                
                textNodes.forEach(textNode => {
                    if (regex.test(textNode.textContent)) {
                        const highlighted = textNode.textContent.replace(
                            regex,
                            '<mark>$1</mark>'
                        );
                        const wrapper = document.createElement('span');
                        wrapper.innerHTML = highlighted;
                        textNode.parentNode.replaceChild(wrapper, textNode);
                    }
                });
            });
        });
    }
}

// Call on search results page
if (window.location.pathname.includes('/search/')) {
    highlightSearchTerms();
}
```

## Part 2: Deployment Preparation

### Update Settings for Production

Create `blog_project/settings_production.py`:

```python
from .settings import *
import os

# Security settings
DEBUG = False
ALLOWED_HOSTS = ['yourdomain.com', 'www.yourdomain.com']

# Database (use PostgreSQL in production)
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.environ.get('DB_NAME'),
        'USER': os.environ.get('DB_USER'),
        'PASSWORD': os.environ.get('DB_PASSWORD'),
        'HOST': os.environ.get('DB_HOST', 'localhost'),
        'PORT': os.environ.get('DB_PORT', '5432'),
    }
}

# Static files
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')

# Security
SECURE_SSL_REDIRECT = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
SECURE_BROWSER_XSS_FILTER = True
SECURE_CONTENT_TYPE_NOSNIFF = True
X_FRAME_OPTIONS = 'DENY'

# Email configuration
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = os.environ.get('EMAIL_HOST')
EMAIL_PORT = int(os.environ.get('EMAIL_PORT', 587))
EMAIL_USE_TLS = True
EMAIL_HOST_USER = os.environ.get('EMAIL_USER')
EMAIL_HOST_PASSWORD = os.environ.get('EMAIL_PASSWORD')
```

### Create requirements.txt

```bash
pip freeze > requirements.txt
```

Your `requirements.txt` should include:
```
Django>=4.2.0
Pillow>=10.0.0
psycopg2-binary>=2.9.0  # For PostgreSQL
gunicorn>=21.0.0  # WSGI server
whitenoise>=6.5.0  # Static file serving
```

### Create .env.example

Create a template for environment variables:

```env
DEBUG=False
SECRET_KEY=your-secret-key-here
ALLOWED_HOSTS=yourdomain.com,www.yourdomain.com
DB_NAME=blog_db
DB_USER=blog_user
DB_PASSWORD=your-db-password
DB_HOST=localhost
DB_PORT=5432
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your-email@gmail.com
EMAIL_PASSWORD=your-email-password
```

## Part 3: Deployment Options

### Option 1: Deploy to Heroku

1. **Install Heroku CLI** and login:
```bash
heroku login
```

2. **Create Heroku app**:
```bash
heroku create your-blog-app
```

3. **Create Procfile**:
```
web: gunicorn blog_project.wsgi --log-file -
```

4. **Set environment variables**:
```bash
heroku config:set SECRET_KEY=your-secret-key
heroku config:set DEBUG=False
```

5. **Deploy**:
```bash
git push heroku main
heroku run python manage.py migrate
heroku run python manage.py createsuperuser
```

### Option 2: Deploy to DigitalOcean

1. **Create a Droplet** (Ubuntu 22.04)
2. **Install dependencies**:
```bash
sudo apt update
sudo apt install python3-pip python3-venv nginx postgresql
```

3. **Set up your application**:
```bash
git clone your-repo
cd blog_project
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

4. **Configure Gunicorn**:
Create `gunicorn_config.py`:
```python
bind = "127.0.0.1:8000"
workers = 3
```

5. **Create systemd service**:
Create `/etc/systemd/system/blog.service`:
```ini
[Unit]
Description=Blog Gunicorn daemon
After=network.target

[Service]
User=www-data
Group=www-data
WorkingDirectory=/path/to/blog_project
ExecStart=/path/to/venv/bin/gunicorn --config gunicorn_config.py blog_project.wsgi

[Install]
WantedBy=multi-user.target
```

6. **Configure Nginx**:
Create `/etc/nginx/sites-available/blog`:
```nginx
server {
    listen 80;
    server_name yourdomain.com;

    location /static/ {
        alias /path/to/blog_project/staticfiles/;
    }

    location /media/ {
        alias /path/to/blog_project/media/;
    }

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

### Option 3: Deploy to Railway

1. **Connect your GitHub repository** to Railway
2. **Add environment variables** in Railway dashboard
3. **Railway automatically detects Django** and deploys
4. **Run migrations**:
```bash
railway run python manage.py migrate
```

## Part 4: Post-Deployment Checklist

### Essential Steps

- [ ] Set `DEBUG = False` in production
- [ ] Set `ALLOWED_HOSTS` correctly
- [ ] Configure database (PostgreSQL recommended)
- [ ] Collect static files: `python manage.py collectstatic`
- [ ] Run migrations: `python manage.py migrate`
- [ ] Create superuser: `python manage.py createsuperuser`
- [ ] Set up SSL certificate (Let's Encrypt)
- [ ] Configure email backend
- [ ] Set up backups
- [ ] Monitor error logs

### Security Checklist

- [ ] Use strong `SECRET_KEY`
- [ ] Enable HTTPS (SSL/TLS)
- [ ] Set secure cookie flags
- [ ] Configure CORS if needed
- [ ] Set up firewall rules
- [ ] Keep dependencies updated
- [ ] Use environment variables for secrets

### Performance Optimization

1. **Enable caching**:
```python
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.redis.RedisCache',
        'LOCATION': 'redis://127.0.0.1:6379/1',
    }
}
```

2. **Use CDN for static files** (CloudFlare, AWS CloudFront)

3. **Optimize database queries** (already using `select_related`)

4. **Enable compression**:
```python
MIDDLEWARE = [
    # ...
    'django.middleware.gzip.GZipMiddleware',
]
```

## Congratulations!

You've built a complete, production-ready blog application! 🎉

### What You've Accomplished

✅ Created Django project structure  
✅ Designed database models  
✅ Built views and URL routing  
✅ Created responsive HTML templates  
✅ Styled with modern CSS  
✅ Added JavaScript interactivity  
✅ Implemented user authentication  
✅ Added search functionality  
✅ Prepared for deployment  

### Next Steps

- **Extend Features**: Add tags, RSS feeds, social sharing
- **Improve Design**: Add animations, dark mode toggle
- **Add Tests**: Write unit tests for your views and models
- **Monitor**: Set up error tracking (Sentry)
- **SEO**: Add meta tags, sitemap, robots.txt

### Resources

- [Django Documentation](https://docs.djangoproject.com/)
- [Django Deployment Checklist](https://docs.djangoproject.com/en/stable/howto/deployment/checklist/)
- [Mozilla Developer Network](https://developer.mozilla.org/) - HTML, CSS, JavaScript reference

---

**Previous Tutorial:** [User Authentication](08_authentication.md)  
**Project Complete!** 🚀
