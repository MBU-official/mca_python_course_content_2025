.. _module5_assignment:

Module 5: Assignment Questions
===============================

.. note::
   These assignments integrate **NumPy**, **Pandas**, **Matplotlib**, and **Flask**. Build real-world projects that showcase your data science and web development skills! Focus on creating functional, well-styled applications with proper visualizations. 🚀✨

--------------

NumPy Assignments
-----------------

**1. Daily Motivation Levels Tracker** 📊

Create a NumPy-based motivation tracking system for a week (7 days):

- Generate a random motivation array (1-10 scale) for 7 days
- Calculate: average motivation, standard deviation, maximum motivation day, minimum motivation day
- Create a "motivation forecast" for next week by adding random noise to this week's average
- Identify "crisis days" (motivation < 4) and "peak days" (motivation > 8)
- Calculate how many days you were "barely surviving" (< 5) vs "thriving" (> 7)

*Hint:* Use ``np.random.randint(1, 11, 7)`` for random data. Use ``np.mean()``, ``np.std()``, ``np.max()``, ``np.argmax()`` for statistics. Boolean indexing: ``array[array < 4]``.

**2. Grade Analysis System** 🎓

Create a grade analyzer for a class of 30 students across 5 subjects:

- Generate random grades (0-100) using NumPy: ``np.random.randint(0, 101, (30, 5))``
- Calculate each student's average (use ``axis=1``)
- Find top 5 students and bottom 5 students
- Calculate class average for each subject (use ``axis=0``)
- Identify students at risk (average < 50)
- Calculate standard deviation per subject to find hardest/easiest subject
- Create a "normalized" grade array (scale all grades to 0-1 range using min-max normalization)

*Hint:* Use ``np.mean(array, axis=0)`` for column-wise mean. Use ``np.argsort()`` to find top/bottom students. Min-max normalization: ``(x - min) / (max - min)``.

**3. Expense Tracker with Budget Analysis** 💰

Create an expense tracking system for a month:

- Generate 30 days of random expenses across 4 categories: Food, Transport, Entertainment, Others
- Each category has different spending ranges (Food: 50-200, Transport: 20-100, etc.)
- Calculate total spent, average daily spending, spending per category
- Find the most expensive day and category
- Calculate how much over/under budget (assume budget = 4000)
- Create a "spending pattern" array showing percentage distribution across categories
- Identify days where total spending exceeded 200 (danger zone!)

*Hint:* Use ``np.random.randint()`` with different ranges for each category. Stack category arrays: ``np.column_stack()``. Use ``np.sum(axis=1)`` for daily totals.

**4. Time Series Analysis: Sleep Tracker** 😴

Build a sleep pattern analyzer:

- Generate 30 days of sleep data: hours slept (4-12 range, floats)
- Calculate average sleep, sleep debt (assuming 8 hours needed per night)
- Find longest sleep, shortest sleep, and their dates
- Create a "sleep quality" array: Good (≥8h), Okay (6-8h), Poor (<6h)
- Count number of days in each quality category
- Calculate rolling 7-day average sleep (hint: use array slicing in a loop)
- Identify "insomnia weeks" where average < 6 hours

*Hint:* Use ``np.random.uniform(4, 12, 30)`` for float data. For rolling average: ``np.mean(array[i:i+7])`` in a loop. Use ``np.where()`` for conditional categorization.

**5. Matrix Operations: Social Network** 🌐

Create a simple social network adjacency matrix:

- Generate a 10x10 matrix representing friend connections (0 or 1)
- Make it symmetric (if A is friend with B, B is friend with A)
- Set diagonal to 0 (no self-friendship!)
- Calculate: number of friends per person (row sum), most popular person, least popular person
- Find mutual friends: people who have ≥5 common friends
- Create a "friend recommendation" system: suggest people who are friends-of-friends but not direct friends

*Hint:* Generate with ``np.random.randint(0, 2, (10, 10))``. Make symmetric: ``matrix = (matrix + matrix.T) > 0``. Diagonal: ``np.fill_diagonal(matrix, 0)``. Matrix multiplication for friends-of-friends!

--------------

Pandas Assignments
------------------

**6. Life Choices Tracker Dashboard** 🎯

Create a life decisions analyzer using Pandas:

- Create DataFrame with columns: Date, Decision, Category, Regret_Level (1-10), Impact (Positive/Negative/Neutral), Lessons_Learned
- Add at least 20 life decisions (use past month dates)
- Categories: Academic, Career, Social, Health, Finance
- Analyze:
  - Average regret level by category
  - Count of positive/negative/neutral impacts
  - Most regrettable category
  - Filter decisions with regret > 7 (major mistakes!)
  - Group by category and calculate mean regret
  - Find correlation between regret and impact type

*Hint:* Use ``pd.DataFrame()``. ``df.groupby('Category')['Regret_Level'].mean()`` for group analysis. ``df[df['Regret_Level'] > 7]`` for filtering.

**7. COVID-Style Study Hours Analysis** 📚

Build a study pattern analyzer:

- Create DataFrame: Date, Subject, Hours_Studied, Distractions (count), Productivity (1-10), Mood (Happy/Neutral/Sad)
- 30 rows of data across 5 subjects
- Analysis tasks:
  - Total hours per subject
  - Average productivity by mood
  - Correlation between distractions and productivity
  - Best/worst study day (highest/lowest total hours)
  - Subject with highest average productivity
  - Create "efficiency score": Hours * Productivity / (Distractions + 1)
  - Filter days where productivity < 4 (crisis days!)

*Hint:* Use ``pd.to_datetime()`` for date column. ``df.groupby(['Subject', 'Mood']).agg({'Hours_Studied': 'sum', 'Productivity': 'mean'})``. Use ``df.corr()`` for correlation.

**8. Movie Binge Tracker** 🎬

Create a movie watching analysis system:

- DataFrame columns: Date, Title, Genre, Duration_Minutes, Rating (1-5), Platform, Watched_With, Mood_After
- Add 25+ movie entries
- Analysis:
  - Total hours binged
  - Average rating by genre
  - Most binged genre
  - Platform with highest average rating
  - Correlation between duration and rating
  - Filter movies watched alone vs with friends, compare ratings
  - Create "binge score": (Duration/60) * Rating

*Hint:* Use ``pd.cut()`` to categorize duration into Short/Medium/Long. ``df.groupby('Genre')['Rating'].agg(['mean', 'count'])``.

**9. Food Delivery Analysis** 🍕

Build a food ordering pattern analyzer:

- DataFrame: Date, Restaurant, Cuisine, Cost, Delivery_Time, Rating, Day_of_Week, Meal_Type (Breakfast/Lunch/Dinner)
- 40+ orders across different restaurants
- Analysis tasks:
  - Total spent
  - Average cost by cuisine
  - Most ordered cuisine
  - Average rating by restaurant
  - Correlation between delivery time and rating
  - Filter: expensive orders (cost > 300), poor ratings (< 3)
  - Group by day of week: which day you order most?
  - Create "value score": Rating / (Cost/100)

*Hint:* Extract day: ``df['Date'].dt.day_name()``. Pivot table: ``df.pivot_table(values='Cost', index='Day_of_Week', columns='Cuisine', aggfunc='sum')``.

**10. Fitness Challenge Tracker** 💪

Create a fitness progress analyzer:

- DataFrame: Date, Exercise, Duration_Minutes, Calories_Burned, Difficulty (Easy/Medium/Hard), Completed (Yes/No), Mood_Before, Mood_After
- 30 days of workout data
- Analysis:
  - Total calories burned
  - Average duration by difficulty
  - Completion rate (percentage)
  - Correlation between duration and calories
  - Compare mood before vs after (create mood improvement column)
  - Filter: incomplete workouts, analyze why
  - Group by exercise type: which burns most calories per minute?

*Hint:* Create calculated column: ``df['Mood_Improvement'] = df['Mood_After'] - df['Mood_Before']``. Use ``df['Completed'].value_counts(normalize=True)`` for completion percentage.

--------------

Matplotlib Assignments
----------------------

**11. Emotional Journey Visualization** 😊😢

Create a multi-chart emotional tracking dashboard:

- Generate 30 days of emotion data: Happiness, Stress, Energy (all 0-10 scales)
- Create 4 subplots:
  - Line plot: All three emotions over time
  - Bar plot: Average of each emotion
  - Scatter plot: Happiness vs Stress (show negative correlation?)
  - Pie chart: Days categorized as Good (H>7), Okay (4-7), Bad (<4)
- Use different colors, labels, titles, legends
- Add annotations for peak stress and lowest energy days

*Hint:* Use ``plt.subplots(2, 2, figsize=(15, 10))``. Use ``ax.annotate()`` for annotations. Color maps: ``plt.cm.rainbow()``.

**12. Academic Performance Dashboard** 📊

Create a comprehensive grade visualization:

- 5 subjects, 6 exams each (30 data points)
- Visualizations:
  - Line plot: Grade trends per subject across exams
  - Bar plot: Average grade per subject (sorted)
  - Horizontal bar: Improvement from Exam 1 to Exam 6 per subject
  - Histogram: Distribution of all grades
- Add grid, custom colors, legends
- Use emojis in titles! 🎓📈

*Hint:* Use ``plt.subplots(2, 2)``. For improvement: ``final_grades - initial_grades``. Histogram: ``plt.hist(all_grades, bins=10, edgecolor='black')``.

**13. Budget Breakdown Pie Chart** 💰

Create a beautiful expense breakdown visualization:

- Categories: Food, Rent, Transport, Entertainment, Shopping, Bills, Savings
- Create:
  - Pie chart with percentages, explode largest expense
  - Donut chart (same as pie but with circle in center)
  - Bar plot: Expense comparison
- Use custom color palette
- Add shadow, startangle for better look
- Display actual amounts in legend

*Hint:* Explode: ``explode = (0.1, 0, 0, 0, 0, 0, 0)`` for first slice. Donut: ``plt.pie(...); plt.Circle((0,0), 0.70, color='white'); plt.gca().add_artist(circle)``.

**14. Time Series: Social Media Usage** 📱

Visualize social media addiction patterns:

- 30 days, 4 platforms: Instagram, Twitter, YouTube, WhatsApp (hours per day)
- Create:
  - Stacked area plot: Cumulative usage across platforms
  - Line plot with multiple lines (one per platform)
  - Scatter plot: Total daily usage vs day number (trend?)
  - Box plot: Usage distribution per platform
- Add horizontal line at y=5 (danger zone!)
- Color code platforms: Instagram (purple), Twitter (blue), YouTube (red), WhatsApp (green)

*Hint:* Stacked area: ``plt.stackplot(x, y1, y2, y3, y4, labels=[...], alpha=0.7)``. Box plot: ``plt.boxplot([data1, data2, data3, data4], labels=[...])``.

**15. Advanced: Interactive Dashboard (Multiple Plots)** 🎨

Create a 3x2 subplot dashboard combining all skills:

- Top row: Line plot (motivation), Bar plot (category comparison), Pie chart (distribution)
- Bottom row: Scatter plot (correlation), Histogram (distribution), Box plot (outliers)
- Use tight_layout, shared x-axis where appropriate
- Custom color scheme throughout
- Add overall title with ``plt.suptitle()``

*Hint:* Use ``fig, axes = plt.subplots(2, 3, figsize=(18, 10))``. Access subplots: ``axes[0, 0]``, ``axes[0, 1]``, etc. Use ``plt.tight_layout()``.

--------------

Flask Web Development Assignments
----------------------------------

**16. Rate My Life Choices (CRUD App)** 🎯

Build a complete life decision tracker web app:

Features:
- Home page: List all decisions with ratings
- Add decision: Form with fields (date, decision, category, rating 1-5, consequences, regret level)
- View decision details: Individual page showing full info
- Edit decision: Update any field
- Delete decision: With confirmation and farewell message
- Statistics page: Show counts by category, average rating, most regrettable category

Styling requirements:
- Use gradient backgrounds
- Color-code categories
- Add emojis for ratings (⭐ for stars)
- Responsive design with CSS

*Hint:* Use list of dictionaries for storage. Implement all CRUD routes. Use ``render_template()`` with data. Add CSS in ``<style>`` or external file.

**17. Student Survival Guide (Multi-Page Flask)** 🎓

Create an interactive survival guide for college:

Pages:
- Home: Welcome page with navigation
- Crisis Center: Different crisis types (Academic, Social, Mental Health, Financial) with advice
- Motivation API: Route that returns random motivational quote (use list of 20+ quotes)
- Confession Booth: Anonymous confessions (create/view)
- Resource Library: Links categorized (Study Tools, Mental Health, Career, Fun)
- About: About the project with stats (total confessions, most common crisis)

Requirements:
- Template inheritance (base.html)
- At least 3 forms
- Dynamic routes (e.g., ``/crisis/<type>``)
- Beautiful navigation bar
- Emojis everywhere!

*Hint:* Create ``base.html`` with nav bar and ``{% block content %}``. Use ``{% extends "base.html" %}`` in other templates. Store data in global lists/dicts.

**18. Mood Journal with Visualization** 🌈

Build a mood tracking app with data visualization:

Features:
- Add mood entry: Date, mood (1-10), activities (checkboxes), notes
- View all entries: List with color-coded moods
- Statistics page: 
  - Total entries
  - Average mood
  - Most common activities
  - Generate simple bar chart (HTML/CSS, not matplotlib) showing mood distribution
- Filter: View entries by date range or mood level

Bonus: 
- Use Flask sessions to store username
- Add login page (simple, no database needed)

*Hint:* Store entries in list. For HTML bar chart: Use ``<div style="height: {{ value }}px">`` with different heights. Use ``request.args.get()`` for filters.

**19. Recipe Manager with Search** 🍕

Create a recipe management system:

Features:
- Add recipe: Name, ingredients (textarea), instructions, cooking time, difficulty, cuisine type, emoji
- View all recipes: Grid/card layout
- View recipe details: Full page with all info
- Edit recipe
- Delete recipe
- Search: By name, cuisine type, or ingredient
- Filter: By difficulty or cooking time range

Styling:
- Card-based layout for recipe list
- Food-themed colors
- Image placeholders (use emoji as "images")
- Hover effects on cards

*Hint:* Search: ``[r for r in recipes if search_term.lower() in r['name'].lower()]``. Use ``request.args.get('search')`` for GET parameters.

**20. Goal Tracker with Progress** 🎯

Build an advanced goal tracking system:

Features:
- Dashboard: All goals with progress bars, statistics (completion rate, total goals, etc.)
- Add goal: Title, description, target date, category, initial progress
- Update progress: Form to update progress percentage
- Mark complete: Celebration page with confetti animation (CSS/HTML)
- Delete goal: Farewell ceremony
- Categories page: Filter goals by category, show category-wise statistics
- Calendar view: Show goals by target date

Advanced:
- Progress visualization using CSS progress bars
- Color-coding: Red (<30%), Yellow (30-70%), Green (>70%)
- Overdue goals indicator (past target date, not complete)
- Achievement badges: First goal, 5 goals completed, etc.

*Hint:* Use datetime to compare dates. CSS progress bar: ``<div style="width: {{ progress }}%; background: green; height: 20px;">``. Use ``{{ "%.0f"|format(value) }}`` to format numbers.

--------------

Integrated Projects (Multiple Technologies)
--------------------------------------------

**21. Personal Dashboard (NumPy + Pandas + Matplotlib + Flask)** 🚀

Build a complete personal analytics dashboard:

Backend:
- Use NumPy to generate sample data for 30 days
- Use Pandas to store and analyze data
- Generate Matplotlib charts, save as images in ``static/`` folder
- Use Flask to serve web interface

Features:
- Home page with navigation
- Data entry form: Daily data (mood, hours studied, hours on social media, money spent, exercise done)
- Analytics page: Display saved chart images
- Statistics page: Show Pandas dataframes as HTML tables
- Raw data page: Show all data in table format

Charts to generate:
- Line plot: Mood over time
- Bar plot: Average hours by activity
- Scatter plot: Study hours vs mood (correlation?)
- Pie chart: Time distribution

*Hint:* Save matplotlib figures: ``plt.savefig('static/chart.png')``. In HTML: ``<img src="{{ url_for('static', filename='chart.png') }}">``. Convert DataFrame to HTML: ``df.to_html()``.

**22. Expense Analyzer Web App** 💰

Full-stack expense tracking:

Features:
- Add expense form (date, category, amount, description, payment method)
- View all expenses table (sortable by date/amount)
- Analytics page:
  - Total spent
  - Pandas DataFrame showing category-wise totals
  - Matplotlib pie chart: Expense breakdown
  - Matplotlib line plot: Daily spending trend
  - Bar chart: Category comparison
- Filter page: Filter by date range, category, or amount range
- Budget page: Set budget, show how much spent vs remaining (progress bar)

Data processing:
- Use Pandas DataFrame to store expenses
- Use NumPy for statistical calculations
- Use Matplotlib to generate charts (save as PNG)

*Hint:* Store DataFrame as global variable or save to CSV using ``df.to_csv('data.csv')``. Load with ``pd.read_csv()``. Generate multiple charts in one route, save with different names.

**23. Study Tracker with Smart Insights** 📚

Advanced study analytics platform:

Features:
- Log study session: Subject, duration, quality (1-10), distractions, date
- Dashboard:
  - Total hours studied
  - Hours per subject (bar chart)
  - Quality over time (line chart)
  - Distractions analysis (scatter: distractions vs quality)
  - Subject distribution (pie chart)
- Insights page (calculate using NumPy/Pandas):
  - Most productive subject (highest average quality)
  - Best study time (if you track time of day)
  - Correlation: Hours studied vs quality
  - Weekly report: Last 7 days summary
  - Recommendations based on data

Advanced:
- Use Pandas for data storage and analysis
- NumPy for statistical calculations
- Matplotlib for all visualizations
- Flask for web interface with beautiful styling

*Hint:* Calculate correlations using Pandas: ``df['Hours'].corr(df['Quality'])``. Generate insights dynamically. Use templates to display calculated values.

**24. Social Media Usage Analyzer** 📱

Track and analyze social media addiction:

Data to track:
- Date, platform (Instagram/Twitter/YouTube/etc.), time_spent (minutes), posts_viewed, posts_created, mood_after

Features:
- Add usage form
- Usage history table
- Analytics dashboard:
  - Total time by platform (bar chart)
  - Daily usage trend (line plot)
  - Platform distribution (pie chart)
  - Usage patterns (heat map style using HTML/CSS)
  - Correlation: Time spent vs mood
- Addiction calculator:
  - Calculate daily average
  - Show "addiction level" (Low/Medium/High/Critical)
  - Recommendations to reduce usage
- Goals: Set daily limits, track if achieved

Visualizations:
- Stacked area plot: Cumulative usage across platforms
- Box plot: Usage distribution
- Scatter plot: Time vs mood correlation

*Hint:* Use Pandas for grouping: ``df.groupby('Platform')['Time_Spent'].sum()``. Create addiction score: ``total_minutes / days``. Use thresholds: <60 (Low), 60-120 (Medium), >120 (High).

**25. Full-Stack Learning Journey Tracker** 🎓

Comprehensive learning analytics platform (Final Boss Project!):

Data model:
- Skills (id, name, category, date_started, date_completed, confidence_level, time_invested)
- Daily logs (id, skill_id, date, hours, quality, notes, challenges)
- Resources (id, skill_id, title, url, type, completed)

Features:
1. **Dashboard**:
   - Total skills, completed skills, in-progress skills
   - Total time invested
   - Charts: Skills by category (pie), Progress over time (line), Confidence distribution (histogram)

2. **Skills Manager**:
   - Add/Edit/Delete/View skills
   - CRUD operations with validation
   - Color-coded by status (Not started/In progress/Completed)

3. **Daily Logger**:
   - Log daily learning sessions
   - Link to skill
   - Track time, quality, challenges faced

4. **Analytics Page**:
   - Skill-wise time investment (bar chart)
   - Quality over time (line plot)
   - Correlation: Time vs Confidence
   - Weekly/Monthly reports using Pandas
   - Heat map: Learning intensity by day of week

5. **Resources Library**:
   - Add learning resources (articles, videos, courses)
   - Link to skills
   - Track completion
   - Filter by type/skill

6. **Insights**:
   - Most productive skill (highest quality sessions)
   - Struggling areas (low quality, high time)
   - Recommendations: "You've invested 50 hours in Python but confidence is only 40% - consider more practice projects!"
   - Learning velocity: Hours per confidence point gained

Technical requirements:
- Flask with template inheritance
- Pandas DataFrames for data storage
- NumPy for calculations
- Matplotlib for 5+ different chart types
- Beautiful CSS styling with gradients, animations
- Mobile-responsive design
- Form validation
- Confirmation dialogs for delete operations

*Hint:* This is a large project - break it down! Start with basic CRUD, then add logging, then add analytics. Store data in multiple DataFrames or use CSV files. Generate charts in separate routes, save to static folder. Use Jinja2 to dynamically generate tables from DataFrames.

--------------

Bonus Challenge: API Integration 🌟
------------------------------------

**26. Flask App with Data API**

Create a Flask app that:
- Accepts form input for mood, activities, notes
- Stores in Pandas DataFrame
- Provides JSON API endpoints:
  - ``/api/moods`` - Returns all moods as JSON
  - ``/api/stats`` - Returns statistics
  - ``/api/chart-data`` - Returns data formatted for charts
- Create a simple HTML page that fetches data using JavaScript ``fetch()`` and displays it

*Hint:* Use ``jsonify()`` from Flask: ``from flask import jsonify; return jsonify(df.to_dict('records'))``. In HTML: ``fetch('/api/moods').then(r => r.json()).then(data => console.log(data))``.

--------------

Summary
-------

These assignments cover:
- ✅ **NumPy**: Array operations, statistics, matrix operations
- ✅ **Pandas**: DataFrames, grouping, filtering, analysis
- ✅ **Matplotlib**: Line, bar, scatter, pie, histogram, subplots
- ✅ **Flask**: Routes, templates, forms, CRUD, Jinja2
- ✅ **Integration**: Combining all technologies

Tips for success:
- Start simple, add features gradually 🐛➡️🦋
- Test each function before moving on 🧪
- Use emojis and colors to make projects fun! 🎨
- Comment your code so you remember what you did 📝
- Save your matplotlib figures before displaying 💾
- Use template inheritance to avoid repetition ♻️
- Store data properly (lists, dicts, DataFrames, CSV) 🗄️

Good luck! Build amazing projects! 🚀✨
