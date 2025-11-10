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

Static Methods vs Instance Methods
-----------------------------------

Understanding the difference between static methods and instance methods is crucial for effective class design.

**Instance Methods**

Instance methods are the default type of methods in a class. They:
- Require ``self`` as the first parameter
- Can access and modify instance variables
- Can access class variables
- Are called on object instances

**Static Methods**

Static methods are marked with ``@staticmethod`` decorator. They:
- Don't require ``self`` or ``cls`` parameters
- Cannot access instance or class variables directly
- Are utility functions that belong logically to the class
- Can be called on the class itself or instances

**Class Methods** (Bonus)

Class methods are marked with ``@classmethod`` decorator. They:
- Require ``cls`` as the first parameter (refers to the class)
- Can access class variables but not instance variables
- Are often used as alternative constructors

.. code-block:: python

   import math

   class MathUtility:
       # Class variable
       pi = 3.14159
       
       def __init__(self, name):
           # Instance variable
           self.calculator_name = name
       
       # Instance method
       def get_calculator_info(self):
           return f"Calculator: {self.calculator_name}"
       
       # Static method - utility function
       @staticmethod
       def add_numbers(a, b):
           """Add two numbers - doesn't need class or instance data"""
           return a + b
       
       @staticmethod
       def is_even(number):
           """Check if number is even - pure utility function"""
           return number % 2 == 0
       
       @staticmethod
       def factorial(n):
           """Calculate factorial - mathematical utility"""
           if n <= 1:
               return 1
           return n * MathUtility.factorial(n - 1)
       
       # Class method
       @classmethod
       def circle_area(cls, radius):
           """Calculate circle area using class variable pi"""
           return cls.pi * radius * radius
       
       # Instance method that uses static method
       def calculate_and_log(self, a, b):
           result = self.add_numbers(a, b)  # Can call static method from instance
           return f"{self.calculator_name} calculated: {a} + {b} = {result}"

   # Using static methods - can call without creating objects
   print("=== Static Methods (No Object Needed) ===")
   print(f"5 + 3 = {MathUtility.add_numbers(5, 3)}")
   print(f"Is 8 even? {MathUtility.is_even(8)}")
   print(f"Factorial of 5: {MathUtility.factorial(5)}")

   # Using class method
   print(f"Circle area (radius=5): {MathUtility.circle_area(5)}")

   # Creating objects and using instance methods
   print("\n=== Instance Methods (Need Object) ===")
   calc1 = MathUtility("Scientific Calculator")
   calc2 = MathUtility("Basic Calculator")

   print(calc1.get_calculator_info())
   print(calc2.get_calculator_info())

   # Instance methods can call static methods
   print(calc1.calculate_and_log(10, 20))

   # Static methods can also be called on instances
   print(f"Using static method on instance: {calc1.add_numbers(100, 200)}")

**Real-World Example: Student Management System**

.. code-block:: python

   class Student:
       # Class variables
       total_students = 0
       school_name = "MBU College"
       
       def __init__(self, name, roll_no):
           # Instance variables
           self.name = name
           self.roll_no = roll_no
           self.grades = []
           Student.total_students += 1
       
       # Instance method
       def add_grade(self, subject, marks):
           """Add grade for a student"""
           self.grades.append({'subject': subject, 'marks': marks})
       
       # Instance method
       def get_average(self):
           """Calculate student's average marks"""
           if not self.grades:
               return 0
           total = sum(grade['marks'] for grade in self.grades)
           return total / len(self.grades)
       
       # Static method - utility functions
       @staticmethod
       def is_passing_grade(marks):
           """Check if marks are passing (>= 40)"""
           return marks >= 40
       
       @staticmethod
       def grade_to_letter(marks):
           """Convert numerical grade to letter grade"""
           if marks >= 90:
               return 'A+'
           elif marks >= 80:
               return 'A'
           elif marks >= 70:
               return 'B'
           elif marks >= 60:
               return 'C'
           elif marks >= 40:
               return 'D'
           else:
               return 'F'
       
       @staticmethod
       def calculate_percentage(obtained, total):
           """Calculate percentage - pure math function"""
           return (obtained / total) * 100
       
       # Class method
       @classmethod
       def get_school_info(cls):
           """Get information about the school and total students"""
           return f"School: {cls.school_name}, Total Students: {cls.total_students}"
       
       @classmethod
       def create_honor_student(cls, name):
           """Alternative constructor for honor students"""
           student = cls(name, f"HON{cls.total_students:03d}")
           student.add_grade("Overall", 95)
           return student
       
       # Instance method using static methods
       def display_report(self):
           avg = self.get_average()
           letter_grade = self.grade_to_letter(avg)  # Using static method
           passing = self.is_passing_grade(avg)      # Using static method
           
           return f"""
   Student Report Card
   Name: {self.name}
   Roll No: {self.roll_no}
   Average: {avg:.1f} ({letter_grade})
   Status: {'Passing' if passing else 'Failing'}
   """

   # Demonstrate usage
   print("=== Static Methods Demo ===")
   print(f"Is 85 passing? {Student.is_passing_grade(85)}")
   print(f"Grade for 92: {Student.grade_to_letter(92)}")
   print(f"Percentage: {Student.calculate_percentage(450, 500)}%")

   print("\n=== Class Methods Demo ===")
   print(Student.get_school_info())

   print("\n=== Creating Students ===")
   student1 = Student("Alice", "CS001")
   student1.add_grade("Python", 85)
   student1.add_grade("Java", 78)
   student1.add_grade("WebDev", 92)

   student2 = Student.create_honor_student("Bob")

   print(student1.display_report())
   print(student2.display_report())
   print(Student.get_school_info())

**When to Use Each Type:**

- **Instance Methods**: When you need to work with specific object data
- **Static Methods**: For utility functions that are related to the class but don't need access to instance or class data
- **Class Methods**: When you need to work with class data or create alternative constructors

.. note::
   **Static methods** are like independent functions that happen to be grouped with a class for organizational purposes. They don't need ``self`` and can be called without creating objects!

--------------

Dynamic Attribute Addition
---------------------------

Python allows you to add, modify, and delete attributes of objects at runtime. This dynamic nature makes Python very flexible but should be used carefully.

**Adding Attributes Dynamically**

.. code-block:: python

   class Person:
       def __init__(self, name, age):
           self.name = name
           self.age = age
       
       def display(self):
           return f"Name: {self.name}, Age: {self.age}"

   # Create a person
   person = Person("Alice", 25)
   print(person.display())

   # Add attributes dynamically
   person.email = "alice@email.com"        # Direct assignment
   person.city = "Mumbai"
   person.is_student = True

   # Access new attributes
   print(f"Email: {person.email}")
   print(f"City: {person.city}")
   print(f"Is Student: {person.is_student}")

   # Check if attribute exists
   if hasattr(person, 'email'):
       print("Person has email attribute")

**Using setattr(), getattr(), hasattr(), delattr()**

.. code-block:: python

   class Product:
       def __init__(self, name, price):
           self.name = name
           self.price = price
       
       def display(self):
           """Display all attributes dynamically"""
           attributes = []
           for attr_name in dir(self):
               if not attr_name.startswith('_') and not callable(getattr(self, attr_name)):
                   attr_value = getattr(self, attr_name)
                   attributes.append(f"{attr_name}: {attr_value}")
           return "Product(" + ", ".join(attributes) + ")"

   product = Product("Laptop", 50000)
   print(product.display())

   # Add attributes using setattr
   setattr(product, 'brand', 'Dell')
   setattr(product, 'warranty_years', 3)
   setattr(product, 'in_stock', True)

   print(product.display())

   # Get attribute using getattr (with default value)
   brand = getattr(product, 'brand', 'Unknown Brand')
   color = getattr(product, 'color', 'Not specified')  # Default for missing attribute

   print(f"Brand: {brand}")
   print(f"Color: {color}")

   # Check if attribute exists
   print(f"Has brand? {hasattr(product, 'brand')}")
   print(f"Has color? {hasattr(product, 'color')}")

   # Delete attribute
   delattr(product, 'warranty_years')
   print(f"Has warranty_years after deletion? {hasattr(product, 'warranty_years')}")

**Dynamic Attribute Management System**

.. code-block:: python

   class FlexibleStudent:
       def __init__(self, name, roll_no):
           self.name = name
           self.roll_no = roll_no
           self._attributes = {}  # Store custom attributes separately
       
       def add_attribute(self, attr_name, attr_value):
           """Safely add custom attributes"""
           if not hasattr(self, attr_name):  # Don't override existing attributes
               setattr(self, attr_name, attr_value)
               self._attributes[attr_name] = attr_value
               print(f"Added {attr_name}: {attr_value}")
           else:
               print(f"Attribute {attr_name} already exists!")
       
       def update_attribute(self, attr_name, new_value):
           """Update existing attribute"""
           if hasattr(self, attr_name):
               setattr(self, attr_name, new_value)
               if attr_name in self._attributes:
                   self._attributes[attr_name] = new_value
               print(f"Updated {attr_name} to: {new_value}")
           else:
               print(f"Attribute {attr_name} doesn't exist! Use add_attribute() first.")
       
       def remove_attribute(self, attr_name):
           """Remove custom attribute"""
           if attr_name in self._attributes:
               delattr(self, attr_name)
               del self._attributes[attr_name]
               print(f"Removed {attr_name}")
           else:
               print(f"Cannot remove {attr_name} - not a custom attribute")
       
       def list_all_attributes(self):
           """List all attributes with their values"""
           print(f"\n=== Attributes for {self.name} ===")
           
           # Core attributes
           print("Core attributes:")
           print(f"  name: {self.name}")
           print(f"  roll_no: {self.roll_no}")
           
           # Custom attributes
           if self._attributes:
               print("Custom attributes:")
               for attr_name, attr_value in self._attributes.items():
                   print(f"  {attr_name}: {attr_value}")
           else:
               print("No custom attributes")
       
       def get_attribute_safely(self, attr_name, default="Not Set"):
           """Get attribute value safely"""
           return getattr(self, attr_name, default)

   # Demonstrate dynamic attributes
   student = FlexibleStudent("Alice", "CS001")
   student.list_all_attributes()

   # Add various attributes dynamically
   student.add_attribute("email", "alice@college.edu")
   student.add_attribute("phone", "9876543210")
   student.add_attribute("cgpa", 8.5)
   student.add_attribute("hobbies", ["Reading", "Coding", "Music"])

   student.list_all_attributes()

   # Update attributes
   student.update_attribute("cgpa", 8.7)
   student.update_attribute("nonexistent", "value")  # Will show error

   # Safely get attributes
   print(f"\nEmail: {student.get_attribute_safely('email')}")
   print(f"Address: {student.get_attribute_safely('address', 'Address not provided')}")

   # Remove attribute
   student.remove_attribute("phone")
   student.list_all_attributes()

**Advanced: Property-like Dynamic Attributes**

.. code-block:: python

   class SmartEmployee:
       def __init__(self, name, base_salary):
           self.name = name
           self.base_salary = base_salary
           self._dynamic_attributes = {}
       
       def __setattr__(self, name, value):
           """Called when setting any attribute"""
           if name.startswith('_') or name in ['name', 'base_salary']:
               # Allow private attributes and core attributes
               super().__setattr__(name, value)
           else:
               # Log dynamic attribute additions
               if not hasattr(self, name):
                   print(f"Adding dynamic attribute: {name} = {value}")
               super().__setattr__(name, value)
       
       def __getattr__(self, name):
           """Called when accessing non-existent attribute"""
           return f"Attribute '{name}' not found"
       
       def __delattr__(self, name):
           """Called when deleting attribute"""
           if name in ['name', 'base_salary']:
               print(f"Cannot delete core attribute: {name}")
           else:
               print(f"Deleting attribute: {name}")
               super().__delattr__(name)

   emp = SmartEmployee("Bob", 50000)
   
   # These will trigger __setattr__
   emp.department = "IT"
   emp.experience_years = 5
   emp.skills = ["Python", "Java", "SQL"]
   
   print(f"Department: {emp.department}")
   print(f"Non-existent: {emp.non_existent}")  # Triggers __getattr__
   
   # Try to delete core attribute
   del emp.department  # Works
   # del emp.name      # Would show warning

**When to Use Dynamic Attributes:**

✅ **Good Uses:**
- Configuration objects that need flexible properties
- Data objects from external APIs with varying fields
- Plugin systems where functionality is added at runtime
- Prototyping and experimentation

❌ **Avoid When:**
- Writing production code where stability is important
- Working in teams where code predictability is crucial
- Performance is critical (dynamic attributes have overhead)

.. note::
   **Dynamic attributes** provide flexibility but can make code harder to debug and understand. Use them judiciously and document their usage clearly! 🎯

--------------

Summary
-------

- Classes are blueprints for creating objects
- Objects are instances of classes with their own data
- Instance variables store object-specific data
- Instance methods define object behavior
- The ``self`` parameter refers to the current object
- Multiple objects of the same class can exist independently
