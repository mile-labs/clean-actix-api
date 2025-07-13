# Clean Actix API

A clean, well-structured REST API built with Actix Web and Diesel ORM, following clean architecture principles. This project was generated using the [cookiecutter-rust-actix-clean-architecture](https://github.com/mile-labs/cookiecutter-rust-actix-clean-architecture) template.

## 🚀 Features

- **RESTful API** with Actix Web framework
- **PostgreSQL** database with Diesel ORM
- **Clean Architecture** with clear separation of concerns
- **Dependency Injection** container pattern
- **Database Migrations** with Diesel
- **Comprehensive Testing** with testcontainers
- **Logging** and error handling
- **Maintenance Mode** support

## 📋 Prerequisites

- Rust (latest stable version)
- PostgreSQL
- Docker (for running tests with testcontainers)

## 🎯 About This Template

This project was generated using the [cookiecutter-rust-actix-clean-architecture](https://github.com/mile-labs/cookie-labs/cookiecutter-rust-actix-clean-architecture) template, which provides:

- **Clean Architecture** implementation with proper layer separation
- **Dependency Injection** container pattern
- **Repository Pattern** for data access
- **Service Layer** for business logic
- **DTO Pattern** for API data transfer
- **Comprehensive Testing** setup with testcontainers
- **Database Migrations** with Diesel ORM
- **Error Handling** with custom error types
- **Logging** configuration
- **Middleware** support

## 🛠️ Installation & Setup

### 1. Clone the repository

```bash
git clone <repository-url>
cd actix-demo
```

### 2. Set up environment variables

Create a `.env` file in the root directory:

```bash
DATABASE_URL=postgres://username:password@localhost/actix_demo
RUST_LOG=info
```

### 3. Set up the database

```bash
# Install Diesel CLI (if not already installed)
cargo install diesel_cli --no-default-features --features postgres

# Run database migrations
diesel migration run
```

### 4. Run the application

```bash
cargo run
```

The server will start on `http://127.0.0.1:8080`

## 🧪 Running Tests

```bash
# Run all tests
cargo test

# Run tests with output
cargo test -- --nocapture
```

## 📚 API Documentation

### Base URL
```
http://127.0.0.1:8080
```

### Endpoints

#### Todos

| Method   | Endpoint      | Description                    |
| -------- | ------------- | ------------------------------ |
| `GET`    | `/todos`      | List all todos with pagination |
| `POST`   | `/todos`      | Create a new todo              |
| `GET`    | `/todos/{id}` | Get a specific todo by ID      |
| `DELETE` | `/todos/{id}` | Delete a todo by ID            |

#### Request/Response Examples

**Create Todo**
```bash
POST /todos
Content-Type: application/json

{
  "title": "Buy groceries",
  "description": "Milk, bread, eggs"
}
```

**Response**
```json
{
  "id": 1,
  "title": "Buy groceries",
  "description": "Milk, bread, eggs",
  "completed": false
}
```

**List Todos**
```bash
GET /todos?page=1&limit=10
```

**Response**
```json
{
  "total": 25,
  "items": [
    {
      "id": 1,
      "title": "Buy groceries",
      "description": "Milk, bread, eggs",
      "completed": false
    }
  ]
}
```

## 🏗️ Project Structure

```
src/
├── api/                    # API layer
│   ├── controllers/        # HTTP handlers
│   ├── dto/               # Data Transfer Objects
│   └── middleware/        # Custom middleware
├── domain/                 # Domain layer
│   ├── models/            # Domain entities
│   ├── repositories/      # Repository interfaces
│   └── services/          # Business logic
├── infrastructure/         # Infrastructure layer
│   ├── databases/         # Database connections
│   ├── models/            # Database models
│   ├── repositories/      # Repository implementations
│   └── services/          # External service implementations
├── container.rs           # Dependency injection container
├── create_app.rs          # Application factory
└── main.rs               # Application entry point
```

## 🔧 Configuration

### Environment Variables

- `DATABASE_URL`: PostgreSQL connection string
- `RUST_LOG`: Logging level (debug, info, warn, error)

### Database Schema

The application uses two main tables:

- `todos`: Stores todo items with id, title, description, and completed status
- `service_contexts`: Stores application context like maintenance mode

## 🧪 Testing

The project includes comprehensive tests using testcontainers for isolated database testing:

- API integration tests
- Repository tests
- Service layer tests

Run tests with:
```bash
cargo test
```

## 🚀 Deployment

### Using Docker

```dockerfile
FROM rust:1.70 as builder
WORKDIR /usr/src/app
COPY . .
RUN cargo build --release

FROM debian:bullseye-slim
RUN apt-get update && apt-get install -y libpq-dev && rm -rf /var/lib/apt/lists/*
COPY --from=builder /usr/src/app/target/release/clean-actix-api /usr/local/bin/
CMD ["clean-actix-api"]
```

### Environment Setup

Ensure your production environment has:
- PostgreSQL database
- Proper environment variables
- Database migrations run

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Run the test suite
6. Submit a pull request

## 📚 Template Information

This project is based on the [cookiecutter-rust-actix-clean-architecture](https://github.com/mile-labs/cookiecutter-rust-actix-clean-architecture) template by Mile Labs. The template provides a solid foundation for building scalable Actix Web applications with clean architecture principles.

### Template Features:
- **Domain-Driven Design** with clear boundaries
- **Hexagonal Architecture** implementation
- **Test-Driven Development** ready setup
- **Production-Ready** configuration
- **Best Practices** for Rust web development

For more information about the template and its features, visit the [template repository](https://github.com/mile-labs/cookiecutter-rust-actix-clean-architecture).

## 📄 License

This project is licensed under the MIT License.

## 🐛 Troubleshooting

### Common Issues

**Database Connection Issues**
- Ensure PostgreSQL is running
- Verify DATABASE_URL in .env file
- Check database permissions

**Migration Issues**
- Run `diesel setup` to initialize Diesel
- Ensure database exists before running migrations

**Compilation Issues**
- Update Rust to latest stable version
- Run `cargo clean` and rebuild

## 📞 Support

For issues and questions, please open an issue on the repository. 