# 🧍‍♂️ Singleton Design Pattern

## 🔍 What is it?

The **Singleton Pattern** is a *creational* design pattern that ensures:
- A class has **only one instance**.
- There is a **global point of access** to that instance.

It restricts instantiation by:
- Making the constructor private.
- Providing a static method that returns the single instance.

\`\`\`java
public class Singleton {
    private static Singleton instance;

    private Singleton() {
        // private constructor to prevent instantiation
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
\`\`\`

## ✅ When to Use It

Use the Singleton Pattern when:
- You need **exactly one instance** of a class for coordination or control.
- You're managing a **shared resource** like:
  - A database connection
  - A configuration manager
  - A logging system
  - A caching layer
- You want **lazy initialization** (i.e., creating the object only when needed).

## 🚫 When *Not* to Use It

Avoid Singletons when:
- You can achieve the same result with **dependency injection** or **static methods**.
- You need to **unit test** — Singletons make mocking harder and introduce global state.
- You’re in **multithreaded** environments (unless implemented carefully).
- You want to avoid **tight coupling** — Singletons implicitly link everything to the same instance.

## ⚠️ Violation of the Single Responsibility Principle (SRP)

The Singleton pattern **violates SRP** because:

> The class has **two responsibilities**:
> 1. **Its core business logic**, and  
> 2. **Managing its own lifecycle** (ensuring only one instance exists)

This bundling of concerns makes the class harder to change, extend, or test. SRP encourages separating those concerns.

For example:
- A Logger class should focus on *logging*, not enforcing singleton behavior.
- That enforcement responsibility could be externalized or injected instead.

## 💻 Thread-Safe Singleton (Java)

```java
public class Singleton {
    private static volatile Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized(Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

This is the **double-checked locking** pattern for safe use in multithreaded environments.

## 🧠 Alternatives

| Pattern / Approach       | When to Use                                              |
|--------------------------|----------------------------------------------------------|
| **Static Methods**       | When you don’t need state or instance-level abstraction. |
| **Dependency Injection** | For better testability and flexibility.                  |
| **Service Locator**      | When objects must be looked up and shared globally.      |

## 📌 Summary

- **Singleton** = One instance, global access  
- Helps manage **shared resources**  
- **Breaks SRP**, adds tight coupling  
- Be cautious — **misused Singletons become glorified globals**
