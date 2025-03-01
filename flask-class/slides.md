---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: true
info: |
  ## Flask: From Basics to Advanced
  A comprehensive guide to Flask web development
drawings:
  persist: false
transition: slide-left
mdc: true
---

# Flask: From Basics to Advanced

A comprehensive journey from Python decorators to deploying Flask applications

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---
transition: fade-out
---

# Agenda

<div grid="~ cols-2 gap-4">
<div>

- **Python Fundamentals**
  - Function Decorators
  - Higher-Order Functions
  
- **Introduction to Flask**
  - What is Flask?
  - Flask vs Other Frameworks
  - Flask Philosophy
  
- **Setup & Basics**
  - Installing Flask
  - First Flask Application
  - Flask Project Structure
</div>
<div>

- **Routing & Views**
  - Creating Routes
  - URL Parameters
  - HTTP Methods
  
- **Templates & Forms**
  - Jinja2 Templates
  - Form Handling
  
- **Deployment**
  - Production Considerations
  - Deployment Options
  - Best Practices
</div>
</div>

---
layout: center
class: text-center
transition: fade
---

# Part 1: Python Fundamentals

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
transition: slide-up
---

# Functions in Python

<div grid="~ cols-2 gap-2">
<div>

- Functions are first-class citizens in Python
- They can be:
  - Assigned to variables
  - Passed as arguments
  - Returned from other functions
  - Stored in data structures

</div>
<div>

```python {all|1|3-5|7-8|all}
# Assigning to a variable
 
def greet(name):
    return f"Hello, {name}!"
 
# Function assigned to variable
greeting_func = greet
greeting_func("World")  # "Hello, World!"
```

</div>
</div>

---
transition: slide-up
---

# Higher-Order Functions

<div grid="~ cols-2 gap-2">
<div>

- Functions that either:
  - Take other functions as arguments
  - Return functions as results
  - Or both
- Enable powerful functional programming patterns

</div>
<div>

```python {all|1-3|5-7|9-10|all}
def apply_twice(func, arg):
    # Takes a function as parameter
    return func(func(arg))
    
def add_five(x):
    return x + 5
    
# Using higher-order function
result = apply_twice(add_five, 10)
print(result)  # 20 (10+5+5)
```

</div>
</div>

---
transition: fade-out
---

# Understanding Function Decorators

<div grid="~ cols-2 gap-2">
<div>

- Decorators are a syntactic sugar for higher-order functions
- They modify or enhance functions without changing their code
- Syntax: `@decorator` placed above function definition
- Used extensively in Flask

</div>
<div>

```python {all|1-4|6-7|9-12|all}
def my_decorator(func):
    def wrapper():
        print("Something before the function is called.")
        func()
        print("Something after the function is called.")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
# Output:
# Something before the function is called.
# Hello!
# Something after the function is called.
```

</div>
</div>

---
transition: slide-left
---

# Decorators with Arguments

<div grid="~ cols-2 gap-2">
<div>

- Decorators can accept arguments
- Requires an additional level of nesting
- Critical for understanding Flask route decorators

</div>
<div>

```python {all|1-7|9-11|13-16|all}
def repeat(n):
    def decorator(func):
        def wrapper():
            for _ in range(n):
                func()
        return wrapper
    return decorator

@repeat(3)
def say_hello():
    print("Hello!")

say_hello()

#Output
#Hello!
#Hello!
#Hello!

```

</div>
</div>

---
layout: center
class: text-center
transition: fade
---

# Part 2: Introduction to Flask

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
transition: slide-up
---

# What is Flask?

<div grid="~ cols-2 gap-2">
<div>

- Lightweight, micro web framework for Python
- Created by Armin Ronacher in 2010
- Based on Werkzeug (WSGI utility) and Jinja2 (template engine)
- "Micro" doesn't mean limited functionality
- Highly extensible with extensions

</div>

<div class="flex items-center justify-center">
  <div class="text-center">
    <div class="text-5xl animate-pulse">
      🧪 + 🐍 = 🌐
    </div>
    <div class="mt-4">
      Flask provides the essential tools while giving you freedom to choose components
    </div>
  </div>
</div>
</div>

---
transition: slide-up
---

# Why Choose Flask?

<div grid="~ cols-2 gap-2">
<div>

- **Simplicity**: Easy to learn and use
- **Flexibility**: No enforced structure or components
- **Extensibility**: Rich ecosystem of extensions
- **Control**: Developer decides what to include
- **Lightweight**: Minimal core with small footprint
- **Perfect for APIs**: Excellent for building RESTful services

</div>
<div>

```python {all}
# This is a complete Flask application!

from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello, World!"

if __name__ == "__main__":
    app.run(debug=True)
```

<div class="text-center mt-4">
Just a few lines of code to create a web server
</div>

</div>
</div>

---
transition: fade
---

# Flask vs Other Frameworks

<div class="grid grid-cols-3 gap-4">
<div class="bg-gray-800 p-4 rounded">
  <h3 class="text-blue-400">Flask</h3>
  <ul class="text-sm">
    <li>✅ Lightweight</li>
    <li>✅ Minimal dependencies</li>
    <li>✅ Highly flexible</li>
    <li>✅ "Explicit is better than implicit"</li>
    <li>❌ More boilerplate for large apps</li>
  </ul>
</div>

<div class="bg-gray-800 p-4 rounded">
  <h3 class="text-green-400">Django</h3>
  <ul class="text-sm">
    <li>✅ Full-featured</li>
    <li>✅ "Batteries included"</li>
    <li>✅ Admin interface</li>
    <li>✅ Built-in ORM</li>
    <li>❌ Steeper learning curve</li>
    <li>❌ Less flexibility</li>
  </ul>
</div>

<div class="bg-gray-800 p-4 rounded">
  <h3 class="text-purple-400">FastAPI</h3>
  <ul class="text-sm">
    <li>✅ Modern, async-first</li>
    <li>✅ Auto-documentation</li>
    <li>✅ Type annotations</li>
    <li>✅ High performance</li>
    <li>❌ Newer ecosystem</li>
    <li>❌ Requires Python 3.6+</li>
  </ul>
</div>
</div>

<div class="mt-8 text-center">
Choose Flask when you want simplicity, control, and flexibility for small to medium-sized projects
</div>

---
transition: slide-left
---

# Flask Philosophy

<div grid="~ cols-2 gap-2">
<div>

### The "Micro" in Microframework

- Lightweight core with just what you need
- No database abstraction layer
- No form validation
- No user authentication
- You choose what to add and how

### Core Principles

- Simplicity
- Explicitness
- Extensibility
- Freedom

</div>
<div>

<div class="text-center">
  <div class="text-4xl mb-4">
  "Flask is fun!"
  </div>
</div>

```python {all}
# Flask follows Python's idea of
# "There should be one obvious way to do it"

@app.route('/hello/<name>')
def hello(name):
    return f'Hello, {name}!'

# Clear, explicit, and straightforward
```

</div>
</div>

---
layout: center
class: text-center
transition: fade
---

# Part 3: Setup & Installation

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
transition: slide-up
---

# Installing Flask

<div grid="~ cols-2 gap-2">
<div>

### Using pip

```bash
pip install flask
```

### Using virtual environment (recommended)

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install Flask
pip install flask
```

</div>
<div>

### Verifying installation

```python
import flask
print(flask.__version__)
```

### What gets installed with flask?

- Markup Safe
- Werkzeug (WSGI utility)
- Jinja2 (template engine)
- ItsDangerous (secure signing)
- Click (CLI utility)
- Blinker (signals support)


</div>
</div>

---
transition: fade-out
---

# Your First Flask Application

<div grid="~ cols-2 gap-2">
<div>

### Create a file named `app.py`

- Import Flask
- Create an application instance
- Define a route
- Run the application

### Running your app

```bash
python app.py
# or
flask run
```

Visit http://127.0.0.1:5000/ in your browser

</div>
<div>

```python {all|1|3|5-7|9-10|all}
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(debug=True)
```

<div class="text-center mt-4">
A complete Flask application in just 10 lines of code!
</div>

</div>
</div>

---
transition: slide-up
---

# Understanding The First App

<div grid="~ cols-2 gap-2">
<div>

### `from flask import Flask`
- Imports the Flask class

### `app = Flask(__name__)`
- Creates an instance of the Flask class
- `__name__` helps Flask locate resources

### `@app.route('/')`
- Decorator registers a route
- Maps URL '/' to the function

### `app.run(debug=True)`
- Runs the development server
- `debug=True` enables auto-reloading and debugging

</div>
<div>

```python {all}
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(debug=True)
```

<div class="text-center mt-4">
Each line has a specific purpose in creating a web application
</div>

</div>
</div>

---
transition: slide-up
---

# Flask Application Structure

<div grid="~ cols-2 gap-2">
<div>

### Simple Structure
```
my_flask_app/
├── app.py
├── static/
│   ├── css/
│   ├── js/
│   └── images/
└── templates/
    ├── base.html
    └── index.html
```

### For Larger Applications
```
my_flask_app/
├── app/
│   ├── __init__.py
│   ├── routes.py
│   ├── models.py
│   ├── forms.py
│   ├── static/
│   └── templates/
├── venv/
├── config.py
└── run.py
```

</div>
<div>

### Key Components

- **app.py/run.py**: Entry point
- **static/**: Static files (CSS, JS, images)
- **templates/**: Jinja2 templates
- **models.py**: Database models
- **forms.py**: Form definitions
- **routes.py**: View functions
- **config.py**: Configuration

<div class="mt-4">
Flask is flexible with structure - choose what works for your project
</div>

</div>
</div>

---
layout: center
class: text-center
transition: fade
---

# Part 4: Routing & Views

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
transition: slide-up
---

# Basic Routing

<div grid="~ cols-2 gap-2">
<div>

- Routes map URLs to view functions
- Use `@app.route()` decorator
- The function name doesn't matter
- Return value becomes HTTP response
- Can return strings, HTML, JSON, etc.

</div>
<div>

```python {all|1-3|5-7|9-11|all}
@app.route('/')
def home():
    return 'Welcome to the home page!'

@app.route('/about')
def about():
    return 'This is the about page.'

@app.route('/contact')
def contact():
    return 'Contact us at contact@example.com'
```

</div>
</div>

---
transition: slide-left
---

# Dynamic Routes with URL Parameters

<div grid="~ cols-2 gap-2">
<div>

- Capture dynamic parts of URLs
- Use `<variable_name>` syntax
- Default type is string
- Can specify types:
  - `<int:id>`
  - `<float:value>`
  - `<path:subpath>`
- Parameters are passed to the view function

</div>
<div>

```python {all|1-3|5-7|9-13|all}
@app.route('/user/<username>')
def show_user(username):
    return f'User: {username}'


@app.route('/post/<int:post_id>')
def show_post(post_id):
    return f'Post ID: {post_id}'

@app.route('/path/<path:subpath>')
def show_subpath(subpath):
    # Can handle paths like 'foo/bar/baz'
    return f'Subpath: {subpath}'
```

</div>
</div>

---
transition: fade-out
---

# HTTP Methods

<div grid="~ cols-2 gap-2">
<div>

- Routes can specify which HTTP methods they accept
- Default is GET only
- Common methods:
  - GET: Retrieve data
  - POST: Submit data
  - PUT: Update data
  - DELETE: Remove data
- Specify with `methods` parameter
- Access request data with `request` object

</div>
<div>

```python {all|1-2|4-9|all}
from flask import Flask, request, redirect
app = Flask(__name__)

@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        # Process login form data
        return redirect('/dashboard')
    else:  # GET request
        return '''
            <form method="post">
                <input type="text" name="username">
                <input type="password" name="password">
                <input type="submit" value="Log In">
            </form>
        '''
```

</div>
</div>

---
transition: slide-up
---

# Redirects and Errors

<div grid="~ cols-2 gap-2">
<div>

### Redirects
- Use `redirect()` to send user to another URL
- Good for "Post/Redirect/Get" pattern
- Can redirect to URLs or endpoint names

### Error Handling
- Use `abort()` to trigger error responses
- Custom error pages with `errorhandler` decorator
- Common HTTP errors: 404, 403, 500

</div>
<div>

```python {all|1-2|4-6|8-11|13-16|all}
from flask import Flask, redirect, url_for, abort
app = Flask(__name__)

@app.route('/redirect-example')
def redirect_example():
    return redirect(url_for('home'))

@app.route('/private')
def private():
    # If not authenticated
    abort(403)  # Forbidden

@app.errorhandler(404)
def page_not_found(e):
    return "Custom 404 page", 404
```

</div>
</div>

---
transition: slide-left
---

# URL Building with `url_for()`

<div grid="~ cols-2 gap-2">
<div>

- Generates URLs for a given endpoint
- Better than hardcoding URLs
- Handles routing complexities automatically
- Works with blueprint namespaces
- Can include dynamic parameters
- Adapts to application changes

</div>
<div>

```python {all|1-2|4-6|8-10|12-15|all}
from flask import Flask, url_for
app = Flask(__name__)

@app.route('/')
def home():
    return 'Home'

@app.route('/user/<username>')
def user_profile(username):
    return f'Profile: {username}'

@app.route('/navigate')
def navigate():
    home_url = url_for('home')
    john_url = url_for('user_profile', username='john')
    return f'''
        <a href="{home_url}">Home</a>
        <a href="{john_url}">John's Profile</a>
    '''
```

</div>
</div>

---
layout: center
class: text-center
transition: fade
---

# Part 5: Templates & Forms

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
transition: slide-up
---

# Jinja2 Templates

<div grid="~ cols-2 gap-2">
<div>

- Flask uses Jinja2 for templating
- Templates go in `templates/` directory
- Render with `render_template()`
- Pass data as keyword arguments
- Supports variables, filters, control structures
- Enables template inheritance

</div>
<div>

```python {all}
from flask import Flask, render_template
app = Flask(__name__)

@app.route('/hello/<name>')
def hello(name):
    return render_template(
        'hello.html', 
        name=name,
        title='Greeting Page'
    )
```

```html
<!-- templates/hello.html -->
<!DOCTYPE html>
<html>
<head>
    <title>{{ title }}</title>
</head>
<body>
    <h1>Hello, {{ name }}!</h1>
</body>
</html>
```

</div>
</div>

---
transition: fade-out
---

# Template Inheritance

<div grid="~ cols-2 gap-2">
<div>

- Create a base template with common elements
- Define "blocks" that child templates can override
- Child templates "extend" the base template
- Reduces duplication
- Makes consistent layout easy
- Modular and maintainable

</div>
<div>

```html {all}
<!-- templates/base.html -->
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}Default Title{% endblock %}</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
</head>
<body>
    <nav>{% block nav %}{% endblock %}</nav>
    <div class="content">
        {% block content %}{% endblock %}
    </div>
    <footer>© 2025 Flask App</footer>
</body>
</html>
```

```html {all}
<!-- templates/page.html -->
{% extends 'base.html' %}

{% block title %}My Page{% endblock %}

{% block content %}
    <h1>Welcome to my page!</h1>
    <p>This is the content of my page.</p>
{% endblock %}
```

</div>
</div>

---
transition: slide-up
---

# Jinja2 Template Syntax

<div grid="~ cols-2 gap-2">
<div>

### Variables
- `{{ variable }}`
- Supports attributes and methods
- Auto-escapes HTML by default

### Control Structures
- `{% if condition %}...{% endif %}`
- `{% for item in items %}...{% endfor %}`
- `{% block name %}...{% endblock %}`

### Filters
- `{{ name|capitalize }}`
- `{{ list|join(', ') }}`
- `{{ date|strftime('%Y-%m-%d') }}`

</div>
<div>

```html {all}
<h1>User Profile: {{ user.username }}</h1>

{% if user.is_admin %}
    <span class="badge">Admin</span>
{% endif %}

<h2>Posts:</h2>
<ul>
{% for post in user.posts %}
    <li>
        {{ post.title }}
        <small>{{ post.date|strftime('%b %d, %Y') }}</small>
    </li>
{% else %}
    <li>No posts found.</li>
{% endfor %}
</ul>

<p>Bio: {{ user.bio|default('No bio provided')|safe }}</p>
```

</div>
</div>

---
transition: slide-left
---

# Form Handling

<div grid="~ cols-2 gap-2">
<div>

### Basic Form Processing
1. Display form (GET request)
2. Process submission (POST request)
3. Validate data
4. Process data or show errors

### With Flask
- Use `request.form` to access form data
- `request.method` to check HTTP method
- Use redirection after successful POST

### Flask-WTF (Extension)
- Form classes with validation
- CSRF protection
- Field rendering

</div>
<div>

```python {all}
from flask import Flask, request, render_template, redirect
app = Flask(__name__)

@app.route('/contact', methods=['GET', 'POST'])
def contact():
    errors = []
    
    if request.method == 'POST':
        email = request.form.get('email', '')
        message = request.form.get('message', '')
        
        if not email:
            errors.append('Email is required')
        if not message:
            errors.append('Message is required')
            
        if not errors:
            # Process form data (e.g., send email)
            return redirect('/thank-you')
    
    return render_template(
        'contact.html', 
        errors=errors
    )
```

</div>
</div>

---
transition: fade-out
---

# Static Files

<div grid="~ cols-2 gap-2">
<div>

- CSS, JavaScript, images, etc.
- Store in `static/` directory
- Access with `url_for('static', filename='...')`
- Automatically served by Flask
- Can organize into subdirectories
- Caching handled by the browser

</div>
<div>

```html {all}
<!DOCTYPE html>
<html>
<head>
    <title>My Flask App</title>
    <!-- CSS -->
    <link rel="stylesheet" href="{{ url_for('static', filename='css/style.css') }}">
</head>
<body>
    <h1>Welcome to my app</h1>
    
    <!-- Image -->
    <img src="{{ url_for('static', filename='images/logo.png') }}" alt="Logo">
    
    <!-- JavaScript -->
    <script src="{{ url_for('static', filename='js/main.js') }}"></script>
</body>
</html>
```

<div class="text-center mt-4">
Using url_for ensures the correct URLs even if the app is mounted in a subdirectory
</div>

</div>
</div>

---
layout: center
class: text-center
transition: fade
---

# Part 6: Deployment

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
transition: slide-up
---

# Production Considerations

<div grid="~ cols-2 gap-2">
<div>

### Flask's Built-in Server
- Not suitable for production
- Single-threaded
- Not designed for security or performance

### Production Requirements
- WSGI server (Gunicorn, uWSGI)
- Reverse proxy (Nginx, Apache)
- Process manager
- Environment variables
- Secret management
- Database connection pooling

</div>
<div>

```bash {all}
# Don't do this in production!
$ flask run

# Use a proper WSGI server
$ pip install gunicorn
$ gunicorn -w 4 -b 0.0.0.0:8000 app:app
```

<div class="mt-4 bg-yellow-900 p-4 rounded">
<div class="text-yellow-400 font-bold">⚠️ Warning</div>
<div class="text-sm mt-1">
Never run Flask's development server in production. It's not designed for security, performance, or reliability.
</div>
</div>

</div>
</div>

---
transition: slide-left
---

# Deployment Options

<div grid="~ cols-2 gap-2">
<div>

### Self-Hosted
- VPS (Digital Ocean, AWS EC2, Linode)
- Bare metal server
- Docker containers

### Platform as a Service (PaaS)
- Heroku
- AWS Elastic Beanstalk
- Google App Engine
- Azure App Service
- Railway
- Render
- Fly.io

### Serverless
- AWS Lambda, GCP etc

</div>
<div>

```bash {all}
# Example: Simple deployment with Gunicorn + Nginx

# Install requirements
pip install gunicorn

# Create a systemd service
sudo nano /etc/systemd/system/flask-app.service

# Start the service
sudo systemctl start flask-app
sudo systemctl enable flask-app

# Configure Nginx as reverse proxy
sudo nano /etc/nginx/sites-available/flask-app
sudo ln -s /etc/nginx/sites-available/flask-app /etc/nginx/sites-enabled
sudo systemctl restart nginx
```

</div>
</div>

---
transition: fade-out
---

# Flask Application Structure for Production

<div grid="~ cols-2 gap-2">
<div>

### Project Structure
```
my_flask_app/
├── app/
│   ├── __init__.py     # App factory
│   ├── models/         # Database models
│   ├── views/          # Blueprint routes
│   ├── templates/      # Jinja templates
│   └── static/         # Static files
├── migrations/         # Database migrations
├── tests/              # Test suite
├── venv/               # Virtual environment
├── config.py           # Configuration
├── wsgi.py             # WSGI entry point
├── requirements.txt    # Dependencies
└── .env                # Environment variables
```

</div>
<div>

### App Factory Pattern

```python {all}
# app/__init__.py
from flask import Flask

def create_app(config_name='default'):
    app = Flask(__name__)
    
    # Load configuration
    app.config.from_object(f'config.{config_name}')
    
    # Initialize extensions
    from app.extensions import db
    db.init_app(app)
    
    # Register blueprints
    from app.views.main import main_bp
    app.register_blueprint(main_bp)
    
    return app
```

```python {all}
# wsgi.py
from app import create_app
app = create_app('production')
```
</div>
</div>

---
---
---

# Environment Variables & Configuration (continued)

<div grid="~ cols-2 gap-2">
<div>

### Environment Variables
- Keep sensitive data out of code
- Different configs for different environments
- Use python-dotenv to load from .env file
- Critical for security

### Configuration Classes
- Base configuration class
- Environment-specific subclasses
- Load config based on environment
- Makes deployment more flexible

</div>
<div>

```python {all}
# config.py
import os
from dotenv import load_dotenv

load_dotenv()  # Load variables from .env file

class Config:
    SECRET_KEY = os.environ.get('SECRET_KEY') or 'hard-to-guess-string'
    SQLALCHEMY_TRACK_MODIFICATIONS = False

class DevelopmentConfig(Config):
    DEBUG = True
    SQLALCHEMY_DATABASE_URI = os.environ.get('DEV_DATABASE_URL')

class ProductionConfig(Config):
    SQLALCHEMY_DATABASE_URI = os.environ.get('DATABASE_URL')

config = {
    'development': DevelopmentConfig,
    'production': ProductionConfig,
    'default': DevelopmentConfig
}
```

</div>
</div>

---
transition: slide-left
---

# Security Best Practices

<div grid="~ cols-2 gap-2">
<div>

### Essential Security Measures
- Use HTTPS (SSL/TLS)
- Set secure cookies
- Store passwords with strong hashing (bcrypt)
- Protect against XSS attacks
- Implement CSRF protection
- Validate all input data
- Use secure HTTP headers
- Keep dependencies updated

### Extensions for Security
- Flask-Security
- Flask-Talisman
- Flask-SeaSurf
- Flask-WTF (CSRF protection)

</div>
<div>

```python {all}
# Setting security headers
from flask import Flask
from flask_talisman import Talisman

app = Flask(__name__)
talisman = Talisman(
    app,
    content_security_policy={
        'default-src': "'self'",
        'script-src': "'self'",
        'style-src': "'self'",
    },
    force_https=True
)

# Secure form with CSRF protection
from flask_wtf import FlaskForm, CSRFProtect
csrf = CSRFProtect(app)
# Setting secure cookie
@app.route('/set_cookie')
def set_cookie():
    resp = make_response(redirect('/'))
    resp.set_cookie('user_id', '123', secure=True, httponly=True, samesite='Lax')
    return resp
```

</div>
</div>

---
transition: fade-out
---

# Monitoring & Logging

<div grid="~ cols-2 gap-2">
<div>

### Logging in Flask
- Flask uses Python's logging module
- Different log levels (DEBUG, INFO, etc.)
- Can log to files, syslog, etc.
- Configure logging based on environment

### Monitoring Options
- Application Performance Monitoring (APM)
  - New Relic
  - Datadog
  - Sentry
- Health checks
- Metrics collection
- Error tracking
- Performance monitoring

</div>
<div>

```python {all}
# Setting up logging
import logging
from logging.handlers import RotatingFileHandler
import os

def configure_logging(app):
    if not os.path.exists('logs'):
        os.mkdir('logs')
        
    file_handler = RotatingFileHandler(
        'logs/flask_app.log', 
        maxBytes=10240, 
        backupCount=10
    )
    formatter = logging.Formatter(
        '%(asctime)s %(levelname)s: %(message)s '
        '[in %(pathname)s:%(lineno)d]'
    )
    file_handler.setFormatter(formatter)
    file_handler.setLevel(logging.INFO)
    
    app.logger.addHandler(file_handler)
    app.logger.setLevel(logging.INFO)
    app.logger.info('Flask application startup')
```

</div>
</div>

---
transition: slide-up
---

# Scaling Flask Applications

<div grid="~ cols-2 gap-2">
<div>

### Horizontal Scaling
- Multiple application instances
- Load balancer
- Shared session store (Redis)
- Stateless application design

### Vertical Scaling
- More CPU/RAM
- Better hardware
- Limited scaling potential

### Application Optimizations
- Database query optimization
- Caching (Flask-Caching)
- Asynchronous tasks (Celery)
- CDN for static assets

</div>
<div>

```python {all}
# Using Redis for session storage
from flask import Flask
from flask_session import Session
import redis

app = Flask(__name__)
app.config['SESSION_TYPE'] = 'redis'
app.config['SESSION_REDIS'] = redis.from_url('redis://localhost:6379')
Session(app)

# Setting up caching
from flask_caching import Cache

cache = Cache(app, config={
    'CACHE_TYPE': 'redis',
    'CACHE_REDIS_URL': 'redis://localhost:6379/0',
})

@app.route('/expensive-operation')
@cache.cached(timeout=300)  # Cache for 5 minutes
def expensive_operation():
    # Perform expensive calculation
    return result
```

</div>
</div>

---
layout: center
class: text-center
transition: fade
---

# Recap & Resources

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
transition: slide-up
---

# What We've Covered

<div class="grid grid-cols-3 gap-4">
<div class="bg-gray-800 p-4 rounded">
  <h3 class="text-blue-400">Python Fundamentals</h3>
  <ul class="text-sm">
    <li>Function Decorators</li>
    <li>Higher-Order Functions</li>
  </ul>
</div>

<div class="bg-gray-800 p-4 rounded">
  <h3 class="text-blue-400">Flask Basics</h3>
  <ul class="text-sm">
    <li>What is Flask?</li>
    <li>Installation & Setup</li>
    <li>First Application</li>
  </ul>
</div>

<div class="bg-gray-800 p-4 rounded">
  <h3 class="text-blue-400">Routing & Views</h3>
  <ul class="text-sm">
    <li>Basic Routes</li>
    <li>Dynamic Routes</li>
    <li>HTTP Methods</li>
    <li>URL Building</li>
  </ul>
</div>

<div class="bg-gray-800 p-4 rounded">
  <h3 class="text-blue-400">Templates</h3>
  <ul class="text-sm">
    <li>Jinja2 Basics</li>
    <li>Template Inheritance</li>
    <li>Template Syntax</li>
  </ul>
</div>

<div class="bg-gray-800 p-4 rounded">
  <h3 class="text-blue-400">Forms & Static Files</h3>
  <ul class="text-sm">
    <li>Form Handling</li>
    <li>Form Validation</li>
    <li>Static File Management</li>
  </ul>
</div>

<div class="bg-gray-800 p-4 rounded">
  <h3 class="text-blue-400">Deployment</h3>
  <ul class="text-sm">
    <li>Production Considerations</li>
    <li>Deployment Options</li>
    <li>Security Best Practices</li>
    <li>Monitoring & Scaling</li>
  </ul>
</div>
</div>

---
transition: slide-left
---

# Resources for Further Learning

<div grid="~ cols-2 gap-2">
<div>

### Official Documentation
- [Flask Documentation](https://flask.palletsprojects.com/)
- [Jinja2 Template Documentation](https://jinja.palletsprojects.com/)
- [Werkzeug Documentation](https://werkzeug.palletsprojects.com/)

### Books
- "Flask Web Development" by Miguel Grinberg
- "Explore Flask" by Robert Picard
- "Flask Framework Cookbook" by Shalabh Aggarwal

### Tutorials
- Miguel Grinberg's "Flask Mega-Tutorial"
- Real Python Flask Tutorials
- Corey Schafer's Flask YouTube Series

</div>
<div>

### Community Resources
- Flask Discourse Forum
- Flask SubReddit
- Stack Overflow Flask Tag

### Extensions to Explore
- Flask-SQLAlchemy: Database ORM
- Flask-Migrate: Database migrations
- Flask-WTF: Forms & validation
- Flask-Login: User authentication
- Flask-RESTful: API development
- Flask-Admin: Admin interface
- Flask-Mail: Email sending
- Flask-Caching: Response caching

</div>
</div>

---
transition: fade
layout: center
class: text-center
---

# Thank You!

<div class="text-xl">
Start building with Flask today!
</div>

<div class="text-sm opacity-50 mt-8">
From Python decorators to production deployment - you now have the knowledge to build and deploy Flask applications.
</div>

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>
