.. _module4_polymorphism_abstraction:

Polymorphism and Abstraction in Python
=======================================

Introduction
------------

Polymorphism and abstraction are advanced OOP concepts that make code more flexible, maintainable, and easier to understand.

.. note::
   **Polymorphism** means "many forms" - the ability to use the same interface for different data types. **Abstraction** means hiding complex implementation details and showing only essential features.

--------------

What is Polymorphism?
---------------------

Polymorphism allows objects of different classes to be treated as objects of a common parent class. The same method name can behave differently based on the object that calls it.

**Types of Polymorphism:**

1. **Method Overriding** (Runtime Polymorphism)
2. **Operator Overloading** (Compile-time Polymorphism)
3. **Duck Typing** (Python-specific)

--------------

Method Overriding - Runtime Polymorphism
-----------------------------------------

Child classes can override parent class methods to provide specific implementations.

.. code-block:: python

   class Animal:
       def speak(self):
           return "Animal makes a sound"

   class Dog(Animal):
       def speak(self):
           return "Dog barks: Woof Woof!"

   class Cat(Animal):
       def speak(self):
           return "Cat meows: Meow Meow!"

   class Cow(Animal):
       def speak(self):
           return "Cow moos: Moo Moo!"

   # Polymorphism in action
   animals = [Dog(), Cat(), Cow()]

   for animal in animals:
       print(animal.speak())  # Same method, different behavior

   # Output:
   # Dog barks: Woof Woof!
   # Cat meows: Meow Meow!
   # Cow moos: Moo Moo!

.. note::
   Polymorphism allows you to write more generic code that works with objects of different types through a common interface.

--------------

Real-World Example: Payment System
-----------------------------------

.. code-block:: python

   class Payment:
       def __init__(self, amount):
           self.amount = amount
       
       def process_payment(self):
           return "Processing generic payment"

   class CreditCardPayment(Payment):
       def __init__(self, amount, card_number):
           super().__init__(amount)
           self.card_number = card_number
       
       def process_payment(self):
           return f"Processing credit card payment of ₹{self.amount} using card {self.card_number[-4:]}"

   class UPIPayment(Payment):
       def __init__(self, amount, upi_id):
           super().__init__(amount)
           self.upi_id = upi_id
       
       def process_payment(self):
           return f"Processing UPI payment of ₹{self.amount} to {self.upi_id}"

   class CashPayment(Payment):
       def process_payment(self):
           return f"Processing cash payment of ₹{self.amount}"

   # Polymorphic behavior
   def make_payment(payment_obj):
       print(payment_obj.process_payment())

   # Same function, different behaviors
   make_payment(CreditCardPayment(1000, "1234-5678-9012-3456"))
   make_payment(UPIPayment(500, "user@paytm"))
   make_payment(CashPayment(200))

--------------

Operator Overloading
--------------------

Python allows you to define how operators work with custom objects using special methods (magic methods).

**Common Magic Methods:**

- ``__add__(self, other)`` for ``+``
- ``__sub__(self, other)`` for ``-``
- ``__mul__(self, other)`` for ``*``
- ``__eq__(self, other)`` for ``==``
- ``__lt__(self, other)`` for ``<``
- ``__str__(self)`` for ``str()``
- ``__len__(self)`` for ``len()``

.. code-block:: python

   class Vector:
       def __init__(self, x, y):
           self.x = x
           self.y = y
       
       def __add__(self, other):
           return Vector(self.x + other.x, self.y + other.y)
       
       def __sub__(self, other):
           return Vector(self.x - other.x, self.y - other.y)
       
       def __mul__(self, scalar):
           return Vector(self.x * scalar, self.y * scalar)
       
       def __eq__(self, other):
           return self.x == other.x and self.y == other.y
       
       def __str__(self):
           return f"Vector({self.x}, {self.y})"

   # Using overloaded operators
   v1 = Vector(3, 4)
   v2 = Vector(1, 2)

   v3 = v1 + v2  # Calls __add__
   print(v3)     # Vector(4, 6)

   v4 = v1 - v2  # Calls __sub__
   print(v4)     # Vector(2, 2)

   v5 = v1 * 2   # Calls __mul__
   print(v5)     # Vector(6, 8)

   print(v1 == v2)  # False (calls __eq__)

--------------

Practical Operator Overloading: Book Comparison
------------------------------------------------

.. code-block:: python

   class Book:
       def __init__(self, title, author, pages):
           self.title = title
           self.author = author
           self.pages = pages
       
       def __str__(self):
           return f"'{self.title}' by {self.author} ({self.pages} pages)"
       
       def __eq__(self, other):
           return self.pages == other.pages
       
       def __lt__(self, other):
           return self.pages < other.pages
       
       def __gt__(self, other):
           return self.pages > other.pages
       
       def __add__(self, other):
           # Combine two books (total pages)
           return self.pages + other.pages

   book1 = Book("Python Basics", "John", 250)
   book2 = Book("Advanced Python", "Jane", 450)
   book3 = Book("Python Projects", "Bob", 250)

   print(book1)                    # 'Python Basics' by John (250 pages)
   print(book1 == book3)           # True (same pages)
   print(book1 < book2)            # True (250 < 450)
   print(f"Total pages: {book1 + book2}")  # Total pages: 700

--------------

Duck Typing in Python
---------------------

"If it walks like a duck and quacks like a duck, it must be a duck." Python uses duck typing - it doesn't check the type, but whether the object has the required methods.

.. code-block:: python

   class Dog:
       def speak(self):
           return "Woof!"

   class Cat:
       def speak(self):
           return "Meow!"

   class Radio:
       def speak(self):
           return "Music playing..."

   # Function doesn't care about type, only that speak() exists
   def make_it_speak(obj):
       print(obj.speak())

   # Duck typing - all work because they have speak()
   make_it_speak(Dog())    # Woof!
   make_it_speak(Cat())    # Meow!
   make_it_speak(Radio())  # Music playing...

.. note::
   Duck typing makes Python flexible - you don't need inheritance for polymorphism, just consistent interfaces.

--------------

What is Abstraction?
--------------------

Abstraction means hiding complex implementation details and exposing only necessary functionality. It helps in:

- Reducing complexity
- Defining clear interfaces
- Enforcing method implementation in child classes

Python provides the ``abc`` (Abstract Base Class) module for creating abstract classes.

--------------

Abstract Base Classes (ABC)
----------------------------

An abstract class cannot be instantiated and may contain abstract methods that must be implemented by child classes.

.. code-block:: python

   from abc import ABC, abstractmethod

   class Shape(ABC):
       @abstractmethod
       def area(self):
           pass
       
       @abstractmethod
       def perimeter(self):
           pass
       
       def description(self):  # Concrete method
           return "This is a shape"

   # Cannot create object of abstract class
   # shape = Shape()  # TypeError: Can't instantiate abstract class

   class Rectangle(Shape):
       def __init__(self, length, width):
           self.length = length
           self.width = width
       
       def area(self):
           return self.length * self.width
       
       def perimeter(self):
           return 2 * (self.length + self.width)

   class Circle(Shape):
       def __init__(self, radius):
           self.radius = radius
       
       def area(self):
           return 3.14159 * self.radius ** 2
       
       def perimeter(self):
           return 2 * 3.14159 * self.radius

   # Now we can create objects of concrete classes
   rect = Rectangle(10, 5)
   print(f"Rectangle Area: {rect.area()}")         # 50
   print(f"Rectangle Perimeter: {rect.perimeter()}")  # 30

   circle = Circle(7)
   print(f"Circle Area: {circle.area():.2f}")      # 153.94
   print(f"Circle Perimeter: {circle.perimeter():.2f}")  # 43.98

.. note::
   Abstract methods must be implemented by all child classes. This ensures a consistent interface across different implementations.

--------------

Real-World Example: Database Connections
-----------------------------------------

.. code-block:: python

   from abc import ABC, abstractmethod

   class Database(ABC):
       @abstractmethod
       def connect(self):
           pass
       
       @abstractmethod
       def disconnect(self):
           pass
       
       @abstractmethod
       def execute_query(self, query):
           pass

   class MySQLDatabase(Database):
       def connect(self):
           return "Connected to MySQL database"
       
       def disconnect(self):
           return "Disconnected from MySQL database"
       
       def execute_query(self, query):
           return f"Executing MySQL query: {query}"

   class PostgreSQLDatabase(Database):
       def connect(self):
           return "Connected to PostgreSQL database"
       
       def disconnect(self):
           return "Disconnected from PostgreSQL database"
       
       def execute_query(self, query):
           return f"Executing PostgreSQL query: {query}"

   class MongoDBDatabase(Database):
       def connect(self):
           return "Connected to MongoDB database"
       
       def disconnect(self):
           return "Disconnected from MongoDB database"
       
       def execute_query(self, query):
           return f"Executing MongoDB query: {query}"

   # Polymorphic function
   def perform_database_operations(db):
       print(db.connect())
       print(db.execute_query("SELECT * FROM users"))
       print(db.disconnect())
       print()

   # Works with any database type
   perform_database_operations(MySQLDatabase())
   perform_database_operations(PostgreSQLDatabase())
   perform_database_operations(MongoDBDatabase())

--------------

Complete Example: Employee Management System
---------------------------------------------

.. code-block:: python

   from abc import ABC, abstractmethod

   class Employee(ABC):
       def __init__(self, name, emp_id):
           self.name = name
           self.emp_id = emp_id
       
       @abstractmethod
       def calculate_salary(self):
           pass
       
       @abstractmethod
       def get_role(self):
           pass
       
       def display_info(self):
           return f"Name: {self.name}, ID: {self.emp_id}, Role: {self.get_role()}"

   class FullTimeEmployee(Employee):
       def __init__(self, name, emp_id, monthly_salary):
           super().__init__(name, emp_id)
           self.monthly_salary = monthly_salary
       
       def calculate_salary(self):
           return self.monthly_salary
       
       def get_role(self):
           return "Full-Time Employee"

   class ContractEmployee(Employee):
       def __init__(self, name, emp_id, hourly_rate, hours_worked):
           super().__init__(name, emp_id)
           self.hourly_rate = hourly_rate
           self.hours_worked = hours_worked
       
       def calculate_salary(self):
           return self.hourly_rate * self.hours_worked
       
       def get_role(self):
           return "Contract Employee"

   class Intern(Employee):
       def __init__(self, name, emp_id, stipend):
           super().__init__(name, emp_id)
           self.stipend = stipend
       
       def calculate_salary(self):
           return self.stipend
       
       def get_role(self):
           return "Intern"

   # Payroll function using polymorphism
   def process_payroll(employees):
       total = 0
       for emp in employees:
           salary = emp.calculate_salary()
           print(f"{emp.display_info()} - Salary: ₹{salary}")
           total += salary
       print(f"\nTotal Payroll: ₹{total}")

   # Create different types of employees
   employees = [
       FullTimeEmployee("Alice", "FT001", 50000),
       ContractEmployee("Bob", "CT001", 500, 160),
       Intern("Charlie", "IN001", 15000)
   ]

   process_payroll(employees)

--------------

Abstract Properties
-------------------

You can also create abstract properties that must be implemented in child classes.

.. code-block:: python

   from abc import ABC, abstractmethod

   class Vehicle(ABC):
       @abstractmethod
       def start(self):
           pass
       
       @property
       @abstractmethod
       def max_speed(self):
           pass

   class Car(Vehicle):
       def __init__(self, brand):
           self.brand = brand
           self._max_speed = 180
       
       def start(self):
           return f"{self.brand} car engine started"
       
       @property
       def max_speed(self):
           return self._max_speed

   car = Car("Tesla")
   print(car.start())       # Tesla car engine started
   print(car.max_speed)     # 180

--------------

Tasks
-----

**Task 1: Media Player Polymorphism**

Create an abstract class ``MediaPlayer`` with abstract methods ``play()``, ``pause()``, and ``stop()``. Create child classes ``MusicPlayer`` and ``VideoPlayer`` with specific implementations.

*Hint:* Use ``from abc import ABC, abstractmethod``. Each child class must implement all abstract methods.

**Task 2: Operator Overloading for Coordinates**

Create a ``Point`` class representing 2D coordinates. Overload ``+`` (add points), ``-`` (subtract points), ``==`` (compare points), and ``__str__`` (display format).

*Hint:* Use ``__add__``, ``__sub__``, ``__eq__``, and ``__str__`` methods. For addition: new point = (x1+x2, y1+y2).

**Task 3: Abstract Shape Calculator**

Create abstract class ``Shape`` with abstract methods ``area()`` and ``perimeter()``. Implement ``Triangle``, ``Square``, and ``Circle`` classes. Create a function to calculate total area of mixed shapes.

*Hint:* Store shapes in a list and iterate to calculate total. Triangle area = 0.5 × base × height.

**Task 4: Banking Operations with Abstraction**

Create abstract class ``Transaction`` with abstract method ``execute()``. Implement ``Deposit``, ``Withdrawal``, and ``Transfer`` classes. Each should execute differently.

*Hint:* Pass account balance to ``execute()`` method. Return updated balance after operation.

**Task 5: Notification System**

Create abstract class ``Notification`` with abstract method ``send()``. Implement ``EmailNotification``, ``SMSNotification``, and ``PushNotification`` classes. Create a function to send notifications to a list of users.

*Hint:* Each notification type should have different ``send()`` implementation showing how the message is delivered.

--------------

Summary
-------

**Polymorphism:**
- Allows same interface for different implementations
- Method overriding enables runtime polymorphism
- Operator overloading customizes operator behavior
- Duck typing provides flexible polymorphism without inheritance

**Abstraction:**
- Hides complexity and shows only essential features
- Abstract classes define contracts for child classes
- Use ``ABC`` and ``@abstractmethod`` from ``abc`` module
- Abstract classes cannot be instantiated directly
- Child classes must implement all abstract methods
- Provides clear interfaces and enforces consistency
