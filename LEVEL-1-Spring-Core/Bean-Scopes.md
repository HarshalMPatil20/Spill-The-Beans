

# 🫘 Bean Scopes in Spring


## 🧠 What is a Bean Scope?


**Bean scope defines _how many objects Spring creates_ and _how long they live_.**

> In simple words:  
> **“Scope decides _who shares the bean_ and _for how long_.”**

* * *

### 🟢 DEFAULT SCOPE (MOST IMPORTANT)


## 1️⃣ `singleton` ✅ (Default)


### What it means

> **Only ONE object per Spring ApplicationContext**

```java
@Service
class OrderService {}
```

➡ Same instance shared everywhere

### Internals

*   Stored in `singletonObjects` cache
*   Created eagerly (by default)

### When to use

*   Services
*   Repositories
*   Stateless beans

📌 **90% of Spring beans are singleton**

* * *

## 🔵 `prototype`


### What it means 

> **New object every time you request the bean**

```java
@Component
@Scope("prototype")
class ReportGenerator {}
```

```java
context.getBean(ReportGenerator.class); // new object each time
```

### Important behavior (INTERVIEW TRAP ⚠️)

*   Spring creates the bean
*   ❌ Spring does **NOT** manage its full lifecycle
*   ❌ `@PreDestroy` is NOT called

### When to use

*   Stateful objects
*   Temporary / short‑lived objects

* * *

## 🌐 WEB‑AWARE SCOPES (Spring MVC)


### 3️⃣ `request`


### What it means

> **One bean per HTTP request**

```java
@Component
@Scope("request")
class RequestTracker {}
```

➡ New instance for every request

### Use case

*   Request‑specific data
*   Correlation IDs

* * *

## 4️⃣ `session`


### What it means

> **One bean per HTTP session**

```java
@Component
@Scope("session")
class UserSession {}
```

➡ Same bean reused for one user session

### Use case

*   User login data
*   Shopping cart

* * *

## 5️⃣ `application`

### What it means

> **One bean per ServletContext**

➡ Similar to singleton, but web‑scoped

* * *

## 🔁 `websocket` (Rare)

### What it means

> One bean per WebSocket session

* * *

## 🔥 MOST IMPORTANT REAL‑WORLD BUG (SCOPE MISMATCH)


### ❌ Injecting shorter‑lived bean into longer‑lived bean


```java
@Component
@Scope("request") // One bean per HTTP request
class RequestTracker {}
```

- `RequestTracker` is **request‑scoped** ➡️ New instance every request
- Injecting into **singleton** bean `OrderService` ➡️ Spring creates OrderService at startup,   
👉 **but RequestTracker doesn't exist yet**

```java
@Service // singleton
class OrderService {

    @Autowired
    private RequestTracker tracker; // request scope ❌
}
```

### ❌ Why this fails

*   Singleton created at startup
*   Request bean exists only during HTTP request

### ✅ Fix: Use proxy

```java
@Component
@Scope(value = "request", proxyMode = ScopedProxyMode.TARGET_CLASS)
class RequestTracker {}
```

➡ Spring injects a **proxy**, real bean resolved at runtime

* * *

### 🧠 Scope vs Lifecycle (VERY IMPORTANT)


| Scope | Created | Destroyed |
| --- | --- | --- |
| singleton | Context startup | Context shutdown |
| prototype | On demand | ❌ Not managed |
| request | Per HTTP request | End of request |
| session | Per HTTP session | Session end |

* * *

### 🧠 EASY MEMORY TRICK


```
Singleton  → One for all
Prototype  → New every time
Request    → One per request
Session    → One per user
```

* * *

### 🎯 Interview‑Perfect Answer

> “Bean scope defines the lifecycle and visibility of a bean. Singleton is the default scope with one instance per ApplicationContext, prototype creates a new instance each time, and web scopes like request and session create beans per HTTP request or session. Scope mismatch issues are handled using scoped proxies.”

* * *

## ❗ When NOT to use Prototype


*   With `@Transactional`
*   With AOP heavy logic
*   When lifecycle management matters

    ### Why ❓
    -  Spring does NOT manage prototype bean lifecycle fully
    -  `@PreDestroy` is NOT called
    -  Can lead to memory leaks if not handled properly
    - Requires manual cleanup
    - Not suitable for stateful beans that need proper destruction

* * *

✅ FINAL TAKEAWAY
----------------

*   **Singleton = default & safest**
*   **Prototype = rare & tricky**
*   **Web scopes = powerful but need proxies**
*   Always consider lifecycle implications when choosing scope

* * *


## ChatGPT:
ChatGPT 11:47 PM

Perfect 👍  
Here’s a **REAL PRODUCTION BUG caused by SCOPE MISMATCH**, exactly how it happens and how seniors debug it.

* * *

## 🐞 Real Prod Bug: **Scope Mismatch**


### ❗ Problem Statement


Random users see **other users’ data** (IDs, locale, headers) in logs or responses.

No exception. App works. **Data leakage** happens under load.

* * *

### 🔥 Root Cause (Classic Mistake)


A **short‑lived bean** is injected into a **long‑lived bean**.

```java
@Service // singleton (default)
public class OrderService {

    @Autowired
    private RequestContext requestContext; // request scope ❌
}
```

```java
@Component
@Scope("request")
public class RequestContext {
    private String userId;
}
```

* * *

### 😱 What Actually Happens Internally


*   `OrderService` (singleton) is created **at startup**
*   `RequestContext` exists **only during an HTTP request**
*   Spring injects **ONE instance** (or a stale reference)
*   That reference is **reused across requests**

👉 Result:

*   User A’s `userId` leaks into User B’s request
*   Appears **random**, only under concurrency

* * *

### 🧪 Symptoms You’ll See in Prod


*   Logs show wrong user IDs
*   Bugs disappear in local testing
*   Reproducible only with multiple users
*   No stacktrace, no error

* * *

### 😵 Why this looks “random” in production


*   Works fine with 1 user
*   Breaks only under concurrency
*   No exception
*   No error logs

That’s why this bug is **very dangerous**.
* * *

### ✅ Correct Fix (PROPER WAY)


### 👉 Use a **Scoped Proxy**

```java
@Component
@Scope(value = "request", proxyMode = ScopedProxyMode.TARGET_CLASS)
public class RequestContext {
    private String userId;
}
```

### Why this works

*   Singleton gets a **proxy**
*   Proxy resolves the **correct request bean at runtime**
*   No shared state

* * *

### 🔁 What Spring Injects Now


```
OrderService
   ↓
RequestContextProxy
   ↓
(real RequestContext for CURRENT request)
```

* * *

### ❌ Common WRONG Fixes (Seen in Prod)


- ❌ Making `OrderService` prototype  
→ Breaks transactions, caching, performance

- ❌ Using `ThreadLocal` manually  
→ Memory leaks, async bugs

- ❌ Using `@Lazy` alone  
→ Delays problem, doesn’t fix scope

* * *

### 🧠 Scope Rules (MEMORIZE)


```
Long‑lived bean
❌ must NOT directly hold
Short‑lived bean
```

If it must:  
👉 **Use a proxy**

* * *

📊 Quick Scope Compatibility Table
----------------------------------

| Injecting Bean | Injected Bean | Safe? |
| --- | --- | --- |
| singleton | singleton | ✅ |
| singleton | request | ❌ (needs proxy) |
| singleton | session | ❌ (needs proxy) |
| request | singleton | ✅ |
| request | request | ✅ |

* * *

🎯 Interview‑Perfect Answer
---------------------------

> “A scope mismatch occurs when a shorter‑lived bean like request or session scope is injected into a singleton. This causes stale or shared data across requests. The correct solution is to use scoped proxies so the actual bean is resolved at runtime.”

* * *

🧠 ONE‑LINE MEMORY TRICK
------------------------

```
Shorter scope inside longer scope → PROXY REQUIRED
```

> **A singleton remembers what you inject into it forever.**

If you inject a short‑lived object into it → 💥 bug.

* * *

✅ FINAL TAKEAWAY
----------------

*   This is a **real, dangerous production bug**
*   Causes **data leakage**
*   Fix = **scoped proxy**

