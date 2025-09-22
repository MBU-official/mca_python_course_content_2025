.. _module3_functions:

Functions in Python
===================

Functions are reusable blocks of code that perform specific tasks.

Function Definition
-------------------

.. code-block:: python

   def greet():
       print("Hello, World!")

   # Call the function
   greet()

Functions with Parameters
-------------------------

.. code-block:: python

   def greet_person(name):
       print(f"Hello, {name}!")

   greet_person("Alice")
   greet_person("Bob")

Functions with Return Values
----------------------------

.. code-block:: python

   def add_numbers(a, b):
       return a + b

   result = add_numbers(5, 3)
   print(result)  # 8

Default Parameters
------------------

.. code-block:: python

   def greet_person(name, greeting="Hello"):
       print(f"{greeting}, {name}!")

   greet_person("Alice")           # Hello, Alice!
   greet_person("Bob", "Hi")       # Hi, Bob!

Keyword Arguments
-----------------

.. code-block:: python

   def create_person(name, age, city):
       return {"name": name, "age": age, "city": city}

   # Using keyword arguments
   person1 = create_person(name="Alice", age=25, city="New York")
   person2 = create_person(city="London", name="Bob", age=30)

   print(person1)
   print(person2)

Variable Number of Arguments
----------------------------

**Using *args** (for positional arguments)

.. code-block:: python

   def sum_all(*numbers):
       total = 0
       for num in numbers:
           total += num
       return total

   print(sum_all(1, 2, 3))      # 6
   print(sum_all(1, 2, 3, 4, 5)) # 15

**Using **kwargs** (for keyword arguments)

.. code-block:: python

   def print_info(**info):
       for key, value in info.items():
           print(f"{key}: {value}")

   print_info(name="Alice", age=25, city="New York")

Recursion
---------

Recursion is when a function calls itself.

**Factorial Example**

.. code-block:: python

   def factorial(n):
       if n == 0 or n == 1:
           return 1
       else:
           return n * factorial(n - 1)

   print(factorial(5))  # 120

**Fibonacci Example**

.. code-block:: python

   def fibonacci(n):
       if n <= 1:
           return n
       else:
           return fibonacci(n - 1) + fibonacci(n - 2)

   # Print first 10 Fibonacci numbers
   for i in range(10):
       print(fibonacci(i), end=" ")  # 0 1 1 2 3 5 8 13 21 34

Function Integration with Strings
---------------------------------

.. code-block:: python

   def count_vowels(text):
       vowels = "aeiouAEIOU"
       count = 0
       for char in text:
           if char in vowels:
               count += 1
       return count

   text = "Hello, World!"
   print(f"Number of vowels: {count_vowels(text)}")  # 3

Function Integration with Collections
-------------------------------------

.. code-block:: python

   def find_max_in_list(numbers):
       if not numbers:
           return None
       max_num = numbers[0]
       for num in numbers:
           if num > max_num:
               max_num = num
       return max_num

   numbers = [3, 1, 4, 1, 5, 9, 2, 6]
   print(f"Maximum: {find_max_in_list(numbers)}")  # 9

   def word_frequency(text):
       words = text.lower().split()
       frequency = {}
       for word in words:
           if word in frequency:
               frequency[word] += 1
           else:
               frequency[word] = 1
       return frequency

   text = "the quick brown fox jumps over the lazy dog"
   print(word_frequency(text))

Variable Scope
--------------

**Local vs Global Scope**

.. code-block:: python

   global_var = "I'm global"

   def test_scope():
       local_var = "I'm local"
       print(global_var)  # Can access global
       print(local_var)   # Can access local

   test_scope()
   # print(local_var)  # Error: local_var not defined

**Modifying Global Variables**

.. code-block:: python

   counter = 0

   def increment_counter():
       global counter
       counter += 1

   increment_counter()
   increment_counter()
   print(counter)  # 2

**Nonlocal Variables (Nested Functions)**

.. code-block:: python

   def outer():
       x = "outer"

       def inner():
           nonlocal x
           x = "inner"
           print(f"Inner: {x}")

       inner()
       print(f"Outer: {x}")

   outer()

Lambda Functions
----------------

Lambda functions are anonymous, single-expression functions.

.. code-block:: python

   # Simple lambda
   square = lambda x: x ** 2
   print(square(5))  # 25

   # Lambda with multiple parameters
   add = lambda x, y: x + y
   print(add(3, 4))  # 7

   # Lambda in sorting
   students = [("Alice", 85), ("Bob", 92), ("Charlie", 78)]
   students.sort(key=lambda student: student[1])  # Sort by grade
   print(students)

   # Lambda with conditional
   is_even = lambda x: "Even" if x % 2 == 0 else "Odd"
   print(is_even(4))  # Even
   print(is_even(5))  # Odd

Higher-Order Functions
----------------------

Functions that take other functions as arguments or return functions.

.. code-block:: python

   def apply_operation(func, x, y):
       return func(x, y)

   def add(x, y):
       return x + y

   def multiply(x, y):
       return x * y

   print(apply_operation(add, 3, 4))      # 7
   print(apply_operation(multiply, 3, 4)) # 12

**Function as Return Value**

.. code-block:: python

   def create_multiplier(factor):
       def multiplier(x):
           return x * factor
       return multiplier

   double = create_multiplier(2)
   triple = create_multiplier(3)

   print(double(5))  # 10
   print(triple(5))  # 15

Function Decorators
-------------------

Decorators modify the behavior of functions.

.. code-block:: python

   def timer_decorator(func):
       def wrapper(*args, **kwargs):
           import time
           start = time.time()
           result = func(*args, **kwargs)
           end = time.time()
           print(f"{func.__name__} took {end - start:.2f} seconds")
           return result
       return wrapper

   @timer_decorator
   def slow_function():
       import time
       time.sleep(1)
       return "Done"

   print(slow_function())

Built-in Functions
------------------

**map() - Apply function to each element**

.. code-block:: python

   numbers = [1, 2, 3, 4, 5]
   squares = list(map(lambda x: x**2, numbers))
   print(squares)  # [1, 4, 9, 16, 25]

**filter() - Filter elements based on condition**

.. code-block:: python

   numbers = [1, 2, 3, 4, 5, 6]
   evens = list(filter(lambda x: x % 2 == 0, numbers))
   print(evens)  # [2, 4, 6]

**reduce() - Reduce sequence to single value**

.. code-block:: python

   from functools import reduce

   numbers = [1, 2, 3, 4, 5]
   product = reduce(lambda x, y: x * y, numbers)
   print(product)  # 120

Function Best Practices
-----------------------

**Docstrings**

.. code-block:: python

   def calculate_area(radius):
       """
       Calculate the area of a circle given its radius.

       Args:
           radius (float): The radius of the circle

       Returns:
           float: The area of the circle

       Raises:
           ValueError: If radius is negative
       """
       if radius < 0:
           raise ValueError("Radius cannot be negative")
       return 3.14159 * radius ** 2

**Type Hints (Python 3.5+)**

.. code-block:: python

   from typing import List, Dict

   def process_students(students: List[Dict[str, str]]) -> Dict[str, int]:
       grades = {}
       for student in students:
           grades[student["name"]] = int(student["grade"])
       return grades

**Error Handling in Functions**

.. code-block:: python

   def divide_numbers(a: float, b: float) -> float:
       """
       Divide two numbers with error handling.
       """
       try:
           return a / b
       except ZeroDivisionError:
           print("Error: Division by zero!")
           return None
       except TypeError:
           print("Error: Invalid input types!")
           return None

   print(divide_numbers(10, 2))   # 5.0
   print(divide_numbers(10, 0))   # Error message, None

Recursion Limits and Optimization
---------------------------------

.. code-block:: python

   import sys

   # Check recursion limit
   print(f"Recursion limit: {sys.getrecursionlimit()}")

   # Set new limit (careful!)
   # sys.setrecursionlimit(2000)

**Tail Recursion Optimization (Conceptual)**

.. code-block:: python

   # Not tail recursive
   def factorial(n):
       if n <= 1:
           return 1
       return n * factorial(n - 1)  # Multiplication after recursion

   # Tail recursive (conceptual - Python doesn't optimize this)
   def factorial_tail(n, accumulator=1):
       if n <= 1:
           return accumulator
       return factorial_tail(n - 1, n * accumulator)  # No operation after recursion

   print(factorial(5))
   print(factorial_tail(5))