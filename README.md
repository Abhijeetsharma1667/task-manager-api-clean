# ✅ Task Manager API – Django + DRF

A lightweight, secure task manager REST API using Django and Django REST Framework with **session-based authentication** and **CSRF protection**.

---

## 🚀 Features

- 🔐 User Registration, Login, Logout using sessions
- 📋 Task CRUD operations (Create, Read, Update, Delete)
- 🧩 Filtering by task completion status
- 🔁 Pagination for task listing
- 🛡️ CSRF protection enabled
- 🧪 Postman & Swagger compatible
- 📘 Swagger UI documentation at `/docs/`

---

## 🛠️ Setup Instructions

```bash
# Clone the repository
git clone https://github.com/Abhijeetsharma1667/task-manager-api-django.git
cd task-manager-api-django

# Create virtual environment
python -m venv venv
venv\Scripts\activate   # On Windows
# OR
source venv/bin/activate   # On Mac/Linux

# Install dependencies
pip install -r requirements.txt

# Run migrations
python manage.py migrate

# Create admin user (optional)
python manage.py createsuperuser

# Start development server
python manage.py runserver
