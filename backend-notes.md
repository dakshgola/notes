# Backend Development Notes
### Node.js + Express + MongoDB — Complete Reference

> **Stack:** Node.js · Express.js · MongoDB · Mongoose  
> **Purpose:** Personal revision notes for backend concepts, patterns & interview prep

---

## Table of Contents

1. [How the Internet Works](#1-how-the-internet-works)
2. [Node.js Fundamentals](#2-nodejs-fundamentals)
3. [NPM Essentials](#3-npm-essentials)
4. [Express.js Fundamentals](#4-expressjs-fundamentals)
5. [Routing](#5-routing)
6. [Middleware](#6-middleware)
7. [HTTP Methods](#7-http-methods)
8. [REST API Design](#8-rest-api-design)
9. [HTTP Status Codes](#9-http-status-codes)
10. [MongoDB Fundamentals](#10-mongodb-fundamentals)
11. [Mongoose ODM](#11-mongoose-odm)
12. [Schema & Models](#12-schema--models)
13. [CRUD Operations](#13-crud-operations)
14. [MVC Architecture](#14-mvc-architecture)
15. [Authentication — Bcrypt + JWT](#15-authentication--bcrypt--jwt)
16. [Cookies & Cookie Parser](#16-cookies--cookie-parser)
17. [Authorization & RBAC](#17-authorization--rbac)
18. [File Uploads & Cloud Storage](#18-file-uploads--cloud-storage)
19. [Environment Variables](#19-environment-variables)
20. [Input Validation](#20-input-validation)
21. [Error Handling](#21-error-handling)
22. [Security Best Practices](#22-security-best-practices)
23. [Rate Limiting & CORS](#23-rate-limiting--cors)
24. [Project Folder Structure](#24-project-folder-structure)
25. [Testing — Jest & Supertest](#25-testing--jest--supertest)
26. [Deployment](#26-deployment)
27. [Interview Questions](#27-interview-questions)
28. [Quick Reference Cheatsheet](#28-quick-reference-cheatsheet)

---

## 1. How the Internet Works

### Request Flow
```
User → Browser → DNS Lookup → HTTP Request → Server → Database
User ← Browser ← Response  ← Server processes & responds
```

### Step-by-Step
1. User types `google.com`
2. DNS resolves domain → IP address (e.g., `142.250.190.78`)
3. Browser sends HTTP request
4. Server receives, processes the request
5. Server queries DB if needed
6. Server constructs response (HTML / JSON)
7. Response travels back to client

### Key Protocols

| Protocol | Purpose | Port |
|----------|---------|------|
| HTTP | Web communication (unencrypted) | 80 |
| HTTPS | Secure web communication | 443 |
| DNS | Domain → IP translation | 53 |
| TCP/IP | Data transmission foundation | — |

### HTTP Request Structure
```
Method:  GET
URL:     /api/users/123
Headers: Content-Type: application/json
         Authorization: Bearer <token>
Body:    (empty for GET, JSON for POST/PUT)
```

### HTTP Response Structure
```
Status:  200 OK
Headers: Content-Type: application/json
Body:    { "id": 123, "name": "John Doe" }
```

---

## 2. Node.js Fundamentals

### What is Node.js?
JavaScript runtime built on Chrome's **V8 engine** — lets JS run on the server.

### Why Node.js?

| Advantage | Description |
|-----------|-------------|
| JS Everywhere | Same language for frontend & backend |
| Non-blocking I/O | Handles many connections efficiently |
| Fast | V8 compiles to machine code |
| Huge Ecosystem | Millions of packages via NPM |

### Node.js vs Browser JS

| Feature | Browser | Node.js |
|---------|---------|---------|
| DOM manipulation | ✅ | ❌ |
| File system access | ❌ | ✅ |
| `window` object | ✅ | ❌ |
| `global` object | ❌ | ✅ |

### Built-in Modules (no install needed)
```js
const fs   = require('fs');            // File system
const path = require('path');          // Path utilities
const http = require('http');          // HTTP server
const os   = require('os');            // OS info
```

### Check versions
```bash
node -v    # v20.x.x
npm -v     # 10.x.x
```

---

## 3. NPM Essentials

### Init a project
```bash
npm init -y          # Skip all prompts
```

### `package.json` key fields
```json
{
  "name": "my-backend",
  "version": "1.0.0",
  "main": "app.js",
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js",
    "test": "jest"
  },
  "dependencies": { "express": "^4.18.2" },
  "devDependencies": { "nodemon": "^3.0.0" }
}
```

### Common Commands
```bash
npm install                    # Install from package.json
npm install express            # Add production dependency
npm install nodemon -D         # Add dev dependency
npm uninstall express          # Remove package
npm update                     # Update all packages
npm run dev                    # Run custom script
```

### Version Symbols
```
^4.18.2  →  Allows 4.x.x (minor + patch)
~4.18.2  →  Allows 4.18.x (patch only)
 4.18.2  →  Exact version only
```

### `.gitignore` (always add these)
```
node_modules/
.env
*.log
dist/
coverage/
```

---

## 4. Express.js Fundamentals

### Minimal Server
```js
const express = require('express');
const app = express();

app.use(express.json());  // Parse JSON bodies

app.get('/', (req, res) => {
  res.json({ message: 'API is live!' });
});

app.listen(3000, () => console.log('Server running on port 3000'));
```

### `req` Object — Key Properties
```js
req.params    // URL params  → /users/:id
req.query     // Query string → ?page=1&limit=10
req.body      // Request body (POST/PUT)
req.headers   // HTTP headers
req.cookies   // Cookies (needs cookie-parser)
req.method    // GET, POST, etc.
req.ip        // Client IP
```

### `res` Object — Key Methods
```js
res.json({ data })                    // Send JSON
res.status(201).json({ created: true }) // With status
res.send('Hello')                     // Plain text
res.redirect('/other')                // Redirect
res.sendFile('/path/to/file.pdf')     // Send file
res.cookie('name', 'value', opts)     // Set cookie
res.clearCookie('name')               // Clear cookie
```

### Built-in Middleware
```js
app.use(express.json());                    // Parse JSON
app.use(express.urlencoded({ extended: true })); // Parse form data
app.use(express.static('public'));          // Serve static files
```

---

## 5. Routing

### Basic Route Syntax
```js
app.METHOD(PATH, HANDLER);
```

### Route Parameters
```js
// Single param
app.get('/users/:id', (req, res) => {
  res.json({ userId: req.params.id });
});

// Multiple params
app.get('/users/:userId/posts/:postId', (req, res) => {
  const { userId, postId } = req.params;
  res.json({ userId, postId });
});
```

### Query Parameters
```js
// URL: /search?q=nodejs&page=2&limit=10
app.get('/search', (req, res) => {
  const { q, page = 1, limit = 10 } = req.query;
  res.json({ searchTerm: q, page: +page, limit: +limit });
});
```

### Express Router (for large apps)
```js
// routes/userRoutes.js
const router = require('express').Router();

router.get('/',    getAllUsers);
router.get('/:id', getUser);
router.post('/',   createUser);
router.put('/:id', updateUser);
router.delete('/:id', deleteUser);

module.exports = router;

// app.js
app.use('/api/users', require('./routes/userRoutes'));
```

### Route Chaining
```js
app.route('/books')
  .get(getAllBooks)
  .post(createBook);

app.route('/books/:id')
  .get(getBook)
  .put(updateBook)
  .delete(deleteBook);
```

---

## 6. Middleware

### What is Middleware?
Functions that run **between request and response**. They have access to `req`, `res`, and `next`.

```
Request → MW1 → MW2 → Route Handler → Response
```

> ⚠️ Always call `next()` unless you're ending the response cycle.

### Types

```js
// Application-level (all routes)
app.use((req, res, next) => {
  console.log(`${req.method} ${req.path}`);
  next();
});

// Route-level (specific path)
app.use('/api', (req, res, next) => {
  console.log('API request');
  next();
});

// Error-handling (4 params — always last)
app.use((err, req, res, next) => {
  res.status(500).json({ message: err.message });
});
```

### Common Third-party Middleware
```js
const cors    = require('cors');
const morgan  = require('morgan');
const helmet  = require('helmet');

app.use(cors());           // Enable CORS
app.use(morgan('dev'));    // HTTP request logger
app.use(helmet());         // Set security headers
```

### Auth Middleware Example
```js
const protect = (req, res, next) => {
  const token = req.headers.authorization?.split(' ')[1];
  if (!token) return res.status(401).json({ message: 'No token' });

  try {
    req.user = jwt.verify(token, process.env.JWT_SECRET);
    next();
  } catch {
    res.status(401).json({ message: 'Invalid token' });
  }
};

// Usage
app.get('/profile', protect, (req, res) => res.json(req.user));
```

### Middleware Order Matters
```js
app.use(express.json());    // 1. Parse body
app.use(morgan('dev'));     // 2. Log request
app.use(protect);           // 3. Auth check
app.use('/api', routes);    // 4. Routes
app.use(errorHandler);      // 5. Error handler (ALWAYS LAST)
```

---

## 7. HTTP Methods

| Method | Purpose | Has Body | Idempotent |
|--------|---------|----------|------------|
| GET | Retrieve data | No | Yes |
| POST | Create data | Yes | No |
| PUT | Replace entire resource | Yes | Yes |
| PATCH | Partial update | Yes | No |
| DELETE | Remove data | Optional | Yes |

### PUT vs PATCH
```
Original: { name: "John", email: "j@gmail.com", age: 25 }

PUT   with { name: "Jane" } → { name: "Jane", email: null, age: null }  ← replaces all
PATCH with { name: "Jane" } → { name: "Jane", email: "j@gmail.com", age: 25 }  ← updates specific
```

---

## 8. REST API Design

### RESTful URL Conventions
```
✅ Good (nouns, plural)
GET    /users
GET    /users/123
POST   /users
PUT    /users/123
DELETE /users/123

❌ Bad (verbs in URL)
GET    /getUsers
POST   /createUser
GET    /user/delete/123
```

### Nested Resources
```
GET  /users/123/posts        # All posts by user
GET  /users/123/posts/456    # Specific post by user
POST /users/123/posts        # Create post for user
```

### Filtering, Sorting, Pagination
```
GET /users?role=admin
GET /users?sort=createdAt&order=desc
GET /users?page=2&limit=10
GET /users?fields=name,email
```

### Response Structure

**Success:**
```json
{
  "success": true,
  "data": { "id": "123", "name": "John" }
}
```

**Collection with Pagination:**
```json
{
  "success": true,
  "count": 25,
  "pagination": { "page": 1, "limit": 10, "totalPages": 3 },
  "data": [...]
}
```

**Error:**
```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid email format"
  }
}
```

---

## 9. HTTP Status Codes

### Quick Reference

| Code | Name | When to Use |
|------|------|-------------|
| **200** | OK | Successful GET / PUT / PATCH |
| **201** | Created | Successful POST |
| **204** | No Content | Successful DELETE |
| **400** | Bad Request | Invalid input / validation error |
| **401** | Unauthorized | Not authenticated |
| **403** | Forbidden | Authenticated but no permission |
| **404** | Not Found | Resource doesn't exist |
| **409** | Conflict | Duplicate entry |
| **429** | Too Many Requests | Rate limit exceeded |
| **500** | Internal Server Error | Unexpected server error |

### Usage in Express
```js
res.status(200).json({ data: users });       // GET success
res.status(201).json({ data: newUser });     // POST success
res.status(204).send();                      // DELETE success
res.status(400).json({ message: 'Bad input' });
res.status(401).json({ message: 'Not authorized' });
res.status(404).json({ message: 'Not found' });
res.status(500).json({ message: 'Server error' });
```

---

## 10. MongoDB Fundamentals

### SQL vs MongoDB Terms

| SQL | MongoDB |
|-----|---------|
| Database | Database |
| Table | Collection |
| Row | Document |
| Column | Field |
| Primary Key | `_id` |

### Document Example (BSON/JSON)
```json
{
  "_id": "ObjectId('507f1f...')",
  "name": "John Doe",
  "email": "john@example.com",
  "address": { "city": "Delhi", "zip": "110001" },
  "hobbies": ["coding", "gym"],
  "createdAt": "2024-01-15T10:30:00Z"
}
```

### When to Use MongoDB
- Flexible / varying data structures
- Rapid prototyping
- Real-time analytics
- Content management

### When to Avoid
- Complex multi-table joins needed
- ACID transactions are critical
- Strict relational data

---

## 11. Mongoose ODM

### Why Mongoose?
Provides **schemas, validation, middleware, and a query API** on top of MongoDB.

### Install & Connect
```bash
npm install mongoose
```

```js
// config/db.js
const mongoose = require('mongoose');

const connectDB = async () => {
  try {
    const conn = await mongoose.connect(process.env.MONGO_URI);
    console.log(`MongoDB connected: ${conn.connection.host}`);
  } catch (error) {
    console.error(error.message);
    process.exit(1);
  }
};

module.exports = connectDB;
```

```js
// app.js
require('dotenv').config();
const connectDB = require('./config/db');
connectDB();
```

### Connection Events
```js
mongoose.connection.on('connected',    () => console.log('DB connected'));
mongoose.connection.on('error',    err => console.log('DB error:', err));
mongoose.connection.on('disconnected', () => console.log('DB disconnected'));
```

---

## 12. Schema & Models

### Basic Schema
```js
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  age: Number,
  isActive: Boolean
});

module.exports = mongoose.model('User', userSchema);
```

### Schema with Full Validation
```js
const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: [true, 'Name is required'],
    trim: true,
    minlength: [2, 'Min 2 chars'],
    maxlength: [50, 'Max 50 chars']
  },
  email: {
    type: String,
    required: [true, 'Email required'],
    unique: true,
    lowercase: true,
    match: [/^\S+@\S+\.\S+$/, 'Invalid email']
  },
  password: {
    type: String,
    required: true,
    minlength: 8,
    select: false        // Exclude from queries by default
  },
  role: {
    type: String,
    enum: ['user', 'admin', 'moderator'],
    default: 'user'
  },
  isVerified: { type: Boolean, default: false },
  createdAt:  { type: Date,    default: Date.now }
});
```

### Schema Types

| Type | Example Value |
|------|--------------|
| String | `"Hello"` |
| Number | `42`, `3.14` |
| Boolean | `true` / `false` |
| Date | `new Date()` |
| ObjectId | `mongoose.Schema.Types.ObjectId` |
| Array | `[String]` |
| Mixed | Any type |

### References (Populate)
```js
const postSchema = new mongoose.Schema({
  title: String,
  author: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User',
    required: true
  }
});
```

### Virtual Properties
```js
userSchema.virtual('fullName').get(function () {
  return `${this.firstName} ${this.lastName}`;
});
userSchema.set('toJSON', { virtuals: true }); // Include in responses
```

### Schema Methods
```js
// Instance method
userSchema.methods.isPasswordCorrect = async function (password) {
  return bcrypt.compare(password, this.password);
};

// Static method
userSchema.statics.findByEmail = function (email) {
  return this.findOne({ email });
};
```

### Middleware (Hooks)
```js
// Hash password before saving
userSchema.pre('save', async function (next) {
  if (!this.isModified('password')) return next();
  this.password = await bcrypt.hash(this.password, 10);
  next();
});
```

---

## 13. CRUD Operations

### Create
```js
// Method 1
const user = await User.create({ name: 'John', email: 'j@gmail.com' });

// Method 2
const user = new User({ name: 'John' });
await user.save();

// Many
await User.insertMany([{ name: 'A' }, { name: 'B' }]);
```

### Read
```js
await User.find();                                      // All
await User.find({ isActive: true });                    // With filter
await User.findOne({ email: 'j@gmail.com' });           // Single
await User.findById('507f1f...');                       // By ID

// Query operators
await User.find({ age: { $gte: 18, $lte: 65 } });
await User.find({ role: { $in: ['admin', 'mod'] } });
await User.find({ name: { $regex: /john/i } });

// Chaining
await User.find()
  .select('name email -_id')  // Fields to return
  .sort({ createdAt: -1 })    // Sort desc
  .skip(10).limit(5);         // Pagination

// Populate references
await Post.find().populate('author', 'name email');

await User.countDocuments({ isActive: true });
await User.exists({ email: 'j@gmail.com' });
```

### Update
```js
await User.updateOne({ email: 'j@gmail.com' }, { $set: { isActive: true } });

const user = await User.findByIdAndUpdate(
  id,
  { $set: { name: 'Jane' } },
  { new: true, runValidators: true }   // Return updated doc
);

await User.updateMany({ isVerified: false }, { $set: { isActive: false } });
```

### Update Operators
```js
$set:       { name: 'New' }         // Set value
$unset:     { tempField: '' }       // Remove field
$inc:       { loginCount: 1 }       // Increment
$push:      { tags: 'new-tag' }     // Add to array
$pull:      { tags: 'old-tag' }     // Remove from array
$addToSet:  { tags: 'unique' }      // Add if not exists
```

### Delete
```js
await User.deleteOne({ email: 'j@gmail.com' });
await User.findByIdAndDelete('507f1f...');
await User.deleteMany({ isActive: false });
```

### Query Operators Cheatsheet

| Operator | Meaning | Example |
|----------|---------|---------|
| `$eq` | Equal | `{ age: { $eq: 25 } }` |
| `$ne` | Not equal | `{ status: { $ne: 'deleted' } }` |
| `$gt` / `$gte` | Greater than | `{ age: { $gt: 18 } }` |
| `$lt` / `$lte` | Less than | `{ age: { $lt: 65 } }` |
| `$in` | In array | `{ role: { $in: ['admin'] } }` |
| `$nin` | Not in array | `{ role: { $nin: ['banned'] } }` |
| `$or` | Logical OR | `{ $or: [{...}, {...}] }` |
| `$and` | Logical AND | `{ $and: [{...}, {...}] }` |
| `$regex` | Pattern match | `{ name: { $regex: /^J/i } }` |
| `$exists` | Field exists | `{ email: { $exists: true } }` |

---

## 14. MVC Architecture

### What is MVC?

| Component | Responsibility |
|-----------|---------------|
| **Model** | Data structure, DB ops, business rules |
| **View** | Presentation (JSON/HTML response) |
| **Controller** | Handles requests, bridges Model & View |

### Request Flow
```
Request → Router → Controller → Model → Database
                       ↓
Response ← View ← Controller
```

### Full MVC Example

**`models/User.js`**
```js
const mongoose = require('mongoose');
const userSchema = new mongoose.Schema({
  name:  { type: String, required: true },
  email: { type: String, required: true, unique: true },
  role:  { type: String, enum: ['user', 'admin'], default: 'user' }
}, { timestamps: true });

module.exports = mongoose.model('User', userSchema);
```

**`controllers/userController.js`**
```js
const User = require('../models/User');

exports.getAllUsers = async (req, res, next) => {
  try {
    const users = await User.find();
    res.status(200).json({ success: true, count: users.length, data: users });
  } catch (err) { next(err); }
};

exports.getUser = async (req, res, next) => {
  try {
    const user = await User.findById(req.params.id);
    if (!user) return res.status(404).json({ success: false, message: 'Not found' });
    res.json({ success: true, data: user });
  } catch (err) { next(err); }
};

exports.createUser = async (req, res, next) => {
  try {
    const user = await User.create(req.body);
    res.status(201).json({ success: true, data: user });
  } catch (err) { next(err); }
};

exports.updateUser = async (req, res, next) => {
  try {
    const user = await User.findByIdAndUpdate(req.params.id, req.body, { new: true, runValidators: true });
    if (!user) return res.status(404).json({ success: false, message: 'Not found' });
    res.json({ success: true, data: user });
  } catch (err) { next(err); }
};

exports.deleteUser = async (req, res, next) => {
  try {
    const user = await User.findByIdAndDelete(req.params.id);
    if (!user) return res.status(404).json({ success: false, message: 'Not found' });
    res.status(204).send();
  } catch (err) { next(err); }
};
```

**`routes/userRoutes.js`**
```js
const router = require('express').Router();
const { getAllUsers, getUser, createUser, updateUser, deleteUser } = require('../controllers/userController');

router.route('/').get(getAllUsers).post(createUser);
router.route('/:id').get(getUser).put(updateUser).delete(deleteUser);

module.exports = router;
```

---

## 15. Authentication — Bcrypt + JWT

### Concepts

| Concept | Question | Example |
|---------|---------|---------|
| **Authentication** | Who are you? | Login |
| **Authorization** | What can you do? | Admin vs User |

### JWT Structure
```
header.payload.signature
```
- **Header** → `{ "alg": "HS256", "typ": "JWT" }`
- **Payload** → `{ "id": "123", "role": "admin" }`
- **Signature** → HMAC of header + payload + secret

### JWT Auth Flow
```
1. User sends credentials (email + password)
2. Server validates → hashes password check
3. Server generates JWT
4. Token sent to client
5. Client includes token in future requests
6. Server verifies token on each request
```

### Install
```bash
npm install bcrypt jsonwebtoken
```

### Password Hashing (Bcrypt)
```js
const bcrypt = require('bcrypt');

// Hash
const hashed = await bcrypt.hash('mypassword', 10);  // 10 = salt rounds

// Compare
const isMatch = await bcrypt.compare('mypassword', hashed);
```

> 💡 **Salt rounds:** 10 ≈ 100ms · 12 ≈ 400ms. Use 10–12 for most apps.

### Mongoose Hook (auto-hash on save)
```js
userSchema.pre('save', async function (next) {
  if (!this.isModified('password')) return next();
  this.password = await bcrypt.hash(this.password, 10);
  next();
});

userSchema.methods.comparePassword = function (candidate) {
  return bcrypt.compare(candidate, this.password);
};
```

### Generate & Verify JWT
```js
const jwt = require('jsonwebtoken');

// Generate
const generateToken = (user) =>
  jwt.sign({ id: user._id, role: user.role }, process.env.JWT_SECRET, { expiresIn: '7d' });

// Verify
const decoded = jwt.verify(token, process.env.JWT_SECRET);
```

### Auth Controller (Register + Login)
```js
const User = require('../models/User');
const jwt  = require('jsonwebtoken');

const signToken = (id) => jwt.sign({ id }, process.env.JWT_SECRET, { expiresIn: '30d' });

exports.register = async (req, res) => {
  try {
    const { name, email, password } = req.body;
    if (await User.findOne({ email }))
      return res.status(400).json({ success: false, message: 'Email already registered' });

    const user  = await User.create({ name, email, password });
    const token = signToken(user._id);

    res.status(201).json({ success: true, data: { _id: user._id, name, email, token } });
  } catch (err) {
    res.status(500).json({ success: false, message: err.message });
  }
};

exports.login = async (req, res) => {
  try {
    const { email, password } = req.body;
    if (!email || !password)
      return res.status(400).json({ message: 'Provide email and password' });

    const user = await User.findOne({ email }).select('+password');
    if (!user || !(await user.comparePassword(password)))
      return res.status(401).json({ success: false, message: 'Invalid credentials' });

    const token = signToken(user._id);
    res.json({ success: true, data: { token } });
  } catch (err) {
    res.status(500).json({ success: false, message: err.message });
  }
};
```

### Protect Middleware
```js
const protect = async (req, res, next) => {
  const token = req.headers.authorization?.startsWith('Bearer')
    ? req.headers.authorization.split(' ')[1]
    : null;

  if (!token) return res.status(401).json({ message: 'No token' });

  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = await User.findById(decoded.id);
    next();
  } catch {
    res.status(401).json({ message: 'Invalid/expired token' });
  }
};
```

---

## 16. Cookies & Cookie Parser

```bash
npm install cookie-parser
```

```js
const cookieParser = require('cookie-parser');
app.use(cookieParser());
```

### Set / Read / Clear Cookies
```js
// Set
res.cookie('token', jwtToken, {
  httpOnly: true,    // JS can't access — protects against XSS
  secure: true,      // HTTPS only
  sameSite: 'strict',// CSRF protection
  maxAge: 7 * 24 * 60 * 60 * 1000  // 7 days (ms)
});

// Read
const token = req.cookies.token;

// Clear
res.clearCookie('token');
```

### Cookie Options

| Option | Purpose | Recommended |
|--------|---------|-------------|
| `httpOnly` | Block JS access | `true` for auth tokens |
| `secure` | HTTPS only | `true` in production |
| `sameSite` | CSRF protection | `'strict'` or `'lax'` |
| `maxAge` | Expiry in ms | Set appropriately |

---

## 17. Authorization & RBAC

### Role-Based Access Control

```js
// Schema role field
role: { type: String, enum: ['user', 'moderator', 'admin'], default: 'user' }
```

### Authorize Middleware
```js
const authorize = (...roles) => (req, res, next) => {
  if (!roles.includes(req.user.role))
    return res.status(403).json({ message: 'Access denied' });
  next();
};
```

### Usage
```js
router.get('/profile',     protect,                          getProfile);
router.delete('/users/:id', protect, authorize('admin'),       deleteUser);
router.put('/posts/:id',   protect, authorize('admin', 'moderator'), updatePost);
```

### Ownership Check
```js
exports.updatePost = async (req, res) => {
  const post = await Post.findById(req.params.id);

  const isOwner = post.author.toString() === req.user._id.toString();
  const isAdmin = req.user.role === 'admin';

  if (!isOwner && !isAdmin)
    return res.status(403).json({ message: 'Not authorized' });

  // proceed...
};
```

---

## 18. File Uploads & Cloud Storage

### Flow
```
Client → Multer (parse file) → Cloud Storage → Save URL to DB
```

```bash
npm install multer cloudinary
```

### Multer Setup
```js
const multer = require('multer');

const upload = multer({
  storage: multer.memoryStorage(),
  fileFilter: (req, file, cb) => {
    file.mimetype.startsWith('image/') ? cb(null, true) : cb(new Error('Only images'), false);
  },
  limits: { fileSize: 5 * 1024 * 1024 }  // 5MB
});
```

### Cloudinary Upload
```js
const cloudinary = require('cloudinary').v2;

cloudinary.config({
  cloud_name: process.env.CLOUDINARY_CLOUD_NAME,
  api_key:    process.env.CLOUDINARY_API_KEY,
  api_secret: process.env.CLOUDINARY_API_SECRET
});

const uploadToCloudinary = (buffer, folder) =>
  new Promise((resolve, reject) => {
    cloudinary.uploader.upload_stream({ folder }, (err, result) =>
      err ? reject(err) : resolve(result)
    ).end(buffer);
  });
```

### Upload Route
```js
router.post('/upload', upload.single('image'), async (req, res) => {
  if (!req.file) return res.status(400).json({ message: 'No file uploaded' });

  const result = await uploadToCloudinary(req.file.buffer, 'avatars');
  res.json({ success: true, url: result.secure_url });
});
```

---

## 19. Environment Variables

```bash
npm install dotenv
```

### `.env` file
```env
NODE_ENV=development
PORT=3000
MONGO_URI=mongodb+srv://user:pass@cluster.mongodb.net/mydb
JWT_SECRET=supersecretkey
CLOUDINARY_CLOUD_NAME=mycloud
CLOUDINARY_API_KEY=123456
CLOUDINARY_API_SECRET=abcdef
```

### Load in app
```js
require('dotenv').config();  // Top of entry file

const PORT = process.env.PORT || 3000;
```

### Validate required vars at startup
```js
const required = ['NODE_ENV', 'PORT', 'MONGO_URI', 'JWT_SECRET'];
const missing  = required.filter(v => !process.env[v]);
if (missing.length) throw new Error(`Missing env vars: ${missing.join(', ')}`);
```

> ⚠️ **Never commit `.env`** — always add to `.gitignore`

---

## 20. Input Validation

```bash
npm install express-validator
```

### Validation Rules
```js
const { body, param, validationResult } = require('express-validator');

const userRules = [
  body('name').trim().notEmpty().isLength({ min: 2, max: 50 }),
  body('email').trim().isEmail().normalizeEmail(),
  body('password').isLength({ min: 8 }).matches(/\d/).withMessage('Must contain a number'),
  body('age').optional().isInt({ min: 0, max: 150 })
];
```

### Validate Middleware
```js
const validate = (req, res, next) => {
  const errors = validationResult(req);
  if (!errors.isEmpty())
    return res.status(400).json({
      success: false,
      errors: errors.array().map(e => ({ field: e.path, message: e.msg }))
    });
  next();
};
```

### Usage in Routes
```js
router.post('/users', userRules, validate, createUser);
```

### Common Validators
```js
body('field').notEmpty()
body('field').isLength({ min, max })
body('email').isEmail()
body('url').isURL()
body('id').isMongoId()
body('age').isInt({ min: 0 })
body('tags').isArray()
body('field').trim().escape()  // Sanitize

// Custom async
body('email').custom(async (val) => {
  if (await User.findOne({ email: val })) throw new Error('Email taken');
});
```

---

## 21. Error Handling

### Custom Error Class
```js
// utils/AppError.js
class AppError extends Error {
  constructor(message, statusCode) {
    super(message);
    this.statusCode  = statusCode;
    this.status      = `${statusCode}`.startsWith('4') ? 'fail' : 'error';
    this.isOperational = true;
  }
}
module.exports = AppError;
```

### Global Error Handler
```js
// middleware/errorHandler.js
const errorHandler = (err, req, res, next) => {
  let { message, statusCode = 500 } = err;

  if (err.name === 'CastError')         { message = 'Resource not found'; statusCode = 404; }
  if (err.code === 11000)               { message = `${Object.keys(err.keyValue)[0]} already exists`; statusCode = 400; }
  if (err.name === 'ValidationError')   { message = Object.values(err.errors).map(e => e.message).join(', '); statusCode = 400; }
  if (err.name === 'JsonWebTokenError') { message = 'Invalid token'; statusCode = 401; }
  if (err.name === 'TokenExpiredError') { message = 'Token expired'; statusCode = 401; }

  res.status(statusCode).json({
    success: false,
    message,
    ...(process.env.NODE_ENV === 'development' && { stack: err.stack })
  });
};
module.exports = errorHandler;
```

### Async Handler (removes try-catch boilerplate)
```js
// utils/asyncHandler.js
const asyncHandler = fn => (req, res, next) =>
  Promise.resolve(fn(req, res, next)).catch(next);

// Usage
exports.getUser = asyncHandler(async (req, res, next) => {
  const user = await User.findById(req.params.id);
  if (!user) return next(new AppError('User not found', 404));
  res.json({ success: true, data: user });
});
```

### 404 Handler
```js
// Add BEFORE error handler
app.use('*', (req, res, next) =>
  next(new AppError(`Cannot find ${req.originalUrl}`, 404))
);
app.use(errorHandler);
```

---

## 22. Security Best Practices

```bash
npm install helmet express-mongo-sanitize xss-clean hpp
```

```js
const helmet        = require('helmet');
const mongoSanitize = require('express-mongo-sanitize');
const xss           = require('xss-clean');
const hpp           = require('hpp');

app.use(helmet());           // Security headers
app.use(mongoSanitize());    // Prevent NoSQL injection
app.use(xss());              // Prevent XSS
app.use(hpp());              // Prevent parameter pollution
app.use(express.json({ limit: '10kb' }));  // Limit body size
```

### Security Checklist

- [x] Hash passwords with bcrypt
- [x] Use JWT with `httpOnly` cookies
- [x] Store secrets in `.env`
- [x] Validate & sanitize all input
- [x] Use Helmet for security headers
- [x] HTTPS in production
- [x] Rate limiting on all routes
- [x] Keep dependencies updated

---

## 23. Rate Limiting & CORS

```bash
npm install express-rate-limit cors
```

### Rate Limiting
```js
const rateLimit = require('express-rate-limit');

const generalLimiter = rateLimit({
  windowMs: 15 * 60 * 1000,  // 15 min
  max: 100,
  message: { success: false, message: 'Too many requests' }
});

const authLimiter = rateLimit({
  windowMs: 60 * 60 * 1000,  // 1 hour
  max: 5,
  message: { success: false, message: 'Too many login attempts' }
});

app.use('/api',             generalLimiter);
app.use('/api/auth/login',  authLimiter);
```

### CORS
```js
const cors = require('cors');

// Development
app.use(cors());

// Production
app.use(cors({
  origin: process.env.ALLOWED_ORIGINS.split(','),
  credentials: true,
  methods: ['GET', 'POST', 'PUT', 'PATCH', 'DELETE'],
  allowedHeaders: ['Content-Type', 'Authorization']
}));
```

---

## 24. Project Folder Structure

### Professional Structure
```
project/
├── src/
│   ├── config/
│   │   ├── db.js              # DB connection
│   │   └── cloudinary.js      # Cloud storage config
│   │
│   ├── controllers/           # Request handlers
│   │   ├── authController.js
│   │   └── userController.js
│   │
│   ├── middleware/            # Middleware functions
│   │   ├── auth.js            # JWT protect
│   │   ├── authorize.js       # RBAC
│   │   ├── errorHandler.js    # Global error handler
│   │   └── upload.js          # Multer setup
│   │
│   ├── models/                # Mongoose schemas
│   │   ├── User.js
│   │   └── Post.js
│   │
│   ├── routes/                # Express routers
│   │   ├── authRoutes.js
│   │   ├── userRoutes.js
│   │   └── index.js           # Aggregate all routes
│   │
│   ├── utils/
│   │   ├── AppError.js        # Custom error class
│   │   ├── asyncHandler.js    # Async wrapper
│   │   └── helpers.js
│   │
│   ├── validators/            # express-validator rules
│   │   └── userValidator.js
│   │
│   └── app.js                 # Express app setup
│
├── tests/
├── .env
├── .env.example               # Template (no secrets)
├── .gitignore
├── package.json
├── README.md
└── server.js                  # Entry point
```

### Entry Point — `server.js`
```js
require('dotenv').config();
const app       = require('./src/app');
const connectDB = require('./src/config/db');

connectDB().then(() => {
  app.listen(process.env.PORT || 3000, () =>
    console.log(`Server on port ${process.env.PORT}`)
  );
});
```

### App Setup — `src/app.js`
```js
const express       = require('express');
const helmet        = require('helmet');
const cors          = require('cors');
const morgan        = require('morgan');
const routes        = require('./routes');
const errorHandler  = require('./middleware/errorHandler');
const AppError      = require('./utils/AppError');

const app = express();

app.use(helmet());
app.use(cors());
if (process.env.NODE_ENV === 'development') app.use(morgan('dev'));
app.use(express.json({ limit: '10kb' }));

app.use('/api', routes);
app.use('*', (req, res, next) => next(new AppError(`Cannot find ${req.originalUrl}`, 404)));
app.use(errorHandler);

module.exports = app;
```

---

## 25. Testing — Jest & Supertest

```bash
npm install jest supertest --save-dev
```

```json
// package.json
{
  "scripts": {
    "test": "NODE_ENV=test jest --coverage",
    "test:watch": "jest --watch"
  },
  "jest": { "testEnvironment": "node", "testTimeout": 10000 }
}
```

### Test Setup (in-memory DB)
```bash
npm install mongodb-memory-server --save-dev
```

```js
// tests/setup.js
const mongoose         = require('mongoose');
const { MongoMemoryServer } = require('mongodb-memory-server');

let mongoServer;
beforeAll(async () => {
  mongoServer = await MongoMemoryServer.create();
  await mongoose.connect(mongoServer.getUri());
});
afterAll(async () => { await mongoose.disconnect(); await mongoServer.stop(); });
afterEach(async () => {
  for (const col of Object.values(mongoose.connection.collections))
    await col.deleteMany({});
});
```

### Example Tests
```js
const request = require('supertest');
const app     = require('../src/app');

describe('POST /api/auth/register', () => {
  it('registers a new user', async () => {
    const res = await request(app).post('/api/auth/register').send({
      name: 'Test', email: 'test@example.com', password: 'password123'
    });
    expect(res.statusCode).toBe(201);
    expect(res.body.data).toHaveProperty('token');
  });

  it('rejects duplicate email', async () => {
    await request(app).post('/api/auth/register').send({ name: 'A', email: 'a@a.com', password: 'pass1234' });
    const res = await request(app).post('/api/auth/register').send({ name: 'B', email: 'a@a.com', password: 'pass1234' });
    expect(res.statusCode).toBe(400);
  });
});
```

```bash
npm test            # Run all
npm run test:watch  # Watch mode
npm test -- --coverage
```

---

## 26. Deployment

### Pre-Deployment Checklist
- [ ] All env vars set for production
- [ ] Production DB URI used
- [ ] Error messages don't expose internals
- [ ] Security middleware enabled
- [ ] CORS configured for prod origins
- [ ] All tests passing
- [ ] `engines` field in `package.json`

```json
{
  "engines": { "node": ">=18.0.0" },
  "scripts": { "start": "node server.js" }
}
```

### Platforms

| Platform | Best For | Pricing |
|----------|---------|---------|
| Railway | Quick deploy | Free + pay-as-you-go |
| Render | Full-stack | Free tier |
| DigitalOcean | Full control | From $5/month |
| AWS | Enterprise | Pay-as-you-go |

### Health Check Endpoint
```js
app.get('/health', (req, res) =>
  res.json({ status: 'healthy', uptime: process.uptime(), timestamp: new Date() })
);
```

---

## 27. Interview Questions

### Node.js
**Q: What is the event loop?**  
The event loop lets Node.js perform non-blocking I/O. It checks the call stack & callback queue continuously, executing callbacks when the stack is empty.

**Q: `require` vs `import`?**

| `require` (CommonJS) | `import` (ES Modules) |
|---------------------|-----------------------|
| Synchronous | Asynchronous |
| Dynamic loading | Static analysis |
| Default in Node.js | Needs `"type": "module"` |

### Express
**Q: What is middleware?**  
Functions with access to `req`, `res`, and `next`. They can modify req/res, end the cycle, or call next middleware.

**Q: `app.use()` vs `app.get()`?**  
`app.use()` matches all HTTP methods; `app.get()` only handles GET on a specific path.

### Database
**Q: SQL vs NoSQL — when?**

| SQL | NoSQL |
|-----|-------|
| Structured data | Flexible schema |
| Complex joins | Nested documents |
| ACID compliance | Horizontal scaling |

**Q: What is indexing?**  
Data structure that speeds up queries — like a book index. Avoids full collection scans.

### Security
**Q: How do you secure an API?**  
HTTPS · JWT auth · Input validation · Password hashing · Rate limiting · Helmet · Updated dependencies

**Q: Authentication vs Authorization?**  
Auth = Who are you? · Authz = What can you do?

### Code Questions

**Q: Write a request timing middleware**
```js
const requestTimer = (req, res, next) => {
  const start = Date.now();
  res.on('finish', () => console.log(`${req.method} ${req.path} - ${Date.now() - start}ms`));
  next();
};
```

**Q: Implement basic rate limiter from scratch**
```js
const rateLimiter = (windowMs, max) => {
  const store = new Map();
  return (req, res, next) => {
    const now  = Date.now();
    const ip   = req.ip;
    const data = store.get(ip);
    if (!data || now - data.start > windowMs) return store.set(ip, { count: 1, start: now }), next();
    if (data.count >= max) return res.status(429).json({ message: 'Too many requests' });
    data.count++;
    next();
  };
};
```

---

## 28. Quick Reference Cheatsheet

### Essential Packages
```bash
# Core
npm install express mongoose dotenv

# Auth & Security
npm install bcrypt jsonwebtoken helmet cors express-rate-limit

# Extras
npm install cookie-parser morgan express-validator multer cloudinary

# Dev
npm install nodemon jest supertest --save-dev
```

### MongoDB Quick Ops
```js
Model.create(data)
Model.find(query).sort().skip().limit().select()
Model.findOne(query)
Model.findById(id)
Model.findByIdAndUpdate(id, data, { new: true })
Model.findByIdAndDelete(id)
Model.countDocuments(query)
Model.exists(query)
```

### Express Patterns
```js
app.get('/path', handler)
app.post('/path', handler)
router.route('/path').get(fn).post(fn)
app.use(middleware)
app.use((err, req, res, next) => {})  // Error handler
```

### Status Code Summary
```
200  OK             — Successful GET/PUT/PATCH
201  Created        — Successful POST
204  No Content     — Successful DELETE
400  Bad Request    — Invalid input
401  Unauthorized   — Not authenticated
403  Forbidden      — No permission
404  Not Found      — Missing resource
409  Conflict       — Duplicate entry
429  Too Many Reqs  — Rate limited
500  Server Error   — Internal error
```

### Auth Flow Summary
```
Register: Receive creds → Validate → Hash password → Save → Issue JWT
Login:    Receive creds → Find user → Compare hash → Issue JWT
Request:  Extract token → Verify JWT → Attach user → next()
```

### Git Commit Convention
```
feat(auth): add JWT refresh token
fix(users): resolve password hashing bug
docs(readme): update setup steps
refactor(routes): simplify router structure
test(auth): add login endpoint tests
chore: update dependencies
```

---

*Last updated: 2025 · Stack: Node.js 20 · Express 4 · MongoDB 7 · Mongoose 8*
