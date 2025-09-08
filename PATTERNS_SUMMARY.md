# Design Patterns Summary - OOP Casino Project

## Question: What types of patterns are used in this project?

This Spring Boot casino application implements **15+ design patterns** across multiple categories:

## 🏗️ Architectural Patterns
- **MVC (Model-View-Controller)** - Core application structure
- **Layered Architecture** - Separation into presentation, business, and data layers

## 🔨 Creational Patterns
- **Dependency Injection** - Spring IoC container
- **Builder Pattern** - Lombok and Spring configuration

## 🔧 Structural Patterns
- **Repository Pattern** - Data access abstraction (`UserRepo`, `GameSessionRepo`)
- **Facade Pattern** - Controllers simplify complex subsystems
- **DTO (Data Transfer Object)** - Payload classes for data transfer

## 🎯 Behavioral Patterns
- **Strategy Pattern** - Different game implementations
- **Template Method** - Security configuration
- **Filter Pattern** - JWT authentication chain

## 💾 Persistence Patterns
- **Entity Pattern** - JPA entities (`@Entity` classes)
- **Active Record** - ORM functionality

## 🏢 Enterprise Patterns
- **Service Layer** - Business logic encapsulation
- **Configuration Pattern** - Spring configuration classes

## 🔐 Security Patterns
- **Authentication Filter** - JWT token validation
- **Authorization Pattern** - Role-based access control

## 🌱 Spring Framework Patterns
- **Inversion of Control (IoC)** - Container-managed dependencies
- **Proxy Pattern** - AOP and security proxies
- **Aspect-Oriented Programming** - Cross-cutting concerns

## Pattern Implementation Examples

### Repository Pattern
```java
public interface UserRepo extends JpaRepository<User, Long> {
    Optional<User> findByUsername(String username);
}
```

### DTO Pattern
```java
public class LoginRequest {
    @NotBlank
    private String usernameOrEmail;
    @NotBlank  
    private String password;
}
```

### Service Layer Pattern
```java
@Service
public class GameService {
    @Autowired
    private GameSessionRepo gameSessionRepository;
    
    public GameSession playSlots(User user, Double betAmount) {
        // Business logic here
    }
}
```

### MVC Pattern
- **Model**: `User.java`, `GameSession.java`
- **View**: REST API endpoints (JSON)
- **Controller**: `AuthController.java`, `GameController.java`

## Benefits
- ✅ **Maintainable** code structure
- ✅ **Testable** through dependency injection
- ✅ **Scalable** layered architecture
- ✅ **Secure** authentication and authorization
- ✅ **Reusable** components

## Conclusion
This project demonstrates a **comprehensive implementation of enterprise design patterns** using Spring Boot framework, showcasing modern Java development best practices for building scalable, maintainable web applications.