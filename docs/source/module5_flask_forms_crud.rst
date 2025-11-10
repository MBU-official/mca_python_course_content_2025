.. _module5_flask_forms_crud:

Flask Forms, Templates & CRUD Operations
=========================================

Introduction
------------

Learn how to handle forms, use Jinja2 templates effectively, and implement CRUD (Create, Read, Update, Delete) operations to build real web applications! 📝✨

.. note::
   CRUD operations are the bread and butter of web apps! Almost every app needs to Create, Read, Update, and Delete data. Let's make it fun! 🎯

--------------

Jinja2 Template Basics
-----------------------

**Variables and Expressions:**

.. code-block:: html

   <!-- templates/home.html -->
   <!DOCTYPE html>
   <html>
   <head>
       <title>{{ page_title }} 🎨</title>
   </head>
   <body>
       <h1>Hello, {{ username }}! {{ emoji }}</h1>
       <p>You have {{ points }} points! ⭐</p>
       <p>Double points: {{ points * 2 }}</p>
   </body>
   </html>

**app.py:**

.. code-block:: python

   from flask import Flask, render_template

   app = Flask(__name__)

   @app.route('/')
   def home():
       return render_template('home.html',
                            page_title='My App',
                            username='Alice',
                            emoji='🎓',
                            points=100)

   if __name__ == '__main__':
       app.run(debug=True)

--------------

Loops in Templates
------------------

.. code-block:: html

   <!-- templates/students.html -->
   <!DOCTYPE html>
   <html>
   <head>
       <title>Student List 📚</title>
       <style>
           body { font-family: Arial; padding: 20px; }
           .student { 
               background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
               color: white;
               padding: 15px;
               margin: 10px 0;
               border-radius: 8px;
           }
       </style>
   </head>
   <body>
       <h1>Students 🎓</h1>
       {% for student in students %}
           <div class="student">
               {{ loop.index }}. {{ student.name }} - Grade: {{ student.grade }} 
               {% if student.grade >= 75 %}⭐{% else %}📚{% endif %}
           </div>
       {% endfor %}
   </body>
   </html>

**app.py:**

.. code-block:: python

   from flask import Flask, render_template

   app = Flask(__name__)

   @app.route('/students')
   def students():
       student_list = [
           {'name': 'Alice', 'grade': 85},
           {'name': 'Bob', 'grade': 72},
           {'name': 'Charlie', 'grade': 90}
       ]
       return render_template('students.html', students=student_list)

   if __name__ == '__main__':
       app.run(debug=True)

.. note::
   ``{% for %}`` loops through lists. ``loop.index`` gives the current iteration number (1-based). Use ``{% if %}`` for conditionals! 🔄

--------------

Template Inheritance (DRY Principle)
-------------------------------------

**base.html (Parent Template):**

.. code-block:: html

   <!-- templates/base.html -->
   <!DOCTYPE html>
   <html>
   <head>
       <title>{% block title %}My App{% endblock %} 🌟</title>
       <style>
           body {
               font-family: Arial, sans-serif;
               margin: 0;
               padding: 0;
               background: #f5f5f5;
           }
           nav {
               background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
               padding: 15px;
               color: white;
           }
           nav a {
               color: white;
               margin: 0 15px;
               text-decoration: none;
           }
           .container {
               max-width: 900px;
               margin: 30px auto;
               padding: 20px;
               background: white;
               border-radius: 10px;
               box-shadow: 0 4px 6px rgba(0,0,0,0.1);
           }
       </style>
   </head>
   <body>
       <nav>
           <a href="/">🏠 Home</a>
           <a href="/about">ℹ️ About</a>
           <a href="/contact">📧 Contact</a>
       </nav>
       <div class="container">
           {% block content %}{% endblock %}
       </div>
   </body>
   </html>

**home.html (Child Template):**

.. code-block:: html

   <!-- templates/home.html -->
   {% extends "base.html" %}

   {% block title %}Home{% endblock %}

   {% block content %}
       <h1>Welcome Home! 🏠</h1>
       <p>This page inherits from base.html! 🎉</p>
   {% endblock %}

--------------

Handling Forms (GET & POST)
----------------------------

**Simple Form Example:**

.. code-block:: python

   from flask import Flask, render_template, request, redirect, url_for

   app = Flask(__name__)

   # In-memory storage (resets when app restarts)
   confessions = []

   @app.route('/')
   def home():
       return render_template('confessions.html', confessions=confessions)

   @app.route('/submit', methods=['GET', 'POST'])
   def submit():
       if request.method == 'POST':
           category = request.form.get('category')
           confession = request.form.get('confession')
           emoji = request.form.get('emoji', '😅')
           
           confessions.append({
               'category': category,
               'confession': confession,
               'emoji': emoji
           })
           return redirect(url_for('home'))
       
       return render_template('submit_form.html')

   if __name__ == '__main__':
       app.run(debug=True)

**templates/submit_form.html:**

.. code-block:: html

   <!DOCTYPE html>
   <html>
   <head>
       <title>Student Confession Booth 🤐</title>
       <style>
           body {
               font-family: Arial;
               max-width: 600px;
               margin: 50px auto;
               padding: 20px;
               background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
           }
           .form-container {
               background: white;
               padding: 30px;
               border-radius: 15px;
               box-shadow: 0 10px 30px rgba(0,0,0,0.2);
           }
           h1 { color: #667eea; text-align: center; }
           input, select, textarea {
               width: 100%;
               padding: 10px;
               margin: 10px 0;
               border: 2px solid #ddd;
               border-radius: 5px;
               font-size: 16px;
           }
           button {
               width: 100%;
               padding: 15px;
               background: #667eea;
               color: white;
               border: none;
               border-radius: 5px;
               font-size: 18px;
               cursor: pointer;
           }
           button:hover {
               background: #764ba2;
           }
       </style>
   </head>
   <body>
       <div class="form-container">
           <h1>🤐 Anonymous Confession Booth</h1>
           <p style="text-align: center; color: #666;">
               Share your college struggles anonymously! 💭
           </p>
           <form method="POST" action="/submit">
               <label>Category:</label>
               <select name="category" required>
                   <option value="">Select a category...</option>
                   <option value="Academic Disasters">📚 Academic Disasters</option>
                   <option value="Social Awkwardness">🙈 Social Awkwardness</option>
                   <option value="Career Confusion">💼 Career Confusion</option>
                   <option value="General Life Failures">🤷 General Life Failures</option>
               </select>

               <label>Your Confession:</label>
               <textarea name="confession" rows="5" 
                         placeholder="Tell us what's on your mind..." 
                         required></textarea>

               <label>How do you feel?</label>
               <select name="emoji">
                   <option value="😅">😅 Embarrassed</option>
                   <option value="😢">😢 Sad</option>
                   <option value="😰">😰 Stressed</option>
                   <option value="🤷">🤷 Confused</option>
                   <option value="💪">💪 Ready to Change</option>
               </select>

               <button type="submit">Submit Confession 🚀</button>
           </form>
           <p style="text-align: center; margin-top: 20px;">
               <a href="/" style="color: #667eea;">← View All Confessions</a>
           </p>
       </div>
   </body>
   </html>

**templates/confessions.html:**

.. code-block:: html

   <!DOCTYPE html>
   <html>
   <head>
       <title>Confession Wall 📋</title>
       <style>
           body {
               font-family: Arial;
               max-width: 800px;
               margin: 50px auto;
               padding: 20px;
               background: #f5f5f5;
           }
           h1 { text-align: center; color: #667eea; }
           .confession {
               background: white;
               padding: 20px;
               margin: 15px 0;
               border-radius: 10px;
               border-left: 5px solid #667eea;
               box-shadow: 0 2px 5px rgba(0,0,0,0.1);
           }
           .category {
               background: #667eea;
               color: white;
               padding: 5px 15px;
               border-radius: 20px;
               display: inline-block;
               font-size: 14px;
               margin-bottom: 10px;
           }
           .add-btn {
               display: block;
               width: 200px;
               margin: 20px auto;
               padding: 15px;
               background: #667eea;
               color: white;
               text-align: center;
               text-decoration: none;
               border-radius: 8px;
               font-weight: bold;
           }
           .add-btn:hover {
               background: #764ba2;
           }
       </style>
   </head>
   <body>
       <h1>🤐 Student Confession Wall</h1>
       <p style="text-align: center; color: #666;">
           Anonymous confessions from fellow students 💭
       </p>

       <a href="/submit" class="add-btn">+ Add Your Confession</a>

       {% if confessions %}
           {% for confession in confessions %}
               <div class="confession">
                   <span class="category">{{ confession.category }}</span>
                   <p style="font-size: 18px; margin: 10px 0;">
                       {{ confession.emoji }} {{ confession.confession }}
                   </p>
               </div>
           {% endfor %}
       {% else %}
           <p style="text-align: center; color: #999; padding: 50px;">
               No confessions yet... be the first! 🤗
           </p>
       {% endif %}
   </body>
   </html>

.. note::
   ``redirect(url_for('home'))`` redirects to a route by function name. Use ``url_for()`` instead of hardcoding URLs! ✨

--------------

CRUD Operations: Learning Journey Tracker
------------------------------------------

Let's build a complete CRUD application! 🚀

**app.py:**

.. code-block:: python

   from flask import Flask, render_template, request, redirect, url_for
   from datetime import datetime

   app = Flask(__name__)

   # In-memory database (list of dictionaries)
   skills = [
       {'id': 1, 'name': 'Python Basics', 'status': 'Completed', 
        'confidence': 80, 'emoji': '🐍', 'date': '2025-01-15'},
       {'id': 2, 'name': 'Web Development', 'status': 'In Progress', 
        'confidence': 50, 'emoji': '🌐', 'date': '2025-02-01'},
       {'id': 3, 'name': 'Machine Learning', 'status': 'Started', 
        'confidence': 20, 'emoji': '🤖', 'date': '2025-02-20'},
   ]

   # Helper to get next ID
   def get_next_id():
       return max([s['id'] for s in skills], default=0) + 1

   # CREATE - Add new skill
   @app.route('/create', methods=['GET', 'POST'])
   def create():
       if request.method == 'POST':
           new_skill = {
               'id': get_next_id(),
               'name': request.form.get('name'),
               'status': request.form.get('status', 'Started'),
               'confidence': int(request.form.get('confidence', 0)),
               'emoji': request.form.get('emoji', '📚'),
               'date': datetime.now().strftime('%Y-%m-%d')
           }
           skills.append(new_skill)
           return redirect(url_for('read_all'))
       
       return render_template('create.html')

   # READ - View all skills
   @app.route('/')
   def read_all():
       # Calculate stats
       total = len(skills)
       completed = len([s for s in skills if s['status'] == 'Completed'])
       in_progress = len([s for s in skills if s['status'] == 'In Progress'])
       
       stats = {
           'total': total,
           'completed': completed,
           'in_progress': in_progress,
           'completion_rate': (completed / total * 100) if total > 0 else 0
       }
       
       return render_template('dashboard.html', skills=skills, stats=stats)

   # READ - View single skill
   @app.route('/skill/<int:skill_id>')
   def read_one(skill_id):
       skill = next((s for s in skills if s['id'] == skill_id), None)
       if skill:
           return render_template('detail.html', skill=skill)
       return "Skill not found! 🤷", 404

   # UPDATE - Edit skill
   @app.route('/update/<int:skill_id>', methods=['GET', 'POST'])
   def update(skill_id):
       skill = next((s for s in skills if s['id'] == skill_id), None)
       
       if not skill:
           return "Skill not found! 🤷", 404
       
       if request.method == 'POST':
           skill['name'] = request.form.get('name')
           skill['status'] = request.form.get('status')
           skill['confidence'] = int(request.form.get('confidence'))
           skill['emoji'] = request.form.get('emoji')
           return redirect(url_for('read_all'))
       
       return render_template('update.html', skill=skill)

   # DELETE - Remove skill (with farewell ceremony 👋)
   @app.route('/delete/<int:skill_id>', methods=['POST'])
   def delete(skill_id):
       global skills
       skill = next((s for s in skills if s['id'] == skill_id), None)
       
       if skill:
           skills = [s for s in skills if s['id'] != skill_id]
           return render_template('farewell.html', skill=skill)
       
       return "Skill not found! 🤷", 404

   if __name__ == '__main__':
       app.run(debug=True)

**templates/dashboard.html:**

.. code-block:: html

   <!DOCTYPE html>
   <html>
   <head>
       <title>Learning Journey Tracker 🚀</title>
       <style>
           * { margin: 0; padding: 0; box-sizing: border-box; }
           body {
               font-family: Arial, sans-serif;
               background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
               min-height: 100vh;
               padding: 20px;
           }
           .container {
               max-width: 1000px;
               margin: 0 auto;
           }
           .header {
               background: white;
               padding: 30px;
               border-radius: 15px;
               text-align: center;
               margin-bottom: 20px;
               box-shadow: 0 10px 30px rgba(0,0,0,0.2);
           }
           .stats {
               display: grid;
               grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
               gap: 15px;
               margin: 20px 0;
           }
           .stat-card {
               background: white;
               padding: 20px;
               border-radius: 10px;
               text-align: center;
               box-shadow: 0 4px 6px rgba(0,0,0,0.1);
           }
           .stat-number {
               font-size: 36px;
               font-weight: bold;
               color: #667eea;
           }
           .skill-grid {
               display: grid;
               grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
               gap: 20px;
               margin: 20px 0;
           }
           .skill-card {
               background: white;
               padding: 25px;
               border-radius: 15px;
               box-shadow: 0 4px 6px rgba(0,0,0,0.1);
               transition: transform 0.2s;
           }
           .skill-card:hover {
               transform: translateY(-5px);
               box-shadow: 0 8px 12px rgba(0,0,0,0.2);
           }
           .skill-emoji {
               font-size: 48px;
               display: block;
               margin-bottom: 15px;
           }
           .status {
               display: inline-block;
               padding: 5px 15px;
               border-radius: 20px;
               font-size: 12px;
               font-weight: bold;
               margin: 10px 0;
           }
           .status-completed { background: #2ecc71; color: white; }
           .status-inprogress { background: #f39c12; color: white; }
           .status-started { background: #3498db; color: white; }
           .confidence-bar {
               background: #ecf0f1;
               height: 20px;
               border-radius: 10px;
               overflow: hidden;
               margin: 10px 0;
           }
           .confidence-fill {
               height: 100%;
               background: linear-gradient(90deg, #667eea, #764ba2);
               transition: width 0.3s;
           }
           .btn {
               display: inline-block;
               padding: 10px 20px;
               margin: 5px;
               border-radius: 5px;
               text-decoration: none;
               font-weight: bold;
               transition: all 0.2s;
           }
           .btn-primary { background: #667eea; color: white; }
           .btn-secondary { background: #95a5a6; color: white; }
           .btn-danger { background: #e74c3c; color: white; }
           .btn:hover { opacity: 0.9; transform: scale(1.05); }
           .add-btn {
               position: fixed;
               bottom: 30px;
               right: 30px;
               width: 60px;
               height: 60px;
               border-radius: 50%;
               background: #2ecc71;
               color: white;
               font-size: 32px;
               display: flex;
               align-items: center;
               justify-content: center;
               text-decoration: none;
               box-shadow: 0 4px 8px rgba(0,0,0,0.3);
               transition: all 0.3s;
           }
           .add-btn:hover {
               transform: scale(1.1) rotate(90deg);
           }
       </style>
   </head>
   <body>
       <div class="container">
           <div class="header">
               <h1>🚀 My Learning Journey Tracker</h1>
               <p style="color: #666; margin-top: 10px;">
                   Track your skills, celebrate progress, and say goodbye to abandoned dreams! 😅
               </p>
           </div>

           <div class="stats">
               <div class="stat-card">
                   <div class="stat-number">{{ stats.total }}</div>
                   <div>Total Skills</div>
               </div>
               <div class="stat-card">
                   <div class="stat-number">{{ stats.completed }}</div>
                   <div>✅ Completed</div>
               </div>
               <div class="stat-card">
                   <div class="stat-number">{{ stats.in_progress }}</div>
                   <div>⏳ In Progress</div>
               </div>
               <div class="stat-card">
                   <div class="stat-number">{{ "%.0f"|format(stats.completion_rate) }}%</div>
                   <div>Completion Rate</div>
               </div>
           </div>

           <div class="skill-grid">
               {% for skill in skills %}
               <div class="skill-card">
                   <span class="skill-emoji">{{ skill.emoji }}</span>
                   <h3>{{ skill.name }}</h3>
                   
                   {% if skill.status == 'Completed' %}
                       <span class="status status-completed">✅ {{ skill.status }}</span>
                   {% elif skill.status == 'In Progress' %}
                       <span class="status status-inprogress">⏳ {{ skill.status }}</span>
                   {% else %}
                       <span class="status status-started">🚀 {{ skill.status }}</span>
                   {% endif %}
                   
                   <div style="margin: 15px 0;">
                       <small style="color: #666;">Confidence Level</small>
                       <div class="confidence-bar">
                           <div class="confidence-fill" 
                                style="width: {{ skill.confidence }}%"></div>
                       </div>
                       <small style="color: #666;">{{ skill.confidence }}%</small>
                   </div>
                   
                   <p style="color: #999; font-size: 12px;">
                       Started: {{ skill.date }}
                   </p>
                   
                   <div style="margin-top: 15px;">
                       <a href="/skill/{{ skill.id }}" class="btn btn-primary">
                           👁️ View
                       </a>
                       <a href="/update/{{ skill.id }}" class="btn btn-secondary">
                           ✏️ Edit
                       </a>
                       <form action="/delete/{{ skill.id }}" method="POST" 
                             style="display: inline;"
                             onsubmit="return confirm('Say goodbye to {{ skill.name }}? 👋')">
                           <button type="submit" class="btn btn-danger" 
                                   style="border: none; cursor: pointer;">
                               🗑️ Delete
                           </button>
                       </form>
                   </div>
               </div>
               {% endfor %}
           </div>

           {% if stats.total == 0 %}
           <div style="text-align: center; color: white; padding: 50px;">
               <h2>No skills yet! 🌱</h2>
               <p>Start your learning journey by adding your first skill! 🚀</p>
           </div>
           {% endif %}
       </div>

       <a href="/create" class="add-btn" title="Add New Skill">+</a>
   </body>
   </html>

**templates/create.html:**

.. code-block:: html

   <!DOCTYPE html>
   <html>
   <head>
       <title>Add New Skill 🌱</title>
       <style>
           body {
               font-family: Arial;
               background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
               min-height: 100vh;
               display: flex;
               align-items: center;
               justify-content: center;
               padding: 20px;
           }
           .form-container {
               background: white;
               padding: 40px;
               border-radius: 15px;
               box-shadow: 0 10px 30px rgba(0,0,0,0.2);
               max-width: 500px;
               width: 100%;
           }
           h1 { color: #667eea; text-align: center; margin-bottom: 30px; }
           label {
               display: block;
               margin-top: 15px;
               color: #333;
               font-weight: bold;
           }
           input, select {
               width: 100%;
               padding: 12px;
               margin-top: 5px;
               border: 2px solid #ddd;
               border-radius: 5px;
               font-size: 16px;
           }
           input:focus, select:focus {
               outline: none;
               border-color: #667eea;
           }
           button {
               width: 100%;
               padding: 15px;
               margin-top: 20px;
               background: #667eea;
               color: white;
               border: none;
               border-radius: 5px;
               font-size: 18px;
               font-weight: bold;
               cursor: pointer;
               transition: background 0.3s;
           }
           button:hover {
               background: #764ba2;
           }
           .back-link {
               display: block;
               text-align: center;
               margin-top: 20px;
               color: #667eea;
               text-decoration: none;
           }
       </style>
   </head>
   <body>
       <div class="form-container">
           <h1>🌱 Add New Skill</h1>
           <form method="POST">
               <label>Skill Name:</label>
               <input type="text" name="name" 
                      placeholder="e.g., Machine Learning" required>

               <label>Emoji:</label>
               <input type="text" name="emoji" 
                      placeholder="🤖" maxlength="2" required>

               <label>Status:</label>
               <select name="status" required>
                   <option value="Started">🚀 Started</option>
                   <option value="In Progress">⏳ In Progress</option>
                   <option value="Completed">✅ Completed</option>
               </select>

               <label>Confidence Level (0-100):</label>
               <input type="range" name="confidence" 
                      min="0" max="100" value="50" 
                      oninput="this.nextElementSibling.value = this.value + '%'">
               <output style="display: block; text-align: center; 
                             color: #667eea; font-weight: bold;">50%</output>

               <button type="submit">🎉 Add Skill</button>
           </form>
           <a href="/" class="back-link">← Back to Dashboard</a>
       </div>
   </body>
   </html>

**templates/farewell.html:**

.. code-block:: html

   <!DOCTYPE html>
   <html>
   <head>
       <title>Farewell Ceremony 👋</title>
       <style>
           body {
               font-family: Arial;
               background: linear-gradient(135deg, #e74c3c 0%, #c0392b 100%);
               min-height: 100vh;
               display: flex;
               align-items: center;
               justify-content: center;
               padding: 20px;
               color: white;
               text-align: center;
           }
           .ceremony {
               max-width: 600px;
               animation: fadeIn 1s;
           }
           @keyframes fadeIn {
               from { opacity: 0; transform: translateY(-20px); }
               to { opacity: 1; transform: translateY(0); }
           }
           .emoji {
               font-size: 100px;
               animation: float 3s ease-in-out infinite;
           }
           @keyframes float {
               0%, 100% { transform: translateY(0); }
               50% { transform: translateY(-20px); }
           }
           h1 { font-size: 48px; margin: 20px 0; }
           p { font-size: 20px; line-height: 1.6; }
           .btn {
               display: inline-block;
               margin-top: 30px;
               padding: 15px 30px;
               background: white;
               color: #e74c3c;
               text-decoration: none;
               border-radius: 8px;
               font-weight: bold;
               transition: transform 0.2s;
           }
           .btn:hover {
               transform: scale(1.05);
           }
       </style>
   </head>
   <body>
       <div class="ceremony">
           <div class="emoji">👋</div>
           <h1>Farewell, {{ skill.name }}!</h1>
           <p>
               {{ skill.emoji }} We bid farewell to "{{ skill.name }}".<br>
               You served us well with {{ skill.confidence }}% confidence.<br>
               May you rest in peace in the graveyard of abandoned skills. 🪦
           </p>
           <p style="font-style: italic; opacity: 0.8;">
               "It's not you, it's me." - Every developer ever 😅
           </p>
           <a href="/" class="btn">Return to Dashboard 🏠</a>
       </div>
   </body>
   </html>

.. note::
   This complete CRUD application demonstrates all four operations! Notice the beautiful styling, animations, and the humorous "farewell ceremony" for deleted skills! 🎭✨

--------------

Flash Messages
--------------

Show feedback messages after actions:

.. code-block:: python

   from flask import Flask, render_template, flash, redirect, url_for

   app = Flask(__name__)
   app.secret_key = 'your-secret-key-here'  # Required for flash messages

   @app.route('/submit', methods=['POST'])
   def submit():
       # Process form...
       flash('✅ Success! Your data was saved!', 'success')
       flash('⚠️ Warning: This is a demo!', 'warning')
       return redirect(url_for('home'))

   @app.route('/')
   def home():
       return render_template('home.html')

**In template:**

.. code-block:: html

   {% with messages = get_flashed_messages(with_categories=true) %}
       {% if messages %}
           {% for category, message in messages %}
               <div class="alert alert-{{ category }}">
                   {{ message }}
               </div>
           {% endfor %}
       {% endif %}
   {% endwith %}

--------------

File Upload and Download in Flask
----------------------------------

Flask can handle file uploads and serve files back to users. This is useful for document management, image uploads, PDF serving, and more.

**Basic File Upload Setup**

.. code-block:: python

   import os
   from flask import Flask, render_template, request, redirect, url_for, flash, send_file
   from werkzeug.utils import secure_filename

   app = Flask(__name__)
   app.secret_key = 'your-secret-key-here'

   # Configuration for file uploads
   UPLOAD_FOLDER = 'uploads'
   ALLOWED_EXTENSIONS = {'txt', 'pdf', 'png', 'jpg', 'jpeg', 'gif', 'doc', 'docx'}
   MAX_FILE_SIZE = 16 * 1024 * 1024  # 16MB max file size

   app.config['UPLOAD_FOLDER'] = UPLOAD_FOLDER
   app.config['MAX_CONTENT_LENGTH'] = MAX_FILE_SIZE

   # Create uploads directory if it doesn't exist
   os.makedirs(UPLOAD_FOLDER, exist_ok=True)

   # File validation function
   def allowed_file(filename):
       return '.' in filename and filename.rsplit('.', 1)[1].lower() in ALLOWED_EXTENSIONS

   # Store uploaded files info
   uploaded_files = []

**File Upload Routes**

.. code-block:: python

   @app.route('/')
   def home():
       return render_template('file_manager.html', files=uploaded_files)

   @app.route('/upload', methods=['GET', 'POST'])
   def upload_file():
       if request.method == 'POST':
           # Check if file is in the request
           if 'file' not in request.files:
               flash('No file selected! 📁', 'error')
               return redirect(request.url)
           
           file = request.files['file']
           
           # Check if filename is empty
           if file.filename == '':
               flash('No file selected! 📁', 'error')
               return redirect(request.url)
           
           # Validate and save file
           if file and allowed_file(file.filename):
               # Secure the filename to prevent security issues
               filename = secure_filename(file.filename)
               
               # Add timestamp to prevent name conflicts
               import time
               timestamp = str(int(time.time()))
               name, ext = os.path.splitext(filename)
               unique_filename = f"{name}_{timestamp}{ext}"
               
               # Save file
               file_path = os.path.join(app.config['UPLOAD_FOLDER'], unique_filename)
               file.save(file_path)
               
               # Store file info
               file_info = {
                   'id': len(uploaded_files) + 1,
                   'original_name': file.filename,
                   'stored_name': unique_filename,
                   'file_path': file_path,
                   'size': os.path.getsize(file_path),
                   'upload_time': time.strftime('%Y-%m-%d %H:%M:%S')
               }
               uploaded_files.append(file_info)
               
               flash(f'File "{file.filename}" uploaded successfully! ✅', 'success')
               return redirect(url_for('home'))
           else:
               flash('Invalid file type! Only txt, pdf, png, jpg, jpeg, gif, doc, docx allowed 🚫', 'error')
       
       return render_template('upload_form.html')

   @app.route('/download/<int:file_id>')
   def download_file(file_id):
       # Find file by ID
       file_info = next((f for f in uploaded_files if f['id'] == file_id), None)
       
       if file_info and os.path.exists(file_info['file_path']):
           return send_file(
               file_info['file_path'],
               as_attachment=True,
               download_name=file_info['original_name']
           )
       else:
           flash('File not found! 📁❌', 'error')
           return redirect(url_for('home'))

   @app.route('/view_pdf/<int:file_id>')
   def view_pdf(file_id):
       """View PDF file in browser instead of downloading"""
       file_info = next((f for f in uploaded_files if f['id'] == file_id), None)
       
       if file_info and os.path.exists(file_info['file_path']):
           # Check if it's a PDF file
           if file_info['original_name'].lower().endswith('.pdf'):
               return send_file(
                   file_info['file_path'],
                   mimetype='application/pdf'
               )
           else:
               flash('This feature is only for PDF files! 📄', 'error')
               return redirect(url_for('home'))
       else:
           flash('File not found! 📁❌', 'error')
           return redirect(url_for('home'))

   @app.route('/delete/<int:file_id>', methods=['POST'])
   def delete_file(file_id):
       global uploaded_files
       
       # Find and remove file
       file_info = next((f for f in uploaded_files if f['id'] == file_id), None)
       
       if file_info:
           # Delete physical file
           if os.path.exists(file_info['file_path']):
               os.remove(file_info['file_path'])
           
           # Remove from list
           uploaded_files = [f for f in uploaded_files if f['id'] != file_id]
           flash(f'File "{file_info["original_name"]}" deleted! 🗑️', 'success')
       else:
           flash('File not found! 📁❌', 'error')
       
       return redirect(url_for('home'))

**Complete File Manager Template Example**

.. code-block:: html

   <!-- templates/file_manager.html -->
   <!DOCTYPE html>
   <html>
   <head>
       <title>📁 File Manager</title>
       <style>
           body {
               font-family: Arial, sans-serif;
               max-width: 1000px;
               margin: 50px auto;
               padding: 20px;
               background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
               min-height: 100vh;
           }
           .container {
               background: white;
               padding: 30px;
               border-radius: 15px;
               box-shadow: 0 10px 30px rgba(0,0,0,0.2);
           }
           h1 { text-align: center; color: #667eea; margin-bottom: 30px; }
           .upload-btn {
               display: block;
               width: 200px;
               margin: 20px auto;
               padding: 15px;
               background: #28a745;
               color: white;
               text-align: center;
               text-decoration: none;
               border-radius: 8px;
               font-weight: bold;
           }
           .upload-btn:hover { background: #218838; }
           .file-table {
               width: 100%;
               border-collapse: collapse;
               margin-top: 30px;
           }
           .file-table th, .file-table td {
               padding: 12px;
               border: 1px solid #ddd;
               text-align: left;
           }
           .file-table th {
               background: #667eea;
               color: white;
           }
           .file-table tr:nth-child(even) {
               background: #f9f9f9;
           }
           .btn {
               padding: 8px 12px;
               margin: 2px;
               border: none;
               border-radius: 4px;
               cursor: pointer;
               text-decoration: none;
               color: white;
               font-size: 12px;
           }
           .btn-download { background: #17a2b8; }
           .btn-view { background: #28a745; }
           .btn-delete { background: #dc3545; }
       </style>
   </head>
   <body>
       <div class="container">
           <h1>📁 File Manager Dashboard</h1>
           
           <a href="{{ url_for('upload_file') }}" class="upload-btn">📤 Upload New File</a>
           
           {% if files %}
               <table class="file-table">
                   <thead>
                       <tr>
                           <th>📄 File Name</th>
                           <th>📏 Size</th>
                           <th>⏰ Upload Time</th>
                           <th>🔧 Actions</th>
                       </tr>
                   </thead>
                   <tbody>
                       {% for file in files %}
                           <tr>
                               <td>{{ file.original_name }}</td>
                               <td>{{ "%.2f"|format(file.size / 1024) }} KB</td>
                               <td>{{ file.upload_time }}</td>
                               <td>
                                   <a href="{{ url_for('download_file', file_id=file.id) }}" 
                                      class="btn btn-download">📥 Download</a>
                                   {% if file.original_name.lower().endswith('.pdf') %}
                                       <a href="{{ url_for('view_pdf', file_id=file.id) }}" 
                                          class="btn btn-view" target="_blank">👁️ View PDF</a>
                                   {% endif %}
                                   <form style="display:inline;" method="POST" 
                                         action="{{ url_for('delete_file', file_id=file.id) }}"
                                         onsubmit="return confirm('Are you sure?')">
                                       <button type="submit" class="btn btn-delete">🗑️ Delete</button>
                                   </form>
                               </td>
                           </tr>
                       {% endfor %}
                   </tbody>
               </table>
           {% else %}
               <div style="text-align: center; padding: 50px; color: #666;">
                   <h3>📂 No files uploaded yet</h3>
                   <p>Upload your first file to get started!</p>
               </div>
           {% endif %}
       </div>
   </body>
   </html>

**Security Best Practices:**

✅ **Important Security Measures:**
- Use ``secure_filename()`` to sanitize filenames
- Validate file extensions with allowlist
- Set maximum file size limits
- Store files outside web-accessible directories
- Add timestamp to prevent filename conflicts
- Never execute uploaded files directly
- Validate file content, not just extension

.. note::
   **File uploads** are powerful but require security considerations. Always validate, sanitize, and store files safely! Perfect for document management systems, image galleries, and PDF viewers! 📁🔒

--------------

Tasks
-----

**Task 1: Student Confession Booth**

Build a confession submission system with Jinja2 templates. Create: (1) Form page with confession categories (Academic, Social, Career, Life), (2) Display page showing all confessions with appropriate styling per category, (3) Use template inheritance with a base template. Add emojis and CSS styling! 🤐

*Hint:* Store confessions in a list. Use ``{% extends "base.html" %}`` for inheritance. Style each category differently with CSS classes.

**Task 2: Personal Blog with CRUD**

Create a complete blog system: (1) Homepage listing all posts, (2) Create post form, (3) View individual post, (4) Edit post, (5) Delete post with confirmation. Use colorful CSS, emojis for post types (📝 Article, 💡 Idea, 🎉 Achievement). Include post count dashboard.

*Hint:* Use list of dictionaries for posts. Implement all CRUD routes. Use ``redirect(url_for('route_name'))`` after create/update/delete.

**Task 3: Mood Journal with Templates**

Build a mood tracking app: Form to log mood (emoji selector), note, and activities. Display mood history with different colors per mood. Show statistics: most common mood, total entries, mood distribution. Use Jinja2 loops and conditionals for display. Make it beautiful! 🌈

*Hint:* Store moods with timestamps. Calculate statistics in route before passing to template. Use ``{% for %}`` to display history.

**Task 4: Recipe Manager**

Create a recipe management system: Add recipe (name, ingredients list, instructions, cooking time, emoji). List all recipes. View recipe details. Edit recipe. Delete recipe. Use template inheritance. Add search functionality using form GET request. Style with food-themed colors! 🍕

*Hint:* Store ingredients as comma-separated string, split in template with ``{{ ingredients.split(',') }}``. Implement search by filtering list in route.

**Task 5: Goal Tracker with Progress**

Build a goal tracking app: Create goals with title, description, target date, progress (0-100%). Dashboard showing all goals with progress bars. Update progress. Mark as complete. Delete with farewell message. Calculate statistics: total goals, completed, in progress, average progress. Use animations for progress bars! 🎯

*Hint:* Use ``<input type="range">`` for progress. Style progress bars with width: {{ progress }}%. Use JavaScript ``oninput`` to update display value as user drags slider.

--------------

Summary
-------

- **Jinja2** is Flask's templating engine 🎨
- Use ``{{ variable }}`` for variables, ``{% for %}`` for loops, ``{% if %}`` for conditions
- **Template inheritance**: ``{% extends %}`` and ``{% block %}`` enable DRY code
- **Forms**: Use ``methods=['GET', 'POST']`` to handle both display and submission
- **CRUD Operations**:
  - **Create**: POST route to add new data
  - **Read**: GET route to display data
  - **Update**: GET to show form, POST to save changes
  - **Delete**: POST to remove data
- Use ``request.form.get()`` for form data
- ``redirect(url_for('function_name'))`` redirects to routes
- ``flash()`` shows one-time messages (requires ``secret_key``)
- Always use ``url_for()`` instead of hardcoding URLs
- Add emojis and styling to make apps fun! 🎉
