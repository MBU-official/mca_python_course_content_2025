.. _module4_assignment:

Python Assignment Questions: Object-Oriented Programming
=========================================================

.. note::
   These assignments test your understanding of classes, objects, constructors, encapsulation, inheritance, polymorphism, and abstraction. Write clean, well-documented code with meaningful variable names.

Classes and Objects
-------------------

**1. Library Book Management**

Create a class ``Book`` with attributes: title, author, ISBN, and availability status. Implement methods to:
- Display book information
- Mark book as borrowed
- Mark book as returned
- Check if book is available

*Hint:* Use a boolean attribute ``is_available`` to track status. Initialize it to ``True`` in the constructor.

**2. Student Grade Calculator**

Create a class ``Student`` with name, roll number, and a list to store subject marks. Implement methods to:
- Add marks for a subject (validate 0-100 range)
- Calculate total marks
- Calculate average marks
- Determine grade (A: ≥90, B: ≥75, C: ≥60, D: ≥40, F: <40)

*Hint:* Store marks as a list of dictionaries: ``[{'subject': 'Python', 'marks': 85}]``. Use the average for grade calculation.

**3. Shopping Cart System**

Create a class ``ShoppingCart`` that manages items in a shopping cart. Implement methods to:
- Add item with name, price, and quantity
- Remove item by name
- Update quantity of an item
- Calculate total price
- Display all items with subtotals

*Hint:* Use a list to store items as dictionaries. For total price: sum of (price × quantity) for all items.

Constructors and Destructors
-----------------------------

**4. Bank Account with Transaction History**

Create a class ``BankAccount`` with constructor accepting account number, holder name, and initial balance. Implement:
- Deposit method (adds to balance and records transaction)
- Withdraw method (checks sufficient balance, deducts, records transaction)
- Display transaction history
- Destructor that prints final balance when account is closed

*Hint:* Use a list to store transactions with timestamp (you can use simple counter). Store as ``{'type': 'deposit', 'amount': 1000}``.

**5. Temperature Monitor with Statistics**

Create a class ``TemperatureMonitor`` that tracks temperature readings. Constructor accepts location name. Implement:
- Add temperature reading
- Get average temperature
- Get maximum and minimum temperatures
- Reset all readings
- Destructor showing total readings recorded

*Hint:* Store temperatures in a list. Use ``max()`` and ``min()`` built-in functions. Count readings using ``len()``.

**6. Product Inventory Manager**

Create a class ``Product`` with constructor for product name, SKU, price, and initial stock. Implement:
- Add stock (increment quantity)
- Remove stock (decrement if sufficient)
- Update price with validation (must be positive)
- Calculate total inventory value (price × quantity)
- Display product details with stock status

*Hint:* Use default parameter for initial stock (default=0). Total value = ``self.price * self.stock_quantity``.

Encapsulation
-------------

**7. Secure Email Account**

Create a class ``EmailAccount`` with private attributes for email address and password. Implement:
- Constructor to set email and password
- Method to verify password
- Method to change password (requires old password verification)
- Method to send email (requires password verification)
- Property to get email address (read-only)

*Hint:* Use ``__email`` and ``__password`` for private attributes. Use ``@property`` for read-only email access.

**8. Student Record System with Privacy**

Create a class ``StudentRecord`` with private attributes for student ID, name, and grades. Implement:
- Constructor with validation (ID must be non-empty, grades 0-100)
- Getter and setter for name using ``@property``
- Method to add grade with validation
- Method to get average (but not expose individual grades directly)
- Property to get student ID (read-only)

*Hint:* Use ``__id``, ``__name``, ``__grades`` as private. Validate in setter: ``if 0 <= grade <= 100``.

**9. ATM with Daily Withdrawal Limit**

Create a class ``ATMAccount`` with private balance and daily withdrawal limit. Implement:
- Constructor to set initial balance and limit
- Method to withdraw (check balance and daily limit)
- Method to deposit
- Method to reset daily limit counter
- Property to check balance (requires PIN validation)
- Private method to validate PIN

*Hint:* Use ``__daily_withdrawn`` to track total withdrawn today. Reset with a method call at day end.

Inheritance
-----------

**10. Employee Hierarchy**

Create a base class ``Employee`` with name, ID, and base salary. Create child classes:
- ``Manager``: Add department and bonus attributes, override salary calculation to include bonus
- ``Developer``: Add programming language and project count, override salary with project-based calculation
- ``Intern``: Add stipend (fixed amount), override salary to return stipend only

*Hint:* Use ``super().__init__()`` in child constructors. Override a ``calculate_salary()`` method in each child class.

**11. Vehicle Rental System**

Create a base class ``Vehicle`` with brand, model, and daily_rent. Create child classes:
- ``Car``: Add number of seats, calculate rent with seat-based multiplier
- ``Bike``: Add engine capacity, calculate rent with capacity-based multiplier
- ``Truck``: Add cargo capacity, calculate rent with cargo-based multiplier
Each should have a method to display rental information.

*Hint:* Base rent + (additional charge based on vehicle type). Use ``super().display()`` to show common info.

**12. Shape Hierarchy with Area and Perimeter**

Create a base class ``Shape`` with color attribute. Create child classes:
- ``Rectangle``: length and width attributes
- ``Circle``: radius attribute
- ``Triangle``: three sides attributes
Each must implement ``area()`` and ``perimeter()`` methods.

*Hint:* Rectangle area = l×w, perimeter = 2(l+w). Circle area = πr², perimeter = 2πr. Use 3.14159 for π.

Polymorphism
------------

**13. Payment Processing System**

Create an abstract base class ``Payment`` with abstract method ``process_payment()``. Implement child classes:
- ``CreditCard``: Requires card number, CVV, expiry date
- ``DebitCard``: Requires card number, PIN
- ``UPI``: Requires UPI ID
- ``Wallet``: Requires wallet ID and balance check
Each should implement ``process_payment()`` differently.

*Hint:* Use ``from abc import ABC, abstractmethod``. Create a function that accepts any Payment object and calls ``process_payment()``.

**14. Document Converter**

Create an abstract class ``Document`` with abstract methods ``open()`` and ``save()``. Implement:
- ``PDFDocument``: Specific open/save for PDF
- ``WordDocument``: Specific open/save for Word
- ``TextDocument``: Specific open/save for Text
Create a function that processes any document type.

*Hint:* Each document type should print different messages in ``open()`` and ``save()`` methods showing format-specific operations.

**15. Notification System with Multiple Channels**

Create an abstract class ``Notification`` with abstract method ``send(message, recipient)``. Implement:
- ``EmailNotification``: Send via email
- ``SMSNotification``: Send via SMS
- ``PushNotification``: Send push notification
- ``WhatsAppNotification``: Send via WhatsApp
Create a function to send the same message through multiple channels.

*Hint:* Store notification objects in a list and iterate. Each ``send()`` should print how the message is delivered.

Advanced OOP
------------

**16. Library Management System**

Create a complete library system with:
- Abstract class ``LibraryItem`` with title, ID, and abstract methods
- Classes: ``Book``, ``Magazine``, ``DVD`` inheriting from LibraryItem
- Class ``Member`` with name, ID, and borrowed items list
- Class ``Library`` managing items and members
Implement borrowing, returning, and searching functionality.

*Hint:* Use composition (Library contains items and members). Track borrowed items per member. Check availability before borrowing.

**17. Banking System with Multiple Account Types**

Create a banking system with:
- Abstract class ``Account`` with abstract method ``calculate_interest()``
- ``SavingsAccount``: Fixed interest rate, minimum balance requirement
- ``CurrentAccount``: No interest, overdraft facility
- ``FixedDeposit``: High interest, locked period, penalty for early withdrawal
- Class ``Bank`` managing multiple accounts
Implement deposit, withdrawal, interest calculation, and account statements.

*Hint:* Use inheritance for account types. Override ``calculate_interest()`` in each. Bank class should maintain a list of accounts.

**18. E-Commerce Product Catalog**

Create a product catalog system with:
- Abstract class ``Product`` with abstract method ``calculate_price()``
- ``Electronics``: warranty period affects price
- ``Clothing``: size and brand affect price
- ``Grocery``: expiry date affects price (discount near expiry)
- Class ``ShoppingCart`` with multiple products
- Implement discount coupons (percentage or fixed amount)
Calculate final bill with all discounts.

*Hint:* Use polymorphism for price calculation. Cart stores list of products. Apply discounts at cart level.

Operator Overloading
--------------------

**19. Complex Number Operations**

Create a class ``ComplexNumber`` representing complex numbers (a + bi). Overload:
- ``+`` for addition: (a + bi) + (c + di) = (a+c) + (b+d)i
- ``-`` for subtraction
- ``*`` for multiplication: (a + bi)(c + di) = (ac - bd) + (ad + bc)i
- ``==`` for equality comparison
- ``__str__`` for display format "a + bi"

*Hint:* Use ``__add__``, ``__sub__``, ``__mul__``, ``__eq__``, ``__str__``. For multiplication, expand (a+bi)(c+di).

**20. Time Duration Calculator**

Create a class ``Duration`` representing time in hours and minutes. Overload:
- ``+`` to add two durations
- ``-`` to subtract durations
- ``>`` and ``<`` for comparison
- ``__str__`` for display as "Xh Ym"
Handle minute overflow (60 minutes = 1 hour).

*Hint:* Convert to total minutes for comparison. For addition: add minutes, handle overflow with ``//`` and ``%``.

Real-World Projects
-------------------

**21. Hotel Booking System**

Create a complete hotel booking system with:
- Abstract class ``Room`` with room number, type, and price
- Room types: ``StandardRoom``, ``DeluxeRoom``, ``Suite`` (different prices and amenities)
- Class ``Guest`` with personal details
- Class ``Booking`` linking guest, room, check-in/out dates
- Class ``Hotel`` managing rooms and bookings
Implement booking, cancellation, and availability checking.

*Hint:* Use inheritance for room types. Track booking dates to check availability. Calculate total cost based on number of nights.

**22. University Management System**

Create a university system with:
- Class ``Person`` as base (name, ID, contact)
- ``Student`` class: courses enrolled, grades
- ``Professor`` class: courses teaching, department
- ``Course`` class: course code, name, professor, enrolled students
- ``Department`` class: managing courses and faculty
Implement enrollment, grade assignment, and course management.

*Hint:* Use inheritance from Person. Use composition (Course contains professor and students). Maintain bidirectional relationships.

**23. Online Food Delivery System**

Create a food delivery system with:
- Abstract class ``MenuItem`` with abstract method ``prepare()``
- Menu items: ``Pizza``, ``Burger``, ``Beverage`` with different preparation
- Class ``Order`` containing multiple menu items
- Class ``Customer`` with address and order history
- Class ``DeliveryPerson`` with current orders
- Calculate total bill with taxes and delivery charges
Implement order placement, preparation tracking, and delivery.

*Hint:* Use polymorphism for ``prepare()``. Order contains list of items. Calculate bill: sum of items + tax (18%) + delivery (₹50).

Testing and Validation
----------------------

**24. Create Test Cases**

For any of the above assignments (your choice), create a separate test program that:
- Creates multiple objects with different data
- Tests all methods thoroughly
- Tests edge cases (invalid inputs, boundary values)
- Prints results in organized format
- Verifies expected behavior

*Hint:* Test with valid and invalid inputs. Check boundary conditions (empty lists, zero values, negative numbers).

**25. Documentation and Code Quality**

Take your implementation of assignment 16, 17, or 18 and:
- Add comprehensive docstrings to all classes and methods
- Add inline comments for complex logic
- Use meaningful variable names
- Organize code with proper spacing and structure
- Create a README explaining how to use the system

*Hint:* Use triple quotes for docstrings: ``"""This method does..."""``. Explain parameters, return values, and exceptions.

--------------

Submission Guidelines
---------------------

.. note::
   - Test your code thoroughly before submission
   - Use meaningful variable and method names
   - Add comments for complex logic
   - Handle exceptions where appropriate
   - Include example usage/test cases for each program
   - Ensure code follows Python naming conventions (PEP 8)

--------------

Evaluation Criteria
-------------------

Your assignments will be evaluated on:

1. **Correctness**: Does the code work as expected?
2. **OOP Principles**: Proper use of classes, inheritance, encapsulation, etc.
3. **Code Quality**: Clean, readable, well-organized code
4. **Documentation**: Clear comments and docstrings
5. **Testing**: Comprehensive test cases
6. **Error Handling**: Appropriate validation and exception handling
