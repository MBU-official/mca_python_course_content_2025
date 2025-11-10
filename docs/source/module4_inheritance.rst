.. _module4_inheritance:

Inheritance in Python
=====================

Introduction
------------

Inheritance is a fundamental concept in Object-Oriented Programming that allows a class to inherit properties and methods from another class. This promotes code reusability and establishes relationships between classes.

.. note::
   **Inheritance** enables a new class (child/derived class) to acquire attributes and methods from an existing class (parent/base class).

--------------

Why Inheritance?
----------------

**Benefits:**

- **Code Reusability**: Avoid duplicating code by inheriting from existing classes
- **Extensibility**: Add new features to existing classes without modifying them
- **Hierarchy**: Create logical relationships between classes
- **Maintainability**: Changes in parent class automatically reflect in child classes

.. code-block:: python

   # Without inheritance - code duplication
   class Teacher:
       def __init__(self, name, age):
           self.name = name
           self.age = age

   class Student:
       def __init__(self, name, age):
           self.name = name
           self.age = age

   # With inheritance - code reuse
   class Person:
       def __init__(self, name, age):
           self.name = name
           self.age = age

   class Teacher(Person):
       pass  # Inherits name and age from Person

   class Student(Person):
       pass  # Inherits name and age from Person

--------------

Basic Inheritance Syntax
-------------------------

.. code-block:: python

   # Parent/Base/Super class
   class ParentClass:
       # Parent class members
       pass

   # Child/Derived/Sub class
   class ChildClass(ParentClass):
       # Child class members
       # Inherits all members from ParentClass
       pass

--------------

Simple Inheritance Example
---------------------------

.. code-block:: python

   # Parent class
   class Animal:
       def __init__(self, name):
           self.name = name
       
       def speak(self):
           return f"{self.name} makes a sound"
       
       def move(self):
           return f"{self.name} is moving"

   # Child class inheriting from Animal
   class Dog(Animal):
       def bark(self):
           return f"{self.name} says Woof!"

   # Creating objects
   animal = Animal("Generic Animal")
   print(animal.speak())   # Generic Animal makes a sound
   print(animal.move())    # Generic Animal is moving

   dog = Dog("Buddy")
   print(dog.speak())      # Buddy makes a sound (inherited)
   print(dog.move())       # Buddy is moving (inherited)
   print(dog.bark())       # Buddy says Woof! (own method)

--------------

Adding Constructor in Child Class
----------------------------------

When a child class has its own constructor, use ``super()`` to call the parent's constructor.

.. code-block:: python

   class Person:
       def __init__(self, name, age):
           self.name = name
           self.age = age
       
       def display(self):
           return f"Name: {self.name}, Age: {self.age}"

   class Student(Person):
       def __init__(self, name, age, roll_number):
           super().__init__(name, age)  # Call parent constructor
           self.roll_number = roll_number
       
       def display(self):
           return f"{super().display()}, Roll No: {self.roll_number}"

   student = Student("Alice", 20, "CS001")
   print(student.display())  # Name: Alice, Age: 20, Roll No: CS001

.. note::
   ``super()`` is used to access methods from the parent class. It's essential when overriding methods or constructors.

--------------

Method Overriding
-----------------

Child classes can override (redefine) methods from the parent class.

.. code-block:: python

   class Vehicle:
       def __init__(self, brand):
           self.brand = brand
       
       def start(self):
           return f"{self.brand} vehicle is starting"
       
       def stop(self):
           return f"{self.brand} vehicle is stopping"

   class Car(Vehicle):
       def start(self):  # Overriding parent method
           return f"{self.brand} car engine is starting with ignition"
       
       def honk(self):
           return f"{self.brand} car: Beep Beep!"

   class Bicycle(Vehicle):
       def start(self):  # Overriding parent method
           return f"{self.brand} bicycle: Start pedaling!"
       
       def ring_bell(self):
           return f"{self.brand} bicycle: Ring Ring!"

   car = Car("Toyota")
   bicycle = Bicycle("Hero")

   print(car.start())       # Toyota car engine is starting with ignition (overridden)
   print(car.stop())        # Toyota car is stopping (inherited)
   print(car.honk())        # Toyota car: Beep Beep!

   print(bicycle.start())   # Hero bicycle: Start pedaling! (overridden)
   print(bicycle.stop())    # Hero bicycle is stopping (inherited)
   print(bicycle.ring_bell())  # Hero bicycle: Ring Ring!

--------------

Types of Inheritance
--------------------

**1. Single Inheritance**

One child class inherits from one parent class.

.. code-block:: python

   class Parent:
       def parent_method(self):
           return "This is parent method"

   class Child(Parent):
       def child_method(self):
           return "This is child method"

   obj = Child()
   print(obj.parent_method())  # Inherited
   print(obj.child_method())   # Own method

**2. Multiple Inheritance**

One child class inherits from multiple parent classes.

.. code-block:: python

   class Father:
       def father_trait(self):
           return "Father's trait"

   class Mother:
       def mother_trait(self):
           return "Mother's trait"

   class Child(Father, Mother):
       def child_trait(self):
           return "Child's trait"

   child = Child()
   print(child.father_trait())  # Father's trait
   print(child.mother_trait())  # Mother's trait
   print(child.child_trait())   # Child's trait

.. note::
   In multiple inheritance, if both parents have the same method name, Python uses **Method Resolution Order (MRO)** to determine which method to call.

**3. Multilevel Inheritance**

A class inherits from a child class, creating a chain.

.. code-block:: python

   class GrandParent:
       def grand_parent_method(self):
           return "GrandParent method"

   class Parent(GrandParent):
       def parent_method(self):
           return "Parent method"

   class Child(Parent):
       def child_method(self):
           return "Child method"

   child = Child()
   print(child.grand_parent_method())  # GrandParent method
   print(child.parent_method())        # Parent method
   print(child.child_method())         # Child method

**4. Hierarchical Inheritance**

Multiple child classes inherit from one parent class.

.. code-block:: python

   class Animal:
       def eat(self):
           return "Eating..."

   class Dog(Animal):
       def bark(self):
           return "Woof!"

   class Cat(Animal):
       def meow(self):
           return "Meow!"

   dog = Dog()
   cat = Cat()

   print(dog.eat())   # Eating... (inherited)
   print(dog.bark())  # Woof!

   print(cat.eat())   # Eating... (inherited)
   print(cat.meow())  # Meow!

--------------

Real-World Example: Employee Management
----------------------------------------

.. code-block:: python

   class Employee:
       def __init__(self, name, emp_id):
           self.name = name
           self.emp_id = emp_id
       
       def display_info(self):
           return f"Employee: {self.name} (ID: {self.emp_id})"

   class Manager(Employee):
       def __init__(self, name, emp_id, department):
           super().__init__(name, emp_id)
           self.department = department
           self.team = []
       
       def add_team_member(self, member):
           self.team.append(member)
       
       def display_info(self):
           info = super().display_info()
           return f"{info}\nRole: Manager\nDepartment: {self.department}\nTeam Size: {len(self.team)}"

   class Developer(Employee):
       def __init__(self, name, emp_id, programming_language):
           super().__init__(name, emp_id)
           self.programming_language = programming_language
       
       def display_info(self):
           info = super().display_info()
           return f"{info}\nRole: Developer\nLanguage: {self.programming_language}"

   # Creating objects
   manager = Manager("John Smith", "M001", "IT")
   dev1 = Developer("Alice Johnson", "D001", "Python")
   dev2 = Developer("Bob Williams", "D002", "Java")

   manager.add_team_member(dev1.name)
   manager.add_team_member(dev2.name)

   print(manager.display_info())
   print("\n" + dev1.display_info())
   print("\n" + dev2.display_info())

--------------

Complete Example: Banking System
---------------------------------

.. code-block:: python

   class BankAccount:
       def __init__(self, account_number, holder_name, balance=0):
           self.account_number = account_number
           self.holder_name = holder_name
           self.balance = balance
       
       def deposit(self, amount):
           if amount > 0:
               self.balance += amount
               return f"Deposited ₹{amount}. Balance: ₹{self.balance}"
           return "Invalid amount"
       
       def withdraw(self, amount):
           if amount > 0 and amount <= self.balance:
               self.balance -= amount
               return f"Withdrew ₹{amount}. Balance: ₹{self.balance}"
           return "Insufficient funds or invalid amount"
       
       def get_balance(self):
           return f"Balance: ₹{self.balance}"

   class SavingsAccount(BankAccount):
       def __init__(self, account_number, holder_name, balance=0, interest_rate=4.0):
           super().__init__(account_number, holder_name, balance)
           self.interest_rate = interest_rate
       
       def add_interest(self):
           interest = self.balance * self.interest_rate / 100
           self.balance += interest
           return f"Interest of ₹{interest:.2f} added at {self.interest_rate}%"

   class CurrentAccount(BankAccount):
       def __init__(self, account_number, holder_name, balance=0, overdraft_limit=10000):
           super().__init__(account_number, holder_name, balance)
           self.overdraft_limit = overdraft_limit
       
       def withdraw(self, amount):
           if amount > 0 and amount <= (self.balance + self.overdraft_limit):
               self.balance -= amount
               return f"Withdrew ₹{amount}. Balance: ₹{self.balance}"
           return "Overdraft limit exceeded"

   # Using the classes
   savings = SavingsAccount("SA001", "Alice", 10000)
   print(savings.deposit(5000))       # Deposited ₹5000. Balance: ₹15000
   print(savings.add_interest())      # Interest of ₹600.00 added at 4.0%
   print(savings.get_balance())       # Balance: ₹15600.0

   current = CurrentAccount("CA001", "Bob", 5000)
   print(current.withdraw(7000))      # Withdrew ₹7000. Balance: ₹-2000
   print(current.withdraw(9000))      # Withdrew ₹9000. Balance: ₹-11000
   print(current.withdraw(1000))      # Overdraft limit exceeded

--------------

Using ``isinstance()`` and ``issubclass()``
--------------------------------------------

.. code-block:: python

   class Animal:
       pass

   class Dog(Animal):
       pass

   class Cat(Animal):
       pass

   dog = Dog()
   cat = Cat()

   # isinstance() checks if object is instance of a class
   print(isinstance(dog, Dog))      # True
   print(isinstance(dog, Animal))   # True (Dog is subclass of Animal)
   print(isinstance(dog, Cat))      # False

   # issubclass() checks if a class is subclass of another
   print(issubclass(Dog, Animal))   # True
   print(issubclass(Cat, Animal))   # True
   print(issubclass(Dog, Cat))      # False

--------------

Multiple Inheritance Example
-----------------------------

.. code-block:: python

   class Teacher:
       def __init__(self, subject):
           self.subject = subject
       
       def teach(self):
           return f"Teaching {self.subject}"

   class Researcher:
       def __init__(self, research_area):
           self.research_area = research_area
       
       def research(self):
           return f"Researching {self.research_area}"

   class Professor(Teacher, Researcher):
       def __init__(self, name, subject, research_area):
           self.name = name
           Teacher.__init__(self, subject)
           Researcher.__init__(self, research_area)
       
       def display(self):
           return f"Professor {self.name}\n{self.teach()}\n{self.research()}"

   prof = Professor("Dr. Smith", "Python Programming", "Machine Learning")
   print(prof.display())
   # Output:
   # Professor Dr. Smith
   # Teaching Python Programming
   # Researching Machine Learning

--------------

Tasks
-----

**Task 1: Shape Hierarchy**

Create a base class ``Shape`` with method ``area()``. Create child classes ``Rectangle`` and ``Circle`` that inherit from ``Shape`` and override the ``area()`` method with proper calculations.

*Hint:* Rectangle area = length × width, Circle area = π × radius². Use ``3.14159`` for π.

**Task 2: Vehicle Rental System**

Create a ``Vehicle`` base class with attributes brand and rental_price. Create ``Car`` and ``Bike`` child classes with additional attributes (num_doors for Car, type for Bike). Override a method to display rental information.

*Hint:* Use ``super().__init__()`` in child constructors. Add specific attributes after calling parent constructor.

**Task 3: Student and Teacher**

Create a ``Person`` base class with name and age. Create ``Student`` (with roll_no and marks) and ``Teacher`` (with subject and salary) child classes. Add methods to display information for each.

*Hint:* Use ``super().display()`` in child classes to include parent information.

**Task 4: Multiple Inheritance - Smart Device**

Create classes ``Phone`` (with call method) and ``Camera`` (with take_photo method). Create ``Smartphone`` class that inherits from both and adds internet_browsing method.

*Hint:* Use ``class Smartphone(Phone, Camera):`` for multiple inheritance. Call both parent constructors.

**Task 5: Multilevel Inheritance - Organization**

Create ``Organization`` base class, ``Department`` child class, and ``Team`` grandchild class. Each level should add its own attributes and methods. Demonstrate accessing methods from all levels.

*Hint:* Use multilevel inheritance: ``Team(Department)`` and ``Department(Organization)``. Use ``super()`` to access parent methods.

--------------

Summary
-------

- **Inheritance** allows code reuse by inheriting from existing classes
- Use ``class ChildClass(ParentClass):`` syntax
- ``super()`` accesses parent class methods and constructors
- **Method overriding** allows child classes to provide specific implementations
- **Types**: Single, Multiple, Multilevel, Hierarchical inheritance
- ``isinstance()`` checks object type, ``issubclass()`` checks class relationships
- Inheritance creates "is-a" relationships (Dog *is a* Animal)
