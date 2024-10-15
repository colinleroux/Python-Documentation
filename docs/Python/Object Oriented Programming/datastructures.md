# Data Structures in OOP Python

## 1. Lists
- **Description**: A list is an ordered, mutable (modifiable) collection of items. Lists can contain elements of different types.
- **Creation**: 
    ```python
    my_list = [1, 2, 3, 'four', 5.0]
    ```
- **Adding Items**:
    - **Append**: Adds an item to the end of the list.
        ```python
        my_list.append(6)
        ```
    - **Insert**: Inserts an item at a specified index.
        ```python
        my_list.insert(1, 'two')  # Inserts 'two' at index 1
        ```
      - **Insert at beginning of list**: ie (index 0).
        ```python
        my_list.insert(0, 'two')  # Inserts 'two' at index 0
        ```
- **Removing Items**:
    - **Remove**: Removes the first occurrence of a value.
        ```python
        my_list.remove('four')
        ```
    - **Pop**: Removes an item at a specified index (or the last item if no index is specified).
        ```python
        last_item = my_list.pop()  # Removes the last item
        ```

## 2. Empty Objects
- **Description**: An empty object can be created using a class. It serves as a container for attributes and methods.
- **Creation**:
    ```python
    class MyClass:
        pass

    empty_object = MyClass()
    ```
- **Adding Attributes**:
    ```python
    empty_object.name = "John Doe"
    empty_object.age = 30
    ```
- **Accessing Attributes**:
    ```python
    print(empty_object.name)  # Output: John Doe
    ```

## 3. Tuples
**Description**: A tuple is an ordered, immutable (non-modifiable) collection of items. 
- Once created, the items cannot be changed.

- You cannot add elements to a tuple.
- You cannot append or extend a method.
- You cannot remove elements from a tuple.
- Tuples have no remove or pop method.
- Count and index are the methods available in a tuple.

- **Creation**:
    ```python
    my_tuple = (1, 2, 3, 'four')
    ```
- **Accessing Items**:
    ```python
    first_item = my_tuple[0]  # Output: 1
    ```
- **Slicing**: You can access a range of items.
    ```python
    sliced = my_tuple[1:3]  # Output: (2, 3)
    ```

## 4. Dictionaries
- **Description**: A dictionary is an unordered, mutable collection of key-value pairs. Keys must be unique.
- **Creation**:
    ```python
    my_dict = {'name': 'Alice', 'age': 30, 'city': 'New York'}
    ```
- **Adding Items**:
    ```python
    my_dict['job'] = 'Engineer'  # Adds a new key-value pair
    ```
- **Removing Items**:
    - **Del**: Deletes a key-value pair.
        ```python
        del my_dict['age']  # Removes the key 'age'
        ```
    - **Pop**: Removes a key and returns its value.
        ```python
        city = my_dict.pop('city')  # Removes 'city' and returns its value
        ```
      - **Clear**: Removes all keys and values.
        ```python
        my_dict.clear()  # Clears the list
        ```

Take note : 

  - Empty dictionary: {} is always interpreted as an empty dictionary.
  - Empty set: To create an empty set, you must use set().

Key Points:
- Dictionaries hold key-value pairs, while sets only contain unique values.
- {} by default represents an empty dictionary, not a set.
- To create a non-empty set, you can use curly braces with values, but for an empty set, you must use set().
```python
# This is an empty dictionary
my_dict = {}
print(type(my_dict))  # Output: <class 'dict'>

# This is an empty set
my_set = set()
print(type(my_set))  # Output: <class 'set'>

# Non-empty set using curly braces
non_empty_set = {1, 2, 3}
print(type(non_empty_set))  # Output: <class 'set'>

# Non-empty dictionary with curly braces
non_empty_dict = {'a': 1, 'b': 2}
print(type(non_empty_dict))  # Output: <class 'dict'>
```
Why the Difference?

Dictionaries need a specific syntax to represent key-value pairs ({key: value}).
Sets use curly braces too, but only contain values ({value1, value2}), so Python reserved {} for empty dictionaries to avoid confusion.

## 5. Sets
- **Description**: A set is an unordered collection of unique items. It is mutable but does not allow duplicate values.
- **Creation**:
    ```python
    my_set = {1, 2, 3, 4}
    ```
- **Adding Items**:
    ```python
    my_set.add(5)  # Adds 5 to the set
    ```
- **Removing Items**:
    - **Remove**: Removes a specified item. Raises an error if the item is not found.
        ```python
        my_set.remove(2)
        ```
    - **Discard**: Removes a specified item. Does not raise an error if the item is not found.
        ```python
        my_set.discard(3)
        ```
- **Operations**: Sets support mathematical operations like union, intersection, and difference.
    ```python
    another_set = {3, 4, 5, 6}
    union_set = my_set | another_set  # Union
    intersection_set = my_set & another_set  # Intersection
    ```

## Summary Table

| Data Structure | Mutability | Ordered | Example                                   | Adding Items                  | Removing Items                  |
|----------------|------------|---------|-------------------------------------------|-------------------------------|---------------------------------|
| **List**       | Mutable    | Yes     | `my_list = [1, 2, 3]`                    | `my_list.append(4)`          | `my_list.remove(2)`            |
| **Empty Object** | Mutable | Yes     | `empty_object = MyClass()`                | `empty_object.attr = value`   | N/A (can delete attributes)     |
| **Tuple**      | Immutable  | Yes     | `my_tuple = (1, 2, 3)`                   | N/A                           | N/A                             |
| **Dictionary** | Mutable    | No      | `my_dict = {'key': 'value'}`             | `my_dict['new_key'] = 'new_value'` | `del my_dict['key']`          |
| **Set**        | Mutable    | No      | `my_set = {1, 2, 3}`                     | `my_set.add(4)`              | `my_set.remove(2)`             |

## Conclusion
These data structures are fundamental to Python and are used extensively in OOP. Each has its own use cases and advantages, allowing for flexible and efficient data management in your programs. Understanding these data structures will help you design better algorithms and data flows in your applications.
