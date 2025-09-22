.. _module3_data_structures:

Data Structures in Python
=========================

Python provides several built-in data structures for storing and organizing data.

Lists
-----

Lists are ordered, mutable sequences that can contain different types of elements.

**Creating Lists**

.. code-block:: python

   # Empty list
   empty_list = []

   # List with elements
   numbers = [1, 2, 3, 4, 5]
   fruits = ["apple", "banana", "cherry"]
   mixed = [1, "hello", 3.14, True]

**List Operations**

.. code-block:: python

   fruits = ["apple", "banana", "cherry"]

   # Access elements
   print(fruits[0])  # apple
   print(fruits[-1]) # cherry

   # Modify elements
   fruits[1] = "orange"
   print(fruits)  # ['apple', 'orange', 'cherry']

   # Add elements
   fruits.append("grape")
   print(fruits)  # ['apple', 'orange', 'cherry', 'grape']

   # Insert at specific position
   fruits.insert(1, "mango")
   print(fruits)  # ['apple', 'mango', 'orange', 'cherry', 'grape']

   # Remove elements
   fruits.remove("orange")
   print(fruits)  # ['apple', 'mango', 'cherry', 'grape']

   # Remove by index
   popped = fruits.pop(2)
   print(popped)  # cherry
   print(fruits)  # ['apple', 'mango', 'grape']

**List Slicing**

.. code-block:: python

   numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

   print(numbers[2:5])   # [2, 3, 4]
   print(numbers[:5])    # [0, 1, 2, 3, 4]
   print(numbers[5:])    # [5, 6, 7, 8, 9]
   print(numbers[::2])   # [0, 2, 4, 6, 8]
   print(numbers[::-1])  # [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]

**List Methods**

.. code-block:: python

   numbers = [3, 1, 4, 1, 5, 9, 2, 6]

   # Sort the list
   numbers.sort()
   print(numbers)  # [1, 1, 2, 3, 4, 5, 6, 9]

   # Reverse the list
   numbers.reverse()
   print(numbers)  # [9, 6, 5, 4, 3, 2, 1, 1]

   # Find index of element
   print(numbers.index(5))  # 2

   # Count occurrences
   print(numbers.count(1))  # 2

   # Get length
   print(len(numbers))  # 8

Tuples
------

Tuples are ordered, immutable sequences.

**Creating Tuples**

.. code-block:: python

   # Empty tuple
   empty_tuple = ()

   # Tuple with elements
   coordinates = (10, 20)
   person = ("Alice", 25, "Engineer")

   # Single element tuple (note the comma)
   single = (5,)

**Tuple Operations**

.. code-block:: python

   coordinates = (10, 20, 30)

   # Access elements
   print(coordinates[0])  # 10
   print(coordinates[-1]) # 30

   # Slicing
   print(coordinates[1:])  # (20, 30)

   # Unpacking
   x, y, z = coordinates
   print(x, y, z)  # 10 20 30

Dictionaries
------------

Dictionaries store key-value pairs and are unordered.

**Creating Dictionaries**

.. code-block:: python

   # Empty dictionary
   empty_dict = {}

   # Dictionary with data
   student = {
       "name": "Alice",
       "age": 20,
       "grade": "A"
   }

   # Using dict() constructor
   person = dict(name="Bob", age=25, city="New York")

**Dictionary Operations**

.. code-block:: python

   student = {"name": "Alice", "age": 20, "grade": "A"}

   # Access values
   print(student["name"])  # Alice
   print(student.get("age"))  # 20

   # Add new key-value pair
   student["major"] = "Computer Science"
   print(student)

   # Modify existing value
   student["age"] = 21
   print(student)

   # Remove key-value pair
   del student["grade"]
   print(student)

   # Check if key exists
   print("name" in student)  # True

   # Get all keys
   print(student.keys())  # dict_keys(['name', 'age', 'major'])

   # Get all values
   print(student.values())  # dict_values(['Alice', 21, 'Computer Science'])

   # Get all key-value pairs
   print(student.items())  # dict_items([('name', 'Alice'), ('age', 21), ('major', 'Computer Science')])

**Dictionary Example: Student Records**

.. code-block:: python

   students = {
       "001": {"name": "Alice", "grade": "A"},
       "002": {"name": "Bob", "grade": "B"},
       "003": {"name": "Charlie", "grade": "A"}
   }

   # Access nested dictionary
   print(students["001"]["name"])  # Alice

   # Add new student
   students["004"] = {"name": "David", "grade": "B"}

   # Update grade
   students["002"]["grade"] = "A"

**Dictionary Example: Word Frequency Counter**

.. code-block:: python

   text = "hello world hello python world"
   words = text.split()

   word_count = {}
   for word in words:
       if word in word_count:
           word_count[word] += 1
       else:
           word_count[word] = 1

   print(word_count)  # {'hello': 2, 'world': 2, 'python': 1}

Sets
----

Sets are unordered collections of unique elements.

**Creating Sets**

.. code-block:: python

   # Empty set
   empty_set = set()

   # Set with elements
   numbers = {1, 2, 3, 4, 5}
   fruits = {"apple", "banana", "cherry"}

   # From list (removes duplicates)
   numbers = set([1, 2, 2, 3, 3, 3])
   print(numbers)  # {1, 2, 3}

**Set Operations**

.. code-block:: python

   set1 = {1, 2, 3, 4}
   set2 = {3, 4, 5, 6}

   # Add element
   set1.add(5)
   print(set1)  # {1, 2, 3, 4, 5}

   # Remove element
   set1.remove(5)
   print(set1)  # {1, 2, 3, 4}

   # Union
   print(set1 | set2)  # {1, 2, 3, 4, 5, 6}

   # Intersection
   print(set1 & set2)  # {3, 4}

   # Difference
   print(set1 - set2)  # {1, 2}

   # Symmetric difference
   print(set1 ^ set2)  # {1, 2, 5, 6}

Data Structure Comparison
-------------------------

+------------------+--------+----------+----------+----------+
| Feature          | List   | Tuple    | Dict     | Set      |
+==================+========+==========+==========+==========+
| Ordered          | Yes    | Yes      | No       | No       |
+------------------+--------+----------+----------+----------+
| Mutable          | Yes    | No       | Yes      | Yes      |
+------------------+--------+----------+----------+----------+
| Allows Duplicates| Yes    | Yes      | Keys: No | No       |
|                  |        |          | Values: Yes|         |
+------------------+--------+----------+----------+----------+
| Indexed Access   | Yes    | Yes      | By Key   | No       |
+------------------+--------+----------+----------+----------+
| Use Case         | Sequence| Fixed    | Key-Value| Unique   |
|                  | of items| data     | pairs    | items    |
+------------------+--------+----------+----------+----------+

Advanced List Operations
------------------------

**List Comprehensions**

.. code-block:: python

   # Create list of squares
   squares = [x**2 for x in range(10)]
   print(squares)  # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

   # Filter even numbers
   evens = [x for x in range(10) if x % 2 == 0]
   print(evens)  # [0, 2, 4, 6, 8]

   # Nested comprehensions
   matrix = [[i*j for j in range(3)] for i in range(3)]
   print(matrix)  # [[0, 0, 0], [0, 1, 2], [0, 2, 4]]

**List as Stack and Queue**

.. code-block:: python

   # Stack (LIFO)
   stack = []
   stack.append(1)  # Push
   stack.append(2)
   stack.append(3)
   print(stack.pop())  # 3 (Pop)

   # Queue (FIFO) - inefficient for large lists
   queue = []
   queue.append(1)  # Enqueue
   queue.append(2)
   queue.append(3)
   print(queue.pop(0))  # 1 (Dequeue)

Advanced Dictionary Operations
------------------------------

**Dictionary Comprehensions**

.. code-block:: python

   # Create dict of squares
   squares = {x: x**2 for x in range(5)}
   print(squares)  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

   # Filter dictionary
   grades = {'Alice': 85, 'Bob': 92, 'Charlie': 78}
   passed = {name: grade for name, grade in grades.items() if grade >= 80}
   print(passed)  # {'Alice': 85, 'Bob': 92}

**Merging Dictionaries**

.. code-block:: python

   dict1 = {'a': 1, 'b': 2}
   dict2 = {'c': 3, 'd': 4}

   # Python 3.9+
   merged = dict1 | dict2
   print(merged)  # {'a': 1, 'b': 2, 'c': 3, 'd': 4}

   # Update method
   dict1.update(dict2)
   print(dict1)  # {'a': 1, 'b': 2, 'c': 3, 'd': 4}

**Default Values with defaultdict**

.. code-block:: python

   from collections import defaultdict

   # Default list
   word_groups = defaultdict(list)
   words = ['apple', 'banana', 'cherry', 'apricot']
   for word in words:
       word_groups[word[0]].append(word)

   print(word_groups)  # {'a': ['apple', 'apricot'], 'b': ['banana'], 'c': ['cherry']}

   # Default counter
   word_count = defaultdict(int)
   text = "hello world hello python"
   for word in text.split():
       word_count[word] += 1

   print(word_count)  # defaultdict(<class 'int'>, {'hello': 2, 'world': 1, 'python': 1})

Advanced Set Operations
-----------------------

**Set Comprehensions**

.. code-block:: python

   # Create set of squares
   squares = {x**2 for x in range(10)}
   print(squares)  # {0, 1, 4, 9, 16, 25, 36, 49, 64, 81}

   # Filter unique even numbers
   numbers = [1, 2, 2, 3, 4, 4, 5]
   evens = {x for x in numbers if x % 2 == 0}
   print(evens)  # {2, 4}

**Frozen Sets (Immutable Sets)**

.. code-block:: python

   # Create frozen set
   frozen = frozenset([1, 2, 3, 4])
   print(frozen)  # frozenset({1, 2, 3, 4})

   # Can be used as dictionary keys
   my_dict = {frozen: "value"}
   print(my_dict[frozen])  # value

Common Data Structure Use Cases
-------------------------------

**Lists**

- Storing sequences of items
- Implementing stacks and queues
- Matrix operations
- Dynamic arrays

**Tuples**

- Returning multiple values from functions
- Dictionary keys (immutable)
- Unpacking assignments
- Fixed configuration data

**Dictionaries**

- Key-value data storage
- Caching results
- Counting frequencies
- Configuration settings

**Sets**

- Removing duplicates
- Membership testing
- Mathematical set operations
- Finding unique elements

Performance Considerations
--------------------------

**Time Complexity**

+------------------+--------+--------+--------+--------+
| Operation        | List   | Tuple  | Dict   | Set    |
+==================+========+========+========+========+
| Access by index  | O(1)   | O(1)   | O(1)   | N/A    |
+------------------+--------+--------+--------+--------+
| Search           | O(n)   | O(n)   | O(1)   | O(1)   |
+------------------+--------+--------+--------+--------+
| Insert           | O(n)   | N/A    | O(1)   | O(1)   |
+------------------+--------+--------+--------+--------+
| Delete           | O(n)   | N/A    | O(1)   | O(1)   |
+------------------+--------+--------+--------+--------+

**Space Complexity**

- Lists: O(n)
- Tuples: O(n)
- Dictionaries: O(n)
- Sets: O(n)

**Tips**

- Use lists for ordered collections you need to modify
- Use tuples for immutable sequences
- Use dictionaries for fast lookups by key
- Use sets for unique items and set operations
- Consider `collections.deque` for efficient queue operations
- Use `collections.Counter` for counting frequencies