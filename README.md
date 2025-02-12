# Laravel Project Management API

## Overview
This is a Laravel-based API for managing projects, users, timesheets, and dynamic project attributes using an Entity-Attribute-Value (EAV) model. The API supports user authentication, project assignments, timesheet logging, and flexible filtering for both standard and dynamic attributes.

## Features
- User authentication using Laravel Passport
- CRUD operations for Users, Projects, and Timesheets
- Many-to-Many relationship between Users and Projects
- EAV (Entity-Attribute-Value) system for dynamic project attributes
- Flexible filtering on both standard and dynamic attributes
- API endpoints secured with authentication

## Installation & Setup
### Prerequisites
Ensure you have the following installed:
- PHP 8.x
- Composer
- MySQL or PostgreSQL
- Laravel 9+
- Laravel Passport

### Steps to Set Up
1. **Clone the Repository**
   ```sh
   git clone https://github.com/your-repo/project-management-api.git
   cd project-management-api
   ```
2. **Install Dependencies**
   ```sh
   composer install
   ```
3. **Set Up Environment Variables**
   Copy `.env.example` to `.env` and configure database settings:
   ```sh
   cp .env.example .env
   ```
4. **Generate Application Key**
   ```sh
   php artisan key:generate
   ```
5. **Run Migrations and Seed Database**
   ```sh
   php artisan migrate --seed
   ```
6. **Install Laravel Passport**
   ```sh
   php artisan passport:install
   ```
7. **Run the Application**
   ```sh
   php artisan serve
   ```

## API Documentation
### Authentication
#### Register a User
- **Endpoint:** `POST /api/register`
- **Request Body:**
  ```json
  {
    "first_name": "John",
    "last_name": "Doe",
    "email": "john@example.com",
    "password": "password"
  }
  ```
- **Response:**
  ```json
  {
    "user": { "id": 1, "first_name": "John", "last_name": "Doe" },
    "token": "your-access-token"
  }
  ```

#### Login
- **Endpoint:** `POST /api/login`
- **Request Body:**
  ```json
  {
    "email": "john@example.com",
    "password": "password"
  }
  ```

#### Logout
- **Endpoint:** `POST /api/logout`
- **Requires:** Bearer Token Authentication

### Project Management
#### Get All Projects
- **Endpoint:** `GET /api/projects`

#### Create a Project
- **Endpoint:** `POST /api/projects`
- **Request Body:**
  ```json
  {
    "name": "Project A",
    "status": "Active"
  }
  ```

### EAV Attributes
#### Add a New Attribute
- **Endpoint:** `POST /api/attributes`
- **Request Body:**
  ```json
  {
    "name": "Department",
    "type": "text"
  }
  ```

#### Assign an Attribute to a Project
- **Endpoint:** `POST /api/attribute-values`
- **Request Body:**
  ```json
  {
    "attribute_id": 1,
    "entity_id": 1,
    "value": "IT"
  }
  ```

### Filtering Projects
- **Example:**
  ```sh
  GET /api/projects?filters[name]=ProjectA&filters[department]=IT
  ```

## Database Structure
- **users** (id, first_name, last_name, email, password)
- **projects** (id, name, status)
- **timesheets** (id, task_name, date, hours, user_id, project_id)
- **attributes** (id, name, type)
- **attribute_values** (id, attribute_id, entity_id, value)
- **project_user** (user_id, project_id)

## Test Credentials
- **Email:** `test@example.com`
- **Password:** `password`

## License
This project is licensed under the MIT License.
