.. _module5_pandas_dataframes:

Pandas DataFrames: Data Analysis Made Easy
===========================================

Introduction
------------

Pandas is a powerful Python library for data manipulation and analysis. It provides DataFrames - table-like structures that make working with structured data intuitive and efficient.

.. note::
   Pandas is built on top of NumPy and is the go-to library for data analysis in Python. Think of it as Excel on steroids, but programmable and much more powerful! 🐼

--------------

Installing Pandas
-----------------

.. code-block:: bash

   pip install pandas

--------------

Baby Steps: Creating DataFrames
--------------------------------

**1. From Dictionaries**

.. code-block:: python

   import pandas as pd

   # Create DataFrame from dictionary
   data = {
       'Name': ['Alice', 'Bob', 'Charlie', 'Diana'],
       'Age': [20, 21, 19, 22],
       'Grade': [85, 78, 92, 88]
   }

   df = pd.DataFrame(data)
   print(df)
   #       Name  Age  Grade
   # 0    Alice   20     85
   # 1      Bob   21     78
   # 2  Charlie   19     92
   # 3    Diana   22     88

   # Check data types
   print(df.dtypes)
   # Name     object
   # Age       int64
   # Grade     int64

**2. From Lists of Lists**

.. code-block:: python

   import pandas as pd

   # Data as list of lists
   data = [
       ['Alice', 20, 85],
       ['Bob', 21, 78],
       ['Charlie', 19, 92],
       ['Diana', 22, 88]
   ]

   df = pd.DataFrame(data, columns=['Name', 'Age', 'Grade'])
   print(df)

**3. From CSV Files**

.. code-block:: python

   import pandas as pd

   # Read from CSV file
   df = pd.read_csv('students.csv')

   # Save to CSV file
   df.to_csv('output.csv', index=False)

.. note::
   CSV (Comma-Separated Values) files are the most common way to store tabular data. Pandas makes reading and writing CSV files incredibly easy!

--------------

DataFrame Basics
----------------

.. code-block:: python

   import pandas as pd

   data = {
       'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
       'Age': [20, 21, 19, 22, 20],
       'Grade': [85, 78, 92, 88, 75],
       'City': ['Mumbai', 'Delhi', 'Mumbai', 'Bangalore', 'Delhi']
   }

   df = pd.DataFrame(data)

   # Basic information
   print(df.shape)          # (5, 4) - 5 rows, 4 columns
   print(df.columns)        # Column names
   print(df.index)          # Row indices
   print(len(df))           # Number of rows

   # First and last rows
   print(df.head(3))        # First 3 rows
   print(df.tail(2))        # Last 2 rows

   # Statistical summary
   print(df.describe())     # Statistics for numerical columns

   # Information about DataFrame
   print(df.info())         # Data types and memory usage

--------------

Selecting Data
--------------

.. code-block:: python

   import pandas as pd

   data = {
       'Name': ['Alice', 'Bob', 'Charlie', 'Diana'],
       'Age': [20, 21, 19, 22],
       'Grade': [85, 78, 92, 88],
       'City': ['Mumbai', 'Delhi', 'Mumbai', 'Bangalore']
   }

   df = pd.DataFrame(data)

   # Select single column (returns Series)
   print(df['Name'])
   # 0      Alice
   # 1        Bob
   # 2    Charlie
   # 3      Diana

   # Select multiple columns (returns DataFrame)
   print(df[['Name', 'Grade']])

   # Select rows by index
   print(df.iloc[0])        # First row
   print(df.iloc[1:3])      # Rows 1 and 2

   # Select by label (if index has labels)
   print(df.loc[0, 'Name']) # Value at row 0, column 'Name'

   # Select specific cells
   print(df.at[0, 'Grade']) # 85

.. note::
   ``iloc`` uses integer positions (0, 1, 2...), while ``loc`` uses labels. For beginners, think of ``iloc`` as "integer location" and ``loc`` as "label location".

--------------

Filtering Data
--------------

.. code-block:: python

   import pandas as pd

   data = {
       'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
       'Age': [20, 21, 19, 22, 20],
       'Grade': [85, 78, 92, 88, 75],
       'City': ['Mumbai', 'Delhi', 'Mumbai', 'Bangalore', 'Delhi']
   }

   df = pd.DataFrame(data)

   # Filter students with grade >= 80
   high_scorers = df[df['Grade'] >= 80]
   print(high_scorers)

   # Multiple conditions (AND)
   young_high_scorers = df[(df['Age'] < 21) & (df['Grade'] >= 85)]
   print(young_high_scorers)

   # Multiple conditions (OR)
   mumbai_or_high = df[(df['City'] == 'Mumbai') | (df['Grade'] >= 90)]
   print(mumbai_or_high)

   # Filter by string methods
   names_with_e = df[df['Name'].str.contains('e')]
   print(names_with_e)

.. note::
   Use ``&`` for AND, ``|`` for OR, and ``~`` for NOT in conditions. Always use parentheses around each condition!

--------------

Adding and Modifying Data
--------------------------

.. code-block:: python

   import pandas as pd

   data = {
       'Name': ['Alice', 'Bob', 'Charlie'],
       'Age': [20, 21, 19],
       'Grade': [85, 78, 92]
   }

   df = pd.DataFrame(data)

   # Add new column
   df['Pass'] = df['Grade'] >= 80
   print(df)

   # Add calculated column
   df['Grade_Percent'] = (df['Grade'] / 100) * 100
   df['Age_Group'] = df['Age'].apply(lambda x: 'Teen' if x < 20 else 'Adult')
   
   # Modify existing column
   df['Grade'] = df['Grade'] + 5  # Bonus marks!

   # Add new row
   new_student = {'Name': 'Diana', 'Age': 22, 'Grade': 88, 'Pass': True}
   df = pd.concat([df, pd.DataFrame([new_student])], ignore_index=True)

   # Drop column
   df = df.drop('Grade_Percent', axis=1)

   # Drop row
   df = df.drop(0)  # Drop first row

--------------

Sorting Data
------------

.. code-block:: python

   import pandas as pd

   data = {
       'Name': ['Alice', 'Bob', 'Charlie', 'Diana'],
       'Age': [20, 21, 19, 22],
       'Grade': [85, 78, 92, 88]
   }

   df = pd.DataFrame(data)

   # Sort by single column
   df_sorted = df.sort_values('Grade', ascending=False)
   print(df_sorted)

   # Sort by multiple columns
   df_sorted = df.sort_values(['Age', 'Grade'], ascending=[True, False])
   print(df_sorted)

   # Sort index
   df_sorted = df.sort_index()

--------------

Grouping and Aggregation
-------------------------

.. code-block:: python

   import pandas as pd

   data = {
       'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve', 'Frank'],
       'City': ['Mumbai', 'Delhi', 'Mumbai', 'Delhi', 'Mumbai', 'Delhi'],
       'Grade': [85, 78, 92, 88, 75, 82],
       'Age': [20, 21, 19, 22, 20, 21]
   }

   df = pd.DataFrame(data)

   # Group by city and calculate mean
   city_avg = df.groupby('City')['Grade'].mean()
   print(city_avg)
   # City
   # Delhi     82.666667
   # Mumbai    84.000000

   # Multiple aggregations
   city_stats = df.groupby('City').agg({
       'Grade': ['mean', 'min', 'max'],
       'Age': 'mean'
   })
   print(city_stats)

   # Count students per city
   city_count = df.groupby('City').size()
   print(city_count)

.. note::
   ``groupby()`` is like SQL's GROUP BY - it splits data into groups and applies functions to each group independently.

--------------

Real-World Example: Student Performance Dashboard
--------------------------------------------------

.. code-block:: python

   import pandas as pd
   import numpy as np

   # Create realistic student data
   np.random.seed(42)
   
   data = {
       'Student_ID': range(1, 21),
       'Name': [f'Student_{i}' for i in range(1, 21)],
       'Python': np.random.randint(40, 100, 20),
       'Java': np.random.randint(40, 100, 20),
       'WebDev': np.random.randint(40, 100, 20),
       'Database': np.random.randint(40, 100, 20),
       'Attendance': np.random.randint(60, 100, 20)
   }

   df = pd.DataFrame(data)

   # Calculate total and average
   df['Total'] = df[['Python', 'Java', 'WebDev', 'Database']].sum(axis=1)
   df['Average'] = df[['Python', 'Java', 'WebDev', 'Database']].mean(axis=1)

   # Assign grades
   def assign_grade(avg):
       if avg >= 90: return 'A'
       elif avg >= 75: return 'B'
       elif avg >= 60: return 'C'
       elif avg >= 40: return 'D'
       else: return 'F'

   df['Grade'] = df['Average'].apply(assign_grade)

   # Find top 5 students
   top_5 = df.nlargest(5, 'Average')[['Name', 'Average', 'Grade']]
   print("=== Top 5 Students ===")
   print(top_5)

   # Subject-wise performance
   print("\n=== Subject Averages ===")
   subjects = ['Python', 'Java', 'WebDev', 'Database']
   for subject in subjects:
       avg = df[subject].mean()
       print(f"{subject}: {avg:.2f}")

   # Students needing attention
   struggling = df[df['Average'] < 60]
   print(f"\n=== Students Needing Help: {len(struggling)} ===")
   print(struggling[['Name', 'Average', 'Attendance']])

--------------

Handling Missing Data
---------------------

.. code-block:: python

   import pandas as pd
   import numpy as np

   data = {
       'Name': ['Alice', 'Bob', 'Charlie', 'Diana'],
       'Age': [20, np.nan, 19, 22],
       'Grade': [85, 78, np.nan, 88]
   }

   df = pd.DataFrame(data)

   # Check for missing values
   print(df.isnull())       # Boolean DataFrame
   print(df.isnull().sum()) # Count per column

   # Drop rows with any missing values
   df_dropped = df.dropna()

   # Fill missing values
   df_filled = df.fillna(0)                    # Fill with 0
   df_filled = df.fillna(df.mean())            # Fill with column mean
   df_filled = df.fillna(method='ffill')       # Forward fill
   df_filled = df.fillna({'Age': 20, 'Grade': 75})  # Different values per column

--------------

Merging and Joining DataFrames
-------------------------------

.. code-block:: python

   import pandas as pd

   # Student details
   students = pd.DataFrame({
       'Student_ID': [1, 2, 3, 4],
       'Name': ['Alice', 'Bob', 'Charlie', 'Diana']
   })

   # Student grades
   grades = pd.DataFrame({
       'Student_ID': [1, 2, 3, 4],
       'Grade': [85, 78, 92, 88],
       'Subject': ['Python', 'Python', 'Python', 'Python']
   })

   # Merge on Student_ID
   merged = pd.merge(students, grades, on='Student_ID')
   print(merged)

   # Concatenate vertically (stack DataFrames)
   more_students = pd.DataFrame({
       'Student_ID': [5, 6],
       'Name': ['Eve', 'Frank']
   })
   all_students = pd.concat([students, more_students], ignore_index=True)

--------------

Complete Example: Life Choices Tracker
---------------------------------------

.. code-block:: python

   import pandas as pd
   import numpy as np

   # Create the infamous Life Choices Tracker
   data = {
       'Decision': [
           'Chose CS',
           'Bought Expensive Course',
           'Believed I Could Code',
           'Started Learning AI',
           'Said Yes to Group Project',
           'Procrastinated Assignment',
           'Pulled All-Nighter',
           'Skipped Documentation',
           'Used ChatGPT for Assignment',
           'Promised to Exercise'
       ],
       'Confidence_Level': [9, 8, 10, 7, 6, 3, 8, 9, 7, 10],
       'Regret_Factor': [2, 7, 5, 6, 9, 10, 7, 8, 4, 9],
       'Friends_Who_Warned_You': [2, 5, 1, 3, 7, 8, 6, 4, 2, 10],
       'Time_Until_Realization': [365, 30, 7, 60, 2, 1, 1, 14, 3, 1]
   }

   df = pd.DataFrame(data)

   print("=== Life Choices Tracker ===\n")
   print(df)

   # Calculate correlation matrix
   print("\n=== Concerning Correlations ===")
   correlations = df[['Confidence_Level', 'Regret_Factor', 
                       'Friends_Who_Warned_You', 'Time_Until_Realization']].corr()
   print(correlations)

   # Key insights
   print("\n=== Reality Checks ===")
   
   # Correlation between confidence and regret
   conf_regret_corr = df['Confidence_Level'].corr(df['Regret_Factor'])
   print(f"Confidence vs Regret correlation: {conf_regret_corr:.2f}")
   if conf_regret_corr < -0.3:
       print("⚠️  Higher confidence = More regret (Dunning-Kruger effect detected!)")

   # Decisions with high regret
   high_regret = df[df['Regret_Factor'] >= 8]
   print(f"\nDecisions you wish you could undo: {len(high_regret)}")
   print(high_regret[['Decision', 'Regret_Factor']])

   # Average time to reality check
   avg_time = df['Time_Until_Realization'].mean()
   print(f"\nAverage days until reality hits: {avg_time:.1f} days")

   # Find most confident yet most regretted decision
   df['Confidence_Regret_Gap'] = df['Confidence_Level'] - df['Regret_Factor']
   worst_decision = df.loc[df['Confidence_Regret_Gap'].idxmin()]
   print(f"\nWorst decision: {worst_decision['Decision']}")
   print(f"Confidence: {worst_decision['Confidence_Level']}, Regret: {worst_decision['Regret_Factor']}")

   # Warnings ignored
   total_warnings = df['Friends_Who_Warned_You'].sum()
   print(f"\nTotal friend warnings ignored: {total_warnings}")
   print("(Maybe listen to your friends? Just a thought.)")

--------------

Advanced: String Operations
----------------------------

.. code-block:: python

   import pandas as pd

   data = {
       'Name': ['Alice Smith', 'Bob JONES', 'charlie brown'],
       'Email': ['alice@email.com', 'BOB@EMAIL.COM', 'charlie@email.com']
   }

   df = pd.DataFrame(data)

   # String methods
   df['Name_Upper'] = df['Name'].str.upper()
   df['Name_Lower'] = df['Name'].str.lower()
   df['First_Name'] = df['Name'].str.split().str[0]
   df['Email_Domain'] = df['Email'].str.split('@').str[1]
   df['Name_Length'] = df['Name'].str.len()

   print(df)

--------------

Tasks
-----

**Task 1: Personal Life Choices Analyzer**

Create a DataFrame called ``LifeChoicesTracker`` with at least 10 rows containing: Decision, Confidence_Level (1-10), Regret_Factor (1-10), Friends_Who_Warned_You, Time_Until_Realization (days). Calculate: (a) Correlation between all numerical columns, (b) Average regret factor, (c) Decisions where Confidence > 7 but Regret > 7, (d) Total warnings ignored.

*Hint:* Use ``df.corr()`` for correlation matrix. Use filtering: ``df[(df['Confidence_Level'] > 7) & (df['Regret_Factor'] > 7)]``.

**Task 2: Student Grade Management System**

Create a DataFrame with 15 students having: Name, Roll_No, Python, Java, WebDev, Database marks. Calculate: (a) Total and Average for each student, (b) Assign grades (A/B/C/D/F), (c) Find top 3 students, (d) Calculate subject-wise averages, (e) Find students below 60% average.

*Hint:* Add columns using ``df['Total'] = df[['Python', 'Java', 'WebDev', 'Database']].sum(axis=1)``. Use ``nlargest()`` for top students.

**Task 3: Time Tracking Reality Check**

Create a DataFrame with activities: Activity, Claimed_Hours, Actual_Hours for activities like Studying, Gaming, Social Media, Sleep, Productive Procrastination. Calculate: (a) Self-deception margin (Claimed - Actual), (b) Total claimed vs actual hours, (c) Activities where Claimed > Actual, (d) Biggest self-deception.

*Hint:* Add column: ``df['Deception'] = df['Claimed_Hours'] - df['Actual_Hours']``. Use ``idxmax()`` to find biggest deception.

**Task 4: Multi-City Student Performance**

Create a DataFrame with 20 students from 4 cities with Grade and Attendance. Use ``groupby()`` to calculate: (a) Average grade per city, (b) Average attendance per city, (c) City with highest performance, (d) Count of students per city, (e) Find city where attendance is high but grades are low.

*Hint:* Use ``groupby('City').agg({'Grade': 'mean', 'Attendance': 'mean'})``. Compare rankings of cities by grade vs attendance.

**Task 5: Semester Progress Tracker**

Create a DataFrame with Week (1-18), Study_Hours, Assignment_Completion (%), Motivation_Level (1-10), Coffee_Consumed (cups). Analyze: (a) Correlation between study hours and assignment completion, (b) Week with highest/lowest motivation, (c) Average coffee consumption, (d) Weeks where motivation < 5, (e) Create a "Productivity Score" = (Study_Hours × Assignment_Completion) / (Coffee_Consumed + 1).

*Hint:* Use ``df['Week'].loc[df['Motivation_Level'].idxmin()]`` to find week with lowest motivation. Calculate correlation: ``df['Study_Hours'].corr(df['Assignment_Completion'])``.

--------------

Time-Series Analysis with Pandas
---------------------------------

Time-series analysis involves working with data indexed by time. Pandas provides powerful tools for handling dates, times, and time-indexed data.

**Creating Datetime Data**

.. code-block:: python

   import pandas as pd
   import numpy as np
   from datetime import datetime, timedelta

   # Creating date ranges
   dates = pd.date_range(start='2024-01-01', end='2024-12-31', freq='D')
   print(f"Created {len(dates)} daily dates")

   # Different frequency options
   weekly_dates = pd.date_range(start='2024-01-01', periods=52, freq='W')
   monthly_dates = pd.date_range(start='2024-01-01', periods=12, freq='M')
   hourly_dates = pd.date_range(start='2024-01-01', periods=24, freq='H')

   print(f"Weekly dates: {len(weekly_dates)}")
   print(f"Monthly dates: {len(monthly_dates)}")
   print(f"Hourly dates: {len(hourly_dates)}")

**Basic Time-Series DataFrame**

.. code-block:: python

   import pandas as pd
   import numpy as np

   # Create sample sales data for a year
   dates = pd.date_range(start='2024-01-01', end='2024-12-31', freq='D')
   np.random.seed(42)

   # Simulate seasonal sales pattern
   days_of_year = np.arange(1, len(dates) + 1)
   seasonal_pattern = 100 + 50 * np.sin(2 * np.pi * days_of_year / 365)
   noise = np.random.normal(0, 20, len(dates))
   sales = seasonal_pattern + noise

   # Create time-series DataFrame
   df = pd.DataFrame({
       'date': dates,
       'sales': sales,
       'day_of_week': dates.day_name(),
       'month': dates.month_name(),
       'quarter': dates.quarter
   })

   # Set date as index
   df.set_index('date', inplace=True)

   print(df.head())
   print(f"\nDataFrame shape: {df.shape}")
   print(f"Date range: {df.index.min()} to {df.index.max()}")

**Time-Based Indexing and Slicing**

.. code-block:: python

   # Access specific dates
   print("Sales on 2024-01-15:")
   print(df.loc['2024-01-15'])

   # Access date ranges
   print("\nJanuary 2024 sales:")
   january_data = df.loc['2024-01']
   print(january_data.head())

   # Access specific months
   print("\nQ1 2024 (Jan-Mar):")
   q1_data = df.loc['2024-01':'2024-03']
   print(f"Q1 average sales: {q1_data['sales'].mean():.2f}")

   # Access by day of week
   print("\nMonday sales:")
   monday_sales = df[df['day_of_week'] == 'Monday']
   print(f"Average Monday sales: {monday_sales['sales'].mean():.2f}")

**Time-Series Resampling**

.. code-block:: python

   # Resample daily data to monthly
   monthly_sales = df['sales'].resample('M').agg({
       'mean': 'mean',
       'sum': 'sum',
       'count': 'count',
       'std': 'std'
   })

   print("Monthly Sales Summary:")
   print(monthly_sales.head())

   # Resample to weekly data
   weekly_sales = df['sales'].resample('W').agg(['mean', 'sum', 'max', 'min'])
   print("\nWeekly Sales Summary:")
   print(weekly_sales.head())

   # Custom resampling with multiple columns
   quarterly_summary = df.resample('Q').agg({
       'sales': ['mean', 'sum', 'std'],
       'day_of_week': lambda x: x.mode()[0] if len(x.mode()) > 0 else 'Unknown'
   })
   print("\nQuarterly Summary:")
   print(quarterly_summary)

**Rolling Window Analysis**

.. code-block:: python

   # Calculate moving averages
   df['sales_ma_7'] = df['sales'].rolling(window=7).mean()    # 7-day moving average
   df['sales_ma_30'] = df['sales'].rolling(window=30).mean()  # 30-day moving average

   # Calculate rolling statistics
   df['sales_rolling_std'] = df['sales'].rolling(window=30).std()
   df['sales_rolling_max'] = df['sales'].rolling(window=7).max()
   df['sales_rolling_min'] = df['sales'].rolling(window=7).min()

   print("Sales with Moving Averages:")
   print(df[['sales', 'sales_ma_7', 'sales_ma_30']].head(10))

   # Identify trends
   df['trend_signal'] = np.where(df['sales'] > df['sales_ma_30'], 'Above Average', 'Below Average')
   print(f"\nDays above 30-day average: {(df['trend_signal'] == 'Above Average').sum()}")

**Real-World Example: Website Traffic Analysis**

.. code-block:: python

   import pandas as pd
   import numpy as np

   # Create website traffic data
   dates = pd.date_range(start='2024-01-01', end='2024-12-31', freq='D')
   np.random.seed(123)

   # Simulate realistic web traffic patterns
   base_traffic = 1000
   weekend_boost = np.where(pd.Series(dates).dt.dayofweek >= 5, 200, 0)
   seasonal_effect = 300 * np.sin(2 * np.pi * np.arange(len(dates)) / 365)
   random_noise = np.random.normal(0, 100, len(dates))

   traffic_data = pd.DataFrame({
       'date': dates,
       'page_views': base_traffic + weekend_boost + seasonal_effect + random_noise,
       'unique_visitors': (base_traffic + weekend_boost + seasonal_effect + random_noise) * 0.3,
       'bounce_rate': np.random.uniform(0.2, 0.8, len(dates))
   })

   traffic_data.set_index('date', inplace=True)

   print("=== Website Traffic Analysis ===")
   print(traffic_data.head())

   # Add time-based features
   traffic_data['day_of_week'] = traffic_data.index.day_name()
   traffic_data['month'] = traffic_data.index.month_name()
   traffic_data['is_weekend'] = traffic_data.index.dayofweek >= 5

   # Daily analysis
   print(f"\nDaily Statistics:")
   print(f"Average daily page views: {traffic_data['page_views'].mean():.0f}")
   print(f"Peak day page views: {traffic_data['page_views'].max():.0f}")
   print(f"Lowest day page views: {traffic_data['page_views'].min():.0f}")

   # Weekly analysis
   weekly_stats = traffic_data.groupby('day_of_week').agg({
       'page_views': 'mean',
       'unique_visitors': 'mean',
       'bounce_rate': 'mean'
   }).round(2)

   print("\nDay of Week Analysis:")
   print(weekly_stats)

   # Monthly trends
   monthly_traffic = traffic_data.resample('M').agg({
       'page_views': 'sum',
       'unique_visitors': 'sum',
       'bounce_rate': 'mean'
   })

   print("\nMonthly Traffic Summary:")
   print(monthly_traffic.head())

   # Seasonal analysis
   seasonal_analysis = traffic_data.groupby(traffic_data.index.month).agg({
       'page_views': 'mean',
       'bounce_rate': 'mean'
   }).round(2)

   print("\nSeasonal Patterns (by month):")
   print(seasonal_analysis)

   # Growth analysis
   monthly_traffic['page_views_growth'] = monthly_traffic['page_views'].pct_change() * 100
   print("\nMonth-over-Month Growth:")
   print(monthly_traffic[['page_views', 'page_views_growth']].head(6))

**Advanced Time-Series Features**

.. code-block:: python

   # Lag features (previous period values)
   traffic_data['page_views_lag1'] = traffic_data['page_views'].shift(1)  # Previous day
   traffic_data['page_views_lag7'] = traffic_data['page_views'].shift(7)  # Same day last week

   # Forward looking features
   traffic_data['page_views_lead1'] = traffic_data['page_views'].shift(-1)  # Next day

   # Calculate differences
   traffic_data['daily_change'] = traffic_data['page_views'].diff()
   traffic_data['weekly_change'] = traffic_data['page_views'] - traffic_data['page_views_lag7']

   # Percent changes
   traffic_data['daily_pct_change'] = traffic_data['page_views'].pct_change() * 100

   print("Advanced Time-Series Features:")
   print(traffic_data[['page_views', 'page_views_lag1', 'daily_change', 'daily_pct_change']].head(10))

   # Time-based filtering
   peak_days = traffic_data[traffic_data['page_views'] > traffic_data['page_views'].quantile(0.9)]
   print(f"\nTop 10% traffic days: {len(peak_days)} days")
   print(f"Average page views on peak days: {peak_days['page_views'].mean():.0f}")

**Common Time-Series Use Cases:**

✅ **Business Applications:**
- Sales forecasting and trend analysis
- Website traffic monitoring
- Financial data analysis
- Inventory management
- Customer behavior tracking

✅ **Key Pandas Time-Series Functions:**
- ``pd.date_range()``: Create date sequences
- ``df.resample()``: Aggregate data by time periods
- ``df.rolling()``: Calculate moving window statistics
- ``df.shift()``: Create lag/lead features
- ``df.diff()``: Calculate differences between periods
- ``df.pct_change()``: Calculate percentage changes

.. note::
   **Time-series analysis** is crucial for understanding patterns, trends, and seasonality in data over time. Pandas makes it easy to work with dates and perform temporal analysis! 📈⏰

--------------

Summary
-------

- Pandas DataFrames are table-like structures for data analysis
- Create DataFrames from dictionaries, lists, or CSV files
- Select data using ``[]``, ``iloc``, ``loc`` indexing
- Filter data using boolean conditions
- Add/modify columns and rows easily
- Sort data using ``sort_values()``
- Group data using ``groupby()`` for aggregations
- Handle missing data with ``dropna()``, ``fillna()``
- Merge DataFrames using ``merge()`` and ``concat()``
- Calculate correlations using ``corr()``
- Pandas builds on NumPy and is essential for data analysis
