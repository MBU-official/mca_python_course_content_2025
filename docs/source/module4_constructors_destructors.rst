.. _module4_constructors_destructors:

Constructors and Destructors in Python
=======================================

Introduction
------------

Constructors and destructors are special methods that automatically execute when objects are created or destroyed. They help initialize and clean up object resources.

.. note::
   A **constructor** is called when an object is created. A **destructor** is called when an object is destroyed or goes out of scope.

--------------

The Constructor: ``__init__()``
--------------------------------

The ``__init__()`` method is a special method called automatically when you create an object. It initializes the object's attributes.

**Syntax:**

.. code-block:: python

   class ClassName:
       def __init__(self, parameters):
           # Initialize instance variables
           self.variable = value

**Why Use Constructors?**

Without a constructor, you need to manually call methods to set up an object. Constructors make initialization automatic and cleaner.

.. code-block:: python

   # Without constructor (manual setup)
   class Student:
       def set_data(self, name, age):
           self.name = name
           self.age = age

   student = Student()
   student.set_data("Alice", 20)  # Manual initialization

   # With constructor (automatic setup)
   class Student:
       def __init__(self, name, age):
           self.name = name
           self.age = age

   student = Student("Alice", 20)  # Automatic initialization

--------------

Basic Constructor Example
--------------------------

.. code-block:: python

   class Person:
       def __init__(self, name, age):
           self.name = name
           self.age = age
           print(f"Object created for {self.name}")
       
       def display(self):
           return f"Name: {self.name}, Age: {self.age}"

   # Creating objects - constructor is called automatically
   person1 = Person("Bob", 25)      # Output: Object created for Bob
   person2 = Person("Charlie", 30)  # Output: Object created for Charlie

   print(person1.display())  # Name: Bob, Age: 25
   print(person2.display())  # Name: Charlie, Age: 30

--------------

Constructor with Default Parameters
------------------------------------

You can provide default values for constructor parameters.

.. code-block:: python

   class Book:
       def __init__(self, title, author, pages=100, price=0):
           self.title = title
           self.author = author
           self.pages = pages
           self.price = price
       
       def display(self):
           return f"{self.title} by {self.author} - {self.pages} pages, ₹{self.price}"

   # Using default values
   book1 = Book("Python Basics", "John Doe")
   print(book1.display())  # Python Basics by John Doe - 100 pages, ₹0

   # Providing all values
   book2 = Book("Advanced Python", "Jane Smith", 300, 599)
   print(book2.display())  # Advanced Python by Jane Smith - 300 pages, ₹599

   # Using keyword arguments
   book3 = Book("Data Science", "Alex Brown", price=799)
   print(book3.display())  # Data Science by Alex Brown - 100 pages, ₹799

.. note::
   Default parameters must come after non-default parameters in the constructor definition.

--------------

Constructor Overloading in Python
----------------------------------

Unlike languages like Java or C++, Python doesn't support traditional method overloading (multiple methods with the same name but different parameters). However, we can simulate constructor overloading using default arguments and flexible parameter handling.

**Method 1: Using Default Arguments**

.. code-block:: python

   class Employee:
       def __init__(self, name, emp_id=None, salary=0, department="General"):
           self.name = name
           self.emp_id = emp_id or f"EMP{hash(name) % 10000:04d}"
           self.salary = salary
           self.department = department
       
       def display(self):
           return f"Employee: {self.name} (ID: {self.emp_id}), Salary: ₹{self.salary}, Dept: {self.department}"

   # Different ways to create Employee objects (simulating overloading)
   emp1 = Employee("Alice")  # Only name
   emp2 = Employee("Bob", "EMP001")  # Name and ID
   emp3 = Employee("Charlie", "EMP002", 50000)  # Name, ID, and salary
   emp4 = Employee("Diana", "EMP003", 60000, "IT")  # All parameters

   print(emp1.display())
   print(emp2.display())
   print(emp3.display())
   print(emp4.display())

**Method 2: Using *args and **kwargs**

.. code-block:: python

   class Product:
       def __init__(self, *args, **kwargs):
           if len(args) == 1:
               # Single argument: assume it's name
               self.name = args[0]
               self.price = 0
               self.category = "General"
           elif len(args) == 2:
               # Two arguments: name and price
               self.name, self.price = args
               self.category = "General"
           elif len(args) == 3:
               # Three arguments: name, price, and category
               self.name, self.price, self.category = args
           else:
               # Use keyword arguments
               self.name = kwargs.get('name', 'Unknown')
               self.price = kwargs.get('price', 0)
               self.category = kwargs.get('category', 'General')
       
       def display(self):
           return f"Product: {self.name}, Price: ₹{self.price}, Category: {self.category}"

   # Different constructor calls
   product1 = Product("Laptop")
   product2 = Product("Mouse", 500)
   product3 = Product("Keyboard", 1500, "Electronics")
   product4 = Product(name="Monitor", price=15000, category="Electronics")

   for product in [product1, product2, product3, product4]:
       print(product.display())

**Method 3: Using Class Methods as Alternative Constructors**

.. code-block:: python

   class Student:
       def __init__(self, name, roll_no, grade):
           self.name = name
           self.roll_no = roll_no
           self.grade = grade
       
       @classmethod
       def from_string(cls, student_string):
           """Alternative constructor from comma-separated string"""
           name, roll_no, grade = student_string.split(',')
           return cls(name.strip(), roll_no.strip(), float(grade.strip()))
       
       @classmethod
       def from_dict(cls, student_dict):
           """Alternative constructor from dictionary"""
           return cls(student_dict['name'], student_dict['roll_no'], student_dict['grade'])
       
       @classmethod
       def default_student(cls, name):
           """Alternative constructor with default values"""
           return cls(name, "TEMP001", 0.0)
       
       def display(self):
           return f"Student: {self.name}, Roll: {self.roll_no}, Grade: {self.grade}"

   # Using different "constructors"
   student1 = Student("Alice", "MCA001", 85.5)  # Regular constructor
   student2 = Student.from_string("Bob, MCA002, 78.0")  # From string
   student3 = Student.from_dict({'name': 'Charlie', 'roll_no': 'MCA003', 'grade': 92.0})  # From dict
   student4 = Student.default_student("Diana")  # Default student

   for student in [student1, student2, student3, student4]:
       print(student.display())

.. note::
   **Constructor overloading** in Python is achieved through default arguments, flexible parameter handling, or class methods. This provides multiple ways to create objects while maintaining a single ``__init__`` method or using alternative constructors.

--------------

Real-World Example: Bank Account
---------------------------------

.. code-block:: python

   class BankAccount:
       def __init__(self, account_number, holder_name, initial_balance=0):
           self.account_number = account_number
           self.holder_name = holder_name
           self.balance = initial_balance
           print(f"Account {self.account_number} created for {self.holder_name}")
       
       def deposit(self, amount):
           if amount > 0:
               self.balance += amount
               return f"Deposited ₹{amount}. New balance: ₹{self.balance}"
           return "Invalid amount"
       
       def get_balance(self):
           return f"Account: {self.account_number}, Balance: ₹{self.balance}"

   # Creating accounts with constructor
   account1 = BankAccount("ACC001", "John", 5000)
   account2 = BankAccount("ACC002", "Mary")  # Uses default balance of 0

   print(account1.get_balance())  # Account: ACC001, Balance: ₹5000
   print(account2.get_balance())  # Account: ACC002, Balance: ₹0

--------------

The Destructor: ``__del__()``
------------------------------

The ``__del__()`` method is called when an object is about to be destroyed. It's useful for cleanup operations like closing files or database connections.

**Syntax:**

.. code-block:: python

   class ClassName:
       def __del__(self):
           # Cleanup code
           print("Object is being destroyed")

.. note::
   Python's garbage collector automatically manages memory, so destructors are rarely needed in practice. They're mainly used for resource cleanup.

--------------

Destructor Example
------------------

.. code-block:: python

   class FileHandler:
       def __init__(self, filename):
           self.filename = filename
           print(f"Opening file: {self.filename}")
       
       def __del__(self):
           print(f"Closing file: {self.filename}")

   # Creating and destroying objects
   file1 = FileHandler("data.txt")
   # Output: Opening file: data.txt

   file2 = FileHandler("config.txt")
   # Output: Opening file: config.txt

   del file1  # Manually delete object
   # Output: Closing file: data.txt

   # file2 will be destroyed when program ends
   # Output: Closing file: config.txt

--------------

Constructor and Destructor Together
------------------------------------

.. code-block:: python

   class DatabaseConnection:
       def __init__(self, db_name):
           self.db_name = db_name
           self.connected = True
           print(f"✓ Connected to database: {self.db_name}")
       
       def execute_query(self, query):
           if self.connected:
               return f"Executing query on {self.db_name}: {query}"
           return "Not connected"
       
       def __del__(self):
           self.connected = False
           print(f"✗ Disconnected from database: {self.db_name}")

   # Using the class
   db = DatabaseConnection("students_db")
   # Output: ✓ Connected to database: students_db

   print(db.execute_query("SELECT * FROM students"))
   # Output: Executing query on students_db: SELECT * FROM students

   # When program ends or object is deleted:
   # Output: ✗ Disconnected from database: students_db

--------------

Complete Example: Student Management
-------------------------------------

.. code-block:: python

   class Student:
       # Class variable to track total students
       total_students = 0
       
       def __init__(self, name, roll_no, branch):
           self.name = name
           self.roll_no = roll_no
           self.branch = branch
           self.marks = []
           Student.total_students += 1
           print(f"Student {self.name} (Roll: {self.roll_no}) enrolled")
       
       def add_marks(self, subject, marks):
           self.marks.append({'subject': subject, 'marks': marks})
       
       def get_average(self):
           if not self.marks:
               return 0
           total = sum(item['marks'] for item in self.marks)
           return total / len(self.marks)
       
       def display(self):
           avg = self.get_average()
           return f"Name: {self.name}, Roll: {self.roll_no}, Branch: {self.branch}, Average: {avg:.2f}"
       
       def __del__(self):
           Student.total_students -= 1
           print(f"Student {self.name} record deleted")

   # Creating students
   s1 = Student("Alice", "MCA001", "Computer Science")
   s1.add_marks("Python", 85)
   s1.add_marks("Data Structures", 90)

   s2 = Student("Bob", "MCA002", "Computer Science")
   s2.add_marks("Python", 78)
   s2.add_marks("Data Structures", 82)

   print(s1.display())
   print(s2.display())
   print(f"Total students: {Student.total_students}")

   # Deleting an object
   del s1
   print(f"Total students: {Student.total_students}")

--------------

Understanding ``self`` in Constructor
--------------------------------------

The ``self`` parameter in ``__init__()`` refers to the object being created.

.. code-block:: python

   class Circle:
       def __init__(self, radius):
           self.radius = radius  # self refers to the current object
           self.pi = 3.14159
       
       def area(self):
           return self.pi * self.radius ** 2
       
       def circumference(self):
           return 2 * self.pi * self.radius

   circle1 = Circle(5)
   circle2 = Circle(10)

   print(f"Circle 1 - Area: {circle1.area():.2f}, Circumference: {circle1.circumference():.2f}")
   print(f"Circle 2 - Area: {circle2.area():.2f}, Circumference: {circle2.circumference():.2f}")

.. note::
   Each object has its own copy of instance variables. ``self.radius`` in ``circle1`` is different from ``self.radius`` in ``circle2``.

--------------

Tasks
-----

**Task 1: Create a Car Class**

Create a class ``Car`` with a constructor that accepts brand, model, and year. Add a method to display car information. Create at least 3 car objects.

*Hint:* Use ``__init__(self, brand, model, year)`` and store values in instance variables.

**Task 2: Product Inventory**

Create a class ``Product`` with a constructor for product name, price, and quantity (default=0). Add methods to add stock, remove stock, and calculate total value (price × quantity).

*Hint:* Use default parameter for quantity. Total value = ``self.price * self.quantity``.

**Task 3: Library Member**

Create a class ``LibraryMember`` with constructor for member name and ID. Use a destructor to print a message when a member is removed. Track how many books the member has borrowed using a list.

*Hint:* Use ``__del__()`` to print removal message. Use ``self.borrowed_books = []`` to track books.

**Task 4: Temperature Monitor**

Create a class ``TemperatureMonitor`` with constructor accepting location name. Add methods to record temperatures (store in a list) and calculate average temperature. Add destructor to show monitoring has ended.

*Hint:* Store temperatures in a list. Average = sum of temperatures / count.

**Task 5: Employee Counter**

Create a class ``Employee`` with a class variable to count total employees. Use constructor to increment count when employee is created and destructor to decrement when deleted. Display total employee count.

*Hint:* Use a class variable like ``Employee.count = 0``. Increment in ``__init__()``, decrement in ``__del__()``.

--------------

Summary
-------

- ``__init__()`` is the constructor, called when an object is created
- Constructors initialize instance variables automatically
- You can use default parameters in constructors
- ``__del__()`` is the destructor, called when an object is destroyed
- Destructors are used for cleanup operations (less common in Python)
- ``self`` in constructor refers to the object being created
- Constructors make object initialization clean and automatic
