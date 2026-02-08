# 🟢 LEVEL 0: Prerequisites (Foundation)

Spring is not magic.  
Spring is **coordination**.

It coordinates:

- Java objects
- JVM memory
- HTTP requests
- Database access
- Dependencies

If these foundations are weak, Spring becomes:  
❌ confusing  
❌ fragile  
❌ impossible to debug

This level builds the **mental muscles** required before touching Spring Core.

---

# 1️⃣ Core Java (The Bedrock)

Spring applications are nothing more than **Java objects managed by a framework**.

If you remove Spring:

- Your code should still make sense
- Your classes should still follow OOP rules

Spring **does not fix bad Java design**.

---

## 1.1 Object-Oriented Programming (OOP)

### Simple Explanation

OOP is about:

- Breaking a system into **objects**
- Giving each object **one responsibility**
- Making objects **talk to each other safely**

Spring is built on **clean OOP design**.

---

### Interfaces (EXTREMELY IMPORTANT)

#### Simple Explanation

An interface defines **what** something does, not **how**.

Think of it as:

> “I don’t care how you do it, just do this.”

```java
interface NotificationService {
    void send(String message);
}
```

#### Why Spring Depends on Interfaces

- Spring injects implementations, not concrete logic
- Enables loose coupling
- Allows easy replacement (mocking, testing, swapping implementations)

```java
@Service
class EmailNotificationService implements NotificationService {}
```

#### 📌 Dependency Injection works because of interfaces.

Without interfaces:

- Code becomes tightly coupled
- Testing becomes painful
- Spring loses flexibility

---

### Abstraction

#### Simple Explanation

Abstraction hides complexity.

#### Controller:

- Should not care how data is stored

#### Service :

- Should not care how HTTP works

#### Repository :

- Should not care about business rules

#### In Spring Architecture

Each layer talks only to the layer below it.

```java
Controller → Service → Repository
```

📌 Spring encourages abstraction by design, not force.

---

### Encapsulation

#### Simple Explanation
Encapsulation protects object state.

```java
private String name;
```

#### Why It Matters in Spring

- Spring uses reflection
- Frameworks rely on predictable structure
- Poor encapsulation causes hidden bugs

📌 Well-encapsulated beans are safer and easier to manage.

---

## 1.2 Java Collections (How Spring Stores Things)

Spring internally stores beans, configurations, handlers, and metadata using collections.

Core Interfaces You MUST Know

| Interface | Purpose           |
| --------- | ----------------- |
| List      | Ordered elements  |
| Set       | Unique elements   |
| Map       | Key-value storage |


📌 Spring heavily relies on Map<String, Object> internally.

### Important Implementations
#### HashMap

- Fast lookup
- Not thread-safe
- Used where concurrency is controlled

#### ConcurrentHashMap

- Thread-safe
- Used heavily inside Spring containers

#### 📌 Wrong collection choice = concurrency bugs.

## 1.3 Exceptions (Foundation of Stability)
### Simple Explanation

#### Exceptions represent unexpected situations.

Spring uses exceptions to:

- Trigger rollbacks
- Control flows
- Signal failures

| Type      | Example          | Spring Default |
| --------- | ---------------- | -------------- |
| Checked   | IOException      | ❌ No rollback  |
| Unchecked | RuntimeException | ✅ Rollback     |


#### 📌 Transactional methods rollback ONLY for unchecked exceptions by default.

This single rule causes real production bugs when misunderstood.

### Exception Propagation

- Exceptions bubble up the call stack
- Spring intercepts them using AOP
- Global handlers convert them into HTTP responses

📌 Understanding this is mandatory for REST APIs.

---

## 2️⃣ JVM Basics (Where Things Actually Live)

Spring manages objects.   
JVM manages memory.

These are separate responsibilities.

---
### 2.1 Heap Memory
#### Simple Explanation

- All objects live in heap
- Spring beans live in heap
- Garbage Collector cleans unused objects

#### 📌 Spring does NOT free memory — GC does.
---

#### Why This Matters

- Long-lived beans hold references
- Unreleased references = memory leaks
- Caches are common culprits

---
### 2.2 Stack Memory
#### Simple Explanation

- Each method call gets its own stack frame
- Local variables live here
- Stack is cleared automatically

📌 Stack overflow ≠ memory leak.

### 2.3 Garbage Collection
#### Simple Explanation

- Objects without references are eligible for GC
- GC timing is not guaranteed
- Spring only manages references

#### 📌 Memory leaks in Spring = reference leaks.

## 3️⃣ SQL Basics (The Reality Check)

ORMs reduce SQL writing — they do not remove SQL responsibility.

---
### 3.1 CRUD Operations

These operations happen **even when using JPA.**

```sql
SELECT
INSERT
UPDATE
DELETE
```

#### 📌 JPA generates SQL — bad queries still hurt performance.

---

### 3.2 Joins (MOST IMPORTANT SQL TOPIC)

#### Simple Explanation

Joins combine data from multiple tables.

- INNER JOIN
- LEFT JOIN

#### 📌 N+1 problems are JOIN problems in disguise.

### 3.3 Keys and Indexes

- Primary Key → identity
- Foreign Key → relationship
- Index → speed

#### 📌 Indexing often matters more than Java optimization.

## 4️⃣ HTTP & REST Fundamentals (Spring MVC Backbone)

Spring MVC is an HTTP **request processing engine.**

---
### 4.1 HTTP Basics
#### Simple Explanation

- Client sends request
- Server responds
- Server remembers nothing

#### 📌 HTTP is stateless.

---

### 4.2 HTTP Methods

| Method | Purpose    |
| ------ | ---------- |
| GET    | Fetch data |
| POST   | Create     |
| PUT    | Update     |
| DELETE | Remove     |


#### 📌 Using wrong methods breaks REST semantics.

---

### 4.3 HTTP Status Codes (INTERVIEW FAVORITE)

| Code | Meaning                |
| ---- | ---------------------- |
| 200  | OK                     |
| 201  | Created                |
| 400  | Client error           |
| 401  | Not authenticated      |
| 403  | Authenticated but forbidden |
| 404  | Resource missing       |
| 500  | Server failure         |

#### 📌 401 ≠ 403 — very common mistake.

---

### 4.4 REST Principles

- Resource-based URLs
- Stateless communication
- Clear status codes

#### 📌 Spring controllers expose REST resources.

---

## 5️⃣ Maven / Gradle (How Spring Boot Even Runs)

Spring Boot projects **cannot exist without a build tool**.

### 5.1 Simple Explanation

Build tools:

- Download dependencies
- Compile code
- Run tests
- Package applications

---

### 5.2 Maven (Most Common)

Key file:

``` xml
pom.xml
```

Key concepts:

- Dependency
- Transitive dependency
- Scope (compile, test, runtime)

#### 📌 Spring Boot starters are dependency bundles, nothing magical.

---

### 5.3 Gradle (Optional)

- Faster builds
- Script-based
- Popular in modern systems

#### 📌 One build tool is enough — Maven is sufficient.

---

### 🎯 When Is LEVEL 0 Complete?

You are ready when:

- Java OOP is instinctive
- Collections feel obvious
- Exceptions don’t surprise you
- HTTP errors make sense
- Maven errors are readable

---

### 🧠 Final Mental Model

```markdown
Java Objects
+ JVM Memory
+ HTTP Protocol
+ SQL Database
+ Build Tool
  = Spring Foundation
```

#### ✅ LEVEL 0 COMPLETE

Now Spring Core will feel logical, not magical.

---

If you want next, I strongly recommend:

👉 **LEVEL 1: Spring Core (IoC + DI + Bean Internals)**  
This is where _real Spring understanding begins_ 🔥
