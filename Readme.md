
# 🍃 Spill The Beans

![alt text](/src/wolf-of-wall-street-wall-street.gif)


> _Demystifying Spring Boot — no magic, just beans._

Spring Boot feels magical…  
until it throws a `NoSuchBeanDefinitionException` at 2 AM.

**Spill the Beans** exists to remove the magic, expose the internals,  
and help you understand **why things work — and why they break**.

This repository is a **zero-to-production Spring Boot mastery roadmap**,  
designed for developers who want to go beyond tutorials and actually
**think like Spring**.

&nbsp;


# 🛣️ Roadmap

## 🟢 [LEVEL 0: Prerequisites (Foundation)](https://github.com/HarshalMPatil20/Spill-The-Beans/tree/3b327242aa41335ce95da33c5868197a75e3bbbf/LEVEL-0-Prerequisites)

### Must Know

- Core Java
  - OOP (interfaces, abstraction)
  - Collections
  - Exceptions (checked vs unchecked)
- JVM basics (heap, stack, GC – conceptual)
- SQL basics
- HTTP & REST fundamentals
- Maven / Gradle

🎯 Goal: Understand what Spring abstracts for you.

---

## 🟢 LEVEL 1: Spring Core (The Heart)

### Concepts

- Inversion of Control (IoC)
- Dependency Injection (DI)
- `ApplicationContext`
- Bean lifecycle
- Bean scopes
- Constructor vs Field Injection

### Internals

- Bean creation process
- Dependency resolution
- Lazy vs eager initialization

🎯 You’re strong when:

- You can debug `NoSuchBeanDefinitionException`
- You can explain why constructor injection is preferred

---

## 🟢 LEVEL 2: Spring Boot Internals (Magic Explained)

### Concepts

- `@SpringBootApplication`
- Auto-configuration
- Starter dependencies
- External configuration
- Profiles (dev / test / prod)

### Internals

- Conditional annotations
- Classpath scanning
- Configuration precedence

🎯 You’re strong when:

- You know why a bean exists without defining it

---

## 🟢 LEVEL 3: Spring MVC (Request Lifecycle Mastery)

### Concepts

- Servlet container (Tomcat)
- Filters vs Interceptors vs AOP
- DispatcherServlet
- HandlerMapping
- HandlerAdapter
- Controllers

### Core Flow

```text
Client → Filters → DispatcherServlet → Controller → Service → Repository → Database
```

🎯 You’re strong when:

- You can explain 401 vs 403 vs 404
- You know why a controller is not hit

---

## 🟢 LEVEL 4: Data Binding & Validation

### Concepts

- `@RequestBody`
- JSON ↔ Java (Jackson)
- `@Valid`
- Custom validators
- Global exception handling

### Internals

- HttpMessageConverters
- MethodArgumentResolver

🎯 You’re strong when:

- You can debug `400 Bad Request`

---

## 🟢 LEVEL 5: AOP (Real Power of Spring)

### Concepts

- Proxy pattern
- JDK vs CGLIB proxies
- Cross-cutting concerns
- Self-invocation problem

### Annotations

- `@Transactional`
- `@Async`
- `@Cacheable`
- `@PreAuthorize`

🎯 You’re strong when:

- You know why annotations sometimes don’t work

---

## 🟢 LEVEL 6: JPA & Database (Real-World Core)

### Core JPA

- Entity lifecycle
- Persistence Context
- Dirty checking

### Relationships

- OneToMany / ManyToOne
- FetchType (Lazy vs Eager)
- Cascading rules

### Performance

- N+1 problem
- Pagination
- Batch operations

🎯 You’re strong when:

- You can fix N+1 without Googling

---

## 🟢 LEVEL 7: Transactions (Data Safety)

### Concepts

- Propagation
- Isolation levels
- Rollback rules
- Read-only transactions

### Internals

- PlatformTransactionManager
- Transaction boundaries

🎯 You’re strong when:

- You know where a transaction actually starts

---

## 🟢 LEVEL 8: Spring Security (Filter + AOP)

### Concepts

- Authentication vs Authorization
- SecurityContext
- Filter chain

### Implementations

- Form login
- JWT authentication
- Method-level security

### Security Flow

```text
Security Filter → DispatcherServlet → AOP (@PreAuthorize)
```

🎯 You’re strong when:

- You can explain the security filter chain
- You know why method-level security works
- You know where security blocks a request

---

## 🟢 LEVEL 9: Performance & Scalability

### Concepts

- Caching (Redis)
- Async execution
- Thread pools
- Connection pooling (HikariCP)

🎯 You’re strong when:

- You design for high traffic without thread starvation

---

## 🟢 LEVEL 10: Testing (Senior Skill)

### Concepts

- Unit tests vs Integration tests
- Mocking strategies
- Slice testing

### Annotations

- `@SpringBootTest`
- `@WebMvcTest`
- `@DataJpaTest`

🎯 You’re strong when:

- Tests are fast and focused

---

## 🟢 LEVEL 11: Production Readiness

### Concepts

- Actuator
- Logging strategies
- External configuration
- Docker basics
- CI/CD awareness

🎯 You’re strong when:

- You can debug production issues

---

## 🟡 LEVEL 12: Advanced / Edge Concepts (Optional)

> These are **extensions**, not missing basics.

### Spring Internals

- BeanPostProcessor
- Custom scopes

### Event-Driven Programming

- ApplicationEventPublisher
- `@EventListener`

### Configuration Internals

- Environment
- PropertySource priority

### Reactive Stack (Parallel World)

- WebFlux
- Mono / Flux

### Native / AOT

- Spring AOT
- GraalVM

🎯 Learn these only when required.

---

## 🧠 Master Memory Line

```java
JAVA → CORE → BOOT → MVC → AOP → JPA → TX → SECURITY → PERF → TEST → PROD
```

&nbsp;
# 📚 Resources
- [Spring Framework Documentation](https://docs.spring.io/spring-framework/docs/current/reference/html/)
- [Spring Boot Documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/)
- [Baeldung Spring Tutorials](https://www.baeldung.com/spring-tutorials)
- [Spring in Action (Book)](https://www.manning.com/books/spring-in-action-fifth-edition)
- [Spring Boot in Action (Book)](https://www.manning.com/books/spring-boot-in-action)
