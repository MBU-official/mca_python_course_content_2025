.. _module5_matplotlib_visualization:

Matplotlib: Data Visualization
===============================

Introduction
------------

Matplotlib is Python's most popular library for creating static, interactive, and animated visualizations. It helps turn data into insights through charts and graphs.

.. note::
   "A picture is worth a thousand words" - especially in data analysis! Matplotlib makes it easy to create publication-quality charts that tell your data's story. 📊

--------------

Installing Matplotlib
---------------------

.. code-block:: bash

   pip install matplotlib

--------------

Baby Steps: Your First Plot
----------------------------

.. code-block:: python

   import matplotlib.pyplot as plt

   # Simple line plot
   x = [1, 2, 3, 4, 5]
   y = [2, 4, 6, 8, 10]

   plt.plot(x, y)
   plt.show()

**Adding Labels and Title:**

.. code-block:: python

   import matplotlib.pyplot as plt

   x = [1, 2, 3, 4, 5]
   y = [2, 4, 6, 8, 10]

   plt.plot(x, y)
   plt.xlabel('X-axis Label')
   plt.ylabel('Y-axis Label')
   plt.title('My First Plot')
   plt.grid(True)  # Add grid
   plt.show()

.. note::
   Always label your axes and add a title! A chart without labels is like a story without context.

--------------

Line Graphs
-----------

**Single Line:**

.. code-block:: python

   import matplotlib.pyplot as plt

   weeks = [1, 2, 3, 4, 5, 6, 7, 8]
   confidence = [9, 8, 7, 5, 4, 3, 5, 6]

   plt.plot(weeks, confidence, marker='o', linestyle='-', color='blue', linewidth=2)
   plt.xlabel('Weeks into Semester')
   plt.ylabel('Confidence Level (1-10)')
   plt.title('The Reality of Learning Python')
   plt.grid(True, alpha=0.3)
   plt.show()

**Multiple Lines:**

.. code-block:: python

   import matplotlib.pyplot as plt

   weeks = [1, 2, 3, 4, 5, 6, 7, 8]
   confidence = [9, 8, 7, 5, 4, 3, 5, 6]
   motivation = [10, 9, 7, 6, 4, 3, 4, 5]
   sleep_hours = [7, 6, 6, 5, 4, 3, 4, 5]

   plt.plot(weeks, confidence, marker='o', label='Confidence')
   plt.plot(weeks, motivation, marker='s', label='Motivation')
   plt.plot(weeks, sleep_hours, marker='^', label='Sleep Hours')

   plt.xlabel('Weeks into Semester')
   plt.ylabel('Level / Hours')
   plt.title('Student Life: A Visual Tragedy')
   plt.legend()  # Show legend
   plt.grid(True, alpha=0.3)
   plt.show()

--------------

Real-World Example: Learning Journey
-------------------------------------

.. code-block:: python

   import matplotlib.pyplot as plt
   import numpy as np

   # The emotional journey of learning Python
   events = ['Start', 'Hello\nWorld', 'Variables', 'Loops', 'Functions', 
             'OOP', 'Debugging', 'Projects', 'Realization']
   weeks = np.arange(len(events))
   confidence = [7, 10, 8, 6, 4, 3, 2, 5, 4]

   plt.figure(figsize=(12, 6))
   plt.plot(weeks, confidence, marker='o', linewidth=2, markersize=8, 
            color='#2962FF', markerfacecolor='orange')

   # Annotate key moments
   plt.annotate('Peak of Confidence', xy=(1, 10), xytext=(1.5, 9),
                arrowprops=dict(facecolor='green', shrink=0.05))
   plt.annotate('Valley of Despair', xy=(6, 2), xytext=(6.5, 3),
                arrowprops=dict(facecolor='red', shrink=0.05))

   plt.xticks(weeks, events, rotation=45)
   plt.xlabel('Learning Milestones')
   plt.ylabel('Confidence Level (1-10)')
   plt.title('The Emotional Journey of Learning Python\n(Emotional Support: You\'re Not Alone!)')
   plt.grid(True, alpha=0.3)
   plt.ylim(0, 11)
   plt.tight_layout()
   plt.show()

--------------

Bar Charts
----------

**Vertical Bars:**

.. code-block:: python

   import matplotlib.pyplot as plt

   subjects = ['Python', 'Java', 'WebDev', 'Database']
   scores = [85, 78, 92, 88]

   plt.bar(subjects, scores, color='skyblue', edgecolor='black')
   plt.xlabel('Subjects')
   plt.ylabel('Scores')
   plt.title('My Grades')
   plt.ylim(0, 100)
   plt.show()

**Horizontal Bars:**

.. code-block:: python

   import matplotlib.pyplot as plt

   subjects = ['Python', 'Java', 'WebDev', 'Database']
   scores = [85, 78, 92, 88]

   plt.barh(subjects, scores, color='lightcoral')
   plt.xlabel('Scores')
   plt.ylabel('Subjects')
   plt.title('My Grades (Horizontal)')
   plt.xlim(0, 100)
   plt.show()

**Grouped Bars:**

.. code-block:: python

   import matplotlib.pyplot as plt
   import numpy as np

   activities = ['Studying', 'Gaming', 'Social Media', 'Sleep', 'Procrastination']
   claimed_hours = [8, 2, 1, 8, 1]
   actual_hours = [3, 6, 4, 5, 6]

   x = np.arange(len(activities))
   width = 0.35

   fig, ax = plt.subplots(figsize=(10, 6))
   bars1 = ax.bar(x - width/2, claimed_hours, width, label='Claimed Hours', 
                   color='lightgreen', edgecolor='black')
   bars2 = ax.bar(x + width/2, actual_hours, width, label='Actual Hours',
                   color='salmon', edgecolor='black')

   ax.set_xlabel('Activities')
   ax.set_ylabel('Hours per Day')
   ax.set_title('Time Spent vs Time Claimed to Spend\n(Why Time Tracking Apps Make Students Cry)')
   ax.set_xticks(x)
   ax.set_xticklabels(activities, rotation=45)
   ax.legend()
   ax.grid(True, alpha=0.3, axis='y')

   plt.tight_layout()
   plt.show()

.. note::
   Grouped bar charts are perfect for comparing two or more sets of data across categories. Notice how "Actual Hours" tells a very different story than "Claimed Hours"! 😅

--------------

Scatter Plots
-------------

**Basic Scatter Plot:**

.. code-block:: python

   import matplotlib.pyplot as plt

   study_hours = [2, 4, 6, 8, 10, 3, 5, 7, 9, 11]
   grades = [50, 60, 70, 80, 90, 55, 65, 75, 85, 95]

   plt.scatter(study_hours, grades, color='purple', s=100, alpha=0.6)
   plt.xlabel('Study Hours per Week')
   plt.ylabel('Grade (%)')
   plt.title('Study Hours vs Grades')
   plt.grid(True, alpha=0.3)
   plt.show()

**Advanced Scatter with Categories:**

.. code-block:: python

   import matplotlib.pyplot as plt
   import numpy as np

   # Coffee consumption vs code quality study
   np.random.seed(42)

   # Different student categories
   tea_drinkers_coffee = np.random.uniform(0, 2, 10)
   tea_drinkers_bugs = np.random.uniform(10, 30, 10)

   moderate_coffee = np.random.uniform(2, 5, 10)
   moderate_bugs = np.random.uniform(5, 20, 10)

   addicts_coffee = np.random.uniform(5, 8, 10)
   addicts_bugs = np.random.uniform(15, 40, 10)

   zombies_coffee = np.random.uniform(8, 12, 10)
   zombies_bugs = np.random.uniform(30, 60, 10)

   plt.figure(figsize=(10, 6))
   plt.scatter(tea_drinkers_coffee, tea_drinkers_bugs, 
               label='Tea Drinkers', s=100, alpha=0.6, marker='o')
   plt.scatter(moderate_coffee, moderate_bugs, 
               label='Moderate Coffee Users', s=100, alpha=0.6, marker='s')
   plt.scatter(addicts_coffee, addicts_bugs, 
               label='Caffeine Addicts', s=100, alpha=0.6, marker='^')
   plt.scatter(zombies_coffee, zombies_bugs, 
               label='Energy Drink Zombies', s=100, alpha=0.6, marker='D')

   plt.xlabel('Coffee Cups per Day')
   plt.ylabel('Bugs per 100 Lines of Code')
   plt.title('Relationship Between Coffee Consumption and Code Quality\n(Correlation ≠ Causation... or does it?)')
   plt.legend()
   plt.grid(True, alpha=0.3)
   plt.tight_layout()
   plt.show()

--------------

Pie Charts
----------

.. code-block:: python

   import matplotlib.pyplot as plt

   activities = ['Actually Studying', 'Planning to Study', 'Netflix Research',
                 'Social Media\nNetworking', 'Existential Crisis', 'Sleep']
   time_spent = [5, 15, 25, 30, 15, 10]
   colors = ['#ff6b6b', '#4ecdc4', '#45b7d1', '#96ceb4', '#ffeaa7', '#dfe6e9']
   explode = (0, 0.1, 0.1, 0.1, 0, 0)  # Explode some slices

   plt.figure(figsize=(10, 8))
   plt.pie(time_spent, labels=activities, colors=colors, autopct='%1.1f%%',
           startangle=90, explode=explode, shadow=True)
   plt.title('Where My Semester Went\n(A Pie Chart of Regret)', fontsize=14, fontweight='bold')
   plt.axis('equal')  # Equal aspect ratio ensures circular pie
   plt.tight_layout()
   plt.show()

.. note::
   Pie charts are great for showing proportions, but use them sparingly. If you have more than 6-7 categories, consider a bar chart instead!

--------------

Histograms
----------

.. code-block:: python

   import matplotlib.pyplot as plt
   import numpy as np

   # Generate random exam scores
   np.random.seed(42)
   scores = np.random.normal(70, 15, 100)  # mean=70, std=15, 100 students

   plt.figure(figsize=(10, 6))
   plt.hist(scores, bins=20, color='steelblue', edgecolor='black', alpha=0.7)
   plt.xlabel('Exam Scores')
   plt.ylabel('Number of Students')
   plt.title('Distribution of Exam Scores')
   plt.axvline(scores.mean(), color='red', linestyle='--', linewidth=2, 
               label=f'Mean: {scores.mean():.1f}')
   plt.legend()
   plt.grid(True, alpha=0.3, axis='y')
   plt.show()

--------------

Subplots (Multiple Plots)
--------------------------

.. code-block:: python

   import matplotlib.pyplot as plt
   import numpy as np

   # Create 2x2 grid of plots
   fig, axs = plt.subplots(2, 2, figsize=(12, 10))

   # Plot 1: Line graph
   weeks = np.arange(1, 9)
   confidence = [9, 8, 7, 5, 4, 3, 5, 6]
   axs[0, 0].plot(weeks, confidence, marker='o', color='blue')
   axs[0, 0].set_title('Confidence Over Time')
   axs[0, 0].grid(True, alpha=0.3)

   # Plot 2: Bar chart
   subjects = ['Py', 'Java', 'Web', 'DB']
   scores = [85, 78, 92, 88]
   axs[0, 1].bar(subjects, scores, color='green')
   axs[0, 1].set_title('Subject Scores')

   # Plot 3: Scatter plot
   study = np.random.rand(20) * 10
   grades = study * 8 + np.random.rand(20) * 10
   axs[1, 0].scatter(study, grades, color='red', alpha=0.6)
   axs[1, 0].set_title('Study vs Grades')

   # Plot 4: Pie chart
   activities = ['Study', 'Gaming', 'Sleep', 'Other']
   time = [20, 30, 25, 25]
   axs[1, 1].pie(time, labels=activities, autopct='%1.1f%%')
   axs[1, 1].set_title('Time Distribution')

   plt.tight_layout()
   plt.show()

--------------

Customization and Styling
--------------------------

.. code-block:: python

   import matplotlib.pyplot as plt
   import numpy as np

   # Use built-in styles
   plt.style.use('seaborn-v0_8-darkgrid')  # or 'ggplot', 'bmh', 'fivethirtyeight'

   x = np.linspace(0, 10, 100)
   y = np.sin(x)

   plt.figure(figsize=(10, 6))
   plt.plot(x, y, linewidth=3, color='#2962FF')
   plt.xlabel('X', fontsize=14, fontweight='bold')
   plt.ylabel('Y', fontsize=14, fontweight='bold')
   plt.title('Sine Wave', fontsize=16, fontweight='bold')
   plt.grid(True, alpha=0.3)
   plt.show()

   # Reset to default style
   plt.style.use('default')

--------------

Saving Figures
--------------

.. code-block:: python

   import matplotlib.pyplot as plt

   x = [1, 2, 3, 4, 5]
   y = [2, 4, 6, 8, 10]

   plt.plot(x, y)
   plt.title('My Plot')

   # Save in different formats
   plt.savefig('my_plot.png', dpi=300, bbox_inches='tight')
   plt.savefig('my_plot.pdf', bbox_inches='tight')
   plt.savefig('my_plot.jpg', dpi=150, bbox_inches='tight')

   plt.show()

.. note::
   Always use ``bbox_inches='tight'`` to avoid cutting off labels. Higher DPI (dots per inch) = better quality but larger file size. 300 DPI is good for printing.

--------------

Tasks
-----

**Task 1: Emotional Journey Visualization**

Create a line graph titled "The Emotional Journey of Learning Python" with weeks (1-12) on x-axis and confidence level (1-10) on y-axis. Include data points for: Week 1 (confidence=9, "First Hello World"), Week 3 (confidence=7, "Variables"), Week 5 (confidence=4, "Discovered Debugging"), Week 8 (confidence=6, "Understood OOP"), Week 12 (confidence=3, "Realized How Much I Don't Know"). Add annotations for key events.

*Hint:* Use ``plt.annotate()`` with ``xy`` and ``xytext`` parameters. Use ``plt.plot()`` with ``marker='o'`` for data points.

**Task 2: Time Reality Check Bar Chart**

Create a grouped bar chart comparing "Time Claimed" vs "Actual Time" for 5 activities: Studying, Gaming, Social Media, Productive Procrastination, Sleep. Use different colors for each group. Add error bars representing ±2 hours "Self-Deception Margin". Include subtitle: "Why Time Tracking Apps Make Students Cry".

*Hint:* Use ``plt.bar()`` with ``x - width/2`` and ``x + width/2`` for grouped bars. Add ``yerr`` parameter for error bars.

**Task 3: Coffee vs Code Quality Scatter Plot**

Create a scatter plot with coffee_cups_per_day (0-10) on x-axis and bugs_per_hundred_lines (0-50) on y-axis. Create 4 categories: Tea Drinkers (0-2 cups), Moderate (2-5 cups), Addicts (5-8 cups), Zombies (8+ cups). Use different colors and markers for each. Add a trend line using ``np.polyfit()`` and ``np.poly1d()``.

*Hint:* Generate random data for each category. Use ``np.polyfit(x, y, 1)`` for linear fit, then ``plt.plot()`` for trend line.

**Task 4: Semester Distribution Pie Chart**

Create a pie chart titled "Where My Semester Went" with slices: Actually Studying (8%), Planning to Study (20%), Netflix Research (25%), Social Media Networking (22%), Existential Crisis (15%), Sleep (10%). Use custom colors reflecting emotional states. Explode the "Netflix Research" slice. Add percentage labels.

*Hint:* Use ``explode`` parameter as tuple with 0.1 for slices to explode. Use ``autopct='%1.1f%%'`` for percentages.

**Task 5: Multi-Plot Dashboard**

Create a 2×2 subplot figure showing: (1) Line: Motivation over 8 weeks, (2) Bar: Grades in 4 subjects, (3) Scatter: Study hours vs Assignment scores, (4) Histogram: Distribution of daily screen time. Add appropriate titles, labels, and styling to each subplot.

*Hint:* Use ``fig, axs = plt.subplots(2, 2, figsize=(12, 10))``. Access plots using ``axs[row, col]``. Use ``plt.tight_layout()`` to prevent overlap.

--------------

Summary
-------

- Matplotlib is the standard library for data visualization in Python
- ``plt.plot()`` creates line graphs
- ``plt.bar()`` and ``plt.barh()`` create bar charts
- ``plt.scatter()`` creates scatter plots
- ``plt.pie()`` creates pie charts
- ``plt.hist()`` creates histograms
- Always add labels, titles, and legends for clarity
- Use ``plt.subplots()`` to create multiple plots
- Customize colors, markers, line styles for better visuals
- Save figures using ``plt.savefig()``
- Matplotlib works seamlessly with NumPy and Pandas
