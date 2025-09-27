# Node.js-API-with-authentication-advanced-querying-and-ideas-management

# 💡 Ideas API with Authentication

A Node.js + Express API that allows users to register, log in, and manage ideas.
Includes JWT authentication, advanced database querying (filtering, sorting, pagination), and user-specific CRUD operations.

# 🚀 Features

User registration & login with hashed passwords (bcryptjs).

JWT authentication for protecting routes.

Ideas CRUD API linked to authenticated users.

Advanced querying:

Filtering (by status)

Sorting (by title or createdAt)

Pagination (_limit, _page)

# 🛠️ Technologies Used

Node.js + Express.js

SQLite (or PostgreSQL)

bcryptjs (password hashing)

jsonwebtoken (JWT authentication)

dotenv (environment variables)

# ⚙️ Setup Instructions
1. Clone and Install
git clone <your-repo-url>
cd <your-project>
npm install

2. Setup Database

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

3. Environment Variables

Create a .env file:

JWT_SECRET=your_super_secret_jwt_key

4. Run the Server
node server.js


Server runs at: http://localhost:3000

# 📌 API Documentation
# 🔑 Authentication
Register a new user
POST /api/register


Body:

{
  "username": "alice",
  "password": "mypassword"
}

Login user
POST /api/login


Body:

{
  "username": "alice",
  "password": "mypassword"
}


Response:

{
  "token": "your_jwt_token"
}

💡 Ideas (Protected Routes)

All requests require header:

Authorization: Bearer <your_token>

Create Idea
POST /api/ideas


Body:

{
  "title": "New Project",
  "description": "Awesome idea",
  "status": "Concept"
}

Get Ideas (with filters)
GET /api/ideas?status=Concept&sort=title&order=asc&_limit=5&_page=1

Update Idea
PUT /api/ideas/:id


Body:

{
  "title": "Updated Project",
  "description": "Improved idea",
  "status": "In Progress"
}

Delete Idea
DELETE /api/ideas/:id

# 🔒 Security

Passwords are stored hashed with bcryptjs.

JWT tokens are used to authenticate requests.

Users can only modify/delete their own ideas.

# 🧪 Testing Flow

Register → POST /api/register

Login → POST /api/login → get JWT token

Use JWT in header to call /api/ideas routes

# 🚧 Challenges & Solutions

Challenge: Securing API endpoints → Solution: Added JWT middleware.

# Credit
This was part of USAM initiative, Thanks for them.

Challenge: Avoiding plaintext passwords → Solution: Used bcryptjs hashing.

Challenge: Complex querying → Solution: Implemented dynamic SQL with filters, sorting, pagination.
