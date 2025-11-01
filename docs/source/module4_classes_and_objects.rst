.. _module4_classes_and_objects:

Classes and Objects in Python
==============================

Introduction
------------

Object-Oriented Programming (OOP) is a programming paradigm that organizes code into objects, which are instances of classes. Python is a multi-paradigm language that fully supports OOP.

.. note::
   A **class** is a blueprint for creating objects. An **object** is an instance of a class that contains actual data.

--------------

What is a Class?
----------------

A class defines the structure and behavior of objects. It contains:

- **Attributes** (variables): Data stored in the object
- **Methods** (functions): Actions that the object can perform

**Syntax:**

.. code-block:: python

   class ClassName:
       # Class body
       pass

--------------

Creating Your First Class
--------------------------

.. code-block:: python

   # Simple class definition
   class Dog:
       pass

   # Creating an object (instance) of the class
   my_dog = Dog()
   print(type(my_dog))  # <class '__main__.Dog'>

.. note::
   By convention, class names use **PascalCase** (capitalize the first letter of each word).

--------------

Instance Variables and Methods
-------------------------------

**Instance Variables**

Instance variables are unique to each object and store the object's data.

.. code-block:: python

   class Student:
       # Instance method to set data
       def set_data(self, name, roll_no):
           self.name = name        # Instance variable
           self.roll_no = roll_no  # Instance variable

   # Creating objects
   student1 = Student()
   student1.set_data("Alice", 101)

   student2 = Student()
   student2.set_data("Bob", 102)

   print(student1.name)     # Alice
   print(student2.roll_no)  # 102

**Instance Methods**

Instance methods are functions defined inside a class that operate on the object's data. The first parameter is always ``self``, which refers to the current object.

.. code-block:: python

   class Calculator:
       def set_numbers(self, a, b):
           self.num1 = a
           self.num2 = b
       
       def add(self):
           return self.num1 + self.num2
       
       def multiply(self):
           return self.num1 * self.num2

   # Using the class
   calc = Calculator()
   calc.set_numbers(10, 5)
   print(calc.add())       # 15
   print(calc.multiply())  # 50

--------------

Understanding ``self``
----------------------

The ``self`` parameter represents the current instance of the class. It allows you to access the object's attributes and methods.

.. code-block:: python

   class Person:
       def set_name(self, name):
           self.name = name  # self.name belongs to this object
       
       def greet(self):
           return f"Hello, my name is {self.name}"

   # Create two different objects
   person1 = Person()
   person1.set_name("Charlie")

   person2 = Person()
   person2.set_name("Diana")

   print(person1.greet())  # Hello, my name is Charlie
   print(person2.greet())  # Hello, my name is Diana

.. note::
   The name ``self`` is a convention, not a keyword. You can use any name, but ``self`` is universally recognized.

--------------

Real-World Example: Bank Account
---------------------------------

.. code-block:: python

   class BankAccount:
       def create_account(self, account_holder, balance):
           self.account_holder = account_holder
           self.balance = balance
       
       def deposit(self, amount):
           if amount > 0:
               self.balance += amount
               return f"Deposited ₹{amount}. New balance: ₹{self.balance}"
           return "Invalid amount"
       
       def withdraw(self, amount):
           if amount > 0 and amount <= self.balance:
               self.balance -= amount
               return f"Withdrew ₹{amount}. Remaining balance: ₹{self.balance}"
           return "Insufficient funds or invalid amount"
       
       def check_balance(self):
           return f"Account holder: {self.account_holder}, Balance: ₹{self.balance}"

   # Using the BankAccount class
   account = BankAccount()
   account.create_account("John Doe", 5000)

   print(account.check_balance())  # Account holder: John Doe, Balance: ₹5000
   print(account.deposit(2000))    # Deposited ₹2000. New balance: ₹7000
   print(account.withdraw(1500))   # Withdrew ₹1500. Remaining balance: ₹5500

--------------

Class vs Instance
-----------------

.. code-block:: python

   class Car:
       # Class variable (shared by all instances)
       wheels = 4
       
       def set_details(self, brand, model):
           # Instance variables (unique to each object)
           self.brand = brand
           self.model = model
       
       def display(self):
           return f"{self.brand} {self.model} has {Car.wheels} wheels"

   car1 = Car()
   car1.set_details("Toyota", "Camry")

   car2 = Car()
   car2.set_details("Honda", "Civic")

   print(car1.display())  # Toyota Camry has 4 wheels
   print(car2.display())  # Honda Civic has 4 wheels

   # Class variable is shared
   print(Car.wheels)      # 4

.. note::
   **Class variables** are shared among all instances, while **instance variables** are unique to each object.

--------------

Example: Library Book System
-----------------------------

.. code-block:: python

   class Book:
       def set_book_info(self, title, author, isbn):
           self.title = title
           self.author = author
           self.isbn = isbn
           self.is_available = True
       
       def borrow(self):
           if self.is_available:
               self.is_available = False
               return f"'{self.title}' has been borrowed"
           return f"'{self.title}' is not available"
       
       def return_book(self):
           self.is_available = True
           return f"'{self.title}' has been returned"
       
       def display_info(self):
           status = "Available" if self.is_available else "Not Available"
           return f"Title: {self.title}\nAuthor: {self.author}\nISBN: {self.isbn}\nStatus: {status}"

   # Create book objects
   book1 = Book()
   book1.set_book_info("Python Programming", "John Smith", "978-1234567890")

   print(book1.display_info())
   print(book1.borrow())
   print(book1.display_info())
   print(book1.return_book())

--------------

Tasks
-----

**Task 1: Create a Rectangle Class**

Create a class ``Rectangle`` with methods to set length and width, and calculate area and perimeter.

*Hint:* Use instance variables ``self.length`` and ``self.width``. Area = length × width, Perimeter = 2 × (length + width).

**Task 2: Student Grade Manager**

Create a class ``Student`` that stores a student's name and three subject marks. Add methods to calculate the total marks and average marks.

*Hint:* Use instance variables for name and marks. Total = sum of all marks, Average = total / number of subjects.

**Task 3: Temperature Converter**

Create a class ``Temperature`` with methods to set temperature in Celsius and convert it to Fahrenheit and Kelvin.

*Hint:* Fahrenheit = (Celsius × 9/5) + 32, Kelvin = Celsius + 273.15.

**Task 4: Shopping Cart**

Create a class ``ShoppingCart`` with methods to add items (with prices), remove items, and calculate the total price.

*Hint:* Use a list to store items and their prices. You can use a list of dictionaries like ``[{'name': 'item1', 'price': 100}]``.

**Task 5: Employee Management**

Create a class ``Employee`` with methods to set employee details (name, ID, salary) and give a raise (increase salary by a given percentage).

*Hint:* Store name, ID, and salary as instance variables. For a 10% raise: ``new_salary = old_salary * 1.10``.

--------------

Summary
-------

- Classes are blueprints for creating objects
- Objects are instances of classes with their own data
- Instance variables store object-specific data
- Instance methods define object behavior
- The ``self`` parameter refers to the current object
- Multiple objects of the same class can exist independently
