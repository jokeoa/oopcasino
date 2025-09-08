# OOP Casino - Spring Boot Application

A casino gaming application built with Spring Boot demonstrating object-oriented programming principles and design patterns.

## Features

- User authentication and registration
- JWT-based security
- Multiple casino games (Slots, Black/White)
- User balance management
- Game session tracking

## Technology Stack

- **Java 17**
- **Spring Boot 3.4.1**
- **Spring Security** - Authentication and authorization
- **Spring Data JPA** - Data persistence
- **PostgreSQL** - Database
- **JWT** - Token-based authentication
- **Lombok** - Reducing boilerplate code
- **Maven** - Dependency management

## Architecture

This application follows a layered architecture with clear separation of concerns:

```
Controllers → Services → Repositories → Database
```

## Design Patterns

This project implements multiple design patterns following enterprise best practices. For a comprehensive overview of all design patterns used in this application, see:

**[📋 Design Patterns Documentation](DESIGN_PATTERNS.md)**

### Key Patterns Include:

- **MVC (Model-View-Controller)** - Application structure
- **Repository Pattern** - Data access abstraction
- **Service Layer Pattern** - Business logic encapsulation
- **DTO Pattern** - Data transfer objects
- **Dependency Injection** - IoC container management
- **Filter Pattern** - Security filtering
- **And many more...** (see full documentation)

## Project Structure

```
src/main/java/org/example/groupassignment/
├── controllers/          # REST API endpoints
│   ├── AuthController.java
│   ├── GameController.java
│   └── UserController.java
├── models/              # Entity classes
│   ├── User.java
│   └── GameSession.java
├── repositories/        # Data access layer
│   ├── UserRepo.java
│   └── GameSessionRepo.java
├── services/           # Business logic layer
│   ├── UserService.java
│   └── GameService.java
├── security/           # Security configuration
│   ├── SecurityConfig.java
│   └── JwtAuthenticationFilter.java
├── payload/            # DTOs and request/response objects
│   ├── LoginRequest.java
│   ├── SignUpRequest.java
│   ├── ApiResponse.java
│   └── ...
└── GroupassignmentApplication.java  # Main application class
```

## Getting Started

### Prerequisites

- Java 17+
- Maven 3.6+
- PostgreSQL database

### Running the Application

1. Clone the repository
2. Configure database connection in `application.yml`
3. Build the project:
   ```bash
   mvn clean compile
   ```
4. Run the application:
   ```bash
   mvn spring-boot:run
   ```

## API Endpoints

### Authentication
- `POST /api/auth/login` - User login
- `POST /api/auth/signup` - User registration

### Games
- `POST /api/game/slots` - Play slots game
- `POST /api/game/blackwhite` - Play black/white game

### User Management
- `GET /api/user/profile` - Get user profile
- `GET /api/user/balance` - Get user balance
- `GET /api/user/history` - Get game history

## Contributing

When contributing to this project, please maintain the existing design patterns and architectural principles. Refer to the [Design Patterns Documentation](DESIGN_PATTERNS.md) to understand the current structure.

## License

This project is part of a group assignment demonstrating OOP principles and design patterns.