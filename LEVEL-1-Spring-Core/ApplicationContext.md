# 🌱 ApplicationContext (Spring)

## 🧠 What is `ApplicationContext`?

`ApplicationContext` is the **central container** in Spring that:

- Creates beans
- Manages their lifecycle
- Injects dependencies
- Applies AOP, transactions, security
- Provides configuration & events

> **In one line:**  
> **“ApplicationContext is the brain of a Spring application.”**

---

## 🔁 Where it fits (BIG PICTURE)

```
Spring Boot App Starts
   ↓
ApplicationContext is created
   ↓
Bean definitions loaded
   ↓
PostProcessors run
   ↓
Beans created & wired
   ↓
Application ready
```

👉 **Nothing in Spring works without ApplicationContext**

---

## 🆚 ApplicationContext vs BeanFactory

| Feature              | BeanFactory     | ApplicationContext |
| -------------------- | --------------- | ------------------ |
| Type                 | Basic container | Advanced container |
| Bean creation        | Lazy            | Eager (default)    |
| AOP support          | ❌ Limited      | ✅ Full            |
| Events               | ❌ No           | ✅ Yes             |
| Internationalization | ❌ No           | ✅ Yes             |
| Used in real apps    | ❌ Rare         | ✅ Always          |

📌 **Spring Boot always uses ApplicationContext**

---

## 🔑 What ApplicationContext Actually Does

### 1️⃣ Bean Management

- Creates beans
- Stores them
- Injects dependencies

```java
context.getBean(OrderService.class);
```

---

### 2️⃣ Lifecycle Management

- Calls `@PostConstruct`
- Applies `BeanPostProcessor`
- Handles shutdown (`@PreDestroy`)

---

### 3️⃣ Enables AOP & Proxies

- `@Transactional`
- `@Async`
- `@Cacheable`
- `@PreAuthorize`

👉 Without ApplicationContext → **no proxy → no AOP**

---

### 4️⃣ Event System

```java
ApplicationEventPublisher
@EventListener
```

- Startup events
- Custom domain events

---

### 5️⃣ Configuration & Environment

- `application.properties / yml`
- Profiles
- Property resolution (`@Value`)

---

## 🧠 Types of ApplicationContext (KNOW NAMES)

| Context                              | Used for                 |
| ------------------------------------ | ------------------------ |
| `AnnotationConfigApplicationContext` | Standalone / core Spring |
| `ClassPathXmlApplicationContext`     | Legacy XML               |
| `WebApplicationContext`              | Spring MVC               |
| `ServletWebServerApplicationContext` | Spring Boot (default)    |

📌 **Spring Boot uses:**  
👉 `ServletWebServerApplicationContext`

---

## 🔥 How Spring Boot Creates ApplicationContext

```java
@SpringBootApplication
public class App {
    public static void main(String[] args) {
        SpringApplication.run(App.class, args);
    }
}
```

Internally:

- Detects app type (web / non‑web)
- Creates proper ApplicationContext
- Refreshes context
- Starts embedded server

---

## ❗ Common Bugs Related to ApplicationContext

### ❌ Bean not found

```text
NoSuchBeanDefinitionException
```

➡ Bean not registered in context

---

### ❌ @Transactional not working

➡ Bean not created by ApplicationContext  
➡ Created using `new`

---

### ❌ Circular dependency

➡ Detected during context startup

---

## 🎯 Interview‑Perfect Answer

> “ApplicationContext is the central Spring container responsible for creating, configuring, and managing beans. It extends BeanFactory and provides advanced features like AOP, events, internationalization, and environment management. Spring Boot applications always run inside an ApplicationContext.”

---

## 🧠 ONE‑LINE MEMORY TRICK

```
No ApplicationContext → No Spring
```

or

```
ApplicationContext = Spring runtime
```

---

## ✅ FINAL TAKEAWAY

- ApplicationContext is **the heart of Spring**
- All advanced features depend on it
- Understanding it = **framework‑level clarity**
