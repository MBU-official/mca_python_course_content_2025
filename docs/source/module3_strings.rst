.. _module3_strings:

Strings in Python
=================

Strings are sequences of characters used to represent text data.

String Creation
---------------

.. code-block:: python

   # Single quotes
   name = 'Alice'

   # Double quotes
   greeting = "Hello, World!"

   # Triple quotes for multi-line strings
   poem = """Roses are red,
   Violets are blue,
   Python is great,
   And so are you!"""

   print(name)
   print(greeting)
   print(poem)

**Escape Sequences**

.. code-block:: python

   # Common escape sequences
   text = "Hello\nWorld"        # Newline
   text = "Hello\tWorld"        # Tab
   text = "He said \"Hello\""    # Double quote
   text = 'It\'s raining'        # Single quote
   text = "Path: C:\\folder"     # Backslash

**Raw Strings** (ignore escape sequences)

.. code-block:: python

   # Raw string
   path = r"C:\Users\Documents\file.txt"
   print(path)  # C:\Users\Documents\file.txt

String Indexing
---------------

Strings are indexed, starting from 0.

.. code-block:: python

   text = "Python"

   print(text[0])   # P
   print(text[1])   # y
   print(text[-1])  # n (last character)
   print(text[-2])  # o (second to last)

String Slicing
--------------

Extract substrings using slicing. Slicing uses the syntax `string[start:end:step]`.

**Basic slicing syntax:**

.. code-block:: python

   text = "Hello, World!"

   # [start:end] - extract from start to end-1
   print(text[0:5])    # Hello (characters at indices 0,1,2,3,4)
   print(text[7:12])   # World (characters at indices 7,8,9,10,11)

   # [:end] - from beginning to end-1
   print(text[:5])     # Hello (same as text[0:5])

   # [start:] - from start to end of string
   print(text[7:])     # World! (from index 7 to end)

   # [:] - entire string
   print(text[:])      # Hello, World! (copy of whole string)

**Step parameter for advanced slicing:**

.. code-block:: python

   text = "Hello, World!"

   # [::step] - every step-th character
   print(text[::2])    # Hlo ol! (every 2nd character)
   print(text[1::2])   # el,Wrd (every 2nd character starting from index 1)

   # Negative step - reverse direction
   print(text[::-1])   # !dlroW ,olleH (reverse the string)
   print(text[::-2])   # !lo le (reverse, every 2nd character)

**Negative indices:**

.. code-block:: python

   text = "Python"

   print(text[-1])     # n (last character)
   print(text[-2])     # o (second to last)
   print(text[-3:])    # hon (last 3 characters)
   print(text[:-2])    # Pyth (all except last 2)

**Practical slicing examples:**

.. code-block:: python

   # Extract domain from email
   email = "user@example.com"
   domain = email.split("@")[1]
   print(domain)  # example.com

   # Or using slicing (if you know the position)
   at_index = email.find("@")
   if at_index != -1:
       domain = email[at_index + 1:]
       print(domain)  # example.com

   # Remove file extension
   filename = "document.txt"
   name_without_ext = filename[:-4]  # Remove last 4 characters (.txt)
   print(name_without_ext)  # document

   # Get first and last n characters
   text = "Hello, World!"
   first_3 = text[:3]      # Hel
   last_3 = text[-3:]      # ld!
   print(f"First 3: {first_3}, Last 3: {last_3}")

   # Skip characters from both ends
   text = "xxxHello, World!xxx"
   cleaned = text[3:-3]    # Remove 3 chars from start and end
   print(cleaned)          # Hello, World!

**String slicing vs string methods:**

.. code-block:: python

   text = "  Hello, World!  "

   # Using slicing
   trimmed = text[2:-2]    # Manual trimming
   print(repr(trimmed))    # 'Hello, World!'

   # Using string methods (better)
   trimmed = text.strip()
   print(repr(trimmed))    # 'Hello, World!'

**Slicing creates new strings (immutable behavior):**

.. code-block:: python

   original = "Python"
   sliced = original[1:4]  # "yth"

   print(original)  # Python (unchanged)
   print(sliced)    # yth (new string)

   # Strings are immutable - this would error:
   # original[0] = "J"  # TypeError!

String Immutability
-------------------

Strings cannot be changed after creation.

.. code-block:: python

   text = "Hello"
   # text[0] = "h"  # This will cause an error

   # To "modify" a string, create a new one
   new_text = "h" + text[1:]
   print(new_text)  # hello

String Methods - Character Case
-------------------------------

**upper()** - Convert to uppercase

.. code-block:: python

   text = "hello world"
   print(text.upper())  # HELLO WORLD

**lower()** - Convert to lowercase

.. code-block:: python

   text = "HELLO WORLD"
   print(text.lower())  # hello world

**capitalize()** - Capitalize first letter

.. code-block:: python

   text = "hello world"
   print(text.capitalize())  # Hello world

**title()** - Capitalize first letter of each word

.. code-block:: python

   text = "hello world python"
   print(text.title())  # Hello World Python

**swapcase()** - Swap case of all characters

.. code-block:: python

   text = "Hello World"
   print(text.swapcase())  # hELLO wORLD

**find()** - Find the position of a substring

.. code-block:: python

   text = "Hello, World!"
   print(text.find("World"))  # 7
   print(text.find("Python")) # -1 (not found)

**rfind()** - Find from the right

.. code-block:: python

   text = "Hello, World, Hello!"
   print(text.rfind("Hello"))  # 13

**index()** - Like find() but raises ValueError if not found

.. code-block:: python

   text = "Hello, World!"
   print(text.index("World"))  # 7
   # print(text.index("Python"))  # ValueError!

**count()** - Count occurrences of substring

.. code-block:: python

   text = "hello hello world"
   print(text.count("hello"))  # 2

**replace()** - Replace occurrences of a substring

.. code-block:: python

   text = "Hello, World!"
   new_text = text.replace("World", "Python")
   print(new_text)  # Hello, Python!

   # Replace multiple occurrences
   text = "cat cat cat"
   print(text.replace("cat", "dog"))  # dog dog dog

**split()** - Split string into a list

.. code-block:: python

   text = "apple,banana,cherry"
   fruits = text.split(",")
   print(fruits)  # ['apple', 'banana', 'cherry']

   # Split by whitespace
   text = "Hello World Python"
   words = text.split()
   print(words)  # ['Hello', 'World', 'Python']

   # Limit splits
   text = "a,b,c,d,e"
   parts = text.split(",", 2)
   print(parts)  # ['a', 'b', 'c,d,e']

**join()** - Join elements of a list into a string

.. code-block:: python

   fruits = ['apple', 'banana', 'cherry']
   text = ", ".join(fruits)
   print(text)  # apple, banana, cherry

   # Join with different separator
   text = "-".join(fruits)
   print(text)  # apple-banana-cherry

Other Useful String Methods
---------------------------

.. code-block:: python

   text = "  Hello, World!  "

   # strip() - Remove whitespace from both ends
   print(text.strip())  # "Hello, World!"

   # lstrip() - Remove whitespace from left
   print(text.lstrip())  # "Hello, World!  "

   # rstrip() - Remove whitespace from right
   print(text.rstrip())  # "  Hello, World!"

   text = "Python Programming"

   # startswith() - Check if string starts with substring
   print(text.startswith("Python"))  # True

   # endswith() - Check if string ends with substring
   print(text.endswith("ming"))  # True

   # count() - Count occurrences of substring
   print(text.count("m"))  # 2

   # capitalize() - Capitalize first letter
   print(text.capitalize())  # Python programming

   # title() - Capitalize first letter of each word
   print(text.title())  # Python Programming

   # isalpha() - Check if all characters are alphabetic
   print("Python".isalpha())  # True
   print("Python3".isalpha())  # False

   # isdigit() - Check if all characters are digits
   print("123".isdigit())  # True
   print("123abc".isdigit())  # False

   # isalnum() - Check if all characters are alphanumeric
   print("Python123".isalnum())  # True
   print("Python 123".isalnum())  # False (space is not alphanumeric)

String Formatting
-----------------

**Using f-strings (Python 3.6+)**

.. code-block:: python

   name = "Alice"
   age = 25
   print(f"My name is {name} and I am {age} years old.")

**Using format() method**

.. code-block:: python

   name = "Alice"
   age = 25
   print("My name is {} and I am {} years old.".format(name, age))

   # With positional arguments
   print("My name is {0} and I am {1} years old.".format(name, age))

   # With keyword arguments
   print("My name is {name} and I am {age} years old.".format(name=name, age=age))

**Using % formatting (older style)**

.. code-block:: python

   name = "Alice"
   age = 25
   print("My name is %s and I am %d years old." % (name, age))

String Operations and Tricks
-----------------------------

**String concatenation**

.. code-block:: python

   # Using +
   greeting = "Hello" + " " + "World"
   print(greeting)  # Hello World

   # Using join (more efficient for many strings)
   words = ["Hello", "World"]
   greeting = " ".join(words)
   print(greeting)  # Hello World

**String repetition**

.. code-block:: python

   print("Ha" * 3)  # HaHaHa

**String length**

.. code-block:: python

   text = "Hello"
   print(len(text))  # 5

**Check if substring exists**

.. code-block:: python

   text = "Hello, World!"
   print("World" in text)  # True
   print("Python" not in text)  # True

**String comparison**

.. code-block:: python

   print("apple" < "banana")  # True (lexicographical order)
   print("Apple" < "apple")   # True (ASCII order)

Common String Use Cases
-----------------------

**Parsing CSV data**

.. code-block:: python

   csv_line = "Alice,25,Engineer"
   name, age, profession = csv_line.split(",")
   print(f"Name: {name}, Age: {age}, Profession: {profession}")

**URL parsing**

.. code-block:: python

   url = "https://www.example.com/path?param=value"
   if url.startswith("https://"):
       print("Secure connection")
   domain = url.split("/")[2]
   print(f"Domain: {domain}")

**Text processing**

.. code-block:: python

   text = "This is a SAMPLE text with MIXED case."
   # Normalize to title case
   normalized = text.lower().capitalize()
   print(normalized)

**Password validation**

.. code-block:: python

   password = "MyPass123"
   has_upper = any(c.isupper() for c in password)
   has_lower = any(c.islower() for c in password)
   has_digit = any(c.isdigit() for c in password)
   is_valid = len(password) >= 8 and has_upper and has_lower and has_digit
   print(f"Password valid: {is_valid}")

String Performance Tips
-----------------------

- Use `join()` instead of `+` for concatenating many strings
- Use `in` operator for substring checking (more efficient than `find()`)
- Prefer f-strings for formatting (fastest and most readable)
- Use string methods instead of manual loops when possible

String Encoding
---------------

.. code-block:: python

   # Strings are Unicode in Python 3
   text = "Hello, 世界"
   print(text.encode('utf-8'))  # b'Hello, \xe4\xb8\x96\xe7\x95\x8c'

   # Decode bytes back to string
   bytes_data = b'Hello, \xe4\xb8\x96\xe7\x95\x8c'
   decoded = bytes_data.decode('utf-8')
   print(decoded)  # Hello, 世界