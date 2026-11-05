# 💻 Flask Blog Application

Hello there, let me introduce you to my blog website! 

It is a blog website built with Flask. It has user accounts (register, log in), a dedicated admin who can 
write and manage posts, and a comment section under every post — complete with profile pictures pulled from Gravatar. 
Posts are split across pages so the site stays tidy as it grows, and the whole thing is styled with Bootstrap 5 using 
the Start Bootstrap "Clean Blog" theme.


## ✨ Features

- User registration & login — passwords hashed with Werkzeug (pbkdf2:sha256, 8-byte salt)

- Session management — Flask-Login handles authentication, logout, and @login_required protection

- Admin-only post management — only user with id == 1 can create, edit, and delete posts

- Rich text editing — CKEditor integrated via Flask-CKEditor for post bodies

- Comments — logged-in users can comment on any post; commenters can delete their own comments

- Gravatar avatars — automatically generated profile images in the comment section

- Pagination — posts are paginated 5 per page with "Newer / Older Posts" navigation

- Flash messages — user feedback for login errors, duplicate emails, and unauthenticated commenting

- Dynamic footer year — current year injected into every template via a context processor

- Responsive UI — Bootstrap 5 with the Clean Blog theme


## 🔑 Notes on the "SECRET_KEY"

This project requires a Flask SECRET_KEY. Flask uses it to sign session cookies and flash messages. Without it, any feature that uses sessions will fail.

Every user must generate and use their own key. Do not reuse someone else's key, and never commit your key to this repository.

Here are some guidlines for creating such key (optional):

### 1. Generate a key
Run this in any terminal (Python is already required for this project):

python -c "import secrets; print(secrets.token_hex(32))"

You will get a 64-character random string, for example:

3f9a1c8e2b7d4a6f0e5c9b1d8a7f2e4c6b3a9d1f0e8c7b5a2d4f6e9c1a3b8d7

Copy the whole thing. The secrets module is Python's cryptographically secure random generator. 
Do not use random, and do not use a short or guessable word like "secret" or "changeme".

### 2. Create your .env file
Copy the template:
cp .env.example .env

On Windows PowerShell:
Copy-Item .env.example .env

### 3. Put the key in .env
Open .env and set:

SECRET_KEY=3f9a1c8e2b7d4a6f0e5c9b1d8a7f2e4c6b3a9d1f0e8c7b5a2d4f6e9c1a3b8d7

Rules: no spaces around the equals sign, no quotes needed, one line, no wrapping.


## 🚀 Installation

### 1. Clone the repository
```bash
git clone <your-repo-url>
cd <your-project-folder>
```

### 2. Create a virtual environment
```bash
python -m venv venv
source venv/bin/activate        # macOS / Linux
venv\Scripts\activate           # Windows
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```
Note on Bootstrap packages: This project uses bootstrap-flask (which provides Bootstrap5 under the flask_bootstrap module name), 
not the older flask-bootstrap package. If you see ImportError: cannot import name 'Bootstrap5' from 'flask_bootstrap', 
you have the wrong package installed — see the troubleshooting note below.

### 4. Run the application

The app starts on http://127.0.0.1:5002 with debug mode enabled.

The SQLite database and all tables are created automatically on first launch via db.create_all().


## 🔗 Relationships of the databases

They're a little complicated, but bear with me.

- The posts relationships: (one-to-many → BlogPost), comments (one-to-many → Comment)

- The author relationships: (many-to-one → User), comments (one-to-many → Comment, cascade="all, delete-orphan")

- The comment_author relationships: (many-to-one → User), parent_post (many-to-one → BlogPost)


## 🎨 Templates

header.html — <head>, CSS links, navbar, opening <body>.

footer.html — social icons, copyright line (Copyright © Your Website {{ current_year }}), closing tags.

index.html — extends the above with the masthead, post list, and pagination nav.


## 📄 Note on the Contact page

- The Contact page is decorative only. This is intentional because this project is a learning exercise only. 
There is no actual blogger behind it, so don't expect messages submitted there to go anywhere.


## 🔑 Demo Admin Account

The admin account is:
 - Name: Petya
 - Email: admin@email.com
 - Password: 123

Anyone is free to log in with these credentials and test all admin features — creating posts, editing them, 
deleting them, and managing the site from the admin point of view.

You can also register a brand-new account at /register to experience the site as a regular user — leave comments 
on posts, delete your own comments, and browse the paginated post list. The two roles together cover every feature in 
the application.

⚠️ These credentials are published for demonstration and learning purposes only. This is not a production application. 
If you ever deploy this project publicly, change the admin password immediately and remove these credentials.


## 📜 License

This project uses the Start Bootstrap Clean Blog theme, which is released under the MIT License. 
See the header of static/css/styles.css for the original copyright notice.

## 🎓 Credits

Inspired by Day 69 of the course
"100 Days of Code: The Complete Python Pro Bootcamp".

The course really helped me to understand end correctly execute the database relationships 
as well as keep all the templates in order. 


💬 P.S As always let me know if you find any errors either in the code or in this README file. 
I would greatly appreciate it! 😊
