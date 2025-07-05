# Rust Blog Platform

A full-featured blog platform built with Rust (Actix Web) backend and Next.js frontend, demonstrating modern web development practices with performance and security in mind.

![Rust](https://img.shields.io/badge/Rust-1.70%2B-orange)
![Actix Web](https://img.shields.io/badge/Actix%20Web-4.0%2B-blue)
![Next.js](https://img.shields.io/badge/Next.js-14.0%2B-black)
![TypeScript](https://img.shields.io/badge/TypeScript-5.0%2B-blue)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15.0%2B-blue)

## 📋 Table of Contents

- [Features](#features)
- [Architecture](#architecture)
- [Backend (Rust)](#backend-rust)
- [Frontend (Next.js)](#frontend-nextjs)
- [Database Schema](#database-schema)
- [Getting Started](#getting-started)
- [API Documentation](#api-documentation)
- [Security](#security)
- [Performance](#performance)
- [Testing](#testing)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [License](#license)

## ✨ Features

### Authentication & Authorization
- JWT-based authentication
- Role-based access control (User, Admin)
- Secure password hashing
- Protected routes and API endpoints

### User Profiles
- Complete user profile management
- Profile picture upload and management
- User information editing

### Blog Platform
- Create, read, update, and delete blog posts
- Rich content editor
- Image uploads for blog posts
- Comments system
- Like/favorite functionality
- Drafts support
- Search capabilities
- Tag and category support

### Admin Features
- User management dashboard
- Content moderation tools
- System statistics and monitoring

### Modern UI
- Responsive design
- Optimized for mobile and desktop
- Modern animations and transitions
- Dark/light mode support
- Accessibility compliant

## 🏗️ Architecture

The project follows a modern client-server architecture:

```
┌─────────────┐       ┌─────────────┐      ┌─────────────┐
│             │       │             │      │             │
│  Next.js    │◄─────►│  Rust API   │◄────►│ PostgreSQL  │
│  Frontend   │  HTTP │  Backend    │  SQL │  Database   │
│             │       │             │      │             │
└─────────────┘       └─────────────┘      └─────────────┘
```

- **Backend**: Rust with Actix Web framework, handling business logic, database operations, and API endpoints
- **Frontend**: Next.js with TypeScript, providing a responsive and interactive UI
- **Database**: PostgreSQL for reliable and scalable data storage
- **Authentication**: JWT tokens for stateless authentication
- **File Storage**: Local file system for user uploads (images, etc.)

## 🦀 Backend (Rust)

The backend is built with Rust and the Actix Web framework, providing a high-performance, secure API.

### Key Components

- **main.rs** - Application entry point and server configuration
- **middleware.rs** - Authentication and request processing middleware
- **handlers.rs** - API endpoint handlers
- **database.rs** - Database connection and query management
- **models.rs** - Data structures and database models
- **jwt.rs** - JWT token generation and validation

### Technologies Used

- **Actix Web** - High-performance web framework
- **tokio** - Asynchronous runtime
- **serde** - Serialization/deserialization
- **diesel** - ORM and query builder
- **jsonwebtoken** - JWT implementation
- **bcrypt** - Password hashing
- **dotenv** - Environment configuration

## ⚛️ Frontend (Next.js)

The frontend is built with Next.js and TypeScript, providing a modern, responsive user interface.

### Key Components

- **pages/** - Application routes and pages
  - **blog/** - Blog-related pages (index, create, edit, etc.)
  - **admin/** - Admin dashboard and tools
  - **auth/** - Authentication pages (login, register)
  - **profile/** - User profile management
  
- **components/** - Reusable UI components
  - **blog/** - Blog-specific components
  - **admin/** - Admin dashboard components
  
- **contexts/** - React context providers
  - **AuthContext** - Authentication state and methods
  
- **services/** - API client services
  - **auth.ts** - Authentication API methods
  - **blog.ts** - Blog API methods
  
- **types/** - TypeScript type definitions
  - **auth.ts** - Authentication-related types
  - **blog.ts** - Blog-related types

### Technologies Used

- **Next.js** - React framework with SSR and routing
- **TypeScript** - Type-safe JavaScript
- **Tailwind CSS** - Utility-first CSS framework
- **Axios** - HTTP client
- **React Hook Form** - Form handling
- **js-cookie** - Cookie management
- **date-fns** - Date formatting

## 🗄️ Database Schema

The application uses PostgreSQL with the following core tables:

- **users** - User accounts and authentication
- **profiles** - Extended user profile information
- **blog_posts** - Blog post content and metadata
- **comments** - User comments on blog posts
- **likes** - User likes/favorites for blog posts
- **tags** - Content categorization

## 🚀 Getting Started

### Prerequisites

- Rust (1.70 or newer)
- Node.js (18.0 or newer)
- PostgreSQL (15.0 or newer)
- Git

### Backend Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/rust-blog-platform.git
   cd rust-blog-platform
   ```

2. Set up the backend environment:
   ```bash
   cd backend
   cp .env.example .env  # Configure your environment variables
   ```

3. Set up the database:
   ```bash
   # Run the database setup script
   psql -U postgres -f BLOG_SCHEMA.sql
   ```

4. Build and run the backend:
   ```bash
   cargo run
   ```

### Frontend Setup

1. Set up the frontend environment:
   ```bash
   cd frontend
   cp .env.example .env.local  # Configure your environment variables
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Run the development server:
   ```bash
   npm run dev
   ```

4. Open [http://localhost:3000](http://localhost:3000) in your browser

## 📚 API Documentation

The API provides the following key endpoints:

### Authentication

- `POST /api/auth/register` - Register a new user
- `POST /api/auth/login` - Login and receive JWT token
- `GET /api/auth/me` - Get current user information

### User Profiles

- `GET /api/profile` - Get user profile
- `POST /api/profile` - Create user profile
- `PUT /api/profile` - Update user profile
- `POST /api/profile/picture` - Upload profile picture

### Blog

- `GET /api/blog/posts` - Get blog posts (with pagination)
- `POST /api/blog/posts` - Create new blog post
- `GET /api/blog/posts/{id}` - Get specific blog post
- `PUT /api/blog/posts/{id}` - Update blog post
- `DELETE /api/blog/posts/{id}` - Delete blog post
- `POST /api/blog/posts/{id}/image` - Upload blog post image
- `POST /api/blog/posts/{id}/comments` - Create comment
- `GET /api/blog/posts/{id}/comments` - Get post comments
- `POST /api/blog/posts/{id}/like` - Toggle like status

### Admin

- `GET /api/admin/users` - Get all users
- `GET /api/admin/users/{id}` - Get specific user
- `PUT /api/admin/users/{id}` - Update user
- `DELETE /api/admin/users/{id}` - Delete user

## 🔒 Security

- **Password Security**: Passwords are hashed using bcrypt
- **JWT Authentication**: Short-lived tokens with proper validation
- **CORS**: Properly configured for secure cross-origin requests
- **Input Validation**: All user inputs are validated and sanitized
- **Role-Based Access**: Endpoints protected based on user roles
- **SQL Injection Protection**: Prepared statements and ORM usage

## ⚡ Performance

The application is optimized for performance:

- **Rust Backend**: Extremely fast request processing
- **Connection Pooling**: Efficient database connection management
- **SSR & Static Generation**: Next.js optimizations for fast page loads
- **Image Optimization**: Proper sizing and compression
- **Lazy Loading**: Components and images loaded as needed

## 🧪 Testing

The project includes several testing scripts and methodologies:

- **Unit Tests**: For testing individual functions and components
- **Integration Tests**: For testing API endpoints
- **Load Tests**: For performance evaluation
- **Database Tests**: For verifying data integrity

Various test scripts are included in the project root, such as:
- `test_backend.ps1`
- `test_blog_api.ps1`
- `benchmark_test.ps1`
- And more...

## 📦 Deployment

The application can be deployed using various methods:

### Backend

- Compile for production:
  ```bash
  cd backend
  cargo build --release
  ```

- Run the production binary:
  ```bash
  ./target/release/auth_backend
  ```

### Frontend

- Build for production:
  ```bash
  cd frontend
  npm run build
  ```

- Start the production server:
  ```bash
  npm start
  ```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

Built with ❤️ using Rust and Next.js
