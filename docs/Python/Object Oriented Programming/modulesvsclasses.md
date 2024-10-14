# Modules vs Classes

A module is a file that contains Python code (functions, variables, classes) 
that can be imported and reused across different programs.

Modules are used to organize related functions, variables, and classes into a single namespace, 
making your code more modular and reusable.

Classes, on the other hand, are used to create objects. 
Classes allow you to define the structure (attributes) and behavior (methods) of objects. 

**While a module organizes code at the file level, a class organizes it at a more granular, 
object-oriented level.**

Dictionaries store key-value pairs, whereas modules contain Python objects 
(functions, classes, etc.) that can be accessed using dot notation.

### Modules are like “Dictionaries”
When working on Modules, note the following points:

- A Python module is a package to encapsulate reusable code.
- Modules reside in a folder with a __init__.py file on it.
- Modules contain functions and classes.
- Modules are imported using the import keyword.

Recall that a dictionary is a key-value pair. That means if you have a dictionary with a
key EmployeID and you want to retrieve it, then you will have to use the following lines
of code:
```python
# employee.py
employee_name = "John"
employee_id = 12345

def get_employee_id():
    return employee_id
```
You can import this module and use it like this:

```python
import employee

print(employee.employee_name)  # Access a variable from the module
print(employee.get_employee_id())  # Call a function from the module

```
an equivalent class for the employee module would look like this:

```python
class Employee:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def get_employee_id(self):
        return "Employee ID is: 12345"

# Instantiate an Employee object
employee_obj = Employee("John", 30)

# Access the properties and methods
print(employee_obj.name)  # Access the name attribute
print(employee_obj.get_employee_id())  # Call the method

```

Key Differences between Modules and Classes:
Scope:

- Modules: Contain functions, variables, and classes. They are global and reusable throughout the entire program.
- Classes: Define objects with attributes and methods. They are meant for object-oriented programming and encapsulation.

Reusability:

- Modules: Reused by importing them into different files. You can use their functions and variables directly.
- Classes: Need to be instantiated into objects. You can reuse the class by creating multiple instances (objects).

### Classes are like Modules

Module is a specialized dictionary that can store Python code so you can get to it with the
‘.’ Operator. A class is a way to take a grouping of functions and data and place them
inside a container so you can access them with the ‘.‘operator.

Note: Classes are preferred over modules because you can reuse them as they are and
without much interference. While with modules, you have only one with the entire
program.

A class is like a blueprint for creating objects. When you create (instantiate) an object from a class, you get an independent instance of that class, with its own data.

```python
class Employee:
    def __init__(self, name, age):
        self.name = name
        self.age = age

# Creating two independent objects (instances) from the class
employee1 = Employee("John", 30)
employee2 = Employee("Jane", 25)

# Each object has its own data
print(employee1.name)  # Output: John
print(employee2.name)  # Output: Jane

```

Variable Scope:

Modules have global scope once imported, whereas classes have instance-specific attributes 
(defined with self), making them more suited for encapsulation.

Final Comments and Recommendations:

-  Modules: Use them when you need to group related functions, variables, or classes in a single file for reuse across your project.
-  Classes: Use them for object-oriented design when you need to encapsulate data and functionality that should be grouped together in objects.

Extended Example with Both Modules and Classes:

```python
# employee.py (Module)
class Employee:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def get_employee_info(self):
        return f"{self.name}, {self.age}"

# Utility function outside the class
def greet_employee(employee):
    return f"Welcome {employee.name}!"

```
Usage:

```python
# main.py
import employee  # Importing the module

# Create an instance of Employee class
john = employee.Employee("John", 30)

# Access class method
print(john.get_employee_info())  # Output: John, 30

# Use module-level function
print(employee.greet_employee(john))  # Output: Welcome John!
```

This demonstrates how a module can contain both class definitions and standalone functions.

