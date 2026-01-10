# Blog Project: User Authentication

In this tutorial, we'll add user authentication so users can register, log in, and log out. We'll use Django's built-in authentication system.

## Step 1: Create Authentication URLs

Create `accounts/urls.py`:

```python
from django.urls import path
from django.contrib.auth import views as auth_views
from . import views

app_name = 'accounts'

urlpatterns = [
    path('register/', views.register, name='register'),
    path('login/', auth_views.LoginView.as_view(template_name='accounts/login.html'), name='login'),
    path('logout/', auth_views.LogoutView.as_view(), name='logout'),
    path('profile/', views.profile, name='profile'),
]
```

## Step 2: Configure Authentication Settings

Add to `blog_project/settings.py`:

```python
# Authentication settings
LOGIN_URL = 'accounts:login'
LOGIN_REDIRECT_URL = 'blog:post_list'
LOGOUT_REDIRECT_URL = 'blog:post_list'
```

## Step 3: Create Registration Form

Create `accounts/forms.py`:

```python
from django import forms
from django.contrib.auth.forms import UserCreationForm
from django.contrib.auth.models import User

class UserRegisterForm(UserCreationForm):
    email = forms.EmailField(required=True)
    first_name = forms.CharField(max_length=30, required=False)
    last_name = forms.CharField(max_length=30, required=False)

    class Meta:
        model = User
        fields = ['username', 'email', 'first_name', 'last_name', 'password1', 'password2']

    def __init__(self, *args, **kwargs):
        super().__init__(*args, **kwargs)
        self.fields['username'].widget.attrs.update({'class': 'form-control', 'placeholder': 'Username'})
        self.fields['email'].widget.attrs.update({'class': 'form-control', 'placeholder': 'Email'})
        self.fields['first_name'].widget.attrs.update({'class': 'form-control', 'placeholder': 'First Name'})
        self.fields['last_name'].widget.attrs.update({'class': 'form-control', 'placeholder': 'Last Name'})
        self.fields['password1'].widget.attrs.update({'class': 'form-control', 'placeholder': 'Password'})
        self.fields['password2'].widget.attrs.update({'class': 'form-control', 'placeholder': 'Confirm Password'})
```

## Step 4: Create Authentication Views

Create `accounts/views.py`:

```python
from django.shortcuts import render, redirect
from django.contrib import messages
from django.contrib.auth.decorators import login_required
from .forms import UserRegisterForm

def register(request):
    if request.method == 'POST':
        form = UserRegisterForm(request.POST)
        if form.is_valid():
            user = form.save()
            username = form.cleaned_data.get('username')
            messages.success(request, f'Account created for {username}! You can now log in.')
            return redirect('accounts:login')
    else:
        form = UserRegisterForm()
    return render(request, 'accounts/register.html', {'form': form})

@login_required
def profile(request):
    user_posts = request.user.blog_posts.all()
    return render(request, 'accounts/profile.html', {'user_posts': user_posts})
```

## Step 5: Create Registration Template

Create `templates/accounts/register.html`:

```html
{% extends 'base.html' %}

{% block title %}Register - My Blog{% endblock %}

{% block content %}
<div class="auth-container">
    <div class="auth-card">
        <h2>Create an Account</h2>
        <p class="auth-subtitle">Join our community and start writing!</p>
        
        <form method="post" class="auth-form">
            {% csrf_token %}
            
            <div class="form-group">
                <label for="{{ form.username.id_for_label }}">Username</label>
                {{ form.username }}
                {% if form.username.errors %}
                    <div class="form-errors">{{ form.username.errors }}</div>
                {% endif %}
            </div>
            
            <div class="form-group">
                <label for="{{ form.email.id_for_label }}">Email</label>
                {{ form.email }}
                {% if form.email.errors %}
                    <div class="form-errors">{{ form.email.errors }}</div>
                {% endif %}
            </div>
            
            <div class="form-row">
                <div class="form-group">
                    <label for="{{ form.first_name.id_for_label }}">First Name</label>
                    {{ form.first_name }}
                </div>
                
                <div class="form-group">
                    <label for="{{ form.last_name.id_for_label }}">Last Name</label>
                    {{ form.last_name }}
                </div>
            </div>
            
            <div class="form-group">
                <label for="{{ form.password1.id_for_label }}">Password</label>
                {{ form.password1 }}
                {% if form.password1.errors %}
                    <div class="form-errors">{{ form.password1.errors }}</div>
                {% endif %}
                <small class="form-help">Your password must be at least 8 characters long.</small>
            </div>
            
            <div class="form-group">
                <label for="{{ form.password2.id_for_label }}">Confirm Password</label>
                {{ form.password2 }}
                {% if form.password2.errors %}
                    <div class="form-errors">{{ form.password2.errors }}</div>
                {% endif %}
            </div>
            
            <button type="submit" class="submit-btn">Register</button>
        </form>
        
        <p class="auth-footer">
            Already have an account? <a href="{% url 'accounts:login' %}">Log in</a>
        </p>
    </div>
</div>
{% endblock %}
```

## Step 6: Create Login Template

Create `templates/accounts/login.html`:

```html
{% extends 'base.html' %}

{% block title %}Login - My Blog{% endblock %}

{% block content %}
<div class="auth-container">
    <div class="auth-card">
        <h2>Log In</h2>
        <p class="auth-subtitle">Welcome back!</p>
        
        <form method="post" class="auth-form">
            {% csrf_token %}
            
            {% if form.errors %}
                <div class="alert alert-error">
                    Your username and password didn't match. Please try again.
                </div>
            {% endif %}
            
            <div class="form-group">
                <label for="{{ form.username.id_for_label }}">Username</label>
                <input type="text" name="username" class="form-control" required>
            </div>
            
            <div class="form-group">
                <label for="{{ form.password.id_for_label }}">Password</label>
                <input type="password" name="password" class="form-control" required>
            </div>
            
            <button type="submit" class="submit-btn">Log In</button>
        </form>
        
        <p class="auth-footer">
            Don't have an account? <a href="{% url 'accounts:register' %}">Register</a>
        </p>
    </div>
</div>
{% endblock %}
```

## Step 7: Update Base Template

Update `templates/base.html` to show login/logout links:

```html
<!-- In the navbar section -->
<ul class="nav-menu">
    <li><a href="{% url 'blog:post_list' %}">Home</a></li>
    <li><a href="#categories">Categories</a></li>
    {% if user.is_authenticated %}
        <li><a href="{% url 'accounts:profile' %}">Profile</a></li>
        <li><a href="{% url 'accounts:logout' %}">Logout</a></li>
    {% else %}
        <li><a href="{% url 'accounts:login' %}">Login</a></li>
        <li><a href="{% url 'accounts:register' %}">Register</a></li>
    {% endif %}
</ul>
```

## Step 8: Add Authentication Styles

Add to `static/css/style.css`:

```css
/* ========================================
   Authentication Styles
   ======================================== */
.auth-container {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 60vh;
    padding: 2rem 0;
}

.auth-card {
    background: var(--bg-color);
    border: 1px solid var(--border-color);
    border-radius: var(--radius);
    padding: 2.5rem;
    max-width: 500px;
    width: 100%;
    box-shadow: var(--shadow-md);
}

.auth-card h2 {
    margin-bottom: 0.5rem;
    color: var(--text-color);
}

.auth-subtitle {
    color: var(--text-light);
    margin-bottom: 2rem;
}

.auth-form {
    margin-bottom: 1.5rem;
}

.form-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
}

.form-help {
    display: block;
    margin-top: 0.5rem;
    font-size: 0.875rem;
    color: var(--text-light);
}

.form-errors {
    color: #ef4444;
    font-size: 0.875rem;
    margin-top: 0.5rem;
}

.alert-error {
    background-color: #fee2e2;
    color: #991b1b;
    padding: 1rem;
    border-radius: var(--radius);
    margin-bottom: 1rem;
}

.auth-footer {
    text-align: center;
    color: var(--text-light);
}

.auth-footer a {
    color: var(--primary-color);
    text-decoration: none;
}

.auth-footer a:hover {
    text-decoration: underline;
}
```

## Step 9: Protect Views (Optional)

Require login for certain views:

```python
from django.contrib.auth.decorators import login_required

@login_required
def create_post(request):
    # Only logged-in users can access this
    pass
```

## Testing Authentication

1. Visit http://127.0.0.1:8000/accounts/register/
2. Create a new account
3. Log in with your credentials
4. Check that the navbar shows "Profile" and "Logout"

## Security Best Practices

### Password Requirements

Django automatically enforces:
- Minimum length (configurable)
- Common password validation
- Password strength checks

### CSRF Protection

Always use `{% csrf_token %}` in forms to prevent CSRF attacks.

### Session Security

Django handles session security automatically. Configure in `settings.py`:

```python
SESSION_COOKIE_SECURE = True  # HTTPS only (production)
SESSION_COOKIE_HTTPONLY = True  # Prevent JavaScript access
```

## What's Next?

Now that users can register and log in, we'll add the final touches: search functionality and deployment instructions.

!!! success "Authentication Complete!"
    Users can now register and log in. In the next tutorial, we'll add search functionality and prepare for deployment.

---

**Previous Tutorial:** [JavaScript Interactivity](07_javascript.md)  
**Next Tutorial:** [Search & Deployment](09_search_deployment.md)
