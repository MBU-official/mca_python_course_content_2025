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

Real-World Example: College Survival Guide
-------------------------------------------

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
       return '''
       <html>
       <head>
           <title>College Survival Guide 🎓</title>
           <style>
               body {
                   font-family: Arial, sans-serif;
                   max-width: 800px;
                   margin: 50px auto;
                   padding: 20px;
                   background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
               }
               .container {
                   background: white;
                   padding: 40px;
                   border-radius: 15px;
                   box-shadow: 0 10px 30px rgba(0,0,0,0.2);
               }
               h1 { color: #667eea; text-align: center; }
               .nav-buttons {
                   display: flex;
                   justify-content: space-around;
                   margin-top: 30px;
                   flex-wrap: wrap;
               }
               .btn {
                   background: #667eea;
                   color: white;
                   padding: 15px 25px;
                   text-decoration: none;
                   border-radius: 8px;
                   margin: 10px;
                   display: inline-block;
                   transition: transform 0.2s;
               }
               .btn:hover {
                   transform: scale(1.05);
                   background: #764ba2;
               }
               .emergency {
                   background: #e74c3c;
               }
           </style>
       </head>
       <body>
           <div class="container">
               <h1>🎓 College Survival Guide 🎓</h1>
               <p style="text-align: center; font-size: 18px;">
                   Your emergency handbook for college life! 📖
               </p>
               <div class="nav-buttons">
                   <a href="/advice/academic" class="btn">📚 Academic Tips</a>
                   <a href="/advice/social" class="btn">🎉 Social Life</a>
                   <a href="/advice/mental" class="btn">🧘 Mental Health</a>
                   <a href="/crisis/exam" class="btn emergency">🚨 Exam Crisis</a>
                   <a href="/crisis/project" class="btn emergency">🔥 Project Panic</a>
                   <a href="/crisis/deadline" class="btn emergency">⏰ Deadline Alert</a>
                   <a href="/motivation/5" class="btn">💪 Need Motivation</a>
               </div>
           </div>
       </body>
       </html>
       '''

   @app.route('/advice/<category>')
   def advice(category):
       tips = SURVIVAL_TIPS.get(category, ['Category not found! 🤷'])
       tip = random.choice(tips)
       
       return f'''
       <html>
       <head>
           <title>Survival Tip 💡</title>
           <style>
               body {{
                   font-family: Arial;
                   max-width: 600px;
                   margin: 100px auto;
                   padding: 20px;
                   text-align: center;
               }}
               .tip-card {{
                   background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
                   color: white;
                   padding: 40px;
                   border-radius: 15px;
                   box-shadow: 0 10px 30px rgba(0,0,0,0.3);
               }}
               .emoji {{ font-size: 64px; margin: 20px 0; }}
               h2 {{ font-size: 32px; }}
               a {{
                   color: white;
                   background: rgba(255,255,255,0.2);
                   padding: 10px 20px;
                   border-radius: 5px;
                   text-decoration: none;
                   display: inline-block;
                   margin-top: 20px;
               }}
           </style>
       </head>
       <body>
           <div class="tip-card">
               <div class="emoji">💡</div>
               <h2>{category.title()} Survival Tip</h2>
               <p style="font-size: 20px; line-height: 1.6;">{tip}</p>
               <a href="/">← Back to Home</a>
           </div>
       </body>
       </html>
       '''

   @app.route('/crisis/<crisis_type>')
   def crisis(crisis_type):
       response = CRISIS_RESPONSES.get(crisis_type, 
                   "🤗 Whatever it is, you'll get through it! Take a deep breath. 💙")
       
       return f'''
       <html>
       <head>
           <title>Emergency Response 🚨</title>
           <style>
               body {{
                   font-family: Arial;
                   max-width: 600px;
                   margin: 100px auto;
                   padding: 20px;
                   text-align: center;
               }}
               .emergency-card {{
                   background: linear-gradient(135deg, #e74c3c 0%, #c0392b 100%);
                   color: white;
                   padding: 40px;
                   border-radius: 15px;
                   box-shadow: 0 10px 30px rgba(0,0,0,0.3);
                   animation: pulse 2s infinite;
               }}
               @keyframes pulse {{
                   0%, 100% {{ transform: scale(1); }}
                   50% {{ transform: scale(1.02); }}
               }}
               .emoji {{ font-size: 64px; margin: 20px 0; }}
               h2 {{ font-size: 32px; }}
               a {{
                   color: white;
                   background: rgba(255,255,255,0.3);
                   padding: 10px 20px;
                   border-radius: 5px;
                   text-decoration: none;
                   display: inline-block;
                   margin-top: 20px;
               }}
           </style>
       </head>
       <body>
           <div class="emergency-card">
               <div class="emoji">🚨</div>
               <h2>Emergency Response Activated!</h2>
               <p style="font-size: 20px; line-height: 1.6;">{response}</p>
               <a href="/">← Back to Safety</a>
           </div>
       </body>
       </html>
       '''

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
       
       return f'''
       <html>
       <head>
           <title>Motivation Boost 💪</title>
           <style>
               body {{
                   font-family: Arial;
                   max-width: 600px;
                   margin: 100px auto;
                   padding: 20px;
                   text-align: center;
               }}
               .motivation-card {{
                   background: {color};
                   color: white;
                   padding: 40px;
                   border-radius: 15px;
                   box-shadow: 0 10px 30px rgba(0,0,0,0.3);
               }}
               .emoji {{ font-size: 80px; margin: 20px 0; }}
               h2 {{ font-size: 28px; }}
               .score {{
                   background: rgba(255,255,255,0.3);
                   padding: 10px 20px;
                   border-radius: 10px;
                   display: inline-block;
                   margin: 20px 0;
               }}
               a {{
                   color: white;
                   background: rgba(0,0,0,0.2);
                   padding: 10px 20px;
                   border-radius: 5px;
                   text-decoration: none;
                   display: inline-block;
                   margin-top: 20px;
               }}
           </style>
       </head>
       <body>
           <div class="motivation-card">
               <div class="emoji">{emoji}</div>
               <h2>Motivation Level Check</h2>
               <div class="score">Desperation Score: {desperation_score}/10</div>
               <p style="font-size: 22px; line-height: 1.6;">{message}</p>
               <a href="/">← Back to Home</a>
           </div>
       </body>
       </html>
       '''

   if __name__ == '__main__':
       app.run(debug=True)

.. note::
   This app demonstrates dynamic routing, HTML styling, and how to create an interactive survival guide! Notice how each route handles different scenarios with appropriate responses. 🎯

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
