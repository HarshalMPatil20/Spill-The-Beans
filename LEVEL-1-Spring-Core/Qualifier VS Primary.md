

# 🔹 `@Qualifier` vs `@Primary`


🧠 The core problem they solve
------------------------------

Both are used **when multiple beans of the same type exist** and Spring doesn’t know **which one to inject**.

* * *

## 🟢 `@Primary` — _Default choice_

### What it means

> “If no one specifies anything, use **this** bean.”

### Example

```java
@Service
@Primary
class UpiPaymentService implements PaymentService {}

@Service
class CardPaymentService implements PaymentService {}
```

```java
@Autowired
PaymentService paymentService; // UpiPaymentService injected
```

### Key points

*   Acts as **default**
*   Works automatically
*   Only **one** bean should be `@Primary`

* * *

## 🔵 `@Qualifier` — _Explicit choice_


### What it means

> “I want **THIS specific bean**, no guessing.”

### Example

```java
@Service("upi")
class UpiPaymentService implements PaymentService {}

@Service("card")
class CardPaymentService implements PaymentService {}
```

```java
@Autowired
@Qualifier("card")
PaymentService paymentService; // CardPaymentService injected
```

### Key points

*   Explicit and precise
*   Overrides `@Primary`
*   Best for clarity in large projects

* * *

## ⚔️ What if BOTH are used?

```java
@Service
@Primary
class UpiPaymentService implements PaymentService {}

@Service
class CardPaymentService implements PaymentService {}
```

```java
@Autowired
@Qualifier("cardPaymentService")
PaymentService paymentService;
```

✅ **Result:** `@Qualifier` wins

### Rule (VERY IMPORTANT)

> **`@Qualifier` > `@Primary`**

* * *

## 📊 Side‑by‑Side Comparison


| Feature | `@Primary` | `@Qualifier` |
| --- | --- | --- |
| Purpose | Default bean | Explicit bean selection |
| Where used | Bean class | Injection point |
| Overrides ambiguity | Yes | Yes |
| Overrides the other | ❌ | ✅ |
| Best for | Small/simple setups | Large/real projects |

* * *

🧠 Easy Memory Trick
--------------------

*   **`@Primary`** → _“Use this unless told otherwise”_
*   **`@Qualifier`** → _“Use THIS one, exactly”_

* * *

## 🎯 Interview‑Perfect Answer 

> "`@Primary` defines a default bean when multiple beans of the same type exist, while `@Qualifier` explicitly specifies which bean to inject. If both are present, `@Qualifier` takes precedence."

* * *

## ✅ Best Practice (Real Projects)


*   Use `@Primary` **sparingly**
*   Prefer `@Qualifier` for **clarity and maintainability**
*   Avoid relying on Spring’s guessing

