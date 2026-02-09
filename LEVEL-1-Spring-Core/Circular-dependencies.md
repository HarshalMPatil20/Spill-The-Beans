
# 🔁 Circular Dependency in Spring

![Circular Dependency](/src/stare-intimidate.gif)

### 🧠 What is a circular dependency?


When **two or more beans depend on each other**, directly or indirectly.

### Simple example

```java
@Service
class A {
    @Autowired
    B b;
}

@Service
class B {
    @Autowired
    A a;
}
```

👉 `A → B → A`  
This is a **circular dependency**.

* * *

### ❓ Why is this a problem?


Spring doesn’t know:

*   Which bean to create **first**
*   How to finish creating one without the other

So startup can **fail** (depending on injection type).

* * *

## ✅ IMPORTANT: Does Spring ALWAYS fail?


❌ No — **it depends on how you inject dependencies**.

* * *

### 🟢 Case 1: Field Injection (or Setter Injection)


```java
@Service
class A {
    @Autowired
    B b;
}

@Service
class B {
    @Autowired
    A a;
}
```

### ✅ This WORKS (by default)

**Why?**

*   Spring creates `A` (incomplete)
*   Creates `B`
*   Injects `A` into `B`
*   Goes back and injects `B` into `A`

Spring uses **early bean references**.

📌 This is why people think circular dependency is “okay”.

* * *

### 🔴 Case 2: Constructor Injection (RECOMMENDED STYLE)


```java
@Service
class A {
    A(B b) {}
}

@Service
class B {
    B(A a) {}
}
```

### ❌ This FAILS

**Error:**

```
BeanCurrentlyInCreationException
```

**Why?**

*   `A` needs `B` to be created
*   `B` needs `A` to be created
*   Deadlock 💥

📌 **Spring cannot resolve circular dependency with constructor injection.**

* * *

### 🎯 Interview GOLD LINE


> “Spring can resolve circular dependencies only with setter/field injection, not with constructor injection.”

* * *

## 🧠 Is circular dependency GOOD?


❌ **No. It’s a design smell.**

It usually means:

*   Responsibilities are mixed
*   Poor separation of concerns

* * *

## 🛠️ How to FIX circular dependency (BEST PRACTICES)


### ✅ 1. Refactor the design (BEST)

Extract common logic into a third service.

```java
A → C ← B
```

* * *

### ✅ 2. Use `@Lazy` (Quick Fix)

```java
@Service
class A {
    @Autowired
    @Lazy
    B b;
}
```

👉 Breaks the cycle by delaying injection.

⚠️ Use carefully (not ideal long‑term).

* * *

### ❌ 3. Switch to Field Injection

Technically works, **but NOT recommended**.

Why?

*   Hides design issues
*   Harder to test
*   Against Spring best practices

* * *

### ⚠️ Spring Boot 2.6+ IMPORTANT CHANGE


By default:

```
spring.main.allow-circular-references = false
```

So even field injection may fail unless you explicitly enable it.

```properties
spring.main.allow-circular-references=true
```

📌 **Interview bonus point** if you mention this.

* * *

### 📊 Quick Comparison Table


| Injection Type | Circular Dependency |
| --- | --- |
| Field | ✅ Works (by default) |
| Setter | ✅ Works |
| Constructor | ❌ Fails |
| Constructor + @Lazy | ✅ Works |

* * *

### 🧠 Easy Memory Trick


```
Constructor Injection = NO cycles ❌
Field/Setter Injection = Spring may allow ⚠️
Best Design = NO circular dependency ✅
```

* * *

### 🎯 Interview‑Ready Final Answer


> “A circular dependency occurs when two beans depend on each other. Spring can resolve it using setter or field injection via early bean references, but it fails with constructor injection. The correct solution is to refactor the design or use `@Lazy` if unavoidable.”
