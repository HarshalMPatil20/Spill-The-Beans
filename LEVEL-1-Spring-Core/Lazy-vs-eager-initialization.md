
# ⚡ Lazy vs Eager Initialization (Spring)


## 🧠 What is initialization?


Initialization = **when Spring creates a bean object**.

* * *

## 🟢 EAGER INITIALIZATION (Default)


### What it means

> Bean is created **at application startup**.

### Example

```java
@Service
class OrderService {}
```

➡️ `OrderService` is created **when Spring context starts**.

### Characteristics

*   Default behavior for **singleton beans**
*   Errors show up **early** (startup time)
*   Slower startup if many beans

### When to use

*   Core services
*   Beans used almost always
*   When you want **fail‑fast**

📌 **Rule:**

> If app must fail early → EAGER is good

* * *

## 🔵 LAZY INITIALIZATION

### What it means

> Bean is created **only when it is first used**.

### Example

```java
@Service
@Lazy
class ReportService {}
```

➡️ `ReportService` is created **only when injected or called**.

* * *

### Lazy at injection point

```java
@Autowired
@Lazy
private ReportService reportService;
```

➡️ A **proxy** is injected `(proxy = placeholder object)`  
➡️ Real bean created on first method call

* * *

### Global lazy initialization

```properties
spring.main.lazy-initialization=true
```

➡️ ALL beans become lazy (except some infra beans)

* * *

### Characteristics

*   Faster startup
*   Bean created on demand
*   Errors appear **later at runtime**

* * *

## 🔥 Lazy vs Eager — Side by Side


| Feature | Eager | Lazy |
| --- | --- | --- |
| Creation time | Startup | First use |
| Default | ✅ Yes | ❌ No |
| Startup time | Slower | Faster |
| Error detection | Early | Late |
| Memory usage | Higher initially | Lower initially |
| Uses proxy | ❌ No | ✅ Often |

* * *

## 🧠 VERY IMPORTANT INTERNAL DETAIL (INTERVIEW GOLD)


### Lazy beans are injected as **PROXIES**

*   Actual object not created yet
*   Created only when method is called

📌 This is why `@Lazy` can:

*   Break circular dependencies
*   Delay heavy initialization

* * *

## 🔁 Lazy & Circular Dependency (Connection)


```java
@Service
class A {
    @Autowired
    @Lazy
    B b;
}
```

➡️ Breaks circular dependency  
➡️ Spring injects proxy of `B`

* * *

## ❌ Common Misunderstandings


❌ Lazy is always better → **FALSE**  
❌ Eager wastes memory → **FALSE**  
❌ Lazy improves performance always → **FALSE**

👉 It’s a **trade‑off**.

* * *

## ✅ Best Practices (REAL PROJECTS)


### Use **EAGER** when:

*   Core business services
*   Required at startup
*   Configuration / validation beans

### Use **LAZY** when:

*   Heavy beans (reporting, ML, integrations)
*   Optional features
*   To break circular dependency (last resort)

* * *

## 🎯 Interview‑Ready Answer (Perfect)


> “By default, Spring uses eager initialization for singleton beans, meaning they are created at startup. Lazy initialization delays bean creation until it’s first used, often via a proxy. Lazy initialization improves startup time but delays error detection, so it should be used selectively.”

* * *

## 🧠 1‑LINE MEMORY TRICK


```
EAGER = Create now
LAZY  = Create when needed
```

