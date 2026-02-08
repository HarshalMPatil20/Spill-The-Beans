<svg xmlns="http://www.w3.org/2000/svg" x="0px" y="0px" width="100" height="100" viewBox="0,0,256,256">
<g fill="none" fill-rule="nonzero" stroke="none" stroke-width="1" stroke-linecap="butt" stroke-linejoin="miter" stroke-miterlimit="10" stroke-dasharray="" stroke-dashoffset="0" font-family="none" font-weight="none" font-size="none" text-anchor="none" style="mix-blend-mode: normal"><g transform="scale(5.33333,5.33333)"><path d="M43.982,23.635c0.069,-4.261 -0.891,-9.328 -2.891,-15.273l-1.568,-4.662l-2.13,4.433c-0.114,0.237 -0.244,0.469 -0.38,0.698c-3.499,-3.004 -8.039,-4.831 -13.013,-4.831c-11.046,0 -20,8.954 -20,20c0,11.046 8.954,20 20,20c11.046,0 20,-8.954 20,-20c0,-0.123 -0.016,-0.242 -0.018,-0.365z" fill="#6ead25"></path><path d="M39.385,32.558c-3.123,4.302 -8.651,4.533 -13.854,4.442h-6.781h-1.938c4.428,-1.593 7.063,-1.972 9.754,-3.4c5.068,-2.665 10.078,-8.496 11.121,-14.562c-1.93,5.836 -7.779,10.85 -13.109,12.889c-3.652,1.393 -10.248,2.745 -10.248,2.745l-0.267,-0.145c-4.49,-2.259 -4.626,-12.313 3.537,-15.559c3.574,-1.423 6.993,-0.641 10.854,-1.593c4.122,-1.012 8.89,-4.208 10.83,-8.375c2.172,6.667 4.786,17.106 0.101,23.558zM15.668,38.445c-0.282,0.35 -0.713,0.555 -1.163,0.555c-0.823,0 -1.495,-0.677 -1.495,-1.5c0,-0.823 0.677,-1.5 1.495,-1.5c0.341,0 0.677,0.118 0.941,0.336c0.64,0.519 0.74,1.469 0.222,2.109z" fill="#ffffff"></path></g></g>
</svg>

# Spill The Beans

<div class="tenor-gif-embed" data-postid="4925094154314135136" data-share-method="host" data-aspect-ratio="2.39423" data-width="100%">
  <a href="https://tenor.com/view/wolf-of-wall-street-wall-street-leonardo-dicaprio-cheering-chanting-gif-4925094154314135136">Wolf Of Wall Street Leonardo Dicaprio GIF</a>from <a href="https://tenor.com/search/wolf+of+wall+street-gifs">Wolf Of Wall Street GIFs</a>
</div>
<script type="text/javascript" async src="https://tenor.com/embed.js"></script>


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

## 🟢 LEVEL 0: Prerequisites (Foundation)

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
