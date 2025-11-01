.. _module4_encapsulation:

Encapsulation in Python
========================

Introduction
------------

Encapsulation is one of the fundamental principles of Object-Oriented Programming. It refers to bundling data (attributes) and methods that operate on that data within a single unit (class), and controlling access to that data.

.. note::
   **Encapsulation** means hiding the internal details of an object and exposing only what is necessary through well-defined interfaces.

--------------

Why Encapsulation?
------------------

**Benefits:**

- **Data Protection**: Prevents accidental modification of data
- **Data Validation**: Allows checking values before setting them
- **Flexibility**: Internal implementation can change without affecting external code
- **Modularity**: Clear separation between interface and implementation

.. code-block:: python

   # Without encapsulation - direct access
   class Student:
       def __init__(self, name, age):
           self.name = name
           self.age = age

   student = Student("Alice", 20)
   student.age = -5  # Invalid age, but no protection!
   print(student.age)  # -5 (illogical)

--------------

Access Modifiers in Python
---------------------------

Python uses naming conventions to indicate access levels:

1. **Public**: Accessible from anywhere (no underscore)
2. **Protected**: Should not be accessed outside the class/subclasses (single underscore ``_``)
3. **Private**: Cannot be directly accessed outside the class (double underscore ``__``)

.. note::
   Python doesn't strictly enforce access control. The underscores are conventions that indicate intent to developers.

--------------

Public Attributes and Methods
------------------------------

Public members are accessible from anywhere. They have no underscore prefix.

.. code-block:: python

   class Person:
       def __init__(self, name, age):
           self.name = name        # Public attribute
           self.age = age          # Public attribute
       
       def display(self):          # Public method
           return f"Name: {self.name}, Age: {self.age}"

   person = Person("John", 30)
   print(person.name)              # Direct access - John
   print(person.age)               # Direct access - 30
   person.age = 31                 # Direct modification
   print(person.display())         # Name: John, Age: 31

--------------

Protected Attributes and Methods
---------------------------------

Protected members use a single underscore ``_`` prefix. They indicate "don't access this directly unless you're a subclass."

.. code-block:: python

   class BankAccount:
       def __init__(self, account_number, balance):
           self._account_number = account_number  # Protected
           self._balance = balance                # Protected
       
       def _calculate_interest(self, rate):       # Protected method
           return self._balance * rate / 100
       
       def display_balance(self):                 # Public method
           return f"Account: {self._account_number}, Balance: ₹{self._balance}"
       
       def add_interest(self, rate):
           interest = self._calculate_interest(rate)
           self._balance += interest
           return f"Interest of ₹{interest:.2f} added"

   account = BankAccount("ACC001", 10000)

   # Public method - recommended way
   print(account.display_balance())
   print(account.add_interest(5))

   # Can still access protected members (not recommended)
   print(account._balance)  # Works but not recommended
   print(account._account_number)  # Works but not recommended

.. note::
   Protected members are just a convention. Python allows access but indicates "use at your own risk."

--------------

Private Attributes and Methods
-------------------------------

Private members use double underscore ``__`` prefix. Python performs name mangling to make them harder to access from outside.

.. code-block:: python

   class SecureAccount:
       def __init__(self, account_number, pin):
           self.__account_number = account_number  # Private
           self.__pin = pin                        # Private
           self.holder_name = "Anonymous"          # Public
       
       def __validate_pin(self, entered_pin):      # Private method
           return self.__pin == entered_pin
       
       def change_pin(self, old_pin, new_pin):     # Public method
           if self.__validate_pin(old_pin):
               self.__pin = new_pin
               return "PIN changed successfully"
           return "Invalid PIN"
       
       def get_account_info(self, pin):
           if self.__validate_pin(pin):
               return f"Account Number: {self.__account_number}"
           return "Access denied"

   account = SecureAccount("ACC12345", "1234")

   # Public access works
   print(account.holder_name)

   # Private access doesn't work directly
   # print(account.__pin)  # AttributeError
   # print(account.__account_number)  # AttributeError

   # Public methods provide controlled access
   print(account.get_account_info("1234"))  # Account Number: ACC12345
   print(account.get_account_info("0000"))  # Access denied
   print(account.change_pin("1234", "5678"))  # PIN changed successfully

.. note::
   Python uses **name mangling** for private attributes. ``__pin`` becomes ``_ClassName__pin`` internally.

--------------

Getters and Setters
-------------------

Getters and setters provide controlled access to private attributes with validation.

.. code-block:: python

   class Employee:
       def __init__(self, name, salary):
           self.__name = name
           self.__salary = salary
       
       # Getter for name
       def get_name(self):
           return self.__name
       
       # Setter for name
       def set_name(self, name):
           if name and len(name) > 0:
               self.__name = name
           else:
               print("Invalid name")
       
       # Getter for salary
       def get_salary(self):
           return self.__salary
       
       # Setter for salary with validation
       def set_salary(self, salary):
           if salary >= 0:
               self.__salary = salary
           else:
               print("Salary cannot be negative")
       
       def display(self):
           return f"Employee: {self.__name}, Salary: ₹{self.__salary}"

   emp = Employee("Alice", 50000)

   print(emp.get_name())           # Alice
   print(emp.get_salary())         # 50000

   emp.set_salary(55000)           # Valid
   print(emp.display())            # Employee: Alice, Salary: ₹55000

   emp.set_salary(-1000)           # Invalid - Salary cannot be negative
   print(emp.display())            # Employee: Alice, Salary: ₹55000 (unchanged)

--------------

Using @property Decorator
-------------------------

Python's ``@property`` decorator provides a cleaner syntax for getters and setters.

.. code-block:: python

   class Rectangle:
       def __init__(self, length, width):
           self.__length = length
           self.__width = width
       
       # Getter for length
       @property
       def length(self):
           return self.__length
       
       # Setter for length
       @length.setter
       def length(self, value):
           if value > 0:
               self.__length = value
           else:
               print("Length must be positive")
       
       # Getter for width
       @property
       def width(self):
           return self.__width
       
       # Setter for width
       @width.setter
       def width(self, value):
           if value > 0:
               self.__width = value
           else:
               print("Width must be positive")
       
       # Calculated property (read-only)
       @property
       def area(self):
           return self.__length * self.__width

   rect = Rectangle(10, 5)

   # Access like attributes (but using getters/setters)
   print(rect.length)              # 10
   print(rect.width)               # 5
   print(rect.area)                # 50

   rect.length = 15                # Uses setter
   print(rect.area)                # 75

   rect.length = -5                # Length must be positive (invalid)
   print(rect.length)              # 15 (unchanged)

.. note::
   ``@property`` makes getters and setters look like regular attribute access, providing a cleaner interface.

--------------

Real-World Example: Student Grade System
-----------------------------------------

.. code-block:: python

   class Student:
       def __init__(self, name, roll_number):
           self.__name = name
           self.__roll_number = roll_number
           self.__marks = []
       
       @property
       def name(self):
           return self.__name
       
       @property
       def roll_number(self):
           return self.__roll_number
       
       def add_marks(self, subject, marks):
           if 0 <= marks <= 100:
               self.__marks.append({'subject': subject, 'marks': marks})
               return f"Marks added for {subject}"
           return "Invalid marks (must be 0-100)"
       
       def get_marks(self):
           return self.__marks.copy()  # Return copy to prevent modification
       
       @property
       def average(self):
           if not self.__marks:
               return 0
           total = sum(item['marks'] for item in self.__marks)
           return total / len(self.__marks)
       
       @property
       def grade(self):
           avg = self.average
           if avg >= 90:
               return 'A'
           elif avg >= 75:
               return 'B'
           elif avg >= 60:
               return 'C'
           elif avg >= 40:
               return 'D'
           else:
               return 'F'
       
       def display_report(self):
           print(f"\n{'='*40}")
           print(f"Student Name: {self.name}")
           print(f"Roll Number: {self.roll_number}")
           print(f"{'='*40}")
           for item in self.__marks:
               print(f"{item['subject']:20s}: {item['marks']}")
           print(f"{'='*40}")
           print(f"Average: {self.average:.2f}")
           print(f"Grade: {self.grade}")
           print(f"{'='*40}")

   # Using the Student class
   student = Student("Alice Johnson", "MCA001")

   student.add_marks("Python Programming", 85)
   student.add_marks("Data Structures", 90)
   student.add_marks("Database Management", 78)
   student.add_marks("Web Development", 92)

   # Cannot modify marks directly (encapsulated)
   print(student.name)         # Alice Johnson
   print(student.roll_number)  # MCA001
   print(f"Average: {student.average:.2f}")  # Average: 86.25
   print(f"Grade: {student.grade}")          # Grade: B

   student.display_report()

--------------

Complete Example: ATM System
-----------------------------

.. code-block:: python

   class ATM:
       def __init__(self, card_number, pin, initial_balance=0):
           self.__card_number = card_number
           self.__pin = pin
           self.__balance = initial_balance
           self.__transaction_history = []
       
       def __verify_pin(self, entered_pin):
           return self.__pin == entered_pin
       
       def __add_transaction(self, transaction_type, amount):
           self.__transaction_history.append({
               'type': transaction_type,
               'amount': amount
           })
       
       def check_balance(self, pin):
           if self.__verify_pin(pin):
               return f"Available Balance: ₹{self.__balance}"
           return "Incorrect PIN"
       
       def withdraw(self, pin, amount):
           if not self.__verify_pin(pin):
               return "Incorrect PIN"
           
           if amount <= 0:
               return "Invalid amount"
           
           if amount > self.__balance:
               return "Insufficient balance"
           
           self.__balance -= amount
           self.__add_transaction("Withdrawal", amount)
           return f"Withdrawn: ₹{amount}. Remaining balance: ₹{self.__balance}"
       
       def deposit(self, pin, amount):
           if not self.__verify_pin(pin):
               return "Incorrect PIN"
           
           if amount <= 0:
               return "Invalid amount"
           
           self.__balance += amount
           self.__add_transaction("Deposit", amount)
           return f"Deposited: ₹{amount}. New balance: ₹{self.__balance}"
       
       def get_mini_statement(self, pin):
           if not self.__verify_pin(pin):
               return "Incorrect PIN"
           
           if not self.__transaction_history:
               return "No transactions yet"
           
           statement = "Last 5 Transactions:\n"
           for trans in self.__transaction_history[-5:]:
               statement += f"{trans['type']}: ₹{trans['amount']}\n"
           return statement

   # Using the ATM
   atm = ATM("1234-5678-9012", "1234", 10000)

   print(atm.check_balance("1234"))      # Available Balance: ₹10000
   print(atm.withdraw("1234", 2000))     # Withdrawn: ₹2000. Remaining balance: ₹8000
   print(atm.deposit("1234", 5000))      # Deposited: ₹5000. New balance: ₹13000
   print(atm.withdraw("0000", 1000))     # Incorrect PIN
   print(atm.get_mini_statement("1234")) # Shows transaction history

--------------

Tasks
-----

**Task 1: Create a Secure Password Manager**

Create a class ``PasswordManager`` with private attributes for username and password. Add methods to set password (with minimum 8 characters validation), verify password, and change password.

*Hint:* Use ``__password`` as private attribute. Check ``len(password) >= 8`` before setting.

**Task 2: Product with Price Control**

Create a class ``Product`` with private price attribute. Use ``@property`` for getter and setter. The setter should only accept positive prices. Add a discount method that reduces price by a percentage.

*Hint:* Use ``@property`` and ``@price.setter``. Check ``if price > 0`` before setting.

**Task 3: Grade Book System**

Create a class ``GradeBook`` with private list of grades. Add methods to add grades (0-100 only), remove last grade, and get average. Make sure the grades list cannot be directly modified from outside.

*Hint:* Use ``__grades = []`` as private. Validate ``0 <= grade <= 100`` before adding.

**Task 4: Bank Account with Transaction Limit**

Create a class ``LimitedAccount`` with private balance and a daily transaction limit. Track daily withdrawals and prevent exceeding the limit. Reset limit tracker with a method.

*Hint:* Use ``__daily_withdrawn = 0`` and ``__daily_limit``. Check before allowing withdrawal.

**Task 5: User Profile with Email Validation**

Create a class ``UserProfile`` with private email attribute. Use ``@property`` to ensure email contains ``@`` and ``.`` when setting. Add method to update email with validation.

*Hint:* Use ``@email.setter`` with validation: ``if '@' in email and '.' in email``.

--------------

Summary
-------

- **Encapsulation** bundles data and methods while controlling access
- **Public** members (no underscore) are accessible everywhere
- **Protected** members (single ``_``) indicate "internal use"
- **Private** members (double ``__``) use name mangling for restricted access
- **Getters/setters** provide controlled access with validation
- ``@property`` decorator creates Pythonic getters and setters
- Encapsulation improves data security, validation, and maintainability
