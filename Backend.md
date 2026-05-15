pasted-text.txt

TXT


GENERARE A MD FILE FOR THIS IN A DETAILED VERSION


markdown


# Complete Backend Development Guide
## Node.js + Express + MongoDB
> A comprehensive, beginner-friendly reference for backend development. Covers fundamentals through production-ready practices.
---
## Table of Contents
1. [Introduction to Backend Development](#1-introduction-to-backend-development)
2. [How the Internet Works](#2-how-the-internet-works)
3. [Understanding Servers](#3-understanding-servers)
4. [Request-Response Cycle](#4-request-response-cycle)
5. [Node.js Fundamentals](#5-nodejs-fundamentals)
6. [NPM (Node Package Manager)](#6-npm-node-package-manager)
7. [Creating Your First Backend Project](#7-creating-your-first-backend-project)
8. [Express.js Fundamentals](#8-expressjs-fundamentals)
9. [Routing in Express](#9-routing-in-express)
10. [Middleware](#10-middleware)
11. [HTTP Methods](#11-http-methods)
12. [REST APIs](#12-rest-apis)
13. [HTTP Status Codes](#13-http-status-codes)
14. [API Testing with Postman](#14-api-testing-with-postman)
15. [MongoDB Fundamentals](#15-mongodb-fundamentals)
16. [MongoDB Atlas Setup](#16-mongodb-atlas-setup)
17. [Mongoose ODM](#17-mongoose-odm)
18. [Schema & Models](#18-schema--models)
19. [CRUD Operations](#19-crud-operations)
20. [MVC Architecture](#20-mvc-architecture)
21. [Authentication Concepts](#21-authentication-concepts)
22. [Password Hashing with Bcrypt](#22-password-hashing-with-bcrypt)
23. [JWT Authentication](#23-jwt-authentication)
24. [Cookies & Cookie Parser](#24-cookies--cookie-parser)
25. [Authorization & Role-Based Access](#25-authorization--role-based-access)
26. [File Uploads & Cloud Storage](#26-file-uploads--cloud-storage)
27. [Environment Variables](#27-environment-variables)
28. [Input Validation](#28-input-validation)
29. [Error Handling](#29-error-handling)
30. [Async/Await & Error Management](#30-asyncawait--error-management)
31. [Project Folder Structure](#31-project-folder-structure)
32. [Building Production-Ready APIs](#32-building-production-ready-apis)
33. [Security Best Practices](#33-security-best-practices)
34. [Rate Limiting & CORS](#34-rate-limiting--cors)
35. [Logging & Debugging](#35-logging--debugging)
36. [Testing with Jest & Supertest](#36-testing-with-jest--supertest)
37. [Deployment](#37-deployment)
38. [Git & Version Control](#38-git--version-control)
39. [Interview Questions](#39-interview-questions)
40. [Learning Roadmap](#40-learning-roadmap)
41. [Quick Reference Cheatsheet](#41-quick-reference-cheatsheet)
---
## 1. Introduction to Backend Development
Backend development encompasses everything that happens behind the scenes of a web application—the parts users never directly see but constantly interact with.
### Frontend vs Backend
| Aspect | Frontend | Backend |
|--------|----------|---------|
| **What it is** | User interface, visual elements | Server logic, data processing |
| **Technologies** | HTML, CSS, JavaScript, React | Node.js, Express, databases |
| **User interaction** | Direct | Indirect (through APIs) |
| **Location** | Browser | Server |
### What Backend Handles
- **Authentication & Authorization** — Verifying user identity and permissions
- **Database Operations** — Storing, retrieving, and manipulating data
- **API Development** — Creating endpoints for frontend communication
- **Business Logic** — Rules and calculations specific to your application
- **Security** — Protecting data and preventing unauthorized access
- **File Processing** — Handling uploads, transformations, storage
- **Third-party Integrations** — Payment gateways, email services, external APIs
### Real-World Example: Instagram Login
When a user logs into Instagram:
1. **Frontend** displays the login form and captures input
2. **Backend** receives the credentials and:
   - Validates the email format
   - Checks if the user exists in the database
   - Compares the hashed password
   - Generates an authentication token
   - Returns success/failure response
3. **Frontend** redirects based on the response
The backend handles all the critical logic—the frontend just presents information and collects input.
---
## 2. How the Internet Works
Understanding internet fundamentals helps you build better backend systems.
### The Basic Request Flow
User → Browser → DNS → Internet → Server → Database ↓ User ← Browser ← Internet ←←←←←← Response



### Step-by-Step Breakdown
1. **User Action** — User types `google.com` or clicks a link
2. **DNS Lookup** — Domain name translates to IP address (e.g., `142.250.190.78`)
3. **Request Sent** — Browser sends HTTP request through the internet
4. **Server Processing** — Web server receives and processes the request
5. **Database Query** — Server fetches data if needed
6. **Response Generated** — Server constructs the response (HTML, JSON, etc.)
7. **Response Delivered** — Data travels back through the internet
8. **Browser Renders** — User sees the result
### Key Protocols
| Protocol | Purpose | Port |
|----------|---------|------|
| **HTTP** | Web communication (unencrypted) | 80 |
| **HTTPS** | Secure web communication (encrypted) | 443 |
| **TCP/IP** | Data transmission foundation | — |
| **DNS** | Domain to IP translation | 53 |
---
## 3. Understanding Servers
A server is a computer program or device that provides functionality to other programs or devices (clients).
### Types of Servers
| Type | Purpose | Examples |
|------|---------|----------|
| **Web Server** | Serves web pages and APIs | Nginx, Apache |
| **Application Server** | Runs application logic | Node.js, Django |
| **Database Server** | Stores and retrieves data | MongoDB, PostgreSQL |
| **File Server** | Stores and serves files | AWS S3, ImageKit |
| **Mail Server** | Handles email | SendGrid, Mailgun |
### Server Characteristics
- **Always On** — Runs 24/7 to handle requests anytime
- **Listens on Ports** — Waits for incoming connections on specific ports
- **Handles Multiple Requests** — Processes many requests simultaneously
- **Stateless (typically)** — Each request is independent
### What Happens on a Server
```javascript
// Simplified server concept
while (true) {
  request = waitForRequest();     // Listen for incoming requests
  response = processRequest(request);  // Handle the request
  sendResponse(response);         // Send back the result
}
4. Request-Response Cycle
Every web interaction follows the request-response pattern.

Anatomy of an HTTP Request


┌─────────────────────────────────────────────┐
│  REQUEST                                    │
├─────────────────────────────────────────────┤
│  Method:  GET                               │
│  URL:     /api/users/123                    │
│  Headers:                                   │
│    - Content-Type: application/json         │
│    - Authorization: Bearer <token>          │
│  Body:    (empty for GET, data for POST)    │
└─────────────────────────────────────────────┘
Anatomy of an HTTP Response


┌─────────────────────────────────────────────┐
│  RESPONSE                                   │
├─────────────────────────────────────────────┤
│  Status:  200 OK                            │
│  Headers:                                   │
│    - Content-Type: application/json         │
│    - Set-Cookie: session=abc123             │
│  Body:                                      │
│    {                                        │
│      "id": 123,                             │
│      "name": "John Doe",                    │
│      "email": "john@example.com"            │
│    }                                        │
└─────────────────────────────────────────────┘
Request Components Explained
Component	Description	Example
Method	Action to perform	GET, POST, PUT, DELETE
URL/Path	Resource location	/api/users/123
Headers	Metadata about request	Content-Type, Authorization
Query Params	Filter/modify request	?page=2&limit=10
Body	Data payload	JSON, form data
Response Components Explained
Component	Description	Example
Status Code	Result indicator	200, 404, 500
Headers	Metadata about response	Content-Type, Cache-Control
Body	Actual data	JSON, HTML, file
5. Node.js Fundamentals
Node.js is a JavaScript runtime built on Chrome's V8 engine that allows JavaScript to run on servers.

Why Node.js?
Advantage	Description
JavaScript Everywhere	Same language for frontend and backend
Non-blocking I/O	Handles many connections efficiently
Fast Execution	V8 engine compiles to machine code
Huge Ecosystem	Millions of packages via NPM
Active Community	Extensive documentation and support
Node.js Use Cases
REST APIs and GraphQL servers
Real-time applications (chat, gaming)
Streaming services
Microservices architecture
Command-line tools
Server-side rendering
Installation Verification
bash


# Check Node.js version
node -v
# Output: v20.x.x
# Check NPM version
npm -v
# Output: 10.x.x
Running JavaScript with Node
Create a file hello.js:

javascript


// hello.js
console.log('Hello from Node.js!');
// Access environment info
console.log('Node version:', process.version);
console.log('Current directory:', process.cwd());
Run it:

bash


node hello.js
Node.js vs Browser JavaScript
Feature	Browser	Node.js
DOM manipulation	✅ Yes	❌ No
File system access	❌ No	✅ Yes
window object	✅ Yes	❌ No
global object	❌ No	✅ Yes
require/import	Limited	✅ Full support
Network requests	Restricted	✅ Full access
Built-in Modules
Node.js includes useful modules without installation:

javascript


// File System
const fs = require('fs');
fs.readFileSync('file.txt', 'utf-8');
// Path utilities
const path = require('path');
path.join(__dirname, 'folder', 'file.txt');
// HTTP server
const http = require('http');
// Operating system info
const os = require('os');
console.log(os.platform(), os.cpus().length + ' cores');
6. NPM (Node Package Manager)
NPM is the default package manager for Node.js—it manages project dependencies and scripts.

Initializing a Project
bash


# Create package.json interactively
npm init
# Create with defaults (recommended for learning)
npm init -y
package.json Explained
json


{
  "name": "my-backend",
  "version": "1.0.0",
  "description": "My backend application",
  "main": "app.js",
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js",
    "test": "jest"
  },
  "dependencies": {
    "express": "^4.18.2",
    "mongoose": "^8.0.0"
  },
  "devDependencies": {
    "nodemon": "^3.0.0",
    "jest": "^29.0.0"
  }
}
Field	Purpose
name	Package identifier
version	Semantic versioning
main	Entry point file
scripts	Command shortcuts
dependencies	Required for production
devDependencies	Development only
Essential NPM Commands
bash


# Install all dependencies from package.json
npm install
# Install a production dependency
npm install express
# Install a dev dependency
npm install nodemon --save-dev
# or
npm install nodemon -D
# Install globally (CLI tools)
npm install -g nodemon
# Uninstall a package
npm uninstall express
# Update packages
npm update
# Check for outdated packages
npm outdated
# Run a script
npm run dev
npm start  # 'start' doesn't need 'run'
npm test   # 'test' doesn't need 'run'
Understanding Version Numbers
Format: MAJOR.MINOR.PATCH



^4.18.2  →  Allows 4.x.x (minor + patch updates)
~4.18.2  →  Allows 4.18.x (patch updates only)
4.18.2   →  Exact version only
Important Files
File	Purpose	Git?
package.json	Project metadata & dependencies	✅ Commit
package-lock.json	Exact dependency versions	✅ Commit
node_modules/	Installed packages	❌ Ignore
.gitignore for Node Projects
gitignore


node_modules/
.env
.env.local
*.log
dist/
coverage/
7. Creating Your First Backend Project
Let's build a simple Express server from scratch.

Project Setup
bash


# Create project directory
mkdir my-backend
cd my-backend
# Initialize NPM
npm init -y
# Install Express
npm install express
# Install development tools
npm install nodemon --save-dev
Update package.json Scripts
json


{
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js"
  }
}
Create app.js
javascript


// Import Express
const express = require('express');
// Create Express application
const app = express();
// Define port
const PORT = process.env.PORT || 3000;
// Middleware to parse JSON
app.use(express.json());
// Root route
app.get('/', (req, res) => {
  res.json({
    message: 'Welcome to my API!',
    status: 'Server is running',
    timestamp: new Date().toISOString()
  });
});
// Health check route
app.get('/health', (req, res) => {
  res.json({ status: 'OK' });
});
// Start server
app.listen(PORT, () => {
  console.log(`Server running on http://localhost:${PORT}`);
});
Run the Server
bash


# Development (auto-restarts on changes)
npm run dev
# Production
npm start
Test Your Server
Open browser: [localhost](http://localhost:3000)

Or use curl:

bash


curl [localhost](http://localhost:3000)
Expected response:

json


{
  "message": "Welcome to my API!",
  "status": "Server is running",
  "timestamp": "2024-01-15T10:30:00.000Z"
}
8. Express.js Fundamentals
Express.js is a minimal, flexible Node.js web application framework.

Why Express?
Feature	Benefit
Minimal	Only includes essentials, add what you need
Routing	Easy URL-to-function mapping
Middleware	Modular request processing
Large Ecosystem	Many compatible packages
Well Documented	Extensive guides and examples
Core Concepts
The Application Object
javascript


const express = require('express');
const app = express();
// 'app' is your server instance
// All configuration and routes attach to it
Request Object (req)
Contains information about the HTTP request:

javascript


app.get('/example', (req, res) => {
  req.params      // URL parameters (/users/:id)
  req.query       // Query string (?page=1)
  req.body        // Request body (POST/PUT data)
  req.headers     // HTTP headers
  req.cookies     // Cookies (with cookie-parser)
  req.method      // HTTP method (GET, POST, etc.)
  req.path        // URL path
  req.ip          // Client IP address
});
Response Object (res)
Used to send response back to client:

javascript


app.get('/example', (req, res) => {
  // Send JSON
  res.json({ data: 'value' });
  
  // Send plain text
  res.send('Hello');
  
  // Set status code
  res.status(201).json({ created: true });
  
  // Redirect
  res.redirect('/other-page');
  
  // Send file
  res.sendFile('/path/to/file.pdf');
  
  // Set headers
  res.set('X-Custom-Header', 'value');
  
  // Set cookie
  res.cookie('name', 'value', { httpOnly: true });
});
Built-in Middleware
javascript


// Parse JSON bodies
app.use(express.json());
// Parse URL-encoded bodies (form data)
app.use(express.urlencoded({ extended: true }));
// Serve static files
app.use(express.static('public'));
Application Methods Overview
javascript


// Route methods
app.get(path, handler)
app.post(path, handler)
app.put(path, handler)
app.patch(path, handler)
app.delete(path, handler)
// Middleware
app.use(middleware)
app.use(path, middleware)
// Start server
app.listen(port, callback)
9. Routing in Express
Routes define how your application responds to client requests at specific endpoints.

Basic Route Syntax
javascript


app.METHOD(PATH, HANDLER);
// METHOD: HTTP method (get, post, put, delete, etc.)
// PATH: URL path
// HANDLER: Function executed when route matches
Simple Routes
javascript


// GET request to homepage
app.get('/', (req, res) => {
  res.send('Home Page');
});
// GET request to about page
app.get('/about', (req, res) => {
  res.send('About Page');
});
// POST request to create user
app.post('/users', (req, res) => {
  const userData = req.body;
  res.status(201).json({ message: 'User created', data: userData });
});
Route Parameters
Dynamic segments in the URL:

javascript


// Single parameter
app.get('/users/:id', (req, res) => {
  const userId = req.params.id;
  res.json({ userId });
});
// Multiple parameters
app.get('/users/:userId/posts/:postId', (req, res) => {
  const { userId, postId } = req.params;
  res.json({ userId, postId });
});
// Optional parameters (using regex or separate routes)
app.get('/posts/:year/:month?', (req, res) => {
  // month is captured but Express doesn't have native optional params
  // Better to use query parameters for optional values
});
Query Parameters
Data passed in the URL after ?:

javascript


// URL: /search?q=nodejs&page=2&limit=10
app.get('/search', (req, res) => {
  const { q, page = 1, limit = 10 } = req.query;
  res.json({
    searchTerm: q,
    page: parseInt(page),
    limit: parseInt(limit)
  });
});
Route Organization with Router
For larger applications, organize routes in separate files:

routes/userRoutes.js

javascript


const express = require('express');
const router = express.Router();
// All routes here are relative to where router is mounted
router.get('/', (req, res) => {
  res.json({ message: 'Get all users' });
});
router.get('/:id', (req, res) => {
  res.json({ message: `Get user ${req.params.id}` });
});
router.post('/', (req, res) => {
  res.status(201).json({ message: 'Create user', data: req.body });
});
router.put('/:id', (req, res) => {
  res.json({ message: `Update user ${req.params.id}` });
});
router.delete('/:id', (req, res) => {
  res.json({ message: `Delete user ${req.params.id}` });
});
module.exports = router;
app.js

javascript


const express = require('express');
const userRoutes = require('./routes/userRoutes');
const app = express();
app.use(express.json());
// Mount router at /api/users
app.use('/api/users', userRoutes);
// Routes become:
// GET /api/users
// GET /api/users/:id
// POST /api/users
// etc.
app.listen(3000);
Route Chaining
javascript


app.route('/books')
  .get((req, res) => {
    res.json({ message: 'Get all books' });
  })
  .post((req, res) => {
    res.json({ message: 'Create book' });
  });
app.route('/books/:id')
  .get((req, res) => {
    res.json({ message: `Get book ${req.params.id}` });
  })
  .put((req, res) => {
    res.json({ message: `Update book ${req.params.id}` });
  })
  .delete((req, res) => {
    res.json({ message: `Delete book ${req.params.id}` });
  });
10. Middleware
Middleware functions have access to the request and response objects and can modify them or end the request-response cycle.

Middleware Concept


Request → Middleware 1 → Middleware 2 → Route Handler → Response
Middleware Signature
javascript


function middleware(req, res, next) {
  // Do something with req or res
  next(); // Pass control to next middleware
}
Important: Always call next() unless you're ending the response. Otherwise, the request hangs.

Types of Middleware
Application-Level Middleware
Runs on every request:

javascript


// Runs on ALL requests
app.use((req, res, next) => {
  console.log(`${req.method} ${req.path}`);
  next();
});
// Runs on requests to /api/*
app.use('/api', (req, res, next) => {
  console.log('API request');
  next();
});
Router-Level Middleware
Attached to specific routers:

javascript


const router = express.Router();
router.use((req, res, next) => {
  console.log('Router middleware');
  next();
});
Built-in Middleware
javascript


// Parse JSON bodies
app.use(express.json());
// Parse URL-encoded bodies
app.use(express.urlencoded({ extended: true }));
// Serve static files from 'public' folder
app.use(express.static('public'));
Third-Party Middleware
javascript


const cors = require('cors');
const morgan = require('morgan');
const helmet = require('helmet');
app.use(cors());           // Enable CORS
app.use(morgan('dev'));    // Request logging
app.use(helmet());         // Security headers
Error-Handling Middleware
Has four parameters:

javascript


// Must be defined AFTER all other middleware and routes
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({
    success: false,
    message: 'Something went wrong',
    error: process.env.NODE_ENV === 'development' ? err.message : undefined
  });
});
Practical Middleware Examples
Request Logger
javascript


const requestLogger = (req, res, next) => {
  const timestamp = new Date().toISOString();
  console.log(`[${timestamp}] ${req.method} ${req.originalUrl}`);
  next();
};
app.use(requestLogger);
Authentication Middleware
javascript


const authenticate = (req, res, next) => {
  const token = req.headers.authorization?.split(' ')[1];
  
  if (!token) {
    return res.status(401).json({ message: 'No token provided' });
  }
  
  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = decoded;
    next();
  } catch (error) {
    return res.status(401).json({ message: 'Invalid token' });
  }
};
// Apply to specific routes
app.get('/profile', authenticate, (req, res) => {
  res.json({ user: req.user });
});
Request Timing
javascript


const requestTimer = (req, res, next) => {
  req.startTime = Date.now();
  
  res.on('finish', () => {
    const duration = Date.now() - req.startTime;
    console.log(`${req.method} ${req.path} - ${duration}ms`);
  });
  
  next();
};
app.use(requestTimer);
Middleware Order Matters
javascript


// Middleware executes in order of definition
app.use(express.json());        // 1. Parse body first
app.use(morgan('dev'));         // 2. Log request
app.use(authenticate);          // 3. Check auth
app.use('/api', apiRoutes);     // 4. Handle routes
app.use(errorHandler);          // 5. Handle errors (always last)
11. HTTP Methods
HTTP methods indicate the desired action to perform on a resource.

Method Overview
Method	Purpose	Has Body	Idempotent	Safe
GET	Retrieve data	No	Yes	Yes
POST	Create data	Yes	No	No
PUT	Replace data	Yes	Yes	No
PATCH	Partial update	Yes	No	No
DELETE	Remove data	Optional	Yes	No
HEAD	GET without body	No	Yes	Yes
OPTIONS	Get allowed methods	No	Yes	Yes
Definitions
Idempotent: Multiple identical requests have the same effect as one
Safe: Doesn't modify server state
Method Details
GET — Retrieve Resource
javascript


// Get all users
app.get('/users', async (req, res) => {
  const users = await User.find();
  res.json(users);
});
// Get single user
app.get('/users/:id', async (req, res) => {
  const user = await User.findById(req.params.id);
  res.json(user);
});
POST — Create Resource
javascript


app.post('/users', async (req, res) => {
  const { name, email, password } = req.body;
  
  const user = await User.create({ name, email, password });
  
  res.status(201).json({
    success: true,
    data: user
  });
});
PUT — Replace Entire Resource
javascript


app.put('/users/:id', async (req, res) => {
  // Replaces the entire document
  const user = await User.findByIdAndUpdate(
    req.params.id,
    req.body,
    { new: true, overwrite: true }
  );
  
  res.json(user);
});
PATCH — Partial Update
javascript


app.patch('/users/:id', async (req, res) => {
  // Updates only provided fields
  const user = await User.findByIdAndUpdate(
    req.params.id,
    { $set: req.body },
    { new: true }
  );
  
  res.json(user);
});
DELETE — Remove Resource
javascript


app.delete('/users/:id', async (req, res) => {
  await User.findByIdAndDelete(req.params.id);
  
  res.status(204).send(); // No content
  // or
  res.json({ message: 'User deleted' });
});
PUT vs PATCH
Aspect	PUT	PATCH
Scope	Entire resource	Partial update
Missing fields	Set to null/default	Left unchanged
Use case	Replace completely	Update specific fields
Example:

Original user: { name: "John", email: "john@example.com", age: 25 }

PUT with { name: "Jane" } → { name: "Jane", email: null, age: null }

PATCH with { name: "Jane" } → { name: "Jane", email: "john@example.com", age: 25 }

12. REST APIs
REST (Representational State Transfer) is an architectural style for designing networked applications.

REST Principles
Client-Server Separation — Frontend and backend are independent
Stateless — Each request contains all necessary information
Cacheable — Responses can be cached when appropriate
Uniform Interface — Consistent resource identification and manipulation
Layered System — Client doesn't know if connected directly to server
RESTful URL Design
Resource Naming Conventions


✅ Good (nouns, plural):
GET    /users
GET    /users/123
POST   /users
PUT    /users/123
DELETE /users/123
❌ Bad (verbs, actions in URL):
GET    /getUsers
POST   /createUser
GET    /user/delete/123
Nested Resources


GET    /users/123/posts         # All posts by user 123
GET    /users/123/posts/456     # Specific post by user
POST   /users/123/posts         # Create post for user
Filtering, Sorting, Pagination


GET /users?role=admin                    # Filter
GET /users?sort=createdAt&order=desc     # Sort
GET /users?page=2&limit=10               # Pagination
GET /users?fields=name,email             # Field selection
GET /users?role=admin&sort=-createdAt&page=1&limit=20  # Combined
RESTful Response Structure
Success Response
json


{
  "success": true,
  "data": {
    "id": "123",
    "name": "John Doe",
    "email": "john@example.com"
  }
}
Collection Response with Pagination
json


{
  "success": true,
  "count": 25,
  "pagination": {
    "page": 1,
    "limit": 10,
    "totalPages": 3,
    "totalCount": 25
  },
  "data": [
    { "id": "1", "name": "User 1" },
    { "id": "2", "name": "User 2" }
  ]
}
Error Response
json


{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid email format",
    "details": [
      {
        "field": "email",
        "message": "Must be a valid email address"
      }
    ]
  }
}
Complete REST API Example
javascript


const express = require('express');
const router = express.Router();
// GET /api/products - Get all products
router.get('/', async (req, res) => {
  try {
    const { page = 1, limit = 10, category, sort = '-createdAt' } = req.query;
    
    const query = {};
    if (category) query.category = category;
    
    const products = await Product.find(query)
      .sort(sort)
      .skip((page - 1) * limit)
      .limit(parseInt(limit));
    
    const total = await Product.countDocuments(query);
    
    res.json({
      success: true,
      count: products.length,
      pagination: {
        page: parseInt(page),
        limit: parseInt(limit),
        totalPages: Math.ceil(total / limit),
        totalCount: total
      },
      data: products
    });
  } catch (error) {
    res.status(500).json({ success: false, message: error.message });
  }
});
// GET /api/products/:id - Get single product
router.get('/:id', async (req, res) => {
  try {
    const product = await Product.findById(req.params.id);
    
    if (!product) {
      return res.status(404).json({
        success: false,
        message: 'Product not found'
      });
    }
    
    res.json({ success: true, data: product });
  } catch (error) {
    res.status(500).json({ success: false, message: error.message });
  }
});
// POST /api/products - Create product
router.post('/', async (req, res) => {
  try {
    const product = await Product.create(req.body);
    res.status(201).json({ success: true, data: product });
  } catch (error) {
    res.status(400).json({ success: false, message: error.message });
  }
});
// PATCH /api/products/:id - Update product
router.patch('/:id', async (req, res) => {
  try {
    const product = await Product.findByIdAndUpdate(
      req.params.id,
      req.body,
      { new: true, runValidators: true }
    );
    
    if (!product) {
      return res.status(404).json({
        success: false,
        message: 'Product not found'
      });
    }
    
    res.json({ success: true, data: product });
  } catch (error) {
    res.status(400).json({ success: false, message: error.message });
  }
});
// DELETE /api/products/:id - Delete product
router.delete('/:id', async (req, res) => {
  try {
    const product = await Product.findByIdAndDelete(req.params.id);
    
    if (!product) {
      return res.status(404).json({
        success: false,
        message: 'Product not found'
      });
    }
    
    res.status(204).send();
  } catch (error) {
    res.status(500).json({ success: false, message: error.message });
  }
});
module.exports = router;
13. HTTP Status Codes
Status codes indicate the result of an HTTP request.

Status Code Categories
Range	Category	Description
1xx	Informational	Request received, continuing
2xx	Success	Request successfully received and processed
3xx	Redirection	Further action needed
4xx	Client Error	Request contains errors
5xx	Server Error	Server failed to fulfill request
Common Status Codes
Success (2xx)
Code	Name	When to Use
200	OK	Successful GET, PUT, PATCH, DELETE
201	Created	Successful POST (resource created)
204	No Content	Successful DELETE (no body returned)
Client Errors (4xx)
Code	Name	When to Use
400	Bad Request	Invalid syntax, validation error
401	Unauthorized	Missing or invalid authentication
403	Forbidden	Authenticated but not permitted
404	Not Found	Resource doesn't exist
409	Conflict	Duplicate entry, state conflict
422	Unprocessable Entity	Valid syntax but semantic errors
429	Too Many Requests	Rate limit exceeded
Server Errors (5xx)
Code	Name	When to Use
500	Internal Server Error	Unexpected server error
502	Bad Gateway	Invalid response from upstream
503	Service Unavailable	Server overloaded or down
504	Gateway Timeout	Upstream server timeout
Practical Usage
javascript


// Success responses
res.status(200).json({ data: users });           // GET success
res.status(201).json({ data: newUser });         // POST success
res.status(204).send();                          // DELETE success
// Client error responses
res.status(400).json({ message: 'Invalid data' });
res.status(401).json({ message: 'Authentication required' });
res.status(403).json({ message: 'Access denied' });
res.status(404).json({ message: 'User not found' });
res.status(409).json({ message: 'Email already exists' });
// Server error responses
res.status(500).json({ message: 'Internal server error' });
14. API Testing with Postman
Postman is a popular tool for testing and documenting APIs.

Key Features
Send HTTP requests (GET, POST, PUT, DELETE, etc.)
Set headers and authentication
Send request bodies (JSON, form data, files)
View responses
Create collections and environments
Automate testing
Basic Workflow
Create Request: Select method, enter URL
Add Headers: Content-Type, Authorization
Add Body: For POST/PUT/PATCH requests
Send Request: Click Send
Inspect Response: Check status, body, headers
Example Requests
GET Request


Method: GET
URL: [localhost](http://localhost:3000/api/users)
Headers:
  Authorization: Bearer <your_token>
POST Request


Method: POST
URL: [localhost](http://localhost:3000/api/users)
Headers:
  Content-Type: application/json
  Authorization: Bearer <your_token>
Body (raw JSON):
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "securepassword123"
}
Environment Variables
Store reusable values:



Variable: base_url
Value: [localhost](http://localhost:3000/api)
Variable: token
Value: eyJhbGciOiJIUzI1NiIs...
Usage in requests:
URL: {{base_url}}/users
Header: Bearer {{token}}
Testing Scripts
Postman allows JavaScript tests:

javascript


// Test status code
pm.test("Status code is 200", function () {
  pm.response.to.have.status(200);
});
// Test response structure
pm.test("Response has data", function () {
  const jsonData = pm.response.json();
  pm.expect(jsonData).to.have.property('success', true);
  pm.expect(jsonData).to.have.property('data');
});
// Save value to environment
const jsonData = pm.response.json();
pm.environment.set("userId", jsonData.data._id);
15. MongoDB Fundamentals
MongoDB is a NoSQL document database that stores data in flexible, JSON-like documents.

SQL vs MongoDB Terminology
SQL	MongoDB
Database	Database
Table	Collection
Row	Document
Column	Field
Primary Key	_id
Index	Index
Document Structure
MongoDB stores data as BSON (Binary JSON):

json


{
  "_id": ObjectId("507f1f77bcf86cd799439011"),
  "name": "John Doe",
  "email": "john@example.com",
  "age": 28,
  "address": {
    "city": "New York",
    "zip": "10001"
  },
  "hobbies": ["reading", "gaming", "coding"],
  "createdAt": ISODate("2024-01-15T10:30:00Z")
}
Key Features
Feature	Description
Flexible Schema	Documents in a collection can have different fields
Nested Documents	Embed related data within documents
Arrays	Store lists of values or documents
Scalability	Horizontal scaling through sharding
Rich Queries	Powerful query language with aggregation
Data Types
Type	Example
String	"Hello World"
Number	42, 3.14
Boolean	true, false
Array	["a", "b", "c"]
Object	{ "key": "value" }
Date	ISODate("2024-01-15")
ObjectId	ObjectId("...")
Null	null
When to Use MongoDB
Good for:

Rapid prototyping
Applications with varying data structures
Real-time analytics
Content management
Catalog/inventory systems
Mobile applications
Consider alternatives when:

Complex transactions required
Strong relationships between data
ACID compliance critical
16. MongoDB Atlas Setup
MongoDB Atlas is a fully managed cloud database service.

Setup Steps
Create Account
Go to 
mongodb.com
Sign up for free
Create Cluster
Click "Build a Cluster"
Choose free tier (M0)
Select cloud provider and region
Name your cluster
Create Database User
Go to Security → Database Access
Add new user
Set username and password
Choose appropriate permissions
Configure Network Access
Go to Security → Network Access
Add IP Address
For development: Allow from anywhere (0.0.0.0/0)
For production: Whitelist specific IPs
Get Connection String
Click "Connect"
Choose "Connect your application"
Copy connection string
Connection String Format


mongodb+srv://<username>:<password>@<cluster>.mongodb.net/<database>?retryWrites=true&w=majority
Replace:

<username> — Your database username
<password> — Your database password
<cluster> — Your cluster name
<database> — Your database name
Store Securely
In .env file:

env


MONGO_URI=mongodb+srv://myuser:mypassword@cluster0.abc123.mongodb.net/myapp?retryWrites=true&w=majority
17. Mongoose ODM
Mongoose is an Object Data Modeling (ODM) library for MongoDB and Node.js.

Why Mongoose?
Feature	Benefit
Schema Definition	Enforce structure on documents
Validation	Built-in and custom validators
Type Casting	Automatic type conversion
Middleware	Pre/post hooks for operations
Query Building	Chainable query API
Plugins	Extend functionality
Installation
bash


npm install mongoose
Basic Connection
javascript


const mongoose = require('mongoose');
// Simple connection
mongoose.connect(process.env.MONGO_URI)
  .then(() => console.log('MongoDB connected'))
  .catch(err => console.error('Connection error:', err));
Connection with Options
javascript


const mongoose = require('mongoose');
const connectDB = async () => {
  try {
    const conn = await mongoose.connect(process.env.MONGO_URI, {
      // Options are mostly defaults in Mongoose 6+
    });
    
    console.log(`MongoDB Connected: ${conn.connection.host}`);
  } catch (error) {
    console.error(`Error: ${error.message}`);
    process.exit(1);
  }
};
module.exports = connectDB;
Using in app.js
javascript


const express = require('express');
const connectDB = require('./config/db');
require('dotenv').config();
const app = express();
// Connect to database
connectDB();
// ... rest of app setup
Connection Events
javascript


mongoose.connection.on('connected', () => {
  console.log('Mongoose connected to DB');
});
mongoose.connection.on('error', (err) => {
  console.log('Mongoose connection error:', err);
});
mongoose.connection.on('disconnected', () => {
  console.log('Mongoose disconnected');
});
// Graceful shutdown
process.on('SIGINT', async () => {
  await mongoose.connection.close();
  process.exit(0);
});
18. Schema & Models
Schemas define the structure of documents. Models are constructors compiled from schemas.

Basic Schema
javascript


const mongoose = require('mongoose');
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  age: Number,
  isActive: Boolean
});
const User = mongoose.model('User', userSchema);
module.exports = User;
Schema with Validation
javascript


const mongoose = require('mongoose');
const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: [true, 'Name is required'],
    trim: true,
    minlength: [2, 'Name must be at least 2 characters'],
    maxlength: [50, 'Name cannot exceed 50 characters']
  },
  email: {
    type: String,
    required: [true, 'Email is required'],
    unique: true,
    lowercase: true,
    trim: true,
    match: [/^\S+@\S+\.\S+$/, 'Please provide a valid email']
  },
  password: {
    type: String,
    required: [true, 'Password is required'],
    minlength: [8, 'Password must be at least 8 characters'],
    select: false  // Don't include in queries by default
  },
  role: {
    type: String,
    enum: ['user', 'admin', 'moderator'],
    default: 'user'
  },
  age: {
    type: Number,
    min: [0, 'Age cannot be negative'],
    max: [150, 'Age seems unrealistic']
  },
  profilePicture: {
    type: String,
    default: 'default-avatar.png'
  },
  isVerified: {
    type: Boolean,
    default: false
  },
  createdAt: {
    type: Date,
    default: Date.now
  }
});
const User = mongoose.model('User', userSchema);
module.exports = User;
Schema Types
Type	Description
String	Text data
Number	Numeric data
Date	Date/time
Boolean	true/false
ObjectId	MongoDB ObjectId
Array	Array of any type
Mixed	Any type (flexible)
Buffer	Binary data
Common Schema Options
Option	Purpose
required	Field must have value
default	Default value if not provided
unique	Must be unique in collection
enum	Value must be in specified list
min/max	Numeric/date range
minlength/maxlength	String length limits
trim	Remove whitespace
lowercase/uppercase	Transform case
select	Include in query results by default
Nested Schema
javascript


const addressSchema = new mongoose.Schema({
  street: String,
  city: String,
  state: String,
  zipCode: String,
  country: { type: String, default: 'USA' }
});
const userSchema = new mongoose.Schema({
  name: String,
  address: addressSchema,
  // Or inline:
  contact: {
    phone: String,
    website: String
  }
});
Schema with References
javascript


const postSchema = new mongoose.Schema({
  title: String,
  content: String,
  author: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User',
    required: true
  },
  tags: [String],
  comments: [{
    type: mongoose.Schema.Types.ObjectId,
    ref: 'Comment'
  }]
});
Virtual Properties
Computed properties not stored in database:

javascript


userSchema.virtual('fullName').get(function() {
  return `${this.firstName} ${this.lastName}`;
});
// Include virtuals in JSON
userSchema.set('toJSON', { virtuals: true });
Schema Methods
javascript


// Instance method
userSchema.methods.isPasswordCorrect = async function(password) {
  return await bcrypt.compare(password, this.password);
};
// Usage: user.isPasswordCorrect('password123')
// Static method
userSchema.statics.findByEmail = function(email) {
  return this.findOne({ email });
};
// Usage: User.findByEmail('john@example.com')
Middleware (Hooks)
javascript


// Pre-save hook
userSchema.pre('save', async function(next) {
  if (!this.isModified('password')) return next();
  this.password = await bcrypt.hash(this.password, 10);
  next();
});
// Post-save hook
userSchema.post('save', function(doc) {
  console.log('User saved:', doc._id);
});
19. CRUD Operations
CRUD: Create, Read, Update, Delete—the four basic database operations.

Create Operations
javascript


// Create single document
const user = await User.create({
  name: 'John Doe',
  email: 'john@example.com',
  password: 'hashedpassword'
});
// Alternative: instantiate and save
const user = new User({
  name: 'Jane Doe',
  email: 'jane@example.com'
});
await user.save();
// Create multiple documents
const users = await User.insertMany([
  { name: 'User 1', email: 'user1@example.com' },
  { name: 'User 2', email: 'user2@example.com' }
]);
Read Operations
javascript


// Find all documents
const users = await User.find();
// Find with conditions
const activeUsers = await User.find({ isActive: true });
// Find one document
const user = await User.findOne({ email: 'john@example.com' });
// Find by ID
const user = await User.findById('507f1f77bcf86cd799439011');
// Query with operators
const users = await User.find({
  age: { $gte: 18, $lte: 65 },     // Between 18 and 65
  role: { $in: ['admin', 'moderator'] },  // In array
  name: { $regex: /john/i }         // Pattern match
});
// Select specific fields
const users = await User.find().select('name email -_id');
// Sort results
const users = await User.find().sort({ createdAt: -1 });  // Descending
const users = await User.find().sort('name');              // Ascending
// Limit and skip (pagination)
const users = await User.find()
  .skip(10)    // Skip first 10
  .limit(5);   // Get next 5
// Populate references
const posts = await Post.find()
  .populate('author', 'name email')
  .populate('comments');
// Count documents
const count = await User.countDocuments({ isActive: true });
// Check if exists
const exists = await User.exists({ email: 'john@example.com' });
Update Operations
javascript


// Update one document
const result = await User.updateOne(
  { email: 'john@example.com' },  // Filter
  { $set: { isActive: true } }     // Update
);
// Update and return document
const user = await User.findOneAndUpdate(
  { email: 'john@example.com' },
  { $set: { name: 'Jonathan Doe' } },
  { new: true, runValidators: true }  // Return updated doc
);
// Find by ID and update
const user = await User.findByIdAndUpdate(
  '507f1f77bcf86cd799439011',
  { $set: { role: 'admin' } },
  { new: true }
);
// Update many documents
const result = await User.updateMany(
  { isVerified: false },
  { $set: { isActive: false } }
);
// Update operators
await User.updateOne(
  { _id: userId },
  {
    $set: { name: 'New Name' },      // Set value
    $unset: { tempField: '' },       // Remove field
    $inc: { loginCount: 1 },         // Increment
    $push: { tags: 'new-tag' },      // Add to array
    $pull: { tags: 'old-tag' },      // Remove from array
    $addToSet: { tags: 'unique-tag' } // Add if not exists
  }
);
Delete Operations
javascript


// Delete one document
const result = await User.deleteOne({ email: 'john@example.com' });
// Delete and return document
const user = await User.findOneAndDelete({ email: 'john@example.com' });
// Find by ID and delete
const user = await User.findByIdAndDelete('507f1f77bcf86cd799439011');
// Delete many documents
const result = await User.deleteMany({ isActive: false });
Query Operators Reference
Operator	Description	Example
$eq	Equal	{ age: { $eq: 25 } }
$ne	Not equal	{ status: { $ne: 'deleted' } }
$gt	Greater than	{ age: { $gt: 18 } }
$gte	Greater than or equal	{ age: { $gte: 18 } }
$lt	Less than	{ age: { $lt: 65 } }
$lte	Less than or equal	{ age: { $lte: 65 } }
$in	In array	{ role: { $in: ['admin', 'mod'] } }
$nin	Not in array	{ role: { $nin: ['banned'] } }
$and	Logical AND	{ $and: [{...}, {...}] }
$or	Logical OR	{ $or: [{...}, {...}] }
$not	Logical NOT	{ age: { $not: { $gt: 18 } } }
$exists	Field exists	{ email: { $exists: true } }
$regex	Pattern match	{ name: { $regex: /^J/i } }
20. MVC Architecture
MVC (Model-View-Controller) separates concerns for cleaner, maintainable code.

Components
Component	Responsibility
Model	Data structure, database operations, business rules
View	Presentation layer (HTML/JSON responses)
Controller	Request handling, orchestration between Model and View
Request Flow


Request → Router → Controller → Model → Database
                      ↓
Response ← View ← Controller
Folder Structure


src/
├── config/
│   └── db.js
├── controllers/
│   └── userController.js
├── middleware/
│   ├── auth.js
│   └── errorHandler.js
├── models/
│   └── User.js
├── routes/
│   └── userRoutes.js
├── services/
│   └── emailService.js
├── utils/
│   └── helpers.js
├── validators/
│   └── userValidator.js
└── app.js
Implementation Example
Model (models/User.js)
javascript


const mongoose = require('mongoose');
const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: [true, 'Name is required'],
    trim: true
  },
  email: {
    type: String,
    required: [true, 'Email is required'],
    unique: true,
    lowercase: true
  },
  password: {
    type: String,
    required: [true, 'Password is required'],
    select: false
  },
  role: {
    type: String,
    enum: ['user', 'admin'],
    default: 'user'
  }
}, {
  timestamps: true
});
module.exports = mongoose.model('User', userSchema);
Controller (controllers/userController.js)
javascript


const User = require('../models/User');
// Get all users
exports.getAllUsers = async (req, res, next) => {
  try {
    const users = await User.find();
    
    res.status(200).json({
      success: true,
      count: users.length,
      data: users
    });
  } catch (error) {
    next(error);
  }
};
// Get single user
exports.getUser = async (req, res, next) => {
  try {
    const user = await User.findById(req.params.id);
    
    if (!user) {
      return res.status(404).json({
        success: false,
        message: 'User not found'
      });
    }
    
    res.status(200).json({
      success: true,
      data: user
    });
  } catch (error) {
    next(error);
  }
};
// Create user
exports.createUser = async (req, res, next) => {
  try {
    const user = await User.create(req.body);
    
    res.status(201).json({
      success: true,
      data: user
    });
  } catch (error) {
    next(error);
  }
};
// Update user
exports.updateUser = async (req, res, next) => {
  try {
    const user = await User.findByIdAndUpdate(
      req.params.id,
      req.body,
      { new: true, runValidators: true }
    );
    
    if (!user) {
      return res.status(404).json({
        success: false,
        message: 'User not found'
      });
    }
    
    res.status(200).json({
      success: true,
      data: user
    });
  } catch (error) {
    next(error);
  }
};
// Delete user
exports.deleteUser = async (req, res, next) => {
  try {
    const user = await User.findByIdAndDelete(req.params.id);
    
    if (!user) {
      return res.status(404).json({
        success: false,
        message: 'User not found'
      });
    }
    
    res.status(204).send();
  } catch (error) {
    next(error);
  }
};
Routes (routes/userRoutes.js)
javascript


const express = require('express');
const router = express.Router();
const {
  getAllUsers,
  getUser,
  createUser,
  updateUser,
  deleteUser
} = require('../controllers/userController');
router.route('/')
  .get(getAllUsers)
  .post(createUser);
router.route('/:id')
  .get(getUser)
  .put(updateUser)
  .delete(deleteUser);
module.exports = router;
App (app.js)
javascript


const express = require('express');
const connectDB = require('./config/db');
const userRoutes = require('./routes/userRoutes');
const errorHandler = require('./middleware/errorHandler');
require('dotenv').config();
const app = express();
// Connect to database
connectDB();
// Middleware
app.use(express.json());
// Routes
app.use('/api/users', userRoutes);
// Error handler (must be last)
app.use(errorHandler);
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
21. Authentication Concepts
Authentication verifies a user's identity—confirming they are who they claim to be.

Authentication vs Authorization
Concept	Question	Example
Authentication	Who are you?	Login with credentials
Authorization	What can you do?	Admin vs regular user
Common Authentication Methods
Method	Description	Use Case
Session-based	Server stores session data	Traditional web apps
Token-based (JWT)	Stateless tokens	APIs, SPAs, mobile
OAuth	Third-party authentication	"Login with Google"
API Keys	Simple key-based access	Server-to-server
Authentication Flow (JWT)


1. User submits credentials (email + password)
2. Server validates credentials
3. Server generates JWT token
4. Token sent to client
5. Client stores token (localStorage/cookie)
6. Client sends token with future requests
7. Server verifies token on each request


┌──────────┐                           ┌──────────┐
│  Client  │                           │  Server  │
└────┬─────┘                           └────┬─────┘
     │                                      │
     │  1. POST /login {email, password}    │
     │ ─────────────────────────────────────>│
     │                                      │
     │  2. Validate credentials             │
     │                                      │
     │  3. Generate JWT                     │
     │                                      │
     │  4. {token: "eyJ..."}                │
     │ <─────────────────────────────────────│
     │                                      │
     │  5. Store token                      │
     │                                      │
     │  6. GET /profile                     │
     │     Authorization: Bearer eyJ...     │
     │ ─────────────────────────────────────>│
     │                                      │
     │  7. Verify token                     │
     │                                      │
     │  8. {user data}                      │
     │ <─────────────────────────────────────│
22. Password Hashing with Bcrypt
Never store passwords in plain text. Hashing converts passwords to irreversible strings.

Why Hash Passwords?
Risk	Impact of Plain Text
Database breach	All passwords exposed
Insider threat	Staff can see passwords
Password reuse	Compromises other accounts
Hashing vs Encryption
Aspect	Hashing	Encryption
Reversible	No	Yes
Purpose	Verify data	Protect data
Key required	No	Yes
Use case	Passwords	Sensitive data
Installation
bash


npm install bcrypt
Hashing a Password
javascript


const bcrypt = require('bcrypt');
// Hash a password
const hashPassword = async (plainPassword) => {
  const saltRounds = 10;  // Cost factor
  const hashedPassword = await bcrypt.hash(plainPassword, saltRounds);
  return hashedPassword;
};
// Example
const hashed = await hashPassword('mypassword123');
// Returns: $2b$10$N9qo8uLOickgx2ZMRZoMy...
Comparing Passwords
javascript


const bcrypt = require('bcrypt');
const verifyPassword = async (plainPassword, hashedPassword) => {
  const isMatch = await bcrypt.compare(plainPassword, hashedPassword);
  return isMatch;
};
// Example
const isValid = await verifyPassword('mypassword123', user.password);
if (isValid) {
  // Password correct
}
Integration with Mongoose
javascript


const mongoose = require('mongoose');
const bcrypt = require('bcrypt');
const userSchema = new mongoose.Schema({
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true, select: false }
});
// Hash password before saving
userSchema.pre('save', async function(next) {
  // Only hash if password was modified
  if (!this.isModified('password')) return next();
  
  this.password = await bcrypt.hash(this.password, 10);
  next();
});
// Method to check password
userSchema.methods.comparePassword = async function(candidatePassword) {
  return await bcrypt.compare(candidatePassword, this.password);
};
module.exports = mongoose.model('User', userSchema);
Salt Rounds
The cost factor determines hashing complexity:

Salt Rounds	Approximate Time
10	~100ms
11	~200ms
12	~400ms
13	~800ms
Higher = more secure but slower. 10-12 is typical for most applications.

23. JWT Authentication
JWT (JSON Web Token) is a compact, self-contained token format for secure transmission of information.

JWT Structure
A JWT consists of three parts separated by dots:



header.payload.signature
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
Part	Purpose	Encoded From
Header	Token type & algorithm	{"alg": "HS256", "typ": "JWT"}
Payload	User data (claims)	{"userId": "123", "role": "admin"}
Signature	Verifies authenticity	HMAC of header + payload + secret
Installation
bash


npm install jsonwebtoken
Generating Tokens
javascript


const jwt = require('jsonwebtoken');
// Generate token
const generateToken = (user) => {
  const payload = {
    id: user._id,
    email: user.email,
    role: user.role
  };
  
  const token = jwt.sign(
    payload,
    process.env.JWT_SECRET,
    { expiresIn: '7d' }  // Token expires in 7 days
  );
  
  return token;
};
Verifying Tokens
javascript


const jwt = require('jsonwebtoken');
const verifyToken = (token) => {
  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    return decoded;
  } catch (error) {
    if (error.name === 'TokenExpiredError') {
      throw new Error('Token expired');
    }
    throw new Error('Invalid token');
  }
};
Authentication Middleware
javascript


const jwt = require('jsonwebtoken');
const User = require('../models/User');
const protect = async (req, res, next) => {
  try {
    // Get token from header
    let token;
    
    if (req.headers.authorization?.startsWith('Bearer')) {
      token = req.headers.authorization.split(' ')[1];
    }
    
    if (!token) {
      return res.status(401).json({
        success: false,
        message: 'Not authorized, no token'
      });
    }
    
    // Verify token
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    
    // Get user from token
    const user = await User.findById(decoded.id);
    
    if (!user) {
      return res.status(401).json({
        success: false,
        message: 'User not found'
      });
    }
    
    // Attach user to request
    req.user = user;
    next();
  } catch (error) {
    return res.status(401).json({
      success: false,
      message: 'Not authorized, token failed'
    });
  }
};
module.exports = protect;
Complete Auth Controller
javascript


const User = require('../models/User');
const jwt = require('jsonwebtoken');
const generateToken = (id) => {
  return jwt.sign({ id }, process.env.JWT_SECRET, {
    expiresIn: '30d'
  });
};
// Register user
exports.register = async (req, res) => {
  try {
    const { name, email, password } = req.body;
    
    // Check if user exists
    const userExists = await User.findOne({ email });
    if (userExists) {
      return res.status(400).json({
        success: false,
        message: 'Email already registered'
      });
    }
    
    // Create user (password hashed by pre-save hook)
    const user = await User.create({ name, email, password });
    
    // Generate token
    const token = generateToken(user._id);
    
    res.status(201).json({
      success: true,
      data: {
        _id: user._id,
        name: user.name,
        email: user.email,
        token
      }
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message
    });
  }
};
// Login user
exports.login = async (req, res) => {
  try {
    const { email, password } = req.body;
    
    // Validate input
    if (!email || !password) {
      return res.status(400).json({
        success: false,
        message: 'Please provide email and password'
      });
    }
    
    // Find user and include password
    const user = await User.findOne({ email }).select('+password');
    
    if (!user) {
      return res.status(401).json({
        success: false,
        message: 'Invalid credentials'
      });
    }
    
    // Check password
    const isMatch = await user.comparePassword(password);
    
    if (!isMatch) {
      return res.status(401).json({
        success: false,
        message: 'Invalid credentials'
      });
    }
    
    // Generate token
    const token = generateToken(user._id);
    
    res.json({
      success: true,
      data: {
        _id: user._id,
        name: user.name,
        email: user.email,
        token
      }
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message
    });
  }
};
// Get current user
exports.getMe = async (req, res) => {
  res.json({
    success: true,
    data: req.user
  });
};
Using Protected Routes
javascript


const express = require('express');
const router = express.Router();
const { register, login, getMe } = require('../controllers/authController');
const protect = require('../middleware/auth');
router.post('/register', register);
router.post('/login', login);
router.get('/me', protect, getMe);  // Protected route
module.exports = router;
24. Cookies & Cookie Parser
Cookies store small pieces of data in the browser, commonly used for sessions and tokens.

Installation
bash


npm install cookie-parser
Setup
javascript


const express = require('express');
const cookieParser = require('cookie-parser');
const app = express();
app.use(cookieParser());
Setting Cookies
javascript


// Basic cookie
res.cookie('name', 'value');
// Cookie with options
res.cookie('token', jwtToken, {
  httpOnly: true,      // Not accessible via JavaScript
  secure: true,        // HTTPS only
  sameSite: 'strict',  // CSRF protection
  maxAge: 7 * 24 * 60 * 60 * 1000,  // 7 days in milliseconds
  path: '/'            // Available on all routes
});
Cookie Options Explained
Option	Purpose	Recommended
httpOnly	Prevents JS access	true for auth tokens
secure	HTTPS only	true in production
sameSite	CSRF protection	'strict' or 'lax'
maxAge	Expiration time	Set appropriately
domain	Cookie domain	Usually default
path	Cookie path	Usually '/'
Reading Cookies
javascript


// Access all cookies
const cookies = req.cookies;
// Access specific cookie
const token = req.cookies.token;
Clearing Cookies
javascript


// Clear a cookie
res.clearCookie('token');
// Or set with past expiration
res.cookie('token', '', { maxAge: 0 });
JWT with Cookies Example
javascript


// Login - set cookie
exports.login = async (req, res) => {
  // ... validate user ...
  
  const token = generateToken(user._id);
  
  res.cookie('jwt', token, {
    httpOnly: true,
    secure: process.env.NODE_ENV === 'production',
    sameSite: 'strict',
    maxAge: 30 * 24 * 60 * 60 * 1000  // 30 days
  });
  
  res.json({ success: true, data: user });
};
// Logout - clear cookie
exports.logout = (req, res) => {
  res.clearCookie('jwt');
  res.json({ success: true, message: 'Logged out' });
};
// Auth middleware - read from cookie
const protect = async (req, res, next) => {
  const token = req.cookies.jwt;
  
  if (!token) {
    return res.status(401).json({ message: 'Not authorized' });
  }
  
  // ... verify token ...
};
25. Authorization & Role-Based Access
Authorization determines what actions an authenticated user can perform.

Role-Based Access Control (RBAC)
Define roles with specific permissions:

Role	Permissions
User	Read own data, update profile
Moderator	User permissions + moderate content
Admin	Full access to everything
User Model with Role
javascript


const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  password: String,
  role: {
    type: String,
    enum: ['user', 'moderator', 'admin'],
    default: 'user'
  }
});
Authorization Middleware
javascript


// Restrict to specific roles
const authorize = (...roles) => {
  return (req, res, next) => {
    if (!roles.includes(req.user.role)) {
      return res.status(403).json({
        success: false,
        message: 'Not authorized to access this route'
      });
    }
    next();
  };
};
module.exports = authorize;
Using Authorization
javascript


const protect = require('../middleware/auth');
const authorize = require('../middleware/authorize');
// Only authenticated users
router.get('/profile', protect, getProfile);
// Only admins
router.delete('/users/:id', protect, authorize('admin'), deleteUser);
// Admins and moderators
router.put('/posts/:id', protect, authorize('admin', 'moderator'), updatePost);
Resource Ownership
Check if user owns the resource:

javascript


exports.updatePost = async (req, res) => {
  const post = await Post.findById(req.params.id);
  
  // Check ownership (unless admin)
  if (post.author.toString() !== req.user._id.toString() && req.user.role !== 'admin') {
    return res.status(403).json({
      success: false,
      message: 'Not authorized to update this post'
    });
  }
  
  // Proceed with update...
};
Combined Middleware Example
javascript


// Protect route + check ownership
const checkOwnership = (Model, resourceName = 'Resource') => {
  return async (req, res, next) => {
    const resource = await Model.findById(req.params.id);
    
    if (!resource) {
      return res.status(404).json({
        success: false,
        message: `${resourceName} not found`
      });
    }
    
    // Check if user owns resource or is admin
    const isOwner = resource.user?.toString() === req.user._id.toString();
    const isAdmin = req.user.role === 'admin';
    
    if (!isOwner && !isAdmin) {
      return res.status(403).json({
        success: false,
        message: 'Not authorized'
      });
    }
    
    req.resource = resource;
    next();
  };
};
// Usage
router.put(
  '/posts/:id',
  protect,
  checkOwnership(Post, 'Post'),
  updatePost
);
26. File Uploads & Cloud Storage
Handle file uploads and store them securely in the cloud.

Why Cloud Storage?
Local Storage	Cloud Storage
Limited disk space	Virtually unlimited
Single server	Global CDN
No backup	Automatic redundancy
Slow delivery	Fast delivery
Popular Cloud Storage Services
AWS S3 — Industry standard
Cloudinary — Image/video focused
ImageKit — Optimized for images
Firebase Storage — Google's solution
DigitalOcean Spaces — S3-compatible
File Upload Flow


1. Client sends file in request
2. Server receives file (multer)
3. Server uploads to cloud storage
4. Cloud returns URL
5. Server saves URL to database
6. Client uses URL to display file
Multer for File Handling
Installation:

bash


npm install multer
Basic setup:

javascript


const multer = require('multer');
// Memory storage (for cloud upload)
const storage = multer.memoryStorage();
// File filter
const fileFilter = (req, file, cb) => {
  if (file.mimetype.startsWith('image/')) {
    cb(null, true);
  } else {
    cb(new Error('Only images allowed'), false);
  }
};
const upload = multer({
  storage,
  fileFilter,
  limits: {
    fileSize: 5 * 1024 * 1024  // 5MB limit
  }
});
module.exports = upload;
Cloudinary Integration Example
Installation:

bash


npm install cloudinary
Configuration:

javascript


// config/cloudinary.js
const cloudinary = require('cloudinary').v2;
cloudinary.config({
  cloud_name: process.env.CLOUDINARY_CLOUD_NAME,
  api_key: process.env.CLOUDINARY_API_KEY,
  api_secret: process.env.CLOUDINARY_API_SECRET
});
module.exports = cloudinary;
Upload helper:

javascript


const cloudinary = require('../config/cloudinary');
const uploadToCloudinary = async (fileBuffer, folder = 'uploads') => {
  return new Promise((resolve, reject) => {
    cloudinary.uploader.upload_stream(
      { folder },
      (error, result) => {
        if (error) reject(error);
        else resolve(result);
      }
    ).end(fileBuffer);
  });
};
module.exports = uploadToCloudinary;
Upload Route
javascript


const express = require('express');
const router = express.Router();
const upload = require('../middleware/upload');
const uploadToCloudinary = require('../utils/cloudinary');
router.post('/upload', upload.single('image'), async (req, res) => {
  try {
    if (!req.file) {
      return res.status(400).json({ message: 'No file uploaded' });
    }
    
    const result = await uploadToCloudinary(req.file.buffer, 'avatars');
    
    res.json({
      success: true,
      data: {
        url: result.secure_url,
        publicId: result.public_id
      }
    });
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
});
module.exports = router;
Frontend Upload Example
html


<form id="uploadForm" enctype="multipart/form-data">
  <input type="file" name="image" accept="image/*">
  <button type="submit">Upload</button>
</form>
<script>
document.getElementById('uploadForm').addEventListener('submit', async (e) => {
  e.preventDefault();
  
  const formData = new FormData(e.target);
  
  const response = await fetch('/api/upload', {
    method: 'POST',
    body: formData
  });
  
  const data = await response.json();
  console.log(data.url);
});
</script>
27. Environment Variables
Environment variables store configuration that changes between environments.

Why Use Them?
Hard-coded Values	Environment Variables
Exposed in code	Kept secret
Same in all environments	Different per environment
Requires code changes	No code changes needed
Security risk	Secure
Setup with dotenv
Installation:

bash


npm install dotenv
Create .env file:

env


# Server
NODE_ENV=development
PORT=3000
# Database
MONGO_URI=mongodb+srv://user:pass@cluster.mongodb.net/mydb
# JWT
JWT_SECRET=your-super-secret-key-here
JWT_EXPIRE=30d
# Cloud Storage
CLOUDINARY_CLOUD_NAME=your-cloud-name
CLOUDINARY_API_KEY=your-api-key
CLOUDINARY_API_SECRET=your-api-secret
# Email
SMTP_HOST=smtp.example.com
SMTP_PORT=587
SMTP_USER=your-email@example.com
SMTP_PASS=your-password
Load in application:

javascript


// At the very top of entry file
require('dotenv').config();
// Now access variables
const port = process.env.PORT || 3000;
const mongoUri = process.env.MONGO_URI;
const jwtSecret = process.env.JWT_SECRET;
Environment-Specific Configuration
javascript


// config/index.js
require('dotenv').config();
const config = {
  development: {
    db: process.env.MONGO_URI_DEV,
    logLevel: 'debug'
  },
  production: {
    db: process.env.MONGO_URI_PROD,
    logLevel: 'error'
  },
  test: {
    db: process.env.MONGO_URI_TEST,
    logLevel: 'silent'
  }
};
module.exports = config[process.env.NODE_ENV || 'development'];
Security Rules
Never commit .env — Add to .gitignore
Use strong secrets — Generate random strings
Different values per environment — Dev, staging, production
Validate required variables — Check at startup
Validation Example
javascript


// config/validateEnv.js
const requiredEnvVars = [
  'NODE_ENV',
  'PORT',
  'MONGO_URI',
  'JWT_SECRET'
];
const validateEnv = () => {
  const missing = requiredEnvVars.filter(varName => !process.env[varName]);
  
  if (missing.length > 0) {
    throw new Error(`Missing environment variables: ${missing.join(', ')}`);
  }
};
module.exports = validateEnv;
// In app.js
require('dotenv').config();
require('./config/validateEnv')();
.gitignore Example
gitignore


# Environment variables
.env
.env.local
.env.*.local
# Dependencies
node_modules/
# Logs
*.log
npm-debug.log*
# Build output
dist/
build/
# IDE
.vscode/
.idea/
# OS
.DS_Store
Thumbs.db
28. Input Validation
Validation ensures incoming data meets expected formats before processing.

Why Validate?
Prevent invalid data in database
Protect against injection attacks
Provide helpful error messages
Improve application reliability
express-validator
Installation:

bash


npm install express-validator
Basic Validation
javascript


const { body, param, query, validationResult } = require('express-validator');
// Validation rules
const userValidationRules = [
  body('name')
    .trim()
    .notEmpty().withMessage('Name is required')
    .isLength({ min: 2, max: 50 }).withMessage('Name must be 2-50 characters'),
  
  body('email')
    .trim()
    .notEmpty().withMessage('Email is required')
    .isEmail().withMessage('Invalid email format')
    .normalizeEmail(),
  
  body('password')
    .notEmpty().withMessage('Password is required')
    .isLength({ min: 8 }).withMessage('Password must be at least 8 characters')
    .matches(/\d/).withMessage('Password must contain a number'),
  
  body('age')
    .optional()
    .isInt({ min: 0, max: 150 }).withMessage('Age must be 0-150')
];
Validation Middleware
javascript


const validate = (req, res, next) => {
  const errors = validationResult(req);
  
  if (!errors.isEmpty()) {
    return res.status(400).json({
      success: false,
      errors: errors.array().map(err => ({
        field: err.path,
        message: err.msg
      }))
    });
  }
  
  next();
};
module.exports = { validate, userValidationRules };
Using in Routes
javascript


const { userValidationRules, validate } = require('../validators/userValidator');
router.post('/users', userValidationRules, validate, createUser);
Common Validators
javascript


const validators = {
  // String validators
  body('field').notEmpty()           // Not empty
  body('field').isLength({min, max}) // Length range
  body('field').trim()               // Remove whitespace
  body('field').escape()             // Escape HTML
  
  // Email & URL
  body('email').isEmail()
  body('url').isURL()
  
  // Numbers
  body('age').isInt({min: 0})
  body('price').isFloat({min: 0})
  body('quantity').isNumeric()
  
  // Arrays & Objects
  body('tags').isArray()
  body('tags.*').isString()
  body('address').isObject()
  
  // Custom validation
  body('username').custom(async (value) => {
    const user = await User.findOne({ username: value });
    if (user) {
      throw new Error('Username already taken');
    }
    return true;
  })
  
  // Sanitization
  body('field').trim()
  body('field').toLowerCase()
  body('field').toInt()
  body('field').toDate()
};
Parameter & Query Validation
javascript


// URL parameter validation
const idValidation = [
  param('id')
    .isMongoId().withMessage('Invalid ID format')
];
// Query parameter validation
const paginationValidation = [
  query('page')
    .optional()
    .isInt({ min: 1 }).withMessage('Page must be positive integer'),
  query('limit')
    .optional()
    .isInt({ min: 1, max: 100 }).withMessage('Limit must be 1-100')
];
router.get('/users/:id', idValidation, validate, getUser);
router.get('/users', paginationValidation, validate, getAllUsers);
29. Error Handling
Proper error handling makes applications robust and user-friendly.

Error Types
Type	Examples
Operational	Invalid input, auth failure, resource not found
Programming	Undefined variables, type errors, syntax errors
External	Database down, API timeout, network issues
Custom Error Class
javascript


// utils/AppError.js
class AppError extends Error {
  constructor(message, statusCode) {
    super(message);
    
    this.statusCode = statusCode;
    this.status = `${statusCode}`.startsWith('4') ? 'fail' : 'error';
    this.isOperational = true;
    
    Error.captureStackTrace(this, this.constructor);
  }
}
module.exports = AppError;
Global Error Handler
javascript


// middleware/errorHandler.js
const errorHandler = (err, req, res, next) => {
  let error = { ...err };
  error.message = err.message;
  
  // Log for debugging
  console.error('Error:', err);
  
  // Mongoose bad ObjectId
  if (err.name === 'CastError') {
    error = {
      message: 'Resource not found',
      statusCode: 404
    };
  }
  
  // Mongoose duplicate key
  if (err.code === 11000) {
    const field = Object.keys(err.keyValue)[0];
    error = {
      message: `${field} already exists`,
      statusCode: 400
    };
  }
  
  // Mongoose validation error
  if (err.name === 'ValidationError') {
    const messages = Object.values(err.errors).map(val => val.message);
    error = {
      message: messages.join(', '),
      statusCode: 400
    };
  }
  
  // JWT errors
  if (err.name === 'JsonWebTokenError') {
    error = {
      message: 'Invalid token',
      statusCode: 401
    };
  }
  
  if (err.name === 'TokenExpiredError') {
    error = {
      message: 'Token expired',
      statusCode: 401
    };
  }
  
  res.status(error.statusCode || 500).json({
    success: false,
    message: error.message || 'Server Error',
    ...(process.env.NODE_ENV === 'development' && { stack: err.stack })
  });
};
module.exports = errorHandler;
Using Custom Errors
javascript


const AppError = require('../utils/AppError');
exports.getUser = async (req, res, next) => {
  try {
    const user = await User.findById(req.params.id);
    
    if (!user) {
      return next(new AppError('User not found', 404));
    }
    
    res.json({ success: true, data: user });
  } catch (error) {
    next(error);
  }
};
Async Handler Wrapper
Eliminate try-catch boilerplate:

javascript


// utils/asyncHandler.js
const asyncHandler = (fn) => (req, res, next) => {
  Promise.resolve(fn(req, res, next)).catch(next);
};
module.exports = asyncHandler;
// Usage in controller
const asyncHandler = require('../utils/asyncHandler');
exports.getUser = asyncHandler(async (req, res, next) => {
  const user = await User.findById(req.params.id);
  
  if (!user) {
    return next(new AppError('User not found', 404));
  }
  
  res.json({ success: true, data: user });
});
404 Handler
javascript


// Handle undefined routes
app.use('*', (req, res, next) => {
  next(new AppError(`Cannot find ${req.originalUrl}`, 404));
});
// Error handler must be last
app.use(errorHandler);
30. Async/Await & Error Management
Modern JavaScript uses async/await for cleaner asynchronous code.

Callbacks vs Promises vs Async/Await
javascript


// Callback (old way)
User.find({}, (err, users) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(users);
});
// Promise (then/catch)
User.find({})
  .then(users => console.log(users))
  .catch(err => console.error(err));
// Async/Await (modern)
const getUsers = async () => {
  try {
    const users = await User.find({});
    console.log(users);
  } catch (err) {
    console.error(err);
  }
};
Try-Catch Pattern
javascript


const fetchData = async () => {
  try {
    const result = await someAsyncOperation();
    return result;
  } catch (error) {
    // Handle error
    throw error;  // Or handle gracefully
  } finally {
    // Always runs (cleanup)
  }
};
Parallel Operations
javascript


// Sequential (slower)
const user = await User.findById(userId);
const posts = await Post.find({ author: userId });
const comments = await Comment.find({ author: userId });
// Parallel (faster)
const [user, posts, comments] = await Promise.all([
  User.findById(userId),
  Post.find({ author: userId }),
  Comment.find({ author: userId })
]);
// Handle partial failures
const results = await Promise.allSettled([
  User.findById(userId),
  Post.find({ author: userId }),
  risky.operation()  // Might fail
]);
// results: [{status: 'fulfilled', value: ...}, {status: 'rejected', reason: ...}]
Error Handling Patterns
javascript


// Pattern 1: Try-catch wrapper
const asyncHandler = fn => (req, res, next) =>
  Promise.resolve(fn(req, res, next)).catch(next);
// Pattern 2: Inline try-catch
exports.createUser = async (req, res) => {
  try {
    const user = await User.create(req.body);
    res.status(201).json({ data: user });
  } catch (error) {
    res.status(400).json({ error: error.message });
  }
};
// Pattern 3: Controller with next()
exports.createUser = async (req, res, next) => {
  try {
    const user = await User.create(req.body);
    res.status(201).json({ data: user });
  } catch (error) {
    next(error);  // Pass to error handler
  }
};
31. Project Folder Structure
A well-organized structure makes projects maintainable and scalable.

Simple Structure (Small Projects)


project/
├── node_modules/
├── .env
├── .gitignore
├── package.json
├── app.js
├── routes/
│   └── index.js
└── models/
    └── User.js
Professional Structure (Medium-Large Projects)


project/
├── src/
│   ├── config/
│   │   ├── db.js             # Database connection
│   │   ├── cloudinary.js     # Cloud storage config
│   │   └── index.js          # Config aggregation
│   │
│   ├── controllers/
│   │   ├── authController.js
│   │   ├── userController.js
│   │   └── postController.js
│   │
│   ├── middleware/
│   │   ├── auth.js           # Authentication
│   │   ├── authorize.js      # Authorization
│   │   ├── errorHandler.js   # Global error handler
│   │   └── upload.js         # File upload
│   │
│   ├── models/
│   │   ├── User.js
│   │   ├── Post.js
│   │   └── Comment.js
│   │
│   ├── routes/
│   │   ├── authRoutes.js
│   │   ├── userRoutes.js
│   │   ├── postRoutes.js
│   │   └── index.js          # Route aggregation
│   │
│   ├── services/
│   │   ├── emailService.js
│   │   └── paymentService.js
│   │
│   ├── utils/
│   │   ├── AppError.js       # Custom error class
│   │   ├── asyncHandler.js   # Async wrapper
│   │   └── helpers.js        # Utility functions
│   │
│   ├── validators/
│   │   ├── authValidator.js
│   │   └── userValidator.js
│   │
│   └── app.js                # Express app setup
│
├── tests/
│   ├── auth.test.js
│   └── user.test.js
│
├── .env
├── .env.example              # Template without secrets
├── .gitignore
├── package.json
├── README.md
└── server.js                 # Entry point
File Responsibilities
Folder	Purpose
config/	Configuration and connections
controllers/	Request handlers, business logic
middleware/	Request processing functions
models/	Database schemas
routes/	URL-to-controller mapping
services/	External service integrations
utils/	Helper functions and classes
validators/	Input validation rules
tests/	Automated tests
Entry Point (server.js)
javascript


// server.js - Entry point
require('dotenv').config();
const app = require('./src/app');
const connectDB = require('./src/config/db');
const PORT = process.env.PORT || 3000;
// Connect to database then start server
connectDB().then(() => {
  app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
  });
});
App Setup (src/app.js)
javascript


// src/app.js - Express configuration
const express = require('express');
const cors = require('cors');
const helmet = require('helmet');
const morgan = require('morgan');
const routes = require('./routes');
const errorHandler = require('./middleware/errorHandler');
const AppError = require('./utils/AppError');
const app = express();
// Security
app.use(helmet());
app.use(cors());
// Logging
if (process.env.NODE_ENV === 'development') {
  app.use(morgan('dev'));
}
// Body parsing
app.use(express.json({ limit: '10kb' }));
app.use(express.urlencoded({ extended: true }));
// Routes
app.use('/api', routes);
// 404 handler
app.use('*', (req, res, next) => {
  next(new AppError(`Cannot find ${req.originalUrl}`, 404));
});
// Error handler
app.use(errorHandler);
module.exports = app;
32. Building Production-Ready APIs
Best practices for APIs that can handle real-world traffic.

API Response Format
Consistent structure for all responses:

javascript


// Success response
{
  "success": true,
  "data": { ... },
  "message": "Operation successful"  // Optional
}
// Collection response
{
  "success": true,
  "count": 50,
  "pagination": {
    "page": 1,
    "limit": 10,
    "totalPages": 5,
    "totalCount": 50
  },
  "data": [ ... ]
}
// Error response
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input",
    "details": [ ... ]  // Optional field-level errors
  }
}
Response Helper
javascript


// utils/response.js
const sendSuccess = (res, data, statusCode = 200, message = null) => {
  const response = {
    success: true,
    data
  };
  
  if (message) response.message = message;
  
  res.status(statusCode).json(response);
};
const sendError = (res, message, statusCode = 500, code = null) => {
  const response = {
    success: false,
    error: { message }
  };
  
  if (code) response.error.code = code;
  
  res.status(statusCode).json(response);
};
module.exports = { sendSuccess, sendError };
Pagination Helper
javascript


// utils/pagination.js
const paginate = async (Model, query = {}, options = {}) => {
  const page = parseInt(options.page) || 1;
  const limit = parseInt(options.limit) || 10;
  const skip = (page - 1) * limit;
  const sort = options.sort || '-createdAt';
  
  const [data, totalCount] = await Promise.all([
    Model.find(query)
      .sort(sort)
      .skip(skip)
      .limit(limit)
      .populate(options.populate || ''),
    Model.countDocuments(query)
  ]);
  
  return {
    data,
    pagination: {
      page,
      limit,
      totalPages: Math.ceil(totalCount / limit),
      totalCount
    }
  };
};
module.exports = paginate;
Controller Best Practices
javascript


const asyncHandler = require('../utils/asyncHandler');
const AppError = require('../utils/AppError');
const paginate = require('../utils/pagination');
const { sendSuccess } = require('../utils/response');
const User = require('../models/User');
exports.getAllUsers = asyncHandler(async (req, res) => {
  const { page, limit, sort, role } = req.query;
  
  const query = {};
  if (role) query.role = role;
  
  const result = await paginate(User, query, { page, limit, sort });
  
  sendSuccess(res, result.data, 200);
  res.json({
    success: true,
    count: result.data.length,
    pagination: result.pagination,
    data: result.data
  });
});
exports.getUser = asyncHandler(async (req, res, next) => {
  const user = await User.findById(req.params.id);
  
  if (!user) {
    return next(new AppError('User not found', 404));
  }
  
  sendSuccess(res, user);
});
33. Security Best Practices
Protect your application from common vulnerabilities.

Security Checklist
Category	Practice
Passwords	Hash with bcrypt, never store plain text
Authentication	Use JWT with httpOnly cookies
Secrets	Store in environment variables
Input	Validate and sanitize all input
Headers	Use Helmet for security headers
HTTPS	Always use in production
Rate Limiting	Prevent brute force attacks
Dependencies	Keep packages updated
Helmet for Security Headers
bash


npm install helmet
javascript


const helmet = require('helmet');
app.use(helmet());
// Helmet sets these headers:
// - Content-Security-Policy
// - X-DNS-Prefetch-Control
// - X-Frame-Options
// - X-Content-Type-Options
// - And more...
Data Sanitization
bash


npm install express-mongo-sanitize xss-clean
javascript


const mongoSanitize = require('express-mongo-sanitize');
const xss = require('xss-clean');
// Prevent NoSQL injection
app.use(mongoSanitize());
// Prevent XSS attacks
app.use(xss());
Parameter Pollution Prevention
bash


npm install hpp
javascript


const hpp = require('hpp');
app.use(hpp({
  whitelist: ['sort', 'filter', 'fields']  // Allow these duplicates
}));
Security Middleware Stack
javascript


const express = require('express');
const helmet = require('helmet');
const cors = require('cors');
const rateLimit = require('express-rate-limit');
const mongoSanitize = require('express-mongo-sanitize');
const xss = require('xss-clean');
const hpp = require('hpp');
const app = express();
// Security headers
app.use(helmet());
// CORS
app.use(cors({
  origin: process.env.ALLOWED_ORIGINS?.split(',') || '*',
  credentials: true
}));
// Rate limiting
const limiter = rateLimit({
  windowMs: 15 * 60 * 1000,  // 15 minutes
  max: 100,                   // 100 requests per window
  message: 'Too many requests, please try again later'
});
app.use('/api', limiter);
// Body parser with size limit
app.use(express.json({ limit: '10kb' }));
// Data sanitization
app.use(mongoSanitize());
app.use(xss());
// Parameter pollution
app.use(hpp());
34. Rate Limiting & CORS
Control access to your API.

Rate Limiting
Prevent abuse by limiting requests:

bash


npm install express-rate-limit
javascript


const rateLimit = require('express-rate-limit');
// General limiter
const generalLimiter = rateLimit({
  windowMs: 15 * 60 * 1000,  // 15 minutes
  max: 100,                   // 100 requests per IP
  standardHeaders: true,
  legacyHeaders: false,
  message: {
    success: false,
    message: 'Too many requests, please try again after 15 minutes'
  }
});
// Strict limiter for auth routes
const authLimiter = rateLimit({
  windowMs: 60 * 60 * 1000,  // 1 hour
  max: 5,                     // 5 attempts
  message: {
    success: false,
    message: 'Too many login attempts, please try again after an hour'
  }
});
// Apply limiters
app.use('/api', generalLimiter);
app.use('/api/auth/login', authLimiter);
CORS (Cross-Origin Resource Sharing)
Control which domains can access your API:

bash


npm install cors
javascript


const cors = require('cors');
// Simple: Allow all origins
app.use(cors());
// Configured: Specific origins
const corsOptions = {
  origin: function(origin, callback) {
    const allowedOrigins = [
      '[localhost](http://localhost:3000)',
      '[myapp.com](https://myapp.com)',
      '[myapp.com](https://www.myapp.com)'
    ];
    
    // Allow requests with no origin (mobile apps, Postman)
    if (!origin) return callback(null, true);
    
    if (allowedOrigins.includes(origin)) {
      callback(null, true);
    } else {
      callback(new Error('Not allowed by CORS'));
    }
  },
  credentials: true,  // Allow cookies
  methods: ['GET', 'POST', 'PUT', 'PATCH', 'DELETE'],
  allowedHeaders: ['Content-Type', 'Authorization']
};
app.use(cors(corsOptions));
Environment-Based CORS
javascript


const corsOptions = {
  origin: process.env.NODE_ENV === 'production'
    ? process.env.ALLOWED_ORIGINS.split(',')
    : '*',
  credentials: true
};
app.use(cors(corsOptions));
35. Logging & Debugging
Track what's happening in your application.

Morgan for HTTP Logging
bash


npm install morgan
javascript


const morgan = require('morgan');
// Development: colored, concise output
if (process.env.NODE_ENV === 'development') {
  app.use(morgan('dev'));
  // Output: GET /api/users 200 5.123 ms
}
// Production: detailed logging to file
if (process.env.NODE_ENV === 'production') {
  const fs = require('fs');
  const path = require('path');
  
  const accessLogStream = fs.createWriteStream(
    path.join(__dirname, 'logs', 'access.log'),
    { flags: 'a' }
  );
  
  app.use(morgan('combined', { stream: accessLogStream }));
}
Winston for Application Logging
bash


npm install winston
javascript


// utils/logger.js
const winston = require('winston');
const logger = winston.createLogger({
  level: process.env.LOG_LEVEL || 'info',
  format: winston.format.combine(
    winston.format.timestamp(),
    winston.format.errors({ stack: true }),
    winston.format.json()
  ),
  defaultMeta: { service: 'api' },
  transports: [
    // Write errors to error.log
    new winston.transports.File({
      filename: 'logs/error.log',
      level: 'error'
    }),
    // Write all logs to combined.log
    new winston.transports.File({
      filename: 'logs/combined.log'
    })
  ]
});
// Console logging in development
if (process.env.NODE_ENV !== 'production') {
  logger.add(new winston.transports.Console({
    format: winston.format.combine(
      winston.format.colorize(),
      winston.format.simple()
    )
  }));
}
module.exports = logger;
Usage:

javascript


const logger = require('./utils/logger');
logger.info('Server started', { port: 3000 });
logger.error('Database connection failed', { error: err.message });
logger.warn('Rate limit exceeded', { ip: req.ip });
logger.debug('Query executed', { query, results: results.length });
Debug Module
bash


npm install debug
javascript


const debug = require('debug')('app:server');
debug('Server starting...');
debug('Connected to database');
// Enable with: DEBUG=app:* node app.js
// Or: DEBUG=app:server,app:db node app.js
36. Testing with Jest & Supertest
Automated testing ensures code reliability.

Installation
bash


npm install jest supertest --save-dev
Package.json Setup
json


{
  "scripts": {
    "test": "NODE_ENV=test jest --coverage",
    "test:watch": "NODE_ENV=test jest --watch"
  },
  "jest": {
    "testEnvironment": "node",
    "coveragePathIgnorePatterns": ["/node_modules/"],
    "testTimeout": 10000
  }
}
Test Structure


tests/
├── setup.js           # Test configuration
├── auth.test.js       # Auth endpoint tests
├── users.test.js      # User endpoint tests
└── fixtures/
    └── users.json     # Test data
Test Setup
javascript


// tests/setup.js
const mongoose = require('mongoose');
const { MongoMemoryServer } = require('mongodb-memory-server');
let mongoServer;
beforeAll(async () => {
  mongoServer = await MongoMemoryServer.create();
  await mongoose.connect(mongoServer.getUri());
});
afterAll(async () => {
  await mongoose.disconnect();
  await mongoServer.stop();
});
afterEach(async () => {
  const collections = mongoose.connection.collections;
  for (const key in collections) {
    await collections[key].deleteMany({});
  }
});
API Tests
javascript


// tests/auth.test.js
const request = require('supertest');
const app = require('../src/app');
const User = require('../src/models/User');
describe('Auth Endpoints', () => {
  
  describe('POST /api/auth/register', () => {
    it('should register a new user', async () => {
      const res = await request(app)
        .post('/api/auth/register')
        .send({
          name: 'Test User',
          email: 'test@example.com',
          password: 'password123'
        });
      
      expect(res.statusCode).toBe(201);
      expect(res.body.success).toBe(true);
      expect(res.body.data).toHaveProperty('token');
      expect(res.body.data.email).toBe('test@example.com');
    });
    
    it('should not register with existing email', async () => {
      // Create user first
      await User.create({
        name: 'Existing',
        email: 'test@example.com',
        password: 'password123'
      });
      
      const res = await request(app)
        .post('/api/auth/register')
        .send({
          name: 'Test User',
          email: 'test@example.com',
          password: 'password123'
        });
      
      expect(res.statusCode).toBe(400);
      expect(res.body.success).toBe(false);
    });
    
    it('should require all fields', async () => {
      const res = await request(app)
        .post('/api/auth/register')
        .send({ name: 'Test' });
      
      expect(res.statusCode).toBe(400);
    });
  });
  
  describe('POST /api/auth/login', () => {
    beforeEach(async () => {
      await request(app)
        .post('/api/auth/register')
        .send({
          name: 'Test User',
          email: 'test@example.com',
          password: 'password123'
        });
    });
    
    it('should login with valid credentials', async () => {
      const res = await request(app)
        .post('/api/auth/login')
        .send({
          email: 'test@example.com',
          password: 'password123'
        });
      
      expect(res.statusCode).toBe(200);
      expect(res.body.data).toHaveProperty('token');
    });
    
    it('should reject invalid password', async () => {
      const res = await request(app)
        .post('/api/auth/login')
        .send({
          email: 'test@example.com',
          password: 'wrongpassword'
        });
      
      expect(res.statusCode).toBe(401);
    });
  });
});
Protected Route Tests
javascript


describe('GET /api/users/me', () => {
  let token;
  
  beforeEach(async () => {
    const res = await request(app)
      .post('/api/auth/register')
      .send({
        name: 'Test User',
        email: 'test@example.com',
        password: 'password123'
      });
    
    token = res.body.data.token;
  });
  
  it('should return current user', async () => {
    const res = await request(app)
      .get('/api/users/me')
      .set('Authorization', `Bearer ${token}`);
    
    expect(res.statusCode).toBe(200);
    expect(res.body.data.email).toBe('test@example.com');
  });
  
  it('should reject without token', async () => {
    const res = await request(app)
      .get('/api/users/me');
    
    expect(res.statusCode).toBe(401);
  });
});
Run Tests
bash


npm test                  # Run all tests
npm run test:watch        # Watch mode
npm test -- --coverage    # With coverage report
37. Deployment
Get your application running in production.

Pre-Deployment Checklist
 All environment variables defined
 Database connection uses production URI
 Error messages don't expose sensitive info
 Logging configured for production
 Security middleware enabled
 CORS configured correctly
 Tests passing
 README updated
Popular Hosting Platforms
Platform	Best For	Pricing
Railway	Quick deployment	Free tier + pay-as-you-go
Render	Full-stack apps	Free tier
Vercel	Serverless/Edge	Free tier
DigitalOcean	Full control	From $5/month
AWS	Enterprise scale	Pay-as-you-go
Heroku	Easy deployment	Free tier removed
Deployment with Railway
Install CLI:
bash


npm install -g @railway/cli
Login:
bash


railway login
Initialize:
bash


railway init
Deploy:
bash


railway up
Set environment variables:
bash


railway variables set NODE_ENV=production
railway variables set MONGO_URI=your_uri
railway variables set JWT_SECRET=your_secret
Deployment with Render
Connect GitHub repository
Create new Web Service
Configure:
Build Command: npm install
Start Command: npm start
Add environment variables
Deploy
Production package.json
json


{
  "name": "my-api",
  "version": "1.0.0",
  "engines": {
    "node": ">=18.0.0"
  },
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  }
}
Health Check Endpoint
javascript


app.get('/health', (req, res) => {
  res.status(200).json({
    status: 'healthy',
    timestamp: new Date().toISOString(),
    uptime: process.uptime()
  });
});
38. Git & Version Control
Essential Git commands for backend development.

Initial Setup
bash


# Initialize repository
git init
# Configure user
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
Daily Workflow
bash


# Check status
git status
# Stage changes
git add .                    # All files
git add filename.js          # Specific file
# Commit
git commit -m "Add user authentication"
# Push
git push origin main
Branching
bash


# Create and switch to new branch
git checkout -b feature/user-auth
# Switch branches
git checkout main
# Merge branch
git merge feature/user-auth
# Delete branch
git branch -d feature/user-auth
Common Commands
bash


# View history
git log --oneline
# Undo last commit (keep changes)
git reset --soft HEAD~1
# Undo changes to file
git checkout -- filename.js
# Stash changes
git stash
git stash pop
# Pull latest
git pull origin main
.gitignore
gitignore


# Dependencies
node_modules/
# Environment
.env
.env.local
.env.*.local
# Logs
logs/
*.log
npm-debug.log*
# Build
dist/
build/
# IDE
.vscode/
.idea/
# OS
.DS_Store
Thumbs.db
# Test coverage
coverage/
Commit Message Convention


type(scope): subject
Types:
- feat: New feature
- fix: Bug fix
- docs: Documentation
- style: Formatting
- refactor: Code restructuring
- test: Adding tests
- chore: Maintenance
Examples:
feat(auth): add JWT authentication
fix(users): resolve password hashing issue
docs(readme): update installation steps
39. Interview Questions
Common backend interview questions and answers.

Node.js Questions
Q: What is Node.js?

Node.js is a JavaScript runtime built on Chrome's V8 engine. It allows JavaScript to run on the server side, enabling full-stack JavaScript development.

Q: What is the event loop?

The event loop is a mechanism that allows Node.js to perform non-blocking I/O operations. It continuously checks the call stack and callback queue, executing callbacks when the stack is empty.

Q: What's the difference between require and import?

require (CommonJS)	import (ES Modules)
Synchronous	Asynchronous
Dynamic loading	Static analysis
module.exports	export
Default in Node.js	Needs "type": "module"
Express Questions
Q: What is middleware?

Middleware are functions that have access to the request and response objects. They can execute code, modify req/res, end the request-response cycle, or call the next middleware.

Q: Explain the difference between app.use() and app.get()?

app.use() — Mounts middleware for all HTTP methods
app.get() — Handles only GET requests to specific path
Database Questions
Q: SQL vs NoSQL - when to use each?

SQL	NoSQL
Structured data	Flexible schema
Complex joins	Nested documents
ACID compliance	Horizontal scaling
Relationships	Document-based
Q: What is database indexing?

Indexing creates a data structure that improves the speed of data retrieval. Like a book's index, it allows the database to find data without scanning every row.

Security Questions
Q: How do you secure an API?

Use HTTPS
Implement authentication (JWT)
Validate all input
Hash passwords
Use rate limiting
Set security headers (Helmet)
Keep dependencies updated
Q: What's the difference between authentication and authorization?

Authentication: Verifying identity (who are you?)
Authorization: Verifying permissions (what can you do?)
Architecture Questions
Q: What is MVC?

Model-View-Controller is an architectural pattern:

Model: Data and business logic
View: Presentation layer
Controller: Handles requests, coordinates Model and View
Q: What is REST?

REST (Representational State Transfer) is an architectural style for APIs using:

HTTP methods (GET, POST, PUT, DELETE)
Stateless communication
Resource-based URLs
Standard status codes
Coding Questions
Q: Write a middleware that logs request time

javascript


const requestLogger = (req, res, next) => {
  const start = Date.now();
  
  res.on('finish', () => {
    const duration = Date.now() - start;
    console.log(`${req.method} ${req.path} - ${duration}ms`);
  });
  
  next();
};
Q: Implement rate limiting from scratch

javascript


const rateLimiter = (windowMs, maxRequests) => {
  const requests = new Map();
  
  return (req, res, next) => {
    const ip = req.ip;
    const now = Date.now();
    
    if (!requests.has(ip)) {
      requests.set(ip, { count: 1, start: now });
      return next();
    }
    
    const record = requests.get(ip);
    
    if (now - record.start > windowMs) {
      requests.set(ip, { count: 1, start: now });
      return next();
    }
    
    if (record.count >= maxRequests) {
      return res.status(429).json({ message: 'Too many requests' });
    }
    
    record.count++;
    next();
  };
};
40. Learning Roadmap
Progressive path from beginner to advanced.

Beginner (1-2 months)
Focus Areas:

JavaScript fundamentals
Node.js basics
NPM and package management
Express.js fundamentals
REST API concepts
MongoDB basics
CRUD operations
Projects:

Todo API
Notes app backend
Simple blog API
Intermediate (2-4 months)
Focus Areas:

Authentication (JWT, sessions)
Authorization (roles, permissions)
Input validation
Error handling
File uploads
Testing basics
API documentation
Projects:

User authentication system
E-commerce backend
Social media API
Advanced (4-6+ months)
Focus Areas:

Database optimization (indexing, aggregation)
Caching (Redis)
Real-time communication (WebSockets, Socket.io)
Message queues (RabbitMQ, Redis)
Microservices architecture
Docker & containerization
CI/CD pipelines
Cloud services (AWS, GCP)
System design
Projects:

Real-time chat application
Payment integration
Multi-tenant SaaS backend
Microservices system
Technologies to Learn Next
Category	Technologies
Language	TypeScript
Database	PostgreSQL, Redis
ORM	Prisma
API	GraphQL
Real-time	Socket.io, WebSockets
DevOps	Docker, Kubernetes
Cloud	AWS, GCP, Azure
Testing	Cypress, Playwright
Monitoring	Prometheus, Grafana
41. Quick Reference Cheatsheet
Core Stack


Node.js + Express.js + MongoDB + Mongoose
Essential Packages
bash


# Core
express mongoose dotenv
# Security
bcrypt jsonwebtoken helmet cors
# Utilities
cookie-parser morgan express-validator
# Development
nodemon jest supertest
Request Flow


Client Request
     ↓
Express App
     ↓
Middleware Stack
     ↓
Route Handler
     ↓
Controller
     ↓
Model/Database
     ↓
Response
Authentication Flow


Register/Login
     ↓
Validate Credentials
     ↓
Hash Password (register) / Compare Password (login)
     ↓
Generate JWT
     ↓
Send Token (cookie or body)
     ↓
Client Stores Token
     ↓
Include Token in Requests
     ↓
Server Verifies Token
     ↓
Grant/Deny Access
Common Commands
bash


# Initialize project
npm init -y
npm install express mongoose dotenv
# Development
npm run dev
# Testing
npm test
# Production
npm start
MongoDB Operations
javascript


// Create
Model.create(data)
new Model(data).save()
// Read
Model.find(query)
Model.findOne(query)
Model.findById(id)
// Update
Model.updateOne(query, update)
Model.findByIdAndUpdate(id, update, {new: true})
// Delete
Model.deleteOne(query)
Model.findByIdAndDelete(id)
Express Patterns
javascript


// Route definition
app.get('/path', handler)
app.post('/path', handler)
router.route('/path').get(fn).post(fn)
// Middleware
app.use(middleware)
app.use('/path', middleware)
// Error handling
app.use((err, req, res, next) => {...})
Status Code Quick Reference


200 OK           - Success
201 Created      - Resource created
204 No Content   - Deleted successfully
400 Bad Request  - Invalid input
401 Unauthorized - Not authenticated
403 Forbidden    - Not permitted
404 Not Found    - Resource missing
500 Server Error - Internal error
Sample Project: Notes API
A complete example tying concepts together.

Project Structure


notes-api/
├── src/
│   ├── config/
│   │   └── db.js
│   ├── controllers/
│   │   ├── authController.js
│   │   └── noteController.js
│   ├── middleware/
│   │   ├── auth.js
│   │   └── errorHandler.js
│   ├── models/
│   │   ├── User.js
│   │   └── Note.js
│   ├── routes/
│   │   ├── authRoutes.js
│   │   └── noteRoutes.js
│   └── app.js
├── .env
├── .gitignore
├── package.json
└── server.js
Models
User.js

javascript


const mongoose = require('mongoose');
const bcrypt = require('bcrypt');
const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true, select: false }
}, { timestamps: true });
userSchema.pre('save', async function(next) {
  if (!this.isModified('password')) return next();
  this.password = await bcrypt.hash(this.password, 10);
});
userSchema.methods.comparePassword = function(password) {
  return bcrypt.compare(password, this.password);
};
module.exports = mongoose.model('User', userSchema);
Note.js

javascript


const mongoose = require('mongoose');
const noteSchema = new mongoose.Schema({
  title: { type: String, required: true },
  content: { type: String, required: true },
  user: { type: mongoose.Schema.Types.ObjectId, ref: 'User', required: true }
}, { timestamps: true });
module.exports = mongoose.model('Note', noteSchema);
API Endpoints


Auth:
POST   /api/auth/register
POST   /api/auth/login
GET    /api/auth/me
Notes:
GET    /api/notes          (all user's notes)
POST   /api/notes          (create note)
GET    /api/notes/:id      (single note)
PATCH  /api/notes/:id      (update note)
DELETE /api/notes/:id      (delete note)



