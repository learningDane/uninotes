#uni 
Flask is a lightweight web framework for Python that allows you to build web applications quickly and with minimal code.

Created by Armin Ronacher in 2010, Flask is considered a "micro" framework because it doesn't require particular tools or libraries, giving developers flexibility in their implementation choices.

Key features:
- Minimal core with extensible architecture
- Built-in development server and debugger
- RESTful request dispatching
- Support for secure cookies (client-side sessions)
- Template engine (Jinja2)
- Unit testing support

```bash
pip install Flask
```

```python
from flask import Flask

app = Flask(__name__) # the __name__ parameter determines the root path of the pplication, which is used to find resources like templates and static files

# define a route
@app.route('/')
def hello_world():
	return 'Hello,World!'
	
# run the application
if __name__ == '__main__':
	app.run(debug=True)
```
# Routing
Routing in Flask maps URLs to specific functions that handle requests:
```python
@app.route('/')
def home():
	return 'Welcome to the homepage!'

@app.route('/about')
def about():
	return 'About this website'

# Dynamic routing with parameters
@app.route('/user/<username>')
def show_user_profile(username):
	return f'User: {username}'

# Specifying the parameter type
@app.route('/post/<int:post_id>')
def show_post(post_id):
	return f'Post: {post_id}'
```
# HTTP methods
Flask routes can handle different HTTP methods:
- GET: retrieve data (default)
- POST: submit data
- PUT: updated existing data
- DELETE: remove data
- more
```python
@app.route('/login', methods=['GET', 'POST'])
def login():
	if request.method == 'POST':
		# Handle form submission
		username = request.form.get('username')
		password = request.form.get('password')
		# Process login logic
		return f'Logged in as {username}'
	else:
		# Display login form
		return render_template('login.html')
```
# Template
Flask uses [[Jinja2]] as its template engine:
```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/hello/<name>')
def hello(name):
	return render_template('hello.html', name=name)

<!DOCTYPE html>
<html>
<head>
	<title>Hello Page</title>
</head>
<body>
	<h1>Hello, {{ name }}!</h1>
	{% if name == 'admin' %}
		<p>Welcome, administrator!</p>
	{% else %}
		<p>Welcome, user!</p>
	{% endif %}
</body>
</html>
```