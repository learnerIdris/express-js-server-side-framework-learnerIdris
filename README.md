# Express.js Product Management API

A RESTful API built with **Express.js** and **MongoDB** for managing product. This project demonstrates fundamental Express.js concepts including routing, middleware, database integration, and CRUD operations.

## 📋 Table of Contents

- [About Express.js](#about-expressjs)
- [Features](#features)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [API Endpoints](#api-endpoints)
- [Express.js Core Concepts](#expressjs-core-concepts)
- [Middleware Explained](#middleware-explained)
- [Routing in Express](#routing-in-express)
- [Error Handling](#error-handling)
- [Testing with Postman/cURL](#testing-with-postmancurl)
- [Common Issues & Solutions](#common-issues--solutions)

---

## 🚀 About Express.js

**Express.js** is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications. It simplifies the process of building server-side applications and APIs.

### Why Express.js?

- **Minimalist & Unopinionated**: Provides the essentials without enforcing structure
- **Robust Routing**: Advanced routing with support for parameters, query strings, and middleware
- **Middleware Support**: Extensive middleware ecosystem for various functionalities
- **HTTP Utilities**: Simplified HTTP request/response handling
- **Performance**: Lightweight and fast
- **Community**: Large ecosystem with numerous plugins and extensions

---

## ✨ Features

- ✅ RESTful API architecture
- ✅ MongoDB database integration with Mongoose ODM
- ✅ CRUD operations (Create, Read, Update, Delete)
- ✅ Environment variable configuration
- ✅ JSON request/response handling
- ✅ Error handling middleware
- ✅ Modular route organization
- ✅ Auto-restart with Nodemon

---

## 📁 Project Structure

```
Week 2/
│
├── config/
│   └── db.js                 # Database connection configuration
│
├── models/
│   └── Product.js            # Mongoose schema and model for Student
│
├── routes/
│   └── products.js           # Student-related API routes
│
├── .env                      # Environment variables (not in repo)
├── .gitignore                # Git ignore file
├── package.json              # Project dependencies and scripts
├── server.js                 # Main application entry point
└── README.md                 # Project documentation
```

---

## 📦 Prerequisites

Before running this project, ensure you have the following installed:

- **Node.js** (v14 or higher) - [Download](https://nodejs.org/)
- **npm** (comes with Node.js) or **yarn**
- **MongoDB** (local installation or MongoDB Atlas account) - [Download](https://www.mongodb.com/)
- **Postman** (optional, for API testing) - [Download](https://www.postman.com/)

---

## ⚙️ Installation

1. **Clone the repository** (or navigate to the project directory):
   ```bash
   https://github.com/PLP-MERN-Stack-Development/Week2-express-JS.git
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

   This will install:
   - `express` - Web framework
   - `mongoose` - MongoDB ODM
   - `dotenv` - Environment variable management
   - `nodemon` - Development server with auto-restart

---

## 🔧 Configuration

1. **Create a `.env` file** in the root directory:
   ```bash
   touch .env
   ```

2. **Add the following environment variables**:
   ```env
   PORT=5000
   MONGO_URI=mongodb://localhost:27017/studentDB
   ```

   For **MongoDB Atlas** (cloud database):
   ```env
   PORT=5000
   MONGO_URI=mongodb+srv://<username>:<password>@cluster0.xxxxx.mongodb.net/studentDB?retryWrites=true&w=majority
   ```

   Replace `<username>` and `<password>` with your MongoDB Atlas credentials.

---

## 🏃 Running the Application

### Development Mode (with auto-restart):
```bash
npm start
```

### Production Mode:
```bash
npm run dev
```

The server will start at: **http://localhost:3000**

You should see:
```
Server running on http://localhost:3000
MongoDB Connected.....
```

---

## 🛣️ API Endpoints

### Base URL: `http://localhost:3000`




## 🧠 Express.js Core Concepts

### 1. **Application Instance**
The Express application is created using:
```javascript
const express = require('express');
const app = express();
```

The `app` object represents your Express application and provides methods for:
- Routing HTTP requests
- Configuring middleware
- Rendering HTML views
- Registering template engines

### 2. **Request (req) Object**
Represents the HTTP request and contains properties for:
- `req.body` - Request body (requires `express.json()` middleware)
- `req.params` - Route parameters (e.g., `/students/:id`)
- `req.query` - Query string parameters (e.g., `?name=John&age=20`)
- `req.headers` - Request headers
- `req.method` - HTTP method (GET, POST, etc.)

### 3. **Response (res) Object**
Represents the HTTP response that Express sends back:
- `res.json()` - Send JSON response
- `res.send()` - Send various types of responses
- `res.status()` - Set HTTP status code
- `res.redirect()` - Redirect to another route

### 4. **Routing**
Express provides methods for each HTTP verb:
```javascript
app.get('/', (req, res) => { /* ... */ });     // GET request
app.post('/', (req, res) => { /* ... */ });    // POST request
app.put('/', (req, res) => { /* ... */ });     // PUT request
app.delete('/', (req, res) => { /* ... */ });  // DELETE request
```

---

## 🔌 Middleware Explained

Middleware functions are functions that have access to the request (`req`), response (`res`), and the next middleware function in the application's request-response cycle.

### Types of Middleware:

#### 1. **Application-Level Middleware**
Applied to all routes:
```javascript
app.use(express.json()); // Parses incoming JSON requests
```

#### 2. **Router-Level Middleware**
Applied to specific router instances:
```javascript
app.use("/students", require("./routes/studentRoutes"));
```

#### 3. **Built-in Middleware**
- `express.json()` - Parses JSON payloads
- `express.urlencoded()` - Parses URL-encoded payloads
- `express.static()` - Serves static files

#### 4. **Third-Party Middleware**
- `dotenv` - Loads environment variables
- `cors` - Enables Cross-Origin Resource Sharing
- `morgan` - HTTP request logger

#### 5. **Error-Handling Middleware**
Special middleware with 4 parameters:
```javascript
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).json({ message: 'Something went wrong!' });
});
```

### Middleware Flow:
```
Request → Middleware 1 → Middleware 2 → Route Handler → Response
```

Each middleware can:
- Execute code
- Modify request/response objects
- End the request-response cycle
- Call the next middleware using `next()`

---

## 🛤️ Routing in Express

### Basic Route Structure:
```javascript
app.METHOD(PATH, HANDLER)
```

- **METHOD**: HTTP method (get, post, put, delete)
- **PATH**: URL path
- **HANDLER**: Callback function to execute

### Route Parameters:
```javascript
// URL: /students/123
router.get("/:id", (req, res) => {
    const studentId = req.params.id; // "123"
    // ... fetch student by ID
});
```

### Query Strings:
```javascript
// URL: /students?age=20&name=John
router.get("/", (req, res) => {
    const age = req.query.age;     // "20"
    const name = req.query.name;   // "John"
    // ... filter students
});
```

### Router Modules:
Organize routes in separate files:
```javascript
// studentRoutes.js
const router = express.Router();
router.get("/", getAllStudents);
router.post("/", createStudent);
module.exports = router;

// server.js
app.use("/students", studentRoutes);
```

---

## ⚠️ Error Handling

### Try-Catch Blocks:
All async operations use try-catch for error handling:
```javascript
router.get("/", async (req, res) => {
    try {
        const students = await Student.find();
        res.json(students);
    } catch (error) {
        res.status(500).json({ message: error.message });
    }
});
```

### Common HTTP Status Codes:
- **200**: OK - Successful request
- **201**: Created - Resource created successfully
- **400**: Bad Request - Invalid request data
- **404**: Not Found - Resource not found
- **500**: Internal Server Error - Server error

---

## 🧪 Testing with Postman/cURL

### Using Postman:

1. **GET Request**:
   - Method: GET
   - URL: `http://localhost:5000/students`
   - Click "Send"

2. **POST Request**:
   - Method: POST
   - URL: `http://localhost:5000/students`
   - Headers: `Content-Type: application/json`
   - Body (raw JSON):
     ```json
     {
       "name": "John Doe",
       "age": 20,
       "email": "john@example.com"
     }
     ```

3. **PUT Request**:
   - Method: PUT
   - URL: `http://localhost:5000/students/6501234567890abcdef12345`
   - Headers: `Content-Type: application/json`
   - Body: Updated fields

4. **DELETE Request**:
   - Method: DELETE
   - URL: `http://localhost:5000/students/6501234567890abcdef12345`

---

## 🐛 Common Issues & Solutions

### 1. **MongoDB Connection Failed**
**Error**: `MongooseServerSelectionError: connect ECONNREFUSED`

**Solutions**:
- Ensure MongoDB is running locally: `sudo systemctl start mongodb`
- Check `MONGO_URI` in `.env` file
- For Atlas, verify network access settings (allow your IP)

### 2. **Port Already in Use**
**Error**: `EADDRINUSE: address already in use :::5000`

**Solutions**:
- Change port in `.env` file
- Kill process using port: `lsof -ti:5000 | xargs kill -9`

### 3. **Cannot POST/GET Data**
**Possible Causes**:
- Missing `express.json()` middleware
- Incorrect Content-Type header
- Route not properly defined

**Solution**:
```javascript
app.use(express.json()); // Add this before routes
```

### 4. **Module Not Found**
**Error**: `Cannot find module 'express'`

**Solution**:
```bash
npm install
```

### 5. **Environment Variables Not Loading**
**Solution**:
- Ensure `.env` file is in root directory
- Add `require('dotenv').config()` at top of `server.js`
- Restart server after changes

---

## 📚 Additional Resources

### Official Documentation:
- [Express.js Official Docs](https://expressjs.com/)
- [Mongoose Documentation](https://mongoosejs.com/)
- [Node.js Documentation](https://nodejs.org/docs/)

### Tutorials:
- [Express.js Guide](https://expressjs.com/en/guide/routing.html)
- [REST API Best Practices](https://restfulapi.net/)
- [MongoDB University](https://university.mongodb.com/)

### Tools:
- [Postman](https://www.postman.com/) - API testing
- [MongoDB Compass](https://www.mongodb.com/products/compass) - Database GUI
- [Nodemon](https://nodemon.io/) - Auto-restart server

---

## 🤝 Contributing

Feel free to fork this project, submit issues, or create pull requests for improvements!

---

## 📝 License

This project is open-source and available under the ISC License.

---

## 👨‍💻 Author
Learner Idris 

---

**Happy Coding! 🚀**
