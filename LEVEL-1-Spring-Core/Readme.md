# 🟢 LEVEL 1: Spring Core (The Heart ❤️)


Perfect — now we’ll **lock this in as a true “Spill the Beans”–level explanation** 🫘  
I’ll walk through **Spring Core end-to-end**, **structured for future expansion**, and **every section will include simple + real examples** so it’s _intuitive_, not abstract.

I’ll keep it **cleanly layered**, so later you can go deeper **without rewriting anything**.


Think of Spring Core as the **engine room** of Spring.

Everything else (Boot, MVC, Security, JPA) **plugs into this engine**.

* * *

### 🔷 BIG MENTAL MODEL (START HERE)


Spring Core exists to solve one problem:

> **Managing object creation, wiring, lifecycle, and behavior in large applications**

Spring Core =  
**IoC + DI + Container + Lifecycle + Extension Points**

Keep this mental image in mind:

```
ApplicationContext
 ├── Bean Definitions (metadata)
 ├── Dependency Graph
 ├── Bean Factory
 ├── Lifecycle Manager
 └── Proxy Engine
```

* * *

## 1️⃣ IoC – Inversion of Control


### WHAT (Simple)


Normally **you create objects**.  
With Spring, **the framework creates them**.

Control is inverted.

* * *

### WHY IoC EXISTS

![but why](/src/cruftbox-but-why.gif)


### Without IoC

```java
class OrderService {
    private OrderRepository repo = new OrderRepository();
}
```

Problems:

*   Tightly coupled
*   Hard to test
*   Hard to replace implementations

* * *

### With IoC

```java
@Service
class OrderService {
    private final OrderRepository repo;

    OrderService(OrderRepository repo) {
        this.repo = repo;
    }
}
```

Spring:

*   Creates `OrderRepository`
*   Creates `OrderService`
*   Injects repository

📌 **You describe relationships, Spring handles creation.**

* * *

### HOW IoC Works (Conceptually)


1.  You describe beans (annotations / config)
2.  Spring reads descriptions
3.  Spring creates and wires objects

📌IoC is a **design principle**.  
📌Spring is one **implementation**.

* * *

## 2️⃣ IoC Containers (HOW IoC IS IMPLEMENTED)


### IoC needs a **container**.

* * *

### 2.1 `BeanFactory` (Basic Container)


### WHAT

Minimal object factory.

### HOW

```java
BeanFactory factory =
    new ClassPathXmlApplicationContext("beans.xml");

MyBean bean = factory.getBean(MyBean.class);
```

*   Beans created **only when requested**
*   Mostly lazy

📌 Rarely used today.

* * *

### 2.2 `ApplicationContext` (Real Container)


### WHAT❓

Enterprise-grade IoC container.

### HOW❓

```java
ApplicationContext context =
    new AnnotationConfigApplicationContext(AppConfig.class);
```

Spring Boot does this automatically.

### WHY IT’S USED❓

*   Eager initialization
*   Full lifecycle
*   AOP support
*   Events
*   Validation

📌 **Spring Boot always uses `ApplicationContext`.**

* * *

## 3️⃣ Bean Model (WHAT SPRING MANAGES)


### WHAT IS A BEAN ❓


A bean is:

> A normal Java object managed by Spring.

Nothing special.

* * *

### Example

```java
@Component
class PaymentService {}
```

Spring:

*   Knows about it
*   Creates it
*   Manages it

* * *

### Bean Definition (IMPORTANT INTERNAL IDEA)


Spring does **not** start by creating objects.

It first creates **BeanDefinitions** (metadata).

### Example (Conceptual)

```text
BeanDefinition:
- class: PaymentService
- scope: singleton
- dependencies: none
- lazy: false
```

📌 This separation enables:

*   Dependency analysis
*   Proxy creation
*   Lifecycle control

* * *

## 4️⃣ Dependency Injection (DI)


### WHAT (Simple)


Objects get dependencies **from outside**, not by creating them.

* * *

### Bad (No DI)

```java
class UserService {
    UserRepository repo = new UserRepository();
}
```

* * *

### Good (DI)

```java
class UserService {
    private final UserRepository repo;

    UserService(UserRepository repo) {
        this.repo = repo;
    }
}
```

Spring injects `UserRepository`.

* * *

WHY DI EXISTS
-------------

*   Loose coupling
*   Easy testing
*   Swappable implementations

* * *

### HOW DI WORKS (Internally)


Spring:

1.  Finds constructor parameters
2.  Searches matching beans
3.  Resolves ambiguity
4.  Injects dependencies

* * *

## 5️⃣ Types of Dependency Injection (WITH EXAMPLES)


### 5.1 Constructor Injection (Preferred)


```java
@Service
class OrderService {
    private final OrderRepository repo;

    OrderService(OrderRepository repo) {
        this.repo = repo;
    }
}
```

WHY:

*   Mandatory dependencies
*   Fail fast
*   Immutable
*   Testable

* * *

### 5.2 Setter Injection


```java
@Service
class OrderService {
    private OrderRepository repo;

    @Autowired
    void setRepo(OrderRepository repo) {
        this.repo = repo;
    }
}
```

Use when dependency is optional.

* * *

### 5.3 Field Injection (Avoid)


```java
@Autowired
private OrderRepository repo;
```

Problems:

*   Hidden dependencies
*   Runtime failures
*   Hard testing

* * *

## 6️⃣ ApplicationContext (CORE BRAIN)


### WHAT IT DOES


*   Stores bean definitions
*   Creates beans
*   Injects dependencies
*   Applies lifecycle hooks
*   Wraps proxies

Think of it as:

```text
Smart Map + Lifecycle Engine
```

* * *

## 7️⃣ Bean Lifecycle (STEP-BY-STEP WITH EXAMPLE)

### Example Bean

```java
@Component
class ExampleBean {

    @PostConstruct
    void init() {
        System.out.println("Initialized");
    }

    @PreDestroy
    void destroy() {
        System.out.println("Destroyed");
    }
}
```

### Lifecycle Flow

1.  BeanDefinition created
2.  Bean instantiated
3.  Dependencies injected
4.  `@PostConstruct` called
5.  Bean ready
6.  App runs
7.  `@PreDestroy` called on shutdown

📌 AOP & transactions hook into this lifecycle.

* * *

## 8️⃣ Bean Scopes (WITH EXAMPLES)


### Singleton (Default)


```java
@Component
class UserService {}
```

*   One instance per container

* * *

### Prototype


```java
@Component
@Scope("prototype")
class TempObject {}
```

*   New instance every request
*   Spring does not manage destruction

* * *

## 9️⃣ Component Scanning


### HOW SPRING FINDS BEANS


```java
@Component
@Service
@Repository
@Controller
```

Spring scans packages and registers beans.

📌 Wrong package structure = missing beans.

* * *

## 🔟 Bean Creation Process (ENGINE VIEW)


### Example Dependency Graph

```text
Controller → Service → Repository
```

Spring creates:

1.  Repository
2.  Service
3.  Controller

In that order.

* * *

## 1️⃣1️⃣ Dependency Resolution Rules


Example:

```java
@Autowired
PaymentService service;
```

Spring resolves:

1.  By type
2.  [@Qualifier](https://github.com/HarshalMPatil20/Spill-The-Beans/blob/main/LEVEL-1-Spring-Core/Qualifier%20VS%20Primary.md#-qualifier--explicit-choice)
3.  [@Primary](https://github.com/HarshalMPatil20/Spill-The-Beans/blob/main/LEVEL-1-Spring-Core/Qualifier%20VS%20Primary.md#-primary--default-choice)
4.  Bean name

Ambiguity → startup failure.

* * *

## 1️⃣2️⃣ [Circular Dependencies](https://github.com/HarshalMPatil20/Spill-The-Beans/blob/main/LEVEL-1-Spring-Core/Circular-dependencies.md#-circular-dependency-in-spring)


```java
A → B
B → A
```

*   Setter/field injection: works
*   Constructor injection: fails

📌 Design smell → refactor.

* * *

## 1️⃣3️⃣ [Lazy vs Eager Initialization](https://github.com/HarshalMPatil20/Spill-The-Beans/blob/main/LEVEL-1-Spring-Core/Lazy-vs-eager-initialization.md#-lazy-vs-eager-initialization-spring)


```java
@Lazy
@Component
class HeavyBean {}
```

*   Eager (default): fail fast
*   Lazy: faster startup, risk runtime failure

* * *

## 1️⃣4️⃣ Extension Points (WHY SPRING IS POWERFUL)


### Examples: 
[`BeanPostProcessor`,
`BeanFactoryPostProcessor`,
`BeanDefinitionRegistryPostProcessor`](https://github.com/HarshalMPatil20/Spill-The-Beans/blob/main/LEVEL-1-Spring-Core/BeanPostProcessors.md#%EF%B8%8F-beandefinitionregistrypostprocessor)

Spring uses this to:
*   Add behavior (AOP, transactions)
*   Modify beans before creation


📌 This is how Spring adds behavior **without touching your code**.

* * *

## 🚨 Common Spring Core Exception


### `NoSuchBeanDefinitionException`


WHY:

*   Bean not scanned
*   Wrong qualifier
*   Profile mismatch

HOW TO DEBUG:

*   Check annotations
*   Check package scan
*   Check profiles

* * *

## 🧠 FINAL SPRING CORE MAP (EXPANDABLE)


```
Spring Core
 ├── IoC & Containers
 ├── Bean Model
 ├── Dependency Injection
 ├── Lifecycle & Scopes
 ├── Creation & Resolution Engine
 └── Extension Points
```


