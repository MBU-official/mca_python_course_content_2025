.. _module5_flask_basics:

Flask Basics: Web Development in Python
========================================

Introduction
------------

Flask is a lightweight and flexible Python web framework that makes building web applications easy and fun. It's perfect for beginners and powerful enough for production applications! 🚀

.. note::
   Flask follows the motto "micro but mighty" 💪. It gives you the essentials to build web apps without forcing you into a specific way of doing things. Perfect for learning and rapid prototyping!

--------------

Installing Flask
----------------

.. code-block:: bash

   pip install flask

--------------

Baby Steps: Your First Flask App
---------------------------------

**The Simplest Flask App:**

.. code-block:: python

   # app.py
   from flask import Flask

   app = Flask(__name__)

   @app.route('/')
   def home():
       return "Hello, World! 🌍"

   if __name__ == '__main__':
       app.run(debug=True)

**Run it:**

.. code-block:: bash

   python app.py

**Open browser:** http://127.0.0.1:5000/ ✨

.. note::
   ``debug=True`` enables auto-reload and better error messages. Super helpful during development! But remember: **NEVER** use debug mode in production! 🚫

--------------

Understanding Routes
--------------------

Routes tell Flask which function to run for different URLs.

.. code-block:: python

   from flask import Flask

   app = Flask(__name__)

   @app.route('/')
   def home():
       return "🏠 Welcome Home!"

   @app.route('/about')
   def about():
       return "📖 About Us: We teach Python!"

   @app.route('/contact')
   def contact():
       return "📧 Contact: email@example.com"

   if __name__ == '__main__':
       app.run(debug=True)

**Try these URLs:**
- http://127.0.0.1:5000/
- http://127.0.0.1:5000/about
- http://127.0.0.1:5000/contact

--------------

Dynamic Routes (URL Parameters)
-------------------------------

.. code-block:: python

   from flask import Flask

   app = Flask(__name__)

   @app.route('/user/<username>')
   def show_user(username):
       return f"👤 User Profile: {username}"

   @app.route('/post/<int:post_id>')
   def show_post(post_id):
       return f"📝 Post ID: {post_id}"

   @app.route('/motivation/<int:desperation_score>')
   def motivation(desperation_score):
       if desperation_score < 3:
           return "💪 You're doing great! Keep going!"
       elif desperation_score < 7:
           return "😅 Hang in there! Coffee break recommended."
       else:
           return "🆘 Emergency! Take a break. You've got this! 🫂"

   if __name__ == '__main__':
       app.run(debug=True)

**Try:**
- http://127.0.0.1:5000/user/alice
- http://127.0.0.1:5000/post/42
- http://127.0.0.1:5000/motivation/8

.. note::
   Use ``<variable>`` for string parameters and ``<int:variable>`` for integers. Flask automatically converts and validates! ✅

--------------

Returning HTML
--------------

.. code-block:: python

   from flask import Flask

   app = Flask(__name__)

   @app.route('/')
   def home():
       return '''
       <!DOCTYPE html>
       <html>
       <head>
           <title>My Flask App 🎨</title>
           <style>
               body { 
                   font-family: Arial; 
                   text-align: center; 
                   padding: 50px;
                   background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
                   color: white;
               }
               h1 { font-size: 48px; }
               .emoji { font-size: 64px; }
           </style>
       </head>
       <body>
           <div class="emoji">🚀</div>
           <h1>Welcome to Flask!</h1>
           <p>This is way cooler than plain text! ✨</p>
       </body>
       </html>
       '''

   if __name__ == '__main__':
       app.run(debug=True)

.. note::
   **Wait! 🛑** This is getting messy! Mixing HTML in Python strings becomes unreadable fast. There's a better way... **Templates!** 🎨✨

--------------

Using Templates (Jinja2)
------------------------

Instead of writing HTML in strings, use templates! 📁

**Project Structure:**

.. code-block:: text

   my_flask_app/
   ├── app.py
   └── templates/
       └── index.html

**app.py:**

.. code-block:: python

   from flask import Flask, render_template

   app = Flask(__name__)

   @app.route('/')
   def home():
       return render_template('index.html', 
                            name='Student', 
                            emoji='🎓')

   if __name__ == '__main__':
       app.run(debug=True)

**templates/index.html:**

.. code-block:: html

   <!DOCTYPE html>
   <html>
   <head>
       <title>Flask Template 🎨</title>
       <style>
           body {
               font-family: Arial;
               text-align: center;
               padding: 50px;
               background: #f0f0f0;
           }
           .card {
               background: white;
               padding: 30px;
               border-radius: 10px;
               box-shadow: 0 4px 6px rgba(0,0,0,0.1);
               max-width: 500px;
               margin: 0 auto;
           }
       </style>
   </head>
   <body>
       <div class="card">
           <h1>Hello, {{ name }}! {{ emoji }}</h1>
           <p>Welcome to Flask Templates!</p>
       </div>
   </body>
   </html>

.. note::
   Flask uses **Jinja2** templating. ``{{ variable }}`` displays values, ``{% for %}`` creates loops, ``{% if %}`` adds conditions. It's like Python in HTML! 🎯

--------------

Real-World Example: College Survival Guide (Using Templates!)
--------------------------------------------------------------

**Project Structure:**

.. code-block:: text

   survival_guide/
   ├── app.py
   ├── static/
   │   └── style.css
   └── templates/
       ├── base.html
       ├── home.html
       ├── advice.html
       ├── crisis.html
       └── motivation.html

**app.py (Clean Python code):**

.. code-block:: python

   from flask import Flask, render_template
   import random

   app = Flask(__name__)

   # Survival tips database 💡
   SURVIVAL_TIPS = {
       'academic': [
           "📚 Start assignments early (we know you won't, but we have to say it)",
           "🤝 Form study groups (even if they become gaming sessions)",
           "📝 Attend classes (Netflix can wait!)",
           "🎯 Set realistic goals (not 'finish entire syllabus tonight')",
           "☕ Coffee is your friend, but so is sleep!"
       ],
       'social': [
           "🎉 Join clubs and activities",
           "💬 Network with seniors (they know the shortcuts)",
           "🤗 Be kind to everyone (you never know who'll save you in group projects)",
           "🎮 Balance is key: study hard, play harder!",
           "😊 Remember: everyone is faking confidence"
       ],
       'mental': [
           "🧘 Take breaks (burnout is real!)",
           "🌟 Celebrate small wins",
           "💪 It's okay to ask for help",
           "🌈 Your worth isn't defined by grades",
           "🎭 Imposter syndrome? Everyone has it!"
       ]
   }

   CRISIS_RESPONSES = {
       'exam': "🚨 Emergency Protocol: 1) Don't panic 2) Make a study plan 3) Start NOW 4) Breathe! You've got this! 💪",
       'project': "🔥 Project Crisis: Break it into tiny chunks. Do ONE thing. Then another. Progress > Perfection! 🎯",
       'life': "🌊 Life feels overwhelming? That's normal! Talk to someone. Take a walk. Remember: this too shall pass. 🌈",
       'deadline': "⏰ Deadline approaching? Priority mode activated! Turn off distractions. Focus on must-haves. You can do this! 🚀"
   }

   @app.route('/')
   def home():
       return render_template('home.html')

   @app.route('/advice/<category>')
   def advice(category):
       tips = SURVIVAL_TIPS.get(category, ['Category not found! 🤷'])
       tip = random.choice(tips)
       return render_template('advice.html', category=category, tip=tip)

   @app.route('/crisis/<crisis_type>')
   def crisis(crisis_type):
       response = CRISIS_RESPONSES.get(crisis_type, 
                   "🤗 Whatever it is, you'll get through it! Take a deep breath. 💙")
       return render_template('crisis.html', crisis_type=crisis_type, response=response)

   @app.route('/motivation/<int:desperation_score>')
   def motivation(desperation_score):
       if desperation_score < 3:
           message = "🌟 You're absolutely crushing it! Keep that energy! 💪"
           color = "#2ecc71"
           emoji = "🎉"
       elif desperation_score < 7:
           message = "😅 Hanging in there! Remember: progress over perfection! 📈"
           color = "#f39c12"
           emoji = "☕"
       else:
           message = "🆘 EMERGENCY MOTIVATION DEPLOYED! You are stronger than you think. This is temporary. You've got this! 🫂💙"
           color = "#e74c3c"
           emoji = "🚀"
       
       return render_template('motivation.html', 
                            score=desperation_score, 
                            message=message, 
                            color=color, 
                            emoji=emoji)

   if __name__ == '__main__':
       app.run(debug=True)

**templates/base.html (Reusable base template):**

.. code-block:: html

   <!DOCTYPE html>
   <html>
   <head>
       <title>{% block title %}College Survival Guide{% endblock %} 🎓</title>
       <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
   </head>
   <body>
       <div class="container">
           {% block content %}{% endblock %}
       </div>
   </body>
   </html>

**templates/home.html:**

.. code-block:: html

   {% extends "base.html" %}

   {% block title %}College Survival Guide{% endblock %}

   {% block content %}
       <h1>🎓 College Survival Guide 🎓</h1>
       <p class="subtitle">Your emergency handbook for college life! 📖</p>
       
       <div class="nav-buttons">
           <a href="{{ url_for('advice', category='academic') }}" class="btn">📚 Academic Tips</a>
           <a href="{{ url_for('advice', category='social') }}" class="btn">🎉 Social Life</a>
           <a href="{{ url_for('advice', category='mental') }}" class="btn">🧘 Mental Health</a>
           <a href="{{ url_for('crisis', crisis_type='exam') }}" class="btn emergency">🚨 Exam Crisis</a>
           <a href="{{ url_for('crisis', crisis_type='project') }}" class="btn emergency">🔥 Project Panic</a>
           <a href="{{ url_for('crisis', crisis_type='deadline') }}" class="btn emergency">⏰ Deadline Alert</a>
           <a href="{{ url_for('motivation', desperation_score=5) }}" class="btn">💪 Need Motivation</a>
       </div>
   {% endblock %}

**templates/advice.html:**

.. code-block:: html

   {% extends "base.html" %}

   {% block title %}{{ category.title() }} Advice{% endblock %}

   {% block content %}
       <div class="tip-card">
           <div class="emoji">💡</div>
           <h2>{{ category.title() }} Survival Tip</h2>
           <p class="tip-text">{{ tip }}</p>
           <a href="{{ url_for('home') }}" class="back-btn">← Back to Home</a>
       </div>
   {% endblock %}

**templates/crisis.html:**

.. code-block:: html

   {% extends "base.html" %}

   {% block title %}Emergency Response{% endblock %}

   {% block content %}
       <div class="emergency-card">
           <div class="emoji">🚨</div>
           <h2>Emergency Response Activated!</h2>
           <p class="response-text">{{ response }}</p>
           <a href="{{ url_for('home') }}" class="back-btn">← Back to Safety</a>
       </div>
   {% endblock %}

**templates/motivation.html:**

.. code-block:: html

   {% extends "base.html" %}

   {% block title %}Motivation Boost{% endblock %}

   {% block content %}
       <div class="motivation-card" style="background: {{ color }};">
           <div class="emoji">{{ emoji }}</div>
           <h2>Motivation Level Check</h2>
           <div class="score">Desperation Score: {{ score }}/10</div>
           <p class="message-text">{{ message }}</p>
           <a href="{{ url_for('home') }}" class="back-btn">← Back to Home</a>
       </div>
   {% endblock %}

**static/style.css (Separated styling):**

.. code-block:: css

   body {
       font-family: Arial, sans-serif;
       margin: 0;
       padding: 20px;
       background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
       min-height: 100vh;
   }

   .container {
       max-width: 800px;
       margin: 0 auto;
       background: white;
       padding: 40px;
       border-radius: 15px;
       box-shadow: 0 10px 30px rgba(0,0,0,0.2);
       text-align: center;
   }

   h1 {
       color: #667eea;
       margin-bottom: 10px;
   }

   .subtitle {
       font-size: 18px;
       color: #666;
       margin-bottom: 30px;
   }

   .nav-buttons {
       display: flex;
       justify-content: space-around;
       flex-wrap: wrap;
       gap: 15px;
   }

   .btn {
       background: #667eea;
       color: white;
       padding: 15px 25px;
       text-decoration: none;
       border-radius: 8px;
       display: inline-block;
       transition: transform 0.2s;
       font-weight: bold;
   }

   .btn:hover {
       transform: scale(1.05);
       background: #764ba2;
   }

   .btn.emergency {
       background: #e74c3c;
   }

   .btn.emergency:hover {
       background: #c0392b;
   }

   .tip-card, .emergency-card, .motivation-card {
       background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
       color: white;
       padding: 40px;
       border-radius: 15px;
       box-shadow: 0 10px 30px rgba(0,0,0,0.3);
   }

   .emergency-card {
       background: linear-gradient(135deg, #e74c3c 0%, #c0392b 100%);
       animation: pulse 2s infinite;
   }

   @keyframes pulse {
       0%, 100% { transform: scale(1); }
       50% { transform: scale(1.02); }
   }

   .emoji {
       font-size: 64px;
       margin: 20px 0;
   }

   .tip-text, .response-text, .message-text {
       font-size: 20px;
       line-height: 1.6;
       margin: 20px 0;
   }

   .score {
       background: rgba(255,255,255,0.2);
       padding: 10px 20px;
       border-radius: 10px;
       display: inline-block;
       margin: 20px 0;
   }

   .back-btn {
       color: white;
       background: rgba(255,255,255,0.3);
       padding: 15px 25px;
       border-radius: 5px;
       text-decoration: none;
       display: inline-block;
       margin-top: 20px;
   }

   .back-btn:hover {
       background: rgba(255,255,255,0.4);
   }

.. note::
   **Much better! 🎉** This example demonstrates proper **separation of concerns**:
   
   - **Python code** handles logic and data (routes, functions, variables)
   - **HTML templates** handle presentation and structure  
   - **CSS files** handle styling and appearance
   - **Template inheritance** eliminates code duplication
   - **url_for()** creates flexible, maintainable links
   
   Notice how clean and readable the Python code is now! Each template focuses on one specific page, and the base template provides consistent styling. This is the **Flask way**! 🚀✨

--------------

HTTP Methods (GET vs POST)
---------------------------

.. code-block:: python

   from flask import Flask, request

   app = Flask(__name__)

   @app.route('/search')
   def search():
       # GET parameters from URL: /search?q=python
       query = request.args.get('q', 'nothing')
       return f"🔍 You searched for: {query}"

   @app.route('/submit', methods=['GET', 'POST'])
   def submit():
       if request.method == 'POST':
           # POST data from form
           name = request.form.get('name')
           return f"✅ Form submitted! Hello, {name}!"
       else:
           # Show form
           return '''
           <form method="POST">
               <input type="text" name="name" placeholder="Your name" required>
               <button type="submit">Submit 🚀</button>
           </form>
           '''

   if __name__ == '__main__':
       app.run(debug=True)

--------------

Error Handling
--------------

.. code-block:: python

   from flask import Flask

   app = Flask(__name__)

   @app.route('/')
   def home():
       return "Home Page 🏠"

   @app.errorhandler(404)
   def page_not_found(error):
       return '''
       <html>
       <head>
           <title>404 - Lost? 🗺️</title>
           <style>
               body {
                   font-family: Arial;
                   text-align: center;
                   padding: 100px;
                   background: #f0f0f0;
               }
               .emoji { font-size: 100px; }
               h1 { color: #e74c3c; }
           </style>
       </head>
       <body>
           <div class="emoji">🤷‍♂️</div>
           <h1>404 - Page Not Found!</h1>
           <p>Looks like you're lost in the internet... 🌐</p>
           <a href="/">Go Home 🏠</a>
       </body>
       </html>
       ''', 404

   @app.route('/help/<problem>')
   def help_route(problem):
       if problem == 'impossible':
           return '''
           <html>
           <body style="text-align: center; padding: 50px; font-family: Arial;">
               <h1>🌟 Nothing is Impossible! 🌟</h1>
               <p style="font-size: 20px;">
                   Remember: Even experienced developers Google stuff daily! 💪<br>
                   Take it step by step. You've got this! 🚀
               </p>
               <a href="/">← Back to Home</a>
           </body>
           </html>
           ''', 404
       return f"Help for: {problem}"

   if __name__ == '__main__':
       app.run(debug=True)

--------------

Static Files (CSS, JS, Images)
-------------------------------

**Project Structure:**

.. code-block:: text

   my_flask_app/
   ├── app.py
   ├── static/
   │   ├── style.css
   │   └── logo.png
   └── templates/
       └── index.html

**Using static files:**

.. code-block:: html

   <!DOCTYPE html>
   <html>
   <head>
       <title>My App 🎨</title>
       <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
   </head>
   <body>
       <img src="{{ url_for('static', filename='logo.png') }}" alt="Logo">
       <h1>Hello from Flask! 👋</h1>
   </body>
   </html>

.. note::
   Flask serves files from the ``static/`` folder automatically. Use ``url_for('static', filename='...')`` to generate correct URLs. 📁

--------------

Working with Dates and Times in Flask
--------------------------------------

Flask applications often need to work with dates and times - for timestamps, scheduling, age calculations, and displaying current information.

**Basic DateTime Display**

.. code-block:: python

   from flask import Flask, render_template
   from datetime import datetime, timedelta
   import time

   app = Flask(__name__)

   @app.route('/')
   def home():
       current_time = datetime.now()
       return f"""
       <h1>🕒 Current Server Time</h1>
       <p><strong>Date:</strong> {current_time.strftime('%A, %B %d, %Y')}</p>
       <p><strong>Time:</strong> {current_time.strftime('%I:%M:%S %p')}</p>
       <p><strong>Timezone:</strong> Server Local Time</p>
       <p><strong>Unix Timestamp:</strong> {int(current_time.timestamp())}</p>
       """

   @app.route('/time/<username>')
   def user_time(username):
       current_time = datetime.now()
       greeting = "Good Morning" if current_time.hour < 12 else \
                 "Good Afternoon" if current_time.hour < 17 else "Good Evening"
       
       return f"""
       <h1>🌟 {greeting}, {username}!</h1>
       <p>Current time: {current_time.strftime('%I:%M %p')}</p>
       <p>Today is {current_time.strftime('%A')}</p>
       <p>Have a wonderful {current_time.strftime('%B')}! ✨</p>
       """

**Advanced DateTime Operations**

.. code-block:: python

   from flask import Flask
   from datetime import datetime, timedelta
   import calendar

   app = Flask(__name__)

   @app.route('/age/<int:birth_year>')
   def calculate_age(birth_year):
       current_year = datetime.now().year
       age = current_year - birth_year
       
       # Calculate days until next birthday
       today = datetime.now()
       next_birthday = datetime(current_year + 1, 1, 1)  # Simplified
       days_to_birthday = (next_birthday - today).days
       
       return f"""
       <h1>🎂 Age Calculator</h1>
       <p><strong>Your age:</strong> {age} years old</p>
       <p><strong>Days until New Year:</strong> {days_to_birthday} days</p>
       <p><strong>You were born in:</strong> {birth_year}</p>
       <p><strong>Fun fact:</strong> You've lived through {age} years! 🎉</p>
       """

   @app.route('/semester-progress')
   def semester_progress():
       # Semester dates (example)
       semester_start = datetime(2024, 8, 1)  # August 1st
       semester_end = datetime(2024, 12, 15)   # December 15th
       current_date = datetime.now()
       
       total_days = (semester_end - semester_start).days
       elapsed_days = (current_date - semester_start).days
       remaining_days = (semester_end - current_date).days
       
       progress_percent = (elapsed_days / total_days) * 100 if elapsed_days > 0 else 0
       
       return f"""
       <h1>📚 Semester Progress Tracker</h1>
       <p><strong>Semester Duration:</strong> {total_days} days</p>
       <p><strong>Days Completed:</strong> {elapsed_days} days</p>
       <p><strong>Days Remaining:</strong> {remaining_days} days</p>
       <p><strong>Progress:</strong> {progress_percent:.1f}%</p>
       <div style="background: #ddd; width: 300px; border-radius: 10px;">
           <div style="background: linear-gradient(90deg, #4CAF50, #8BC34A); 
                       width: {progress_percent}%; height: 20px; border-radius: 10px;"></div>
       </div>
       <p>{'🎉 Almost there!' if progress_percent > 80 else '💪 Keep going!' if progress_percent > 50 else '🚀 Just getting started!'}</p>
       """

**Time-Based Greetings and Content**

.. code-block:: python

   from flask import Flask
   from datetime import datetime

   app = Flask(__name__)

   @app.route('/dashboard/<username>')
   def dashboard(username):
       now = datetime.now()
       hour = now.hour
       day_name = now.strftime('%A')
       
       # Time-based greeting
       if hour < 6:
           greeting = "🌙 Burning the midnight oil"
           advice = "Maybe it's time for some sleep?"
       elif hour < 12:
           greeting = "🌅 Good morning"
           advice = "Start your day with something productive!"
       elif hour < 17:
           greeting = "☀️ Good afternoon"
           advice = "Hope your day is going well!"
       elif hour < 20:
           greeting = "🌆 Good evening"
           advice = "Time to wind down and relax!"
       else:
           greeting = "🌃 Good night"
           advice = "Perfect time for some evening learning!"
       
       # Day-based content
       day_motivation = {
           'Monday': '💪 Fresh start to a new week!',
           'Tuesday': '🚀 Tuesday momentum building!',
           'Wednesday': '🐪 Hump day - halfway there!',
           'Thursday': '⚡ Thursday energy boost!',
           'Friday': '🎉 Friday feeling fantastic!',
           'Saturday': '😎 Saturday chill vibes!',
           'Sunday': '🧘 Sunday self-care day!'
       }
       
       return f"""
       <!DOCTYPE html>
       <html>
       <head>
           <title>Dashboard - {username}</title>
           <style>
               body {{
                   font-family: Arial, sans-serif;
                   background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
                   color: white;
                   text-align: center;
                   padding: 50px;
               }}
               .dashboard {{
                   background: rgba(255,255,255,0.1);
                   padding: 40px;
                   border-radius: 20px;
                   backdrop-filter: blur(10px);
               }}
           </style>
       </head>
       <body>
           <div class="dashboard">
               <h1>{greeting}, {username}!</h1>
               <h2>📅 It's {day_name}, {now.strftime('%B %d, %Y')}</h2>
               <h3>⏰ Current time: {now.strftime('%I:%M %p')}</h3>
               <p><strong>💡 {advice}</strong></p>
               <p><strong>✨ {day_motivation.get(day_name, 'Have a great day!')}</strong></p>
               
               <div style="margin-top: 30px;">
                   <h3>📊 Quick Stats</h3>
                   <p>Week of the year: {now.isocalendar()[1]}</p>
                   <p>Day of the year: {now.timetuple().tm_yday}</p>
                   <p>Days until weekend: {(5 - now.weekday()) if now.weekday() < 5 else 0}</p>
               </div>
           </div>
       </body>
       </html>
       """

**DateTime Formatting and Utilities**

.. code-block:: python

   from flask import Flask, render_template_string
   from datetime import datetime, timedelta

   app = Flask(__name__)

   @app.route('/time-formats')
   def time_formats():
       now = datetime.now()
       
       formats = {
           'Full Date': now.strftime('%A, %B %d, %Y'),
           'Short Date': now.strftime('%m/%d/%Y'),
           'ISO Format': now.isoformat(),
           'Time Only': now.strftime('%I:%M:%S %p'),
           '24 Hour': now.strftime('%H:%M:%S'),
           'Month Year': now.strftime('%B %Y'),
           'Day of Week': now.strftime('%A'),
           'Month Name': now.strftime('%B'),
           'Year': now.strftime('%Y'),
           'Unix Timestamp': str(int(now.timestamp()))
       }
       
       html = """
       <!DOCTYPE html>
       <html>
       <head>
           <title>🕒 DateTime Formats</title>
           <style>
               body { font-family: Arial; padding: 50px; background: #f0f2f5; }
               .format-card {
                   background: white;
                   padding: 15px;
                   margin: 10px 0;
                   border-radius: 8px;
                   box-shadow: 0 2px 4px rgba(0,0,0,0.1);
                   display: flex;
                   justify-content: space-between;
               }
               .format-name { font-weight: bold; color: #333; }
               .format-value { color: #666; font-family: monospace; }
           </style>
       </head>
       <body>
           <h1>🕒 DateTime Format Examples</h1>
           <p>Current server time displayed in various formats:</p>
           {% for name, value in formats.items() %}
               <div class="format-card">
                   <span class="format-name">{{ name }}:</span>
                   <span class="format-value">{{ value }}</span>
               </div>
           {% endfor %}
       </body>
       </html>
       """
       
       return render_template_string(html, formats=formats)

   @app.route('/countdown/<target_date>')
   def countdown(target_date):
       try:
           # Parse target date (format: YYYY-MM-DD)
           target = datetime.strptime(target_date, '%Y-%m-%d')
           current = datetime.now()
           
           if target > current:
               delta = target - current
               days = delta.days
               hours = delta.seconds // 3600
               minutes = (delta.seconds % 3600) // 60
               
               return f"""
               <h1>⏰ Countdown Timer</h1>
               <h2>Time until {target.strftime('%B %d, %Y')}:</h2>
               <div style="font-size: 24px; color: #007bff;">
                   <strong>{days} days, {hours} hours, {minutes} minutes</strong>
               </div>
               <p>{'🎓 Exam season approaching!' if 'exam' in target_date else '📅 Event approaching!'}</p>
               """
           else:
               return f"""
               <h1>⏰ Countdown Timer</h1>
               <h2>The date {target.strftime('%B %d, %Y')} has already passed!</h2>
               <p>🚀 Time to set a new goal!</p>
               """
       except ValueError:
           return """
           <h1>❌ Invalid Date Format</h1>
           <p>Please use format: YYYY-MM-DD (e.g., 2024-12-25)</p>
           """

   if __name__ == '__main__':
       app.run(debug=True)

**Common DateTime Use Cases in Web Apps:**

✅ **Practical Applications:**
- User registration timestamps
- Session expiration tracking
- Event scheduling and reminders
- Age verification and calculations
- Time-zone aware applications
- Log timestamps for debugging
- Progress tracking (deadlines, goals)
- Dynamic greeting messages

✅ **Key Python DateTime Functions:**
- ``datetime.now()`` - Current date and time
- ``strftime()`` - Format datetime as string
- ``strptime()`` - Parse string to datetime
- ``timedelta()`` - Time differences and arithmetic
- ``timestamp()`` - Unix timestamp conversion
- ``isoformat()`` - ISO standard formatting

.. note::
   **DateTime handling** is essential for web applications! Use Flask's timezone-aware functions for production apps. Perfect for dashboards, scheduling apps, and time-tracking systems! ⏰🚀

--------------

Tasks
-----

**Task 1: Personal Portfolio Website**

Create a Flask app with routes: ``/`` (home with intro), ``/projects`` (list of projects with emojis), ``/skills`` (programming skills with progress bars in HTML), ``/contact`` (contact info). Use colorful HTML/CSS styling with gradients and emojis. Make each page visually distinct! 🎨

*Hint:* Create separate routes for each page. Use inline CSS or create a ``static/style.css`` file. Add emojis liberally! Return HTML strings with ``<style>`` tags.

**Task 2: Mood Tracker Web App**

Create a Flask app that tracks your mood. Route ``/`` shows a form to select mood (😊 Happy, 😐 Neutral, 😢 Sad) and a note. Route ``/mood/<mood_type>`` displays an encouraging message based on mood. Store data in a Python list (no database needed). Show mood history on homepage.

*Hint:* Use a global list to store moods: ``moods = []``. Access form data with ``request.form.get()``. Use ``methods=['GET', 'POST']`` for form route.

**Task 3: Random Advice Generator**

Build a "College Survival Advice" web app with categories: Academic 📚, Social 🎉, Mental Health 🧘, Career 💼. Route ``/`` shows category buttons. Route ``/advice/<category>`` displays random advice from a predefined dictionary. Add a "Crisis Help" section with ``/crisis/<type>`` that redirects to counseling resources.

*Hint:* Store advice in a dictionary of lists. Use ``import random`` and ``random.choice(list)``. Create styled HTML responses with emergency colors for crisis routes.

**Task 4: Study Session Timer Page**

Create a Pomodoro-style timer app. Route ``/`` explains the technique with emojis. Route ``/timer/<int:minutes>`` displays a motivational message based on duration (25 min = 🍅 Pomodoro, 5 min = ☕ Break, etc.). Add routes ``/start``, ``/break``, ``/finish`` with appropriate encouragement messages!

*Hint:* No actual timer needed - just display messages! Use URL parameters for duration. Style each route differently with CSS gradients. Add encouraging emojis and messages.

**Task 5: Simple Blog Platform**

Create a mini-blog with: ``/`` (homepage listing post titles), ``/post/<int:id>`` (display post content), ``/about`` (about the blog). Store 5 sample posts in a list of dictionaries with keys: id, title, content, date, emoji. Make it colorful with CSS! 🌈

*Hint:* Posts list: ``[{'id': 1, 'title': '...', 'content': '...', 'emoji': '🎉'}]``. Loop through posts on homepage. Use ``id`` to find specific post in ``/post/<int:id>`` route.

--------------

Summary
-------

- Flask is a micro web framework - simple yet powerful! 💪
- ``@app.route()`` decorator defines URL routes
- Use ``<variable>`` in routes for dynamic URLs
- ``render_template()`` serves HTML templates (Jinja2)
- Templates use ``{{ variable }}`` for variables, ``{% %}`` for logic
- ``request.args`` gets URL parameters (GET)
- ``request.form`` gets form data (POST)
- ``methods=['GET', 'POST']`` handles both methods
- Error handlers customize error pages
- ``static/`` folder serves CSS, JS, images
- ``debug=True`` for development, ``False`` for production
- Flask makes web development fun and approachable! 🚀
