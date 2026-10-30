# ⚙️ Backend (Server) — Kanban Project

## 📌 Overview

This is the **backend of the Kanban-style project management application** built using **Node.js, Express.js, and MySQL**.

It provides REST APIs to manage:

- Boards
- Lists
- Cards

The backend follows a **MVC (Model-View-Controller) architecture** and uses **Sequelize ORM** for database operations.

---

## 🛠️ Tech Stack

- 🟢 Node.js
- 🚀 Express.js
- 🗄️ MySQL
- 🧠 Sequelize ORM
- 🔐 dotenv (environment variables)
- 🌐 CORS

---

## 📂 Folder Structure

```plaintext
server/
├── config/
│   └── db.js
├── controllers/
│   ├── boardController.js
│   ├── listController.js
│   └── cardController.js
├── models/
│   ├── Board.js
│   ├── List.js
│   ├── Card.js
│   └── index.js
├── routes/
│   ├── boardRoutes.js
│   ├── listRoutes.js
│   └── cardRoutes.js
├── .env
├── server.js
└── package.json
```

---

## 🚀 Features

### 🟦 Boards

- Create board
- Get all boards
- Delete board

### 🟨 Lists

- Create list inside board
- Get lists by boardId
- Delete list (with cascade delete)

### 🟩 Cards

- Create card inside list
- Get cards by listId
- Move card between lists
- Delete card

---

## 🔗 API Endpoints

### 📌 Boards

```http
POST   /api/boards
GET    /api/boards
DELETE /api/boards/:id
```

---

### 📌 Lists

```http
POST   /api/lists
GET    /api/lists/:boardId
DELETE /api/lists/:id
```

---

### 📌 Cards

```http
POST   /api/cards
GET    /api/cards/:listId
PUT    /api/cards/move
DELETE /api/cards/:id
```

---

## 🗄️ Database Schema

### Boards Table

```plaintext
id (PK)
title
createdAt
updatedAt
```

---

### Lists Table

```plaintext
id (PK)
title
boardId (FK → Boards.id)
position
createdAt
updatedAt
```

---

### Cards Table

```plaintext
id (PK)
title
listId (FK → Lists.id)
position
createdAt
updatedAt
```

---

## 🔗 Relationships

```js
Board.hasMany(List, { foreignKey: "boardId", onDelete: "CASCADE" });
List.belongsTo(Board);

List.hasMany(Card, { foreignKey: "listId", onDelete: "CASCADE" });
Card.belongsTo(List);
```

---

## ⚙️ Setup Instructions

### 🔹 1. Install Dependencies

```bash
npm install
```

---

### 🔹 2. Create `.env` File

```env
DB_NAME=kanban_db
DB_USER=root
DB_PASSWORD=yourpassword
DB_HOST=localhost
PORT=8000
```

---

### 🔹 3. Run Server

```bash
node server.js
```

---

## 🧠 How It Works

```plaintext
Client → API Request → Express Route → Controller → Sequelize → MySQL → Response → Client
```

---

## ⚠️ Important Notes

- Database must exist before running server
- Foreign key constraints are enforced
- Ensure correct IDs (boardId, listId) while creating data

---

## ❗ Common Errors

### 1. Foreign Key Error

```plaintext
Cannot add or update a child row
```

👉 Cause: Invalid `boardId` or `listId`

---

### 2. JSON Error

```plaintext
Unexpected end of JSON input
```

👉 Cause: Empty or invalid request body

---

## 🔥 Improvements (Future Scope)

- Add authentication (JWT)
- Add validation middleware
- Add logging (Winston/Morgan)
- Add pagination & filtering
- Replace sync with migrations

---

## 💡 Developer Notes

- Uses async/await for API calls
- Follows RESTful API structure
- Uses Sequelize for ORM
- Handles relational database constraints

---

## 👨‍💻 Author

**Shubham Rana**

---

## ⭐ Support

If you like this project, give it a ⭐ on GitHub!
