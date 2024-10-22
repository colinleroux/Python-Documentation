# Flask - Templates

In Flask, templating is the process of dynamically generating HTML content by embedding Python code
within HTML files.

Flask uses Jinja2 as its templating engine, allowing you to create templates that can render variables, 
use control structures (like loops and conditionals), 
and even extend layouts to reuse common elements across different pages.

Key concepts in Flask templating:
1. **Templates**: HTML files with placeholders for dynamic content, typically stored in a `templates/` folder.

2. **Rendering templates**: Using the `render_template()` function, Flask processes a template and replaces placeholders with actual data.
  
      ```python

      from flask import render_template
      
      @app.route('/')
      def index():
          return render_template('index.html', title='Home Page', user='Alice')
      ``` 

    In this example, Flask looks for an `index.html` template and passes the `title` and `user` variables to it.
   
3. **Variables**: Inside a template, you can use variables enclosed in double curly braces to insert data.
   ```html
   <h1>Welcome, {{ user }}!</h1>
   ```

4. **Control structures**: You can use Jinja2’s control structures like `for` loops or `if` statements to dynamically control the content.
   ```html
   {% if user %}
   <h1>Hello, {{ user }}!</h1>
   {% else %}
   <h1>Hello, stranger!</h1>
   {% endif %}
   ```

5. **Template inheritance**: You can create a base template that contains common layout (like headers and footers) and have other templates extend it.
   ```html
   <!-- base.html -->
   <html>
     <head><title>{% block title %}My App{% endblock %}</title></head>
     <body>
       <header>Header</header>
       <div>{% block content %}{% endblock %}</div>
       <footer>Footer</footer>
     </body>
   </html>
   ```
   ```html
   <!-- index.html -->
   {% extends 'base.html' %}
   {% block title %}Home{% endblock %}
   {% block content %}
   <h1>Welcome to the homepage!</h1>
   {% endblock %}
   ```

Templating in Flask is a powerful way to separate the logic of your application from the presentation layer, making your app more maintainable and scalable.
