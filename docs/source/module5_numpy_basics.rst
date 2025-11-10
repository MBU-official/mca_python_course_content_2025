.. _module5_numpy_basics:

NumPy Basics: Arrays and Numerical Computing
=============================================

Introduction
------------

NumPy (Numerical Python) is the fundamental package for scientific computing in Python. It provides powerful tools for working with arrays, mathematical operations, and statistical analysis.

.. note::
   NumPy is essential for data science, machine learning, and scientific computing. It's much faster than regular Python lists for numerical operations because it uses optimized C code under the hood.

--------------

Installing NumPy
----------------

.. code-block:: bash

   pip install numpy

--------------

Why NumPy?
----------

**The Problem with Python Lists:**

.. code-block:: python

   # Using regular Python lists (slow for large data)
   numbers = [1, 2, 3, 4, 5]
   doubled = [x * 2 for x in numbers]
   print(doubled)  # [2, 4, 6, 8, 10]

**The NumPy Solution:**

.. code-block:: python

   import numpy as np

   # Using NumPy arrays (fast and efficient)
   numbers = np.array([1, 2, 3, 4, 5])
   doubled = numbers * 2
   print(doubled)  # [2 4 6 8 10]

.. note::
   NumPy operations are **vectorized** - they apply to entire arrays at once, making them 10-100x faster than Python loops for large datasets.

--------------

Baby Steps: Creating NumPy Arrays
----------------------------------

**1. From Python Lists**

.. code-block:: python

   import numpy as np

   # 1D array
   arr1 = np.array([1, 2, 3, 4, 5])
   print(arr1)           # [1 2 3 4 5]
   print(type(arr1))     # <class 'numpy.ndarray'>

   # 2D array (matrix)
   arr2 = np.array([[1, 2, 3], [4, 5, 6]])
   print(arr2)
   # [[1 2 3]
   #  [4 5 6]]

   # Check dimensions
   print(arr1.shape)     # (5,)
   print(arr2.shape)     # (2, 3) - 2 rows, 3 columns

**2. Using NumPy Functions**

.. code-block:: python

   # Array of zeros
   zeros = np.zeros(5)
   print(zeros)          # [0. 0. 0. 0. 0.]

   # Array of ones
   ones = np.ones((3, 4))
   print(ones)
   # [[1. 1. 1. 1.]
   #  [1. 1. 1. 1.]
   #  [1. 1. 1. 1.]]

   # Range of values
   range_arr = np.arange(0, 10, 2)  # start, stop, step
   print(range_arr)      # [0 2 4 6 8]

   # Evenly spaced values
   linear = np.linspace(0, 1, 5)    # start, stop, count
   print(linear)         # [0.   0.25 0.5  0.75 1.  ]

   # Random numbers
   random = np.random.rand(3, 3)    # 3x3 array of random values
   print(random)

.. note::
   ``np.arange()`` is similar to Python's ``range()``, but returns a NumPy array. ``np.linspace()`` is useful when you need a specific number of evenly spaced points.

--------------

Array Attributes and Information
---------------------------------

.. code-block:: python

   import numpy as np

   arr = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])

   print(arr.shape)      # (3, 4) - shape of array
   print(arr.ndim)       # 2 - number of dimensions
   print(arr.size)       # 12 - total number of elements
   print(arr.dtype)      # int32 or int64 - data type

   # Change data type
   arr_float = arr.astype(float)
   print(arr_float.dtype)  # float64

--------------

Array Indexing and Slicing
---------------------------

.. code-block:: python

   import numpy as np

   # 1D array indexing
   arr = np.array([10, 20, 30, 40, 50])
   print(arr[0])         # 10 - first element
   print(arr[-1])        # 50 - last element
   print(arr[1:4])       # [20 30 40] - slice

   # 2D array indexing
   matrix = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
   print(matrix[0, 0])   # 1 - row 0, column 0
   print(matrix[1, 2])   # 6 - row 1, column 2
   print(matrix[0])      # [1 2 3] - entire first row
   print(matrix[:, 0])   # [1 4 7] - entire first column

   # Slicing 2D arrays
   print(matrix[0:2, 1:3])
   # [[2 3]
   #  [5 6]]

--------------

Basic Array Operations
----------------------

.. code-block:: python

   import numpy as np

   arr1 = np.array([1, 2, 3, 4])
   arr2 = np.array([10, 20, 30, 40])

   # Element-wise operations
   print(arr1 + arr2)    # [11 22 33 44]
   print(arr1 - arr2)    # [-9 -18 -27 -36]
   print(arr1 * arr2)    # [10 40 90 160]
   print(arr2 / arr1)    # [10. 10. 10. 10.]
   print(arr1 ** 2)      # [1 4 9 16]

   # Scalar operations
   print(arr1 + 10)      # [11 12 13 14]
   print(arr1 * 2)       # [2 4 6 8]

   # Comparison operations
   print(arr1 > 2)       # [False False  True  True]
   print(arr2 == 30)     # [False False  True False]

--------------

Statistical Functions (Important!)
-----------------------------------

.. code-block:: python

   import numpy as np

   # Student test scores
   scores = np.array([45, 67, 89, 56, 78, 90, 34, 88, 76, 82])

   print(f"Mean (Average): {np.mean(scores):.2f}")        # 70.50
   print(f"Median (Middle): {np.median(scores):.2f}")     # 77.00
   print(f"Standard Deviation: {np.std(scores):.2f}")     # 18.44
   print(f"Variance: {np.var(scores):.2f}")               # 340.05
   print(f"Minimum: {np.min(scores)}")                    # 34
   print(f"Maximum: {np.max(scores)}")                    # 90
   print(f"Sum: {np.sum(scores)}")                        # 705

.. note::
   **Standard Deviation** tells you how spread out the data is. Higher std = more variation. Lower std = more consistent values. If your std is higher than your average score... you might want to study more consistently! 📚

--------------

Real-World Example: Student Performance Analysis
-------------------------------------------------

.. code-block:: python

   import numpy as np

   # Weekly study hours for 10 students
   study_hours = np.array([5, 12, 8, 15, 3, 20, 7, 10, 18, 6])

   # Their exam scores (out of 100)
   exam_scores = np.array([45, 78, 60, 85, 35, 95, 55, 70, 92, 50])

   # Statistical analysis
   print("=== Study Hours Analysis ===")
   print(f"Average study time: {np.mean(study_hours):.2f} hours")
   print(f"Standard deviation: {np.std(study_hours):.2f} hours")
   print(f"Most hours studied: {np.max(study_hours)}")
   print(f"Least hours studied: {np.min(study_hours)}")

   print("\n=== Exam Scores Analysis ===")
   print(f"Average score: {np.mean(exam_scores):.2f}")
   print(f"Standard deviation: {np.std(exam_scores):.2f}")
   print(f"Highest score: {np.max(exam_scores)}")
   print(f"Lowest score: {np.min(exam_scores)}")

   # Find correlation (do more study hours = better scores?)
   correlation = np.corrcoef(study_hours, exam_scores)[0, 1]
   print(f"\nCorrelation: {correlation:.2f}")
   if correlation > 0.7:
       print("Strong positive correlation - studying helps!")
   elif correlation > 0.4:
       print("Moderate correlation - studying somewhat helps")
   else:
       print("Weak correlation - maybe study smarter, not harder?")

--------------

Advanced: Boolean Indexing and Filtering
-----------------------------------------

.. code-block:: python

   import numpy as np

   scores = np.array([45, 67, 89, 56, 78, 90, 34, 88, 76, 82])

   # Filter scores above 75
   high_scorers = scores[scores > 75]
   print(high_scorers)   # [89 78 90 88 76 82]

   # Count how many passed (>= 40)
   passed = scores[scores >= 40]
   print(f"Students passed: {len(passed)}/{len(scores)}")

   # Multiple conditions
   good_scores = scores[(scores >= 60) & (scores <= 85)]
   print(good_scores)    # [67 78 76 82]

--------------

Array Reshaping and Manipulation
---------------------------------

.. code-block:: python

   import numpy as np

   # Create 1D array
   arr = np.arange(1, 13)
   print(arr)            # [ 1  2  3  4  5  6  7  8  9 10 11 12]

   # Reshape to 3x4 matrix
   matrix = arr.reshape(3, 4)
   print(matrix)
   # [[ 1  2  3  4]
   #  [ 5  6  7  8]
   #  [ 9 10 11 12]]

   # Flatten back to 1D
   flat = matrix.flatten()
   print(flat)           # [ 1  2  3  4  5  6  7  8  9 10 11 12]

   # Transpose (flip rows and columns)
   transposed = matrix.T
   print(transposed)
   # [[ 1  5  9]
   #  [ 2  6 10]
   #  [ 3  7 11]
   #  [ 4  8 12]]

--------------

Real-World Application: Grade Book Analysis
--------------------------------------------

.. code-block:: python

   import numpy as np

   # 5 students, 4 subjects (Python, Java, Web Dev, Database)
   grades = np.array([
       [85, 78, 90, 88],  # Student 1
       [67, 72, 68, 70],  # Student 2
       [92, 88, 95, 90],  # Student 3
       [45, 50, 48, 52],  # Student 4
       [78, 82, 80, 85]   # Student 5
   ])

   # Calculate average per student (axis=1 means across columns)
   student_averages = np.mean(grades, axis=1)
   print("Student averages:", student_averages)

   # Calculate average per subject (axis=0 means across rows)
   subject_averages = np.mean(grades, axis=0)
   print("Subject averages:", subject_averages)

   # Find top performer
   top_student = np.argmax(student_averages)
   print(f"Top student: Student {top_student + 1}")

   # Find easiest subject
   easiest_subject = np.argmax(subject_averages)
   subjects = ['Python', 'Java', 'Web Dev', 'Database']
   print(f"Easiest subject: {subjects[easiest_subject]}")

   # Find students who need help (average < 60)
   struggling = np.where(student_averages < 60)[0]
   print(f"Students needing help: {struggling + 1}")

.. note::
   ``axis=0`` operates on rows (down), ``axis=1`` operates on columns (across). Think of it as: axis=0 gives you one result per column, axis=1 gives you one result per row.

--------------

Advanced: Random Data Generation
---------------------------------

.. code-block:: python

   import numpy as np

   # Set seed for reproducibility
   np.random.seed(42)

   # Random integers
   dice_rolls = np.random.randint(1, 7, size=10)
   print("Dice rolls:", dice_rolls)

   # Random floats (0 to 1)
   probabilities = np.random.rand(5)
   print("Random probabilities:", probabilities)

   # Random from normal distribution (mean=100, std=15)
   iq_scores = np.random.normal(100, 15, size=20)
   print("IQ scores:", iq_scores)

   # Random choice from array
   students = np.array(['Alice', 'Bob', 'Charlie', 'Diana'])
   lucky_winner = np.random.choice(students)
   print(f"Random winner: {lucky_winner}")

--------------

Complete Example: Semester Performance Tracker
-----------------------------------------------

.. code-block:: python

   import numpy as np

   # Simulate 18 weeks of motivation levels (1-10 scale)
   np.random.seed(42)
   motivation = np.array([
       9, 8, 7, 6, 5, 4, 3, 4, 5, 3, 2, 3, 4, 5, 6, 4, 3, 2
   ])

   print("=== University Student Motivation Analysis ===")
   print(f"Weeks tracked: {len(motivation)}")
   print(f"Mean motivation: {np.mean(motivation):.2f}")
   print(f"Median motivation: {np.median(motivation):.2f}")
   print(f"Standard deviation: {np.std(motivation):.2f}")
   print(f"Highest motivation: {np.max(motivation)} (Week {np.argmax(motivation) + 1})")
   print(f"Lowest motivation: {np.min(motivation)} (Week {np.argmin(motivation) + 1})")

   # Reality check
   if np.std(motivation) > np.mean(motivation):
       print("\n⚠️  Reality Check: Your motivation varies more than it exists!")
       print("Standard deviation > Mean suggests emotional roller coaster mode.")
   
   # Count bad weeks
   bad_weeks = np.sum(motivation < 5)
   print(f"\nWeeks below 5 motivation: {bad_weeks}/{len(motivation)}")
   
   # Statistical significance check
   if np.mean(motivation) < 5:
       print("Status: Statistically Depressing 😢")
   elif np.mean(motivation) < 7:
       print("Status: Statistically Surviving 😐")
   else:
       print("Status: Statistically Thriving 🎉")

--------------

Advanced Mathematical Operations
---------------------------------

.. code-block:: python

   import numpy as np

   arr = np.array([1, 4, 9, 16, 25])

   # Mathematical functions
   print(np.sqrt(arr))           # [1. 2. 3. 4. 5.]
   print(np.exp(np.array([1, 2, 3])))  # [2.71828183 7.3890561 20.08553692]
   print(np.log(arr))            # [0.         1.38629436 2.19722458 2.77258872 3.21887582]

   # Trigonometric functions
   angles = np.array([0, 30, 45, 60, 90])
   radians = np.deg2rad(angles)
   print(np.sin(radians))

   # Rounding
   values = np.array([1.23456, 2.34567, 3.45678])
   print(np.round(values, 2))    # [1.23 2.35 3.46]
   print(np.floor(values))       # [1. 2. 3.]
   print(np.ceil(values))        # [2. 3. 4.]

--------------

Tasks
-----

**Task 1: Daily Motivation Tracker**

Create a NumPy array representing your daily motivation levels (1-10) for 18 weeks (126 days). Use ``np.random.randint(1, 11, 126)`` to generate data. Calculate mean, median, standard deviation, and determine if your motivation is "statistically significant" or "statistically depressing". Print a reality check if std > mean.

*Hint:* Use ``np.mean()``, ``np.median()``, ``np.std()``. Compare std with mean for the reality check.

**Task 2: Grade Book Manager**

Create a 2D array for 8 students and 5 subjects with random grades (0-100). Calculate: (a) Average grade per student, (b) Average grade per subject, (c) Overall class average, (d) Find top student and easiest subject, (e) Count students with average >= 75.

*Hint:* Use ``axis=1`` for student averages, ``axis=0`` for subject averages. Use ``np.argmax()`` to find indices.

**Task 3: Coffee vs Code Quality Study**

Create two arrays: ``coffee_cups`` (0-10) and ``bugs_per_100_lines`` (0-50) for 20 developers. Use ``np.random`` to generate data. Calculate correlation using ``np.corrcoef()``. Determine if the relationship is positive (more coffee = more bugs) or negative (more coffee = fewer bugs).

*Hint:* ``correlation = np.corrcoef(arr1, arr2)[0, 1]``. If correlation > 0, it's positive; if < 0, it's negative.

**Task 4: Exam Score Analyzer with Filtering**

Generate 50 random exam scores (0-100). Create separate arrays for: (a) Students who passed (>= 40), (b) Students with distinction (>= 75), (c) Students who failed (< 40). Calculate statistics for each group and print percentage distribution.

*Hint:* Use boolean indexing: ``passed = scores[scores >= 40]``. Use ``len()`` to count elements.

**Task 5: Multi-Dimensional Performance Dashboard**

Create a 3D array representing [10 students × 4 subjects × 3 exams]. Generate random grades. Calculate: (a) Each student's overall average, (b) Each subject's average across all students and exams, (c) Each exam's difficulty (lower average = harder), (d) Find the best performing student-subject combination.

*Hint:* Use ``np.random.randint(40, 100, (10, 4, 3))`` for 3D array. Use multiple axis parameters in mean: ``np.mean(arr, axis=(1,2))`` averages across subjects and exams.

--------------

Summary
-------

- NumPy provides fast, efficient arrays for numerical computing
- Create arrays using ``np.array()``, ``np.zeros()``, ``np.ones()``, ``np.arange()``, ``np.linspace()``
- Access elements using indexing and slicing similar to Python lists
- Perform vectorized operations (faster than loops)
- Use statistical functions: ``mean()``, ``median()``, ``std()``, ``min()``, ``max()``
- Boolean indexing allows filtering data based on conditions
- ``axis`` parameter controls direction of operations (0=rows, 1=columns)
- Use ``reshape()`` to change array dimensions
- NumPy is the foundation for Pandas, Matplotlib, and most data science libraries
