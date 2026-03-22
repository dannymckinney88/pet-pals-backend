# 🐾 Pet Pals API

Backend service for Pet Pals, a social platform for pet owners to register, connect with other users, manage pets, share posts, upload images, and interact through comments and friend requests.

---

## Overview

Pet Pals API is a Node.js and Express backend built around a PostgreSQL database with Sequelize ORM. It uses a modular route/controller structure and supports authentication, session handling, relational data modeling, and social features such as posts, comments, pets, images, and user relationships.  

---

## Tech Stack

- Node.js
- Express
- PostgreSQL
- Sequelize ORM
- Passport.js
- passport-local
- express-session
- bcrypt
- cors
- dotenv   

---

## Core Features

- Session-based authentication with Passport Local Strategy
- User registration and login
- Community posts and comments
- Pet creation, editing, and deletion
- Image management for users and pets
- Friend request and relationship system
- User search with case-insensitive matching
- Relational PostgreSQL data

  
---
## 📸 Screenshots

### Desktop version

<p>
  <img src="./petpals-screenshots/browser-pp-login.png" alt="Login" width="300" />
  <img src="./petpals-screenshots/browser-pp-accountinfo.png" alt="Account Info" width="300" />
  <img src="./petpals-screenshots/browser-pp-home.png" alt="Homepage" width="300" />
  <img src="./petpals-screenshots/browser-pp-profile.png" alt="Profile" width="300" />
  <img src="./petpals-screenshots/browser-pp-mypets.png" alt="My Pets" width="300" />
  <img src="./petpals-screenshots/browser-pp-searchresults.png" alt="Search" width="300" />
  <img src="./petpals-screenshots/browser-pp-palsprofile.png" alt="Pals Profile" width="300" />
  <img src="./petpals-screenshots/browser-pp-notifications.png" alt="Notifications" width="300" />
</p>

### Mobile version

<p>
  <img src="./petpals-screenshots/mobile-register.png" alt="Register" width="220" />
  <img src="./petpals-screenshots/mobile-pp-login.png" alt="Login" width="220" />
  <img src="./petpals-screenshots/mobile-pp-accountinfo.png" alt="Account Info" width="220" />
  <img src="./petpals-screenshots/mobile-pp-homepage.png" alt="Homepage" width="220" />
  <img src="./petpals-screenshots/mobile-profile.png" alt="Profile" width="220" />
  <img src="./petpals-screenshots/results.png" alt="Search Result" width="220" />
  <img src="./petpals-screenshots/mobile-pp-notifications.png" alt="Notifications" width="220" />
  <img src="./petpals-screenshots/mobile-pp-palsprofile.png" alt="Pals Profile" width="220" />
</p>

## Authentication

Authentication is implemented with Passport and a local email/password strategy. Login is handled through `/api/v1/auth/login`, registration through `/api/v1/auth/register`, and logout through `/api/v1/auth/logout`. The authenticated user is serialized into the session by user ID and restored on later requests. Passwords are hashed before user creation, and the user model includes a password validation helper.     

---
## API Routes

All API routes are mounted under:

```text
/api/v1
```

These routes are registered in the Express server through modular route exports.

---

## 🗃️ Database Models

The backend uses Sequelize models for:

- User
- Post
- Comment
- Image
- Pet
- Species
- Relationship
- PetSpecies (join table)

---

## 🔗 Data Relationships

### User

A user has many pets, comments, posts, images, and relationships.  
The user model also strips the password from serialized JSON responses and hashes passwords before creation.

---

### Posts and Comments

- A post belongs to a user
- A post has many comments
- A comment belongs to both a user and a post

---

### Pets and Species

Pets belong to a user and are connected to species through a many-to-many relationship using the `petSpecies` join table.

---

### Relationships

User relationships track social connections using:

- `userOneId`
- `userTwoId`
- `status`
- `actionUserId`

This enables pending requests and accepted friendships.

---

## 🧠 Notable Backend Logic

### Friend System

The relationships controller supports:

- Searching users
- Creating friend requests
- Checking friendship status
- Listing friends
- Limiting profile friend previews
- Finding pending requests

It uses Sequelize operators such as:

- `Op.iLike`
- `Op.or`
- `Op.ne`

---

### Pet-to-Species Association

When a pet is created, the API:

- Finds or creates the matching species
- Associates the pet to that species through the join table

---

### Image Updates

The images controller supports:

- User profile image updates
- Pet image updates
- Standard image CRUD operations

---

## 📁 Project Structure

The backend is organized around:

- `server.js` → Express setup, middleware, sessions, Passport, and route mounting
- `routes/` → endpoint definitions
- `controllers/` → request handling logic
- `models/` → Sequelize models and associations
- `passport/` → authentication strategy and session handling
- `config/config.json` → database configuration

---

## ⚙️ Local Setup

### 1. Clone the repository

```bash
git clone <your-backend-repo-url>
cd pet-pals-backend
```

### 2. Install dependencies

```bash
npm install
```

### 3. Create the PostgreSQL database

Create a local database named:

```text
petpals
```

### 4. Update database credentials

Edit:

```text
config/config.json
```

Add your PostgreSQL username and password if needed.

### 5. Run migrations

```bash
npx sequelize db:migrate
```

### 6. Start the server

```bash
node server.js
```

Server runs on:

```text
http://localhost:4000
```

(or `process.env.PORT` if configured)

---

## ⚠️ Development Notes

- Configured for local PostgreSQL development
- CORS allows requests from `http://localhost:3000`
- Uses session-based authentication with cookies
- Production environment configuration is not included

---

## 📌 Summary

Pet Pals API is a modular Express and Sequelize backend that supports:

- Authentication with sessions
- Relational data modeling
- Social platform features (friends, posts, comments)
- Pet and image management

It demonstrates backend fundamentals beyond basic CRUD through:

- join tables
- social relationship logic
- multi-entity associations
- structured REST API design

## ERD, Wireframe, & User Stories

![ERD](petpals-screenshots/erd.png)
![Wireframe](petpals-screenshots/petpals-wireframe.png)

## Future Development

Perhaps one day this application will allow people in the community to seek out support amongst each other with their pet needs whether that is seeking a pet sitter or setting up playdates.
