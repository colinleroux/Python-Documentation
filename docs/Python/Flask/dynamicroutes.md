# Dynamic Routes in Flask

Flask allows for the creation of **dynamic routes**, 
which enable URLs to change based on values passed into them, 
called **path variables**. 

Path variables are placeholders in the URL that are identified 
inside diamond operators `<>`, like `<variable>`. 

These allow a single route to handle multiple variations of a URL,
depending on the values passed in.

#### Declaring Path Variables

- Path variables are inserted in the URL using the `<type:variable>` pattern.
- **Types** can be specified to enforce data types for the variables:
  - `string`: (default) Takes any valid characters except slashes.
  - `int`: Only accepts integers.
  - `float`: Accepts floating-point numbers.
  - `uuid`: Accepts UUIDs (unique identifiers).
  - `path`: Allows slashes in the variable.

For example, consider the route:

```python
@app.route('/exam/passers/list/<float:rate>/<uuid:docId>')
def report_exam_passers(rating: float, docId: uuid4 = None):
    exams = list_passing_scores(rating)
    return render_template('exam/list_exam_passers.html', exams=exams, docId=docId)
```

In this route:
- `<float:rate>` ensures the `rate` is a float.
- `<uuid:docId>` expects a UUID.
- In the function, `rating` and `docId` hold the values passed in the URL.

#### Custom Path Variables

In some cases, Flask’s built-in types may not suffice (e.g., `date`, `list`). Using unsupported types directly will result in an error (HTTP 500). To handle such cases, **custom converters** can be created using the `BaseConverter` class from Werkzeug.

For example, if you need to handle a `date` type in the URL, you can create a custom converter like this:

```python
from werkzeug.routing import BaseConverter
from datetime import datetime

class DateConverter(BaseConverter):
    def to_python(self, value):
        return datetime.strptime(value, "%Y-%m-%d")
```

This converter uses the `to_python()` method to transform the string value in the URL (e.g., "2024-10-22") into a `datetime` object.

#### Registering the Custom Converter

To use the custom converter, you must register it with Flask:

```python
app = Flask(__name__)
app.url_map.converters['date'] = DateConverter
```

Once registered, you can use it in routes:

```python
@app.route('/certificate/<string:name>/<string:course>/<date:accomplished_date>')
def show_certification(name: str, course: str, accomplished_date: date):
    return f"<h1>Certificate of Accomplishment</h1><p>{name} completed {course} on {accomplished_date}</p>", 200
```

Here, `<date:accomplished_date>` uses the `DateConverter`, which converts the string in the URL into a Python `date`.

### Summary of Key Points
1. **Dynamic URLs**: Created using path variables in the format `<type:variable>`, allowing for flexible URLs.
2. **Data Types**: Flask supports various built-in data types like `string`, `int`, `float`, `uuid`, and `path`.
3. **Custom Converters**: For unsupported types (e.g., `date`), Flask can use custom converters via Werkzeug’s `BaseConverter`.
4. **Usage**: Register custom converters with the `app.url_map.converters` dictionary and use them in your routes.
