# Routing in Flask

Here's how **assigning URLs externally** using `add_url_rule()` works in Flask:

### Usual Method: `@app.route()` Decorator
- Normally, when defining a route (a URL that connects to a specific function), we use the `@app.route()` decorator above a function. For example:

    ```python
    @app.route('/hello')
    def say_hello():
        return "Hello, World!"
    ```

- Here, the URL `/hello` is directly tied to the `say_hello` function using the decorator.

### Alternative Method: `add_url_rule()`
- **`add_url_rule()`** is another way to register a URL to a function without using decorators. It's a more flexible approach.
  
- With `add_url_rule()`, you manually link a URL to a function. This can be useful if you prefer to keep your URL rules separate from your function definitions.

### How it Works:
1. **URL Pattern**: You specify the URL pattern (with optional path variables).
2. **Function Name**: You give the URL rule a name, often the same as the function.
3. **View Function**: You pass the function that will handle requests to that URL.

Here’s an example using `add_url_rule()`:

```python
app = Flask(__name__)

# Define a function to handle a request to this URL
def show_honor_dismissal(counselor: str, effective_date: str, patient: str):
    letter = f"""
    <html>
    <body>
        <h1>Termination of Consultation</h1>
        <p>From: {counselor}</p>
        <p>Date: {effective_date}</p>
        <p>To: {patient}</p>
        <p>Subject: Termination of consultation</p>
        <p>Dear {patient},</p>
        <p>Yours Sincerely,</p>
        <p>{counselor}</p>
    </body>
    </html>
    """
    return letter, 200

# Bind the URL to the function externally using add_url_rule()
app.add_url_rule(
    '/certificate/terminate/<string:counselor>/<string:effective_date>/<string:patient>',
    'show_honor_dismissal',    # Name of the rule
    show_honor_dismissal       # The actual function to call
)
```

### Key Points:
- **URL Pattern**: The first argument is the URL (`/certificate/terminate/...`) where `<string:counselor>`, `<string:effective_date>`, and `<string:patient>` are variables that will be passed to the function.
  
- **Rule Name**: The second argument (`'show_honor_dismissal'`) is a name for the route. This is usually the same as the function name but can be anything.

- **View Function**: The third argument (`show_honor_dismissal`) is the function that handles the request when someone visits that URL.

### Why Use `add_url_rule()`?
- **Separation of Concerns**: It lets you keep your URL mappings and function definitions separate. This can make your code cleaner if you're dealing with many routes.
  
- **Dynamic URLs**: You can define more dynamic or flexible routes in one place instead of using multiple decorators.

### Use Case:
- This method is not only for simple function-based views but also **class-based views**, where you might want more control over URL handling.

In summary, `add_url_rule()` is just a different way of linking URLs to functions, offering more flexibility than decorators when managing routes, especially in more complex or structured projects.
