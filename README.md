# Task Management System API

A RESTful API built with Laravel for managing tasks. The API allows users to create, read, update, delete, and filter tasks. It includes authentication with JWT, rate-limiting middleware to prevent abuse, and supports unit testing.

## Features

- **Authentication**: Register and login users with JWT tokens for secure access.
- **CRUD Operations**: Create, retrieve, update, and delete tasks.
- **Filtering and Sorting**: Fetch tasks with optional filters (priority, due date range) and sorting by due date.
- **Rate-Limiting**: Protect API endpoints from abuse with rate-limiting.
- **Unit Tests**: Tests for the task management endpoints.

## Table of Contents

- [API Documentation](#api-documentation)
- [Rate Limiting](#rate-limiting)
- [Setup Instructions](#setup-instructions)
- [Testing](#testing)
- [Deployment](#deployment)
- [License](#license)

## API Documentation

### 1. User Registration
- **Endpoint**: `POST /api/register`
- **Request Body**:
  ```json
  {
    "name": "Test User",
    "email": "testuser@example.com",
    "password": "passwd123"
  }
  ```

  - **Response**:
  ```json
  {
    "token": "JWT_TOKEN"
  }
  ```

### 2. User Login
- **Endpoint**: `POST /api/login`
- **Request Body**:
  ```json
  {
    "email": "testUser@example.com",
      "password": "passwd123"
  }
  ```

  - **Response**:
  ```json
  {
    "token": "JWT_TOKEN"
  }
  ```

### 3. Create Task
- **Endpoint**: `POST /api/tasks`
- **Request Body**:
  ```json
  {
      "title": "Create New Task",
      "description": "Test adding new task",
      "due_date": "2025-01-15",
      "priority": "high"
  }
  ```

  - **Response**:
  ```json
  {
      "id": 1,
      "title": "Create New Task",
      "description": "Test adding new task",
      "due_date": "2025-01-15",
      "priority": "high",
      "created_at": "2025-01-01T00:00:00Z",
      "updated_at": "2025-01-01T00:00:00Z"
  }
  ```

### 4. Fetch All Tasks
- **Endpoint**: `GET /api/tasks`
- **Optional Query Parameters**:
    -`priority`: Filter tasks by priority (e.g., `low, medium, high`).
    -`due_date`: Filter tasks by due date range (e.g., `due_date=2025-01-01,2025-01-30`).
- **Response**:
  ```json
  [
      {
          "id": 1,
          "title": "Create New Task",
          "description": "Test adding new task",
          "due_date": "2025-01-15",
          "priority": "high",
          "created_at": "2025-01-01T00:00:00Z",
          "updated_at": "2025-01-01T00:00:00Z"
      }
  ]
  ```

  ### 5. Update Task
- **Endpoint**: `PUT /api/tasks{id}`
- **Request Body**:
  ```json
  {
      "title": "Update Task",
      "description": "Test adding new task",
      "due_date": "2025-01-15",
      "priority": "low"
  }
  ```

  - **Response**:
  ```json
  {
      "id": 1,
      "title": "Update Task",
      "description": "Test adding new task",
      "due_date": "2025-01-15",
      "priority": "low"
      "created_at": "2025-01-01T00:00:00Z",
      "updated_at": "2025-01-01T00:00:00Z"
  }
  ```

### 6. Delete Tasks
- **Endpoint**: `DELETE /api/tasks{id}`
- **Response**:
  ```json
   {
      "message": "Task deleted successfully",
   }
  ```

### Rate Limiting
 The API is protected with rate-limiting to prevent abuse. Each user is allowed 60 requests per minute. You will receive a 
 429 status code if the rate limit is exceeded.

 ## Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/Task-Management-System-API.git
```
### 2. Navigate to the Project Directory
```bash
cd Task-Management-System-API
```
### 3. Install Dependencies
```bash
composer install
```
### 4. Set Up the Environment File
Copy the `.env.example` file to `.env`:
```bash
cp .env.example .env
```
### 5. Generate the Application Key
```bash
php artisan key:generate
```
### 6. Set Up the Database
Update the `.env` file with your database credentials:
```bash
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=task_management
DB_USERNAME=root
DB_PASSWORD=
```
### 7. Run Database Migrations
```bash
php artisan migrate
```
### 9. Run the Development Server
```bash
php artisan serve
```

The API will be available at http://127.0.0.1:8000.
