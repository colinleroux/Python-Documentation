# Python Classes: A Summary

In Python, **classes** are used to create objects that encapsulate **state** (data/attributes) and **behaviors** (methods/functions). Objects created from a class are called **instances**.

**Naming**  
    
    classes - The class name must follow standard Python variable naming rules 
    (it must start with a letter or underscore, and can
    only be comprised of letters, underscores, or numbers). 
    
    In addition, the Python style guide (search the web for PEP 8)
    recommends that classes should be named using what PEP 8
    calls CapWords notation (start with a capital letter; any subsequent
    words should also start with a capital).

## 1. Class Behavior and State

- **State** is represented by attributes (variables) that belong to the class.

- **Behavior** is represented by methods (functions) that belong to the class.

 Example:
```python
class Dog:
    # Initializing state with the constructor (__init__)
    def __init__(self, name, breed):
        self.name = name  # instance attribute
        self.breed = breed  # instance attribute
    
    # Behavior method
    def bark(self):
        return f"{self.name} says woof!"
```

- State: The dog's name and breed are attributes.

- Behavior: The bark method is a behavior.

## 2. Class Methods and Attributes

  - Attributes are variables that belong to the class or the instance of a class.
  -  Methods are functions that define the behaviors of the class.
  -  Methods can take self as a parameter to access or modify instance attributes.

Example:
```python
class Car:
    # Class attribute (shared by all instances)
    wheels = 4

    def __init__(self, make, model):
        # Instance attributes (unique to each instance)
        self.make = make
        self.model = model

    # Instance method
    def description(self):
        return f"{self.make} {self.model} has {self.wheels} wheels."
```

  -  Class Attribute: wheels is shared by all Car instances.
  -  Instance Attributes: make and model are unique to each car.
  -  Instance Method: description returns a formatted string.
  - A method is a function you invoke on an instance of the class or the class itself.
  - A method that is invoked on an instance is sometimes called an instance method.
  - You can also invoke a method directly on a class, in which case it is called a class method or a static method.
  - Attributes that take data values on a per-instance basis are frequently referred to as instance variables.
  - Attributes that take on values on a per-class basis are called class attributes or static attributes or class variables.

## 3. Creating and Instantiating Classes

You can create (define) a class and then instantiate (create objects from) the class.
Example:

```python
# Defining the class
class Cat:
    def __init__(self, name, color):
        self.name = name
        self.color = color

    def meow(self):
        return f"{self.name} says meow!"
    
# Instantiating (creating objects)
cat1 = Cat("Whiskers", "white")
cat2 = Cat("Shadow", "black")

print(cat1.meow())  # Output: Whiskers says meow!
print(cat2.meow())  # Output: Shadow says meow!
```

## 4. Instance Methods
   - Instance methods can modify an instance's state (attributes) or perform actions based on that instance.
   - These methods have access to the instance through the self parameter.

Example:
```python
class Counter:
    def __init__(self):
        self.count = 0  # Initializing state
    
    # Instance method to increment count
    def increment(self):
        self.count += 1
    
    # Instance method to get the current count
    def get_count(self):
        return self.count

# Creating an instance of Counter
counter = Counter()

# Using instance methods
counter.increment()
counter.increment()
print(counter.get_count())  # Output: 2
```

- increment method changes the instance state by increasing count.
- get_count retrieves the current count.

## 5. Accessing Methods and Attributes

  -  Instance methods are called on the object (instance).
  -  Attributes can be accessed directly using the dot notation.

Example:
```python
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author

    def info(self):
        return f"'{self.title}' by {self.author}"

# Create an instance
my_book = Book("1984", "George Orwell")

# Access instance attributes
print(my_book.title)  # Output: 1984
print(my_book.author)  # Output: George Orwell

# Call instance method
print(my_book.info())  # Output: '1984' by George Orwell

```
## 6. Class vs. Instance Attributes

  -  Class attributes are shared across all instances.
  -  Instance attributes are unique to each instance.

Example:
```python
class Tree:
    # Class attribute
    species = "Oak"

    def __init__(self, height):
        # Instance attribute
        self.height = height

# Create two instances
tree1 = Tree(10)
tree2 = Tree(20)

# Access class and instance attributes
print(tree1.species)  # Output: Oak (shared)
print(tree1.height)   # Output: 10 (unique)
print(tree2.height)   # Output: 20 (unique)

```
Summary:

  - Attributes store the state of the class or object.
  -  Methods define the behavior of the class or object.
  - Classes are instantiated to create objects.
  -  Objects can access methods and attributes using dot notation.

## 7. Encapsulation in Python

**Encapsulation** is one of the fundamental concepts of Object-Oriented Programming (OOP). 

It enables us to hide the internal complexity of an object and protect the integrity of the data. 

This is achieved by restricting direct access to some of the object's components. 

With appropriate data encapsulation, a class will present a well-defined public interface for its clients,
the users of the class.

A client should only access those data attributes and invoke those methods that are in the public interface.

### 7.1 Advantages of Encapsulation:

1. **Simplifies object usage**: A developer can use an object without needing to understand its internal working.
2. **Ease of maintenance**: Any changes to the internals can be made without affecting the outside code as long as the public interface remains consistent.

Encapsulation is often discussed alongside **abstraction**, but they are not the same. Encapsulation deals with restricting access to internal data, whereas abstraction deals with exposing only relevant aspects to the user.

### 7.2 Data Hiding with Getters and Setters

In Python, encapsulation is usually achieved by making attributes private and controlling their access through **getter** and **setter** methods. This allows for validation and restricting the type of data that is being assigned.

```python
class MyClass:
    def __init__(self):
        self._age = None  # Private-like attribute

    # Setter for age
    def set_age(self, num):
        if isinstance(num, int) and num > 0:
            self._age = num
        else:
            raise ValueError("Age must be a positive integer.")

    # Getter for age
    def get_age(self):
        return self._age

# Example usage
person = MyClass()
person.set_age(45)
print(person.get_age())  # Outputs: 45
```
In the code above, _age is considered a protected attribute (by convention, not enforced). The setter (set_age) ensures that only valid data is assigned to self._age.
Problem of Invalid Input

Without proper validation in the setter, an invalid value could be assigned to the attribute, like a string instead of an integer:
```python
# Example of an invalid input
person.set_age("Forty Five")  # This raises an error now!
```
By using encapsulation and adding validation inside the setter, we ensure that only valid values are assigned to self._age.
Initialization with __init__ Constructor

The __init__ method in Python is the constructor for a class. It is automatically invoked when an object is instantiated and is typically used to initialize attributes of the object.
```python
class MyClass:
    def __init__(self, value):
        self.value = value  # Instance attribute initialized

# Creating an instance of MyClass
x = MyClass(10)
print(x.value)  # Outputs: 10

```
Here, __init__ initializes the value attribute with whatever argument is passed during instantiation. Without __init__, attributes could be added after instantiation, but it's better practice to use __init__ for predictable and consistent initialization.
Constructor with Multiple Arguments

The __init__ method can accept multiple arguments to initialize several attributes at once.
```python
class MyClass:
    def __init__(self, aaa, bbb):
        self.a = aaa
        self.b = bbb

x = MyClass(4.5, 3)
print(x.a, x.b)  # Outputs: 4.5 3

```
Class Attributes vs Instance Attributes
- Class attributes are shared by all instances of the class.
- Instance attributes are unique to each instance.

### 7.3 Class Attributes

Class attributes are defined directly in the class body and are shared across all instances of the class.

```python
class MyClass:
    age = 21  # Class attribute

# Accessing class attribute through the class itself
print(MyClass.age)  # Outputs: 21

# Accessing class attribute through an instance
x = MyClass()
print(x.age)  # Outputs: 21

```
In the example above, age is a class attribute shared by all instances of MyClass.
Instance Attributes

Instance attributes are defined inside the __init__ method or another instance method. They are unique to each instance.

```python
class MyClass:
    def __init__(self, value):
        self.value = value  # Instance attribute

# Creating instances with different values
x = MyClass(10)
y = MyClass(20)

# Accessing instance attributes
print(x.value)  # Outputs: 10
print(y.value)  # Outputs: 20

```
### 7.4 Overriding Class Attributes in Instances

It’s possible to override class attributes in an instance:

```python
class MyClass:
    classy = 'class value'  # Class attribute

# Instance creation
dd = MyClass()
print(dd.classy)  # Outputs: 'class value'

# Overriding class attribute for this instance
dd.classy = "instance value"
print(dd.classy)  # Outputs: 'instance value'

# Deleting the instance attribute reverts to the class attribute
del dd.classy
print(dd.classy)  # Outputs: 'class value'

```
### 7.5 Working with Class and Instance Data

Instances can access class data as well as their own instance data. Here’s an example of how both are used:

```python
class InstanceCounter:
    count = 0  # Class attribute shared by all instances

    def __init__(self, val):
        self.val = val  # Instance attribute unique to each instance
        InstanceCounter.count += 1  # Incrementing class attribute count

    def get_count(self):
        return InstanceCounter.count

# Creating instances
a = InstanceCounter(9)
b = InstanceCounter(18)
c = InstanceCounter(27)

# Accessing both instance and class data
for obj in (a, b, c):
    print(f'val of obj: {obj.val}')  # Outputs: 9, 18, 27
    print(f'count: {obj.get_count()}')  # Outputs: 3 for all, since it's class-wide

```

### 7.6 Summary
Encapsulation allows you to restrict access to internal data and ensure that it is only 
modified in controlled ways (using setters and getters).

__init__ Constructor is used to initialize an object’s attributes upon creation.

Class Attributes are shared across all instances, while Instance Attributes are unique to each instance.

Encapsulation combined with class and instance data management ensures a cleaner and more reliable design.

## 8 Object orientated shortcuts

| Built-in Function | Description                                        | Example                                                                     |
|-------------------|----------------------------------------------------|-----------------------------------------------------------------------------|
| `abs()`           | Returns the absolute value of a number.            | `abs(-5)` returns `5`                                                       |
| `all()`           | Returns `True` if all elements are true.           | `all([True, True, False])` returns `False`                                  |
| `any()`           | Returns `True` if any element is true.             | `any([False, True, False])` returns `True`                                  |
| `ascii()`         | Returns a string containing a printable            | `ascii('é')` returns `"'\\xe9'"`                                            |
|                   | representation of an object.                       |                                                                             |
| `bin()`           | Converts an integer to a binary string.            | `bin(10)` returns `'0b1010'`                                                |
| `bool()`          | Converts a value to a Boolean.                     | `bool(0)` returns `False`                                                   |
| `bytearray()`     | Returns a new array of bytes.                      | `bytearray([50])` returns `bytearray(b'2')`                                 |
| `bytes()`         | Returns a bytes object.                            | `bytes("hello", "utf-8")` returns `b'hello'`                                |
| `callable()`      | Checks if the object appears callable.             | `callable(abs)` returns `True`                                              |
| `chr()`           | Returns the string representing a character        | `chr(97)` returns `'a'`                                                     |
|                   | whose Unicode code point is the integer.           |                                                                             |
| `classmethod()`   | Transforms a method into a class method.           | `class MyClass: @classmethod def my_method(cls): pass`                      |
| `compile()`       | Compiles source into a code object.                | `compile('print("Hello")', '', 'exec')`                                     |
| `complex()`       | Creates a complex number.                          | `complex(1, 2)` returns `(1+2j)`                                            |
| `delattr()`       | Deletes an attribute from an object.               | `delattr(obj, 'attr')` deletes the attribute `attr`                         |
| `dict()`          | Creates a new dictionary.                          | `dict(a=1, b=2)` returns `{'a': 1, 'b': 2}`                                 |
| `divmod()`        | Returns a tuple of quotient and remainder.         | `divmod(10, 3)` returns `(3, 1)`                                            |
| `enumerate()`     | Adds a counter to an iterable.                     | `list(enumerate(['a', 'b', 'c']))` returns `[(0, 'a'), (1, 'b'), (2, 'c')]` |
| `eval()`          | Evaluates a string as a Python expression.         | `eval('2 + 2')` returns `4`                                                 |
| `exec()`          | Executes a dynamically created Python code.        | `exec('a = 5')` sets `a` to `5`                                             |
| `filter()`        | Filters elements from an iterable.                 | `list(filter(lambda x: x > 0, [-2, -1, 0, 1, 2]))` returns `[1, 2]`         |
| `float()`         | Converts a string or integer to a float.           | `float('3.14')` returns `3.14`                                              |
| `format()`        | Formats a value into a string.                     | `format(123, 'd')` returns `'123'`                                          |
| `frozenset()`     | Creates an immutable set.                          | `frozenset([1, 2, 2, 3])` returns `frozenset({1, 2, 3})`                    |
| `getattr()`       | Gets the value of an object's attribute.           | `getattr(obj, 'attr', default)` gets `attr`, or `default` if not found      |
| `globals()`       | Returns a dictionary of the current global         | `globals()` returns global symbol table                                     |
|                   | symbol table.                                      |                                                                             |
| `hasattr()`       | Checks if an object has a specified attribute.     | `hasattr(obj, 'attr')` returns `True` or `False`                            |
| `help()`          | Invokes the built-in help system.                  | `help(str)` provides documentation for the string class                     |
| `hex()`           | Converts an integer to a hexadecimal string.       | `hex(255)` returns `'0xff'`                                                 |
| `id()`            | Returns the identity of an object.                 | `id(obj)` returns unique identifier for `obj`                               |
| `input()`         | Reads a line from input.                           | `input("Enter something: ")` reads user input                               |
| `int()`           | Converts a number or string to an integer.         | `int('10')` returns `10`                                                    |
| `isinstance()`    | Checks if an object is an instance of a class.     | `isinstance(5, int)` returns `True`                                         |
| `issubclass()`    | Checks if a class is a subclass of another.        | `issubclass(bool, int)` returns `True`                                      |
| `len()`           | Returns the length of an object.                   | `len([1, 2, 3])` returns `3`                                                |
| `list()`          | Creates a new list.                                | `list((1, 2, 3))` returns `[1, 2, 3]`                                       |
| `map()`           | Applies a function to all items in an iterable.    | `list(map(str, [1, 2, 3]))` returns `['1', '2', '3']`                       |
| `max()`           | Returns the largest item in an iterable.           | `max([1, 2, 3])` returns `3`                                                |
| `memoryview()`    | Creates a memory view object.                      | `memoryview(b'abc')` returns `<memory at ...>`                              |
| `min()`           | Returns the smallest item in an iterable.          | `min([1, 2, 3])` returns `1`                                                |
| `next()`          | Retrieves the next item from an iterator.          | `next(iter([1, 2, 3]))` returns `1`                                         |
| `open()`          | Opens a file and returns a file object.            | `open('file.txt', 'r')` opens `file.txt` for reading                        |
| `ord()`           | Returns the Unicode code point for a character.    | `ord('a')` returns `97`                                                     |
| `pow()`           | Returns a number raised to the power of another.   | `pow(2, 3)` returns `8`                                                     |
| `print()`         | Prints the specified message to the console.       | `print('Hello, World!')` outputs `Hello, World!`                            |
| `property()`      | Returns a property attribute.                      | `class C: x = property()` defines a property `x`                            |
| `range()`         | Generates a sequence of numbers.                   | `list(range(5))` returns `[0, 1, 2, 3, 4]`                                  |
| `repr()`          | Returns a string representation of an object.      | `repr('hello')` returns `"hello"`                                           |
| `reversed()`      | Returns a reverse iterator.                        | `list(reversed([1, 2, 3]))` returns `[3, 2, 1]`                             |
| `round()`         | Rounds a number to a specified number of decimals. | `round(3.14159, 2)` returns `3.14`                                          |
| `set()`           | Creates a new set.                                 | `set([1, 2, 2, 3])` returns `{1, 2, 3}`                                     |
| `setattr()`       | Sets the value of an object's attribute.           | `setattr(obj, 'attr', value)` sets `attr` to `value`                        |
| `slice()`         | Creates a slice object.                            | `slice(1, 5)` creates a slice from index 1 to 4                             |
| `sorted()`        | Returns a sorted list from an iterable.            | `sorted([3, 1, 2])` returns `[1, 2, 3]`                                     |
| `staticmethod()`  | Transforms a method into a static method.          | `class MyClass: @staticmethod def my_method(): pass`                        |
| `str()`           | Converts an object to a string.                    | `str(123)` returns `'123'`                                                  |
| `sum()`           | Sums items of an iterable.                         | `sum([1, 2, 3])` returns `6`                                                |
| `super()`         | Returns a temporary object of the superclass.      | `super(MyClass, self).method()` calls superclass method                     |
| `tuple()`         | Creates a new tuple.                               | `tuple([1, 2, 3])` returns `(1, 2, 3)`                                      |
| `type()`          | Returns the type of an object.                     | `type(5)` returns `<class 'int'>`                                           |
| `vars()`          | Returns the `__dict__` attribute of an object.     | `vars(obj)` returns the `__dict__` of `obj`                                 |
| `zip()`           | Combines iterables into tuples.                    | `list(zip([1, 2], ['a', 'b']))` returns `[(1, 'a'), (2, 'b')]`              |
| `__import__()`    | Imports a module.                                  | `__import__('math')` imports the `math` module                              |

### 8.1 Callable Objects
Callable Objects: Any object that implements the __call__() method can be invoked as if it were a function. This means you can call an instance of such an object using the usual function call syntax.

Use Cases: Callable objects can be useful for encapsulating behavior in a more object-oriented way. For example, they can maintain state or configure behavior through instance variables while still providing a clear function-like interface.

Example of a Callable Object

Here's a simple example demonstrating a callable object in Python:

```python
class Multiplier:
    def __init__(self, factor):
        # Initialize the multiplier factor
        self.factor = factor

    def __call__(self, number):
        # Return the product of the input number and the factor
        return number * self.factor

# Create an instance of Multiplier with a factor of 2
double = Multiplier(2)

# Call the instance as if it were a function
result1 = double(5)  # This will return 10
result2 = double(10)  # This will return 20

print(result1)  # Output: 10
print(result2)  # Output: 20
```

Breakdown of the Example

**Defining the Class:**

Multiplier: This class has an __init__ method that initializes an instance variable factor,
which is used to multiply the input value when the object is called.


Implementing __call__:

The __call__ method is defined, which takes a parameter number. When an instance of Multiplier is called with a number, it returns the product of that number and the factor.

Creating an Instance:

An instance of Multiplier is created with a factor of 2, which is assigned to the variable double.

Using the Callable Instance:

The instance double is called with different numbers (5 and 10), which internally invokes the __call__ method. The results are 10 and 20, respectively.

Advantages of Using Callable Objects

- Encapsulation: You can encapsulate related behavior and state within a single object.
- Flexibility: Callable objects can be modified easily by changing instance variables or methods without changing the external interface.
- Readability: Using callable objects can improve code readability by providing a clear and concise way to represent actions or transformations.

**Conclusion**

Callable objects in Python provide a powerful way to create function-like behavior within classes, enabling a blend of object-oriented design with functional programming styles. This flexibility can be particularly useful in various programming scenarios, such as callbacks, event handling, or creating reusable components.

### 8.2 __repr__ and __str__

The __str__ and __repr__ methods are special methods used to define how an object is 
represented as a string. 

They serve different purposes and are used in different contexts.
### 8.2.1 __str__

Purpose: The __str__ method is meant to provide a user-friendly string representation of an object. 

This representation is typically more readable and is designed for end-users. 

When you print an object or use str(object), Python calls the __str__ method.

Use Case: 

Use __str__ when you want to create a string representation that is easy for humans to read and understand.

Example:

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"{self.name} is {self.age} years old."

# Usage
p = Person("Alice", 30)
print(p)  # Output: Alice is 30 years old.
```
### 8.2.2  __repr__

Purpose: The __repr__ method is intended to provide an official string representation of an object that can be used to recreate the object using eval() (if possible). The output of __repr__ should be unambiguous and ideally could be used for debugging.

Use Case: Use __repr__ when you want to provide a representation that is more formal and could be useful for developers or debugging. It's aimed at developers rather than end-users.

Example:

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __repr__(self):
        return f"Person(name={self.name!r}, age={self.age})"

# Usage
p = Person("Alice", 30)
print(repr(p))  # Output: Person(name='Alice', age=30)
```

### 8.2.3 Differences between `__str__` and `__repr__`

| Feature                | `__str__`                      | `__repr__`                       |
|------------------------|--------------------------------|----------------------------------|
| **Purpose**            | Readable, user-friendly string | Official string representation    |
| **Context**            | Used by `print()` and `str()` | Used by `repr()` and in the shell |
| **Audience**           | End-users                      | Developers                        |
| **Return Value**       | More informal and concise      | More formal and detailed         |

### 8.2.4 Why use both?

- Clarity: By providing both methods, you can give different representations for different contexts. This helps make the object more usable and understandable for both end-users and developers.
- Flexibility: Users can print an object for human-readable output, while developers can use repr() for debugging and logging purposes, giving a clearer understanding of the object's state.

### 8.2.5 Conclusion

In summary, the __str__ and __repr__ methods allow you to define how objects of your class are represented as strings. Using both methods appropriately can enhance the usability and maintainability of your code, making it easier for both users and developers to work with your objects.

## 9 Using Default Parameters as an Alternative to Method Overloading

- Method overloading allows multiple methods with the same name but different signatures.
- Python does not natively support method overloading. Instead, we can use default parameters.
```python
class Human:
    def sayHello(self, name=None):
        """Greets the person. If a name is provided, it greets that person; otherwise, it greets generically."""
        if name is not None:
            print('Hello ' + name)
        else:
            print('Hello!')


#Create an instance of the Human class
obj = Human()

 #Call the method without parameters; it will execute the else part
obj.sayHello()  # Output: Hello!

# Call the method with a parameter; it will execute the if part
obj.sayHello('Rahul')  # Output: Hello Rahul!
```
## 10 Inheritance and Polymorphism in Python

Inheritance and polymorphism are fundamental concepts in Object-Oriented Programming (OOP) 
that are crucial for writing efficient and reusable code. 

Understanding these concepts will significantly enhance your programming skills.

### 10.1 Inheritance

Inheritance is one of the primary advantages of OOP, allowing programmers to create a base class and extend 
it into more specialized subclasses. 

This mechanism promotes code reusability and organization, reducing the need to rewrite code from scratch.

In object-oriented terminology, when class X extends class Y, Y is referred to as the superclass, 
parent class, or base class, while X is known as the subclass, child class, or derived class. 

One important point to note is that only non-private attributes and methods from the base class are 
accessible by the child class. Private attributes and methods, defined with a single underscore _ or a 
double underscore __, are not accessible to subclasses.

Syntax for Creating a Derived Class

```python
class BaseClass:
    # Body of base class
    pass

class DerivedClass(BaseClass):
    # Body of derived class
    pass

```
Here's a simple example to illustrate inheritance in Python:

```python
# Base class
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        raise NotImplementedError("Subclass must implement abstract method")

# Derived class
class Dog(Animal):
    def speak(self):
        return f"{self.name} says Woof!"

# Another derived class
class Cat(Animal):
    def speak(self):
        return f"{self.name} says Meow!"

# Creating instances of derived classes
dog = Dog("Buddy")
cat = Cat("Whiskers")

# Calling the speak method
print(dog.speak())  # Output: Buddy says Woof!
print(cat.speak())  # Output: Whiskers says Meow!

```
Explanation of the Example

- Base Class (Animal): This class defines a constructor that initializes the name attribute and an abstract method speak() that derived classes must implement.
- Derived Classes (Dog and Cat): These classes inherit from Animal and provide their specific implementations of the speak() method.
- Instantiation: We create instances of Dog and Cat, and when we call the speak() method on each object, we see that each class has its own behavior, demonstrating polymorphism. This allows different objects to be treated uniformly while still retaining their unique behaviors.

**Conclusion**

Inheritance is a powerful concept in Python that enables code reuse and better organization. 

By using inheritance, you can build more specialized classes based on general ones, 
making your code more modular and easier to maintain. 

Understanding inheritance alongside polymorphism will help you harness the full potential
of object-oriented programming in Python.

## 10.2 Polymorphism in Python: Understanding “Many Shapes”

Polymorphism is a key feature of Object-Oriented Programming (OOP) in Python that allows methods to 
operate on objects of different types through a common interface. 
It provides flexibility and loose coupling, making code easier to extend and maintain.

### 10.2.1 What is Polymorphism?

Polymorphism allows functions to use objects of different classes without needing to know their specific types. 

This means that if two or more classes share methods with the same name, these methods can be 
invoked regardless of the object’s class.

**Example of Polymorphism**

Consider a scenario where we have a base class Animal and two subclasses Dog and Cat.

Each subclass implements a common method called show_affection():

```python
class Animal:
    def show_affection(self):
        raise NotImplementedError("Subclass must implement abstract method")

class Dog(Animal):
    def show_affection(self):
        return "The dog wags its tail."

class Cat(Animal):
    def show_affection(self):
        return "The cat purrs."

# Function to demonstrate polymorphism
def display_affection(animal):
    print(animal.show_affection())

# Creating instances
dog = Dog()
cat = Cat()

# Demonstrating polymorphism
display_affection(dog)  # Output: The dog wags its tail.
display_affection(cat)  # Output: The cat purrs.

```
In the above example, the function display_affection() can accept any object of type Animal, regardless of whether it’s a Dog or a Cat. This is the essence of polymorphism.
**Overriding Methods**

In Python, subclasses can override methods from their parent class. 

When a method in a subclass has the same name as a method in the parent class, 
the subclass's method is called instead.

**Example of Overriding**

Here's an example that illustrates method overriding:
```python
class Thought:
    def __init__(self):
        pass

    def message(self):
        print("Thoughts always come and go.")

class Advice(Thought):
    def __init__(self):
        super().__init__()

    def message(self):
        print("Warning: Risk is always involved when dealing with the market!")

# Using the classes
thought = Thought()
advice = Advice()

thought.message()  # Output: Thoughts always come and go.
advice.message()   # Output: Warning: Risk is always involved when dealing with the market!

```
**Inheriting Constructors**

In Python, if a subclass does not define its own constructor (__init__ method), 
it will inherit the constructor of its parent class. 

However, if the subclass does define its constructor, it can still call the parent class's constructor 
using the super() function. 

This is crucial for initializing the parent class's attributes.

**Example of Inheriting Constructors**

Here's an example of inheriting constructors:
```python
class Animal:
    def __init__(self, name):
        self.name = name

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)  # Call the constructor of Animal
        self.breed = breed

# Creating an instance of Dog
my_dog = Dog("Buddy", "Golden Retriever")
print(f"{my_dog.name} is a {my_dog.breed}.")  # Output: Buddy is a Golden Retriever.

```
##### Conclusion
Polymorphism allows objects of different classes to be treated as objects of a common superclass, 
enhancing flexibility in your code.

Method overriding enables subclasses to provide specific implementations for methods defined in their parent classes.

The **super() function** is essential for calling methods in the parent class, 
including constructors, ensuring proper initialization of objects.

By leveraging polymorphism, overriding, and inheritance, you can write cleaner, 
more modular code that is easier to maintain and extend.

## 11 Multiple Inheritance in Python

Multiple Inheritance allows a class to inherit from more than one base class. 

This is useful in scenarios where a class should exhibit behaviors from multiple sources.
**Syntax**

To define a class with multiple inheritance, list the parent classes in parentheses, separated by commas.

**Example of Multiple Inheritance**

Let's consider a simple scenario where we have two base classes, Person and Employee, 
and a derived class Manager that inherits from both:

```python
class Person:
    def __init__(self, name):
        self.name = name

    def display_name(self):
        print(f"Name: {self.name}")

class Employee:
    def __init__(self, employee_id):
        self.employee_id = employee_id

    def display_id(self):
        print(f"Employee ID: {self.employee_id}")

# Manager class inherits from both Person and Employee
class Manager(Person, Employee):
    def __init__(self, name, employee_id, department):
        # Initialize the parent classes
        Person.__init__(self, name)
        Employee.__init__(self, employee_id)
        self.department = department

    def display_info(self):
        self.display_name()
        self.display_id()
        print(f"Department: {self.department}")

# Creating an instance of Manager
manager = Manager("Alice", "E123", "Sales")

# Displaying information
manager.display_info()

```
output
```python
Name: Alice
Employee ID: E123
Department: Sales

```
#### Explanation

##### Base Classes:
Person has an attribute name and a method display_name().

Employee has an attribute employee_id and a method display_id().

#### Derived Class:
Manager inherits from both Person and Employee.

Its constructor initializes both base classes using their respective __init__ methods.

The display_info() method calls methods from both parent classes, demonstrating how the 
derived class can access inherited attributes and methods.

**Method Resolution Order (MRO)**

Python uses the C3 linearization algorithm to determine the order in which classes are looked up when 
searching for a method. 

You can check the MRO of a class using the __mro__ attribute or the mro() method:
```python
print(Manager.__mro__)
# Output: (<class '__main__.Manager'>, <class '__main__.Person'>, <class '__main__.Employee'>, <class 'object'>)

```
**Conclusion**
Flexibility: Multiple inheritance allows a class to combine behaviors from multiple sources, 
increasing flexibility in your design.

Complexity: Be cautious when using multiple inheritance, as it can lead to complexities, 
especially with method name clashes and the MRO. 

Properly understanding the order of resolution is crucial to avoid unexpected behavior.

## 12 Decorators, Static Methods, and Class Methods in Python

In Python, functions (or methods) are typically created using the def statement. 

While methods behave similarly to functions, they have an important distinction: the first argument of a 
method is always the instance object. Methods can be classified based on their behavior:

- Simple Function: Defined outside of a class and can access class attributes via an instance argument.
- Instance Method: Defined within a class and takes self as the first parameter.
- Class Method: Uses the @classmethod decorator and takes cls as the first parameter, allowing access to class attributes.
- Static Method: Uses the @staticmethod decorator and does not take self or cls as a parameter, making it independent of the class and instance state.

**Instance Method**

An instance method is the most common type of method. It takes self as its first parameter, 
allowing it to access instance attributes and methods.

Example
```python
class Dog:
    def __init__(self, name):
        self.name = name

    def bark(self):
        return f"{self.name} says Woof!"

# Creating an instance of Dog
dog = Dog("Buddy")
print(dog.bark())  # Output: Buddy says Woof!

```
**Class Method**

A class method is defined using the @classmethod decorator. 

It takes cls as its first parameter, allowing access to class attributes and methods. 

Class methods are often used to create factory methods that return instances of the class.

Example
```python
class Dog:
    species = "Canis familiaris"

    def __init__(self, name):
        self.name = name

    @classmethod
    def create_with_species(cls, name):
        return cls(name)  # Returns an instance of Dog with a name

# Creating an instance of Dog using the class method
dog = Dog.create_with_species("Max")
print(dog.name)  # Output: Max
print(Dog.species)  # Output: Canis familiaris

```
**Static Method**

A static method is defined using the @staticmethod decorator. 

It does not take self or cls as a parameter, meaning it cannot access instance or class attributes. 

Static methods are often used for utility functions that perform a task without needing to modify 
the class or instance state.

Example
```python
class Math:
    @staticmethod
    def add(a, b):
        return a + b

# Calling the static method
result = Math.add(5, 3)
print(result)  # Output: 8

```
**When to Use Each Type**

- Instance Methods: Use when you need to access or modify instance-specific data.
- Class Methods: Use for factory methods or when you need to access class-level data. They are often used to create alternate constructors.
- Static Methods: Use for utility functions that do not require access to instance or class data.

**Summary**

- Instance Method: Can modify object state and access instance attributes using self.
- Class Method: Can modify class state and access class attributes using cls. Ideal for factory methods.
- Static Method: Cannot modify object or class state. Suitable for utility functions that don't depend on class or instance context.
