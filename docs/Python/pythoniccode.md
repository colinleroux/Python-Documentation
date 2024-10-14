# Pythonic Code 

## Comments:

   - Keep lines within 72–80 characters.
   - Use complete sentences in camel-case.
   - Ensure comments are updated when code changes.

## Block Comments:

   - Used for explaining sections of code or functionality.
   - Follow PEP8: Match indent level with the code, begin with # + space.
   - Use blank comment lines (#) between paragraphs.

```python title="Example of block comment"
# This function calculates the area of a rectangle.
# It takes width and height as inputs and returns the computed area.
def calculate_area(width, height):
    return width * height

```
## Inline Comments:

   - Place them at the end of the line they refer to.
   - Use at least two spaces between the code and the comment.
   - Avoid over-explaining obvious logic.

```python title="Example of inline comment"
def is_even(number):
    return number % 2 == 0  # Check if the number is divisible by 2

```
## Docstrings:

   - Used to explain classes, modules, functions, or methods.
   - Wrapped in triple quotes (""" or ''').
   - Docstrings provide explanation, not justification, and are crucial for documenting expected input types, parameters, and return types.
   - Unlike comments, docstrings are essential in Python for dynamic typing and better code understanding.

```python title="Example of Docstrings"
def greet(name):
    """
    Greets a person by name.
    
    Args:
        name (str): The name of the person to greet.

    Returns:
        str: A greeting message.
    """
    return f"Hello, {name}!"

```
## Type Annotations:

Annotations in Python, introduced with PEP 3107, allow adding type hints to function arguments,
return values, and variables. 

They help clarify what types of data are expected, without enforcing them, 
as Python remains dynamically typed.

Key Points:

   - Type hints suggest expected data types (e.g., float, int) to users, but Python does not enforce
these types.
   - Annotations can be accessed through a special attribute, __annotations__, which returns a 
dictionary of the annotations used in the function.
   - Type Hinting helps in static analysis tools like MyPy, which check data type compatibility.

   - The typing module in Python 3.5+ allows specifying more complex types, like lists of specific 
data types (e.g., List[float]).

   - Starting from Python 3.6, variables can also be annotated, not just function parameters.

```python

class Rectangle:
    length: float   # Type annotation for a variable
    width: float
    area: float

    def __init__(self, length: float, width: float):
        self.length = length
        self.width = width
        self.area = 0

    def compute_area(self) -> float:   # Type annotation for return type
        """Compute area of the rectangle."""
        return self.length * self.width

# Accessing annotations
print(Rectangle.__annotations__)
# Output: {'length': <class 'float'>, 'width': <class 'float'>, 'area': <class 'float'>}
```

In this example, length and width are expected to be floats, and the return type of compute_area is 
also a float.

Annotations can be accessed using __annotations__, and they help document expected types in code.


PEP 484 emphasizes that type hints are optional and Python will remain dynamically typed, 
meaning no mandatory type enforcement will occur.

## Code layout in Python

### Blank Lines in Python:

In Python, spaces and blank lines are important for readability and code aesthetics. 
Proper use of vertical whitespace helps improve clarity and reduces frustration when reading code.

**Key Guidelines:**

  - Classes and top-level functions: Use two blank lines around them to visually isolate and 
separate their functionality.
```python
class ClassOne:
    pass

class ClassTwo:
    pass

def my_top_level_function():
    return None
```

- Methods in a class: Use a single blank line between methods to show they are interrelated yet distinct.
```python
class MyClass:
    def first_method(self):
        return None
    
    def second_method(self):
        return None
```

- Steps within a function: Separate different sections with a blank line if they represent distinct 
steps or operations.
```python

 def variance_computation(list_of_numbers):
        list_sum = sum(list_of_numbers)
        average = list_sum / len(list_of_numbers)

        sum_of_squares = sum(num**2 for num in list_of_numbers)
        average_of_squares = sum_of_squares / len(list_of_numbers)

        return average_of_squares - average**2
```

**Benefits:**

- Improved readability: Blank lines help break up the code logically, making it easier to understand.

- Cleaner code: It prevents clutter and unnecessary scrolling, allowing developers to focus 
on important sections.

## Maximum Line Length and Line Breaking in Python:

PEP 8 recommends limiting a line of code to 79 characters to enhance readability 
and avoid line wrapping, especially when editing multiple files side by side.

**Handling Long Lines:**
Within parentheses, braces, or brackets: The interpreter assumes the code is in continuation.
```python
def sample_method(first_arg, second_arg, third_arg):
    return first_arg
```

Using backslashes: Break long lines with a backslash (\) for continuation outside of these constructs.
```python
from secretPackage import library1, \
                          library2, \
                          library3
```
Implied continuation: Alternatively, use implied continuation by enclosing items in parentheses, brackets, or braces.
```python


from secretPackage import (
    library1,
    library2,
    library3
)
```
Breaking before operators: For better readability, break lines before binary operators.
```python
# Preferred
total = (value_one
         + value_two
         - value_three)
```

Avoid breaking after operators, as it makes code harder to read.
```python

    # Less readable
    total = (value_one + 
             value_two - 
             value_three)

```
**Benefits:**
*    Clarity: Breaking before operators improves readability.
*    Better organization: Helps in editing code and reduces errors, especially when dealing with complex expressions.
