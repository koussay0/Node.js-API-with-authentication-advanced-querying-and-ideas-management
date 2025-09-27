# 🚀 Secure Ideas API

A Node.js + Express.js API for managing ideas, with JWT authentication, user registration/login, and advanced querying (filtering, sorting, pagination).

# ✨ Features

User registration & login with bcryptjs (password hashing).

JWT authentication for secure access to protected routes.

CRUD operations for ideas, each tied to the logged-in user.

Advanced querying:

Filtering (/api/ideas?status=Concept)

Sorting (/api/ideas?sort=title&order=asc)

Pagination (/api/ideas?_limit=5&_page=1)

# 🛠️ Tech Stack

Node.js + Express.js

SQLite (or PostgreSQL)

bcryptjs (password hashing)

jsonwebtoken (JWT handling)

dotenv (environment variables)

# ⚙️ Setup Instructions
#### 1. Clone & Install
git clone <your-repo-url>
cd secure-ideas-api
npm install

### 2. Setup Database

Run these SQL commands:

CREATE TABLE users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  username TEXT UNIQUE NOT NULL,
  password TEXT NOT NULL
);

CREATE TABLE ideas (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  title TEXT NOT NULL,
  description TEXT,
  status TEXT,
  createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  userId INTEGER
);

### 3. Environment Variables

Create a .env file:

JWT_SECRET=your_super_secret_jwt_key

### 4. Run Server
node server.js


## Server runs at 👉 http://localhost:3000

# 🔑 Authentication
Register User
POST /api/register


Body:
```
{
  "username": "alice",
  "password": "mypassword"
}
```
Login User
POST /api/login


Body:
```
{
  "username": "alice",
  "password": "mypassword"
}
```

## ✅ Response:
```
{
  "token": "your_jwt_token"
}
```

# 📌 Use this token in the header:

Authorization: Bearer your_jwt_token

# 💡 Ideas API (Protected Routes)
Create Idea
POST /api/ideas


Headers:

Authorization: Bearer <token>


Body:
```
{
  "title": "My Idea",
  "description": "This is an awesome project",
  "status": "Concept"
}
```
Get Ideas (with queries)
GET /api/ideas?status=Concept&sort=title&order=asc&_limit=2&_page=1

Update Idea
PUT /api/ideas/:id


Body:
```
{
  "title": "Updated Idea",
  "description": "Improved version",
  "status": "In Progress"
}
```
Delete Idea
DELETE /api/ideas/:id

# 🧪 Testing Instructions

Register a new user → /api/register

Login to get a JWT → /api/login

Use JWT token in headers → Authorization: Bearer <token>

Create an idea → /api/ideas

Get ideas with filters → /api/ideas?status=Concept

Update/Delete your own idea → /api/ideas/:id

# Negative tests:

Access without token → 401 Unauthorized

Wrong credentials → 400 Invalid credentials

Try modifying another user’s idea → should fail

🔒 Security

Passwords are stored hashed, never plain text.

JWT tokens secure API access.

Users can only edit/delete their own ideas.
