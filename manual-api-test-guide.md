# 🔬 Task Manager API – Manual Testing Guide (Postman + Django Server)

This guide walks through every step required to manually test the Task Manager API using Django and Postman, including CSRF handling, session authentication, and Postman collection automation.

---

## 1. 🖥️ Run the Server

```bash
# Activate virtual environment
venv\Scripts\activate      # Windows
# OR
source venv/bin/activate   # Mac/Linux

# Run the server
python manage.py runserver
Server runs at:
http://127.0.0.1:8000/

2. 👤 Create Superuser (Optional)
bash
Copy
Edit
python manage.py createsuperuser
Visit:
http://127.0.0.1:8000/admin/

3. 📬 Use Postman to Test All APIs
3.1 📝 Register a New User
Method: POST

URL: http://127.0.0.1:8000/register/

Body (JSON):

json
Copy
Edit
{
  "username": "testuser",
  "password": "testpass123"
}
Response:

json
Copy
Edit
{
  "message": "User registered"
}
3.2 🔑 Login (Start Session)
Method: POST

URL: http://127.0.0.1:8000/login/

Body:

json
Copy
Edit
{
  "username": "testuser",
  "password": "testpass123"
}
Response:

json
Copy
Edit
{
  "message": "Login successful"
}
🟡 After login, Postman stores:

sessionid

csrftoken
under Cookies for domain 127.0.0.1

3.3 🔍 Get CSRF Token
Method: GET

URL: http://127.0.0.1:8000/tasks/

Steps:

Click Cookies tab in Postman

Copy csrftoken

Use it in X-CSRFToken header for POST/PUT/DELETE

4. 🔁 Task API (CRUD Operations)
4.1 ➕ Create a Task
Method: POST

URL: http://127.0.0.1:8000/tasks/

Headers:

Key	Value
Content-Type	application/json
X-CSRFToken	<your csrftoken>

Body:

json
Copy
Edit
{
  "title": "Test Task",
  "description": "Testing CSRF token",
  "completed": false
}
✔ Response: 201 Created

4.2 📄 View All Tasks
Method: GET

URL: http://127.0.0.1:8000/tasks/

Optional filters:

?completed=true

?completed=false

✔ Returns: Tasks created by the logged-in user.

4.3 ✏️ Update a Task
Method: PUT

URL: http://127.0.0.1:8000/tasks/1/

Headers:

Key	Value
Content-Type	application/json
X-CSRFToken	<your csrftoken>

Body:

json
Copy
Edit
{
  "title": "Updated Task",
  "description": "Changed content",
  "completed": true
}
✔ Response: 200 OK

4.4 🗑 Delete a Task
Method: DELETE

URL: http://127.0.0.1:8000/tasks/1/

Headers:

Key	Value
X-CSRFToken	<csrftoken>

✔ Response: 204 No Content

4.5 🔓 Logout
Method: POST

URL: http://127.0.0.1:8000/logout/

Response:

json
Copy
Edit
{
  "message": "Logout successful"
}
5. 📚 Swagger API Docs
Visit:
http://127.0.0.1:8000/docs/

✅ Try endpoints in-browser (login required for POST/PUT/DELETE)

6. 📦 Use Postman Collection (For Easy Testing)
If you want to skip manual steps:

Import the file:
task-manager-api.postman_collection.json

Go to Collections → Variables and add:

Variable	Description
csrftoken	Copy from Cookies tab
sessionid	Copy from Cookies tab

All requests will automatically use the correct session + CSRF tokens.

🧪 Great for quick and repeatable testing!

7. 🚨 Common Errors and Fixes
Error	Reason	Fix
403 Forbidden - CSRF Failed	Missing or incorrect CSRF token	Use X-CSRFToken + cookie
401 Unauthorized	Session expired or missing	Re-login to get new sessionid
400 Bad Request	Malformed request body	Check JSON structure and fields
405 Method Not Allowed	Using incorrect HTTP verb	Ensure you're using GET/POST/PUT/etc
204 No Content	Successful DELETE response	✅ Expected after task is deleted

