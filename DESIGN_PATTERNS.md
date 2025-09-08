# Design Patterns Used in OOP Casino Project

This document provides a comprehensive overview of the design patterns implemented in the OOP Casino Spring Boot application.

## 1. Architectural Patterns

### Model-View-Controller (MVC) Pattern
The application follows the MVC architectural pattern:

- **Models**: Located in `src/main/java/org/example/groupassignment/models/`
  - `User.java` - Represents user entities
  - `GameSession.java` - Represents game session entities

- **Controllers**: Located in `src/main/java/org/example/groupassignment/controllers/`
  - `AuthController.java` - Handles authentication endpoints
  - `GameController.java` - Manages game-related operations  
  - `UserController.java` - Handles user management operations

- **View**: REST API endpoints (JSON responses) - no traditional web views

### Layered Architecture Pattern
The application is organized into distinct layers:

```
┌─────────────────┐
│   Controllers   │ (Presentation Layer)
├─────────────────┤
│    Services     │ (Business Logic Layer)
├─────────────────┤
│  Repositories   │ (Data Access Layer)
├─────────────────┤
│    Models       │ (Domain/Entity Layer)
└─────────────────┘
```

## 2. Creational Patterns

### Dependency Injection Pattern
Implemented through Spring Framework's IoC container:

```java
@RestController
public class AuthController {
    @Autowired
    private AuthService authService;
    
    @Autowired
    private JwtTokenProvider tokenProvider;
}
```

### Builder Pattern (Implicit)
- Lombok's `@Data` annotation provides builder-like functionality
- Spring Boot configuration uses builder patterns internally

## 3. Structural Patterns

### Repository Pattern
Abstracts data access logic from business logic:

```java
public interface UserRepo extends JpaRepository<User, Long> {
    Optional<User> findByUsername(String username);
    Boolean existsByUsername(String username);
    Boolean existsByEmail(String email);
}
```

```java
public interface GameSessionRepo extends JpaRepository<GameSession, Long> {
    List<GameSession> findByUser(User user);
}
```

### Facade Pattern
Controllers act as facades, providing simplified interfaces:

```java
@RestController
@RequestMapping("/api/auth")
public class AuthController {
    @PostMapping("/login")
    public ResponseEntity<?> authenticateUser(@Valid @RequestBody LoginRequest loginRequest) {
        String jwt = authService.authenticateUser(loginRequest);
        return ResponseEntity.ok(new JwtAuthenticationResponse(jwt));
    }
}
```

### Data Transfer Object (DTO) Pattern
Located in `src/main/java/org/example/groupassignment/payload/`:

- `LoginRequest.java` - For login data transfer
- `SignUpRequest.java` - For registration data transfer
- `ApiResponse.java` - For standardized API responses
- `JwtAuthenticationResponse.java` - For JWT token responses
- `UserSummary.java` - For user data transfer

## 4. Behavioral Patterns

### Strategy Pattern (Implicit)
Different game types can be implemented as strategies:

```java
@Service
public class GameService {
    public GameSession playSlots(User user, Double betAmount) {
        // Slots game strategy implementation
    }

    public GameSession playBlackWhite(User user, Double betAmount, String choice) {
        // Black/White game strategy implementation  
    }
}
```

### Template Method Pattern
Spring Security configuration follows template method pattern:

```java
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        // Template method implementation
    }
}
```

### Filter Pattern (Chain of Responsibility)
JWT Authentication filter in the security chain:

```java
public class JwtAuthenticationFilter extends OncePerRequestFilter {
    @Override
    protected void doFilterInternal(HttpServletRequest request,
                                    HttpServletResponse response, 
                                    FilterChain filterChain) {
        // Filter implementation
    }
}
```

## 5. Persistence Patterns

### Entity Pattern
JPA entities with proper annotations:

```java
@Data
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(unique = true)
    private String username;
    // ... other fields
}
```

### Active Record Pattern (via JPA)
Entities are mapped to database tables with ORM functionality

## 6. Enterprise Patterns

### Service Layer Pattern
Business logic encapsulated in service classes:

```java
@Service
public class UserService {
    @Autowired
    private UserRepo userRepository;
    
    public User registerUser(User user) {
        // Business logic implementation
    }
}
```

### Configuration Pattern
Spring configuration classes:

```java
@EnableWebSecurity
public class SecurityConfig {
    @Bean
    public JwtAuthenticationFilter jwtAuthenticationFilter() {
        return new JwtAuthenticationFilter();
    }
}
```

## 7. Security Patterns

### Authentication Filter Pattern
JWT-based authentication filtering

### Authorization Pattern
Role-based access control (intended with `@PreAuthorize`)

## 8. Spring Framework Patterns

### Inversion of Control (IoC)
Spring container manages object lifecycle and dependencies

### Aspect-Oriented Programming (AOP)
Implicit through Spring Security and transaction management

### Proxy Pattern
Spring uses proxies for:
- Security enforcement
- Transaction management
- Repository implementations

## Pattern Benefits in This Project

1. **Separation of Concerns**: Each layer has distinct responsibilities
2. **Maintainability**: Clear structure makes code easy to modify
3. **Testability**: Dependency injection enables easy mocking
4. **Scalability**: Layered architecture supports growth
5. **Security**: Filter and configuration patterns provide robust security
6. **Data Integrity**: Repository pattern ensures consistent data access

## Technology Stack Supporting Patterns

- **Spring Boot**: Provides framework for most patterns
- **Spring Security**: Implements security patterns
- **Spring Data JPA**: Enables repository pattern
- **Lombok**: Reduces boilerplate code
- **Maven**: Dependency management
- **PostgreSQL**: Data persistence

This architecture demonstrates a well-structured enterprise application following established design patterns and best practices.