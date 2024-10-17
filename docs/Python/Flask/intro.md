# Flask - Initial setup
```python
$ mkdir microblog
$ cd microblog
$ python3 -m venv venv
$ source venv/bin/activate
```

**What happens when you run /venv/bin/activate:**

- This command temporarily modifies your shell's environment variables, particularly the PATH variable, so that the shell prioritizes the virtual environment's bin directory over the system-wide directories.
- This ensures that the Python interpreter and any packages you install come from this virtual environment, not from the system-wide Python installation.
- You'll notice the shell prompt changes to indicate the virtual environment is active, typically appearing as (venv).

**Deactivating the virtual environment:**

To exit the virtual environment and return to the system-wide Python environment, simply run:
`deactivate`

**Install flask**

To install Flask within the virtual environment, use:
`(venv) $ pip install flask`
**Setting Up the Application Package**

Let's create a package called app, which will host the Flask application:

`(venv) $ mkdir app`

The `__init__.py`  file in the app package will initialize the Flask application:

```python title="app/__init__.py -  Flask application instance"
from flask import Flask
app = Flask(__name__)
from app import routes
```
Now, let's define the routes for the application:
```python title="app/routes.py - the Home page route"
from app import app

@app.route('/')
@app.route('/index')
def index():
    return "Hello, World!"
```
**Understanding the @app.route Decorators**

The @app.route lines above the index function are decorators—a powerful feature of the Python language. 

Decorators allow you to modify or extend the behavior of functions or methods. 

In Flask, they are commonly used to register a function as a callback for a specific URL.

- The @app.route('/') decorator associates the root URL (/) with the index function.
- The second @app.route('/index') decorator associates the /index URL with the same function.

This means that when a browser requests either / or /index, Flask invokes the index function and 
sends the return value ("Hello, World!") as a response.

**Main Application Module**

Next, create the main module that will run the application:

```python title="microblog.py: Main application module"
from app import app
```
```python title="the project structure so far:"

microblog/
  venv/
  app/
    __init__.py
    routes.py
  microblog.py
```
**Running the Application**

Flask needs to know how to import the application, which is specified by 
setting the FLASK_APP environment variable:

`(venv) $ export FLASK_APP=microblog.py`

`(venv) $ flask run --port 5001`

**Persistent Environment Variables with .flaskenv**

Since environment variables aren't preserved across terminal sessions, setting FLASK_APP each time can be tedious. 
To automate this, install the python-dotenv package:

`(venv) $ pip install python-dotenv`

Create a .flaskenv file in the project's root directory to store the environment variable:

`# .flaskenv: Environment variables for Flask command
FLASK_APP=microblog.py
`

Now, when you run flask run, Flask will automatically read the .flaskenv file and apply the environment variables, simplifying your workflow.

