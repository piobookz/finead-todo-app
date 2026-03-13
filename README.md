# MERN TODO List App
*Forked from [AtharvaKulkarniIT](https://github.com/AtharvaKulkarniIT/mern-todo-app)*

This is a TODO List application built using the MERN stack. 

## Prerequisites

Before running the application, ensure you have the following installed:
- Node.js and npm. Tested with Node.js 22.
- MongoDB

## Setup Instructions

### 1. Install dependencies

```bash
cd mern-todo-app/TODO

# Split the terminal :

# Install backend dependencies
cd todo_backend
npm install

# Install frontend dependencies
cd todo_frontend
npm install
```

### 2. Move the frontend to backend folder.
Build the frontend
```
cd todo_frontend
npm run build
```
The build artifact is in build/. Copy or move it to the backend folder.
```
cd todo_frontend
mkdir -o ../todo_backend/static
mv build ../todo_backend/static
```
In todo_backend/static, there should be a build/ in it.

### 3. Environment Setup

```bash
export PORT=5000  # Port number for the server (you can change it if needed)
export MONGODB_URI=mongodb://127.0.0.1:27017/todo  # MongoDB connection URI

```

### 4. Running the App

```bash
# Start the server (from the 'todo_backend' directory)
npm start
```

- Open your web browser and go to `http://localhost:5000`.
- You can add, update tasks, mark them as completed or delete them.
