.. _module3_lambda_map_filter:

Lambda Functions, map(), and filter()
=====================================

Lambda functions are small, anonymous functions that can be defined in a single line.

Lambda Functions
----------------

.. code-block:: python

   # Regular function
   def square(x):
       return x ** 2

   # Equivalent lambda function
   square_lambda = lambda x: x ** 2

   print(square(5))          # 25
   print(square_lambda(5))   # 25

**Lambda with multiple parameters**

.. code-block:: python

   add = lambda x, y: x + y
   print(add(3, 5))  # 8

   # Lambda in conditional expression
   max_value = lambda x, y: x if x > y else y
   print(max_value(10, 20))  # 20

The map() Function
------------------

`map()` applies a function to all items in an iterable.

.. code-block:: python

   # Using map with regular function
   def square(x):
       return x ** 2

   numbers = [1, 2, 3, 4, 5]
   squared = list(map(square, numbers))
   print(squared)  # [1, 4, 9, 16, 25]

   # Using map with lambda
   squared_lambda = list(map(lambda x: x ** 2, numbers))
   print(squared_lambda)  # [1, 4, 9, 16, 25]

   # map with multiple iterables
   numbers1 = [1, 2, 3]
   numbers2 = [4, 5, 6]
   sums = list(map(lambda x, y: x + y, numbers1, numbers2))
   print(sums)  # [5, 7, 9]

The filter() Function
---------------------

`filter()` creates a new iterable with elements that pass a test.

.. code-block:: python

   # Using filter with regular function
   def is_even(x):
       return x % 2 == 0

   numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
   even_numbers = list(filter(is_even, numbers))
   print(even_numbers)  # [2, 4, 6, 8, 10]

   # Using filter with lambda
   even_lambda = list(filter(lambda x: x % 2 == 0, numbers))
   print(even_lambda)  # [2, 4, 6, 8, 10]

   # Filter strings
   words = ["apple", "banana", "cherry", "date"]
   long_words = list(filter(lambda word: len(word) > 5, words))
   print(long_words)  # ['banana', 'cherry']

Combining map() and filter()
-----------------------------

.. code-block:: python

   numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

   # Filter even numbers and square them
   result = list(map(lambda x: x ** 2, filter(lambda x: x % 2 == 0, numbers)))
   print(result)  # [4, 16, 36, 64, 100]

   # Alternative using list comprehension
   result_comprehension = [x ** 2 for x in numbers if x % 2 == 0]
   print(result_comprehension)  # [4, 16, 36, 64, 100]

Practical Examples
------------------

**Convert temperatures from Celsius to Fahrenheit**

.. code-block:: python

   celsius = [0, 10, 20, 30, 40]
   fahrenheit = list(map(lambda c: (c * 9/5) + 32, celsius))
   print(fahrenheit)  # [32.0, 50.0, 68.0, 86.0, 104.0]

**Filter students who passed**

.. code-block:: python

   students = [
       {"name": "Alice", "grade": 85},
       {"name": "Bob", "grade": 72},
       {"name": "Charlie", "grade": 90},
       {"name": "David", "grade": 65}
   ]

   passed_students = list(filter(lambda student: student["grade"] >= 75, students))
   print(passed_students)

**Extract names of students who passed**

.. code-block:: python

   passed_names = list(map(lambda student: student["name"],
                          filter(lambda student: student["grade"] >= 75, students)))
   print(passed_names)  # ['Alice', 'Charlie']

The reduce() Function
---------------------

`reduce()` applies a function cumulatively to the items of an iterable, reducing it to a single value.

.. code-block:: python

   from functools import reduce

   # Sum all numbers
   numbers = [1, 2, 3, 4, 5]
   total = reduce(lambda x, y: x + y, numbers)
   print(total)  # 15

   # Find maximum
   max_num = reduce(lambda x, y: x if x > y else y, numbers)
   print(max_num)  # 5

   # String concatenation
   words = ["Hello", " ", "World", "!"]
   sentence = reduce(lambda x, y: x + y, words)
   print(sentence)  # "Hello World!"

   # With initial value
   numbers = [1, 2, 3, 4, 5]
   total_with_init = reduce(lambda x, y: x + y, numbers, 10)
   print(total_with_init)  # 25 (10 + 15)

List Comprehensions vs map() and filter()
------------------------------------------

**When to use list comprehensions:**

.. code-block:: python

   # Simple transformations
   squares = [x**2 for x in range(10)]
   print(squares)  # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

   # Simple filtering
   evens = [x for x in range(10) if x % 2 == 0]
   print(evens)  # [0, 2, 4, 6, 8]

   # Nested comprehensions
   matrix = [[i*j for j in range(3)] for i in range(3)]
   print(matrix)

**When to use map() and filter():**

.. code-block:: python

   # When you have existing functions
   def square(x):
       return x ** 2

   def is_even(x):
       return x % 2 == 0

   numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
   result = list(map(square, filter(is_even, numbers)))
   print(result)  # [4, 16, 36, 64, 100]

   # With lambda functions for one-time use
   result_lambda = list(map(lambda x: x**2, filter(lambda x: x % 2 == 0, numbers)))
   print(result_lambda)  # [4, 16, 36, 64, 100]

Advanced Lambda Patterns
------------------------

**Lambda with default arguments**

.. code-block:: python

   # Default arguments in lambda
   power = lambda x, y=2: x ** y
   print(power(3))     # 9 (3^2)
   print(power(3, 3))  # 27 (3^3)

**Lambda in sorting with multiple keys**

.. code-block:: python

   students = [
       ("Alice", 85, "A"),
       ("Bob", 92, "A"),
       ("Charlie", 78, "B"),
       ("David", 85, "B")
   ]

   # Sort by grade descending, then by name ascending
   sorted_students = sorted(students, key=lambda x: (-x[1], x[0]))
   print(sorted_students)

**Lambda for creating functions dynamically**

.. code-block:: python

   def create_operation(op):
       if op == "add":
           return lambda x, y: x + y
       elif op == "multiply":
           return lambda x, y: x * y
       elif op == "power":
           return lambda x, y: x ** y

   add_func = create_operation("add")
   multiply_func = create_operation("multiply")
   power_func = create_operation("power")

   print(add_func(3, 4))      # 7
   print(multiply_func(3, 4)) # 12
   print(power_func(3, 4))    # 81

Functional Programming Patterns
-------------------------------

**Function composition**

.. code-block:: python

   def compose(f, g):
       return lambda x: f(g(x))

   # Create composed functions
   square_then_add_one = compose(lambda x: x + 1, lambda x: x ** 2)
   add_one_then_square = compose(lambda x: x ** 2, lambda x: x + 1)

   print(square_then_add_one(3))  # (3^2) + 1 = 10
   print(add_one_then_square(3))  # (3+1)^2 = 16

**Partial application**

.. code-block:: python

   from functools import partial

   # Create specialized functions
   multiply_by_2 = partial(lambda x, y: x * y, 2)
   multiply_by_3 = partial(lambda x, y: x * y, 3)

   print(multiply_by_2(5))  # 10
   print(multiply_by_3(5))  # 15

   # Partial with keyword arguments
   greet = lambda greeting, name: f"{greeting}, {name}!"
   greet_hello = partial(greet, greeting="Hello")
   greet_hi = partial(greet, greeting="Hi")

   print(greet_hello("Alice"))  # "Hello, Alice!"
   print(greet_hi("Bob"))       # "Hi, Bob!"

Performance Considerations
--------------------------

**Memory efficiency with generators**

.. code-block:: python

   # List comprehension creates entire list in memory
   squares_list = [x**2 for x in range(1000000)]

   # Generator expression is memory efficient
   squares_gen = (x**2 for x in range(1000000))

   # Use generator with map/filter for large datasets
   large_numbers = range(1000000)
   even_squares = map(lambda x: x**2, filter(lambda x: x % 2 == 0, large_numbers))

   # Get first 10 results without computing all
   first_10 = []
   for i, square in enumerate(even_squares):
       if i >= 10:
           break
       first_10.append(square)
   print(first_10)

**Execution time comparison**

.. code-block:: python

   import time

   numbers = list(range(100000))

   # List comprehension
   start = time.time()
   result1 = [x**2 for x in numbers if x % 2 == 0]
   time1 = time.time() - start

   # map + filter
   start = time.time()
   result2 = list(map(lambda x: x**2, filter(lambda x: x % 2 == 0, numbers)))
   time2 = time.time() - start

   print(f"List comprehension: {time1:.4f} seconds")
   print(f"map + filter: {time2:.4f} seconds")
   print(f"Results equal: {result1 == result2}")

Best Practices
--------------

- Use list comprehensions for simple transformations and filtering
- Use `map()` and `filter()` when you have existing functions or need lazy evaluation
- Prefer generator expressions for large datasets
- Use meaningful lambda parameter names for readability
- Consider readability: sometimes a regular function is clearer than a complex lambda
- Use `functools.partial` for creating specialized functions
- Remember that `map()` and `filter()` return iterators in Python 3