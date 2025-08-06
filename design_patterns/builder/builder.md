# 🏗️ Builder Design Pattern

## 🔍 What is it?

The **Builder Pattern** is a *creational* design pattern used to construct complex objects step by step.

Unlike telescoping constructors or setters, the Builder:
- Helps avoid constructor overloads
- Promotes immutability
- Makes object creation more readable
- Can enforce valid construction sequences or defaults

It's especially useful when:
- An object has many optional fields
- You want a clear, fluent API
- You need to ensure a valid object state before building

---

## ✅ When to Use

- When constructors become too complex due to many parameters
- When you want to enforce immutability
- When object construction requires validation or defaults
- When you want a readable and flexible alternative to chaining setters

---

## 🚫 When *Not* to Use

- When the object is simple and can be created with a basic constructor
- When no defaults or validation are needed
- When object mutability is acceptable and few fields exist

---

## 🧱 Typical Structure

- The **Builder** holds intermediate fields
- The **Product** is created via a `build()` method
- The **Product** class often has a private constructor that takes a builder

---

## 💻 Java Example

\`\`\`java
class Meal {
    private final double cost;
    private final boolean takeOut;
    private final String main;
    private final String drink;

    private Meal(MealBuilder builder) {
        this.cost = builder.cost;
        this.takeOut = builder.takeOut;
        this.main = builder.main;
        this.drink = builder.drink;
    }

    static class MealBuilder {
        private double cost = 0.0;
        private boolean takeOut = false;
        private String main;
        private String drink;

        public MealBuilder main(String main) {
            this.main = main;
            return this;
        }

        public MealBuilder drink(String drink) {
            this.drink = drink;
            return this;
        }

        public MealBuilder takeOut(boolean takeOut) {
            this.takeOut = takeOut;
            return this;
        }

        public MealBuilder cost(double cost) {
            if (cost < 0) throw new IllegalArgumentException("Cost cannot be negative");
            this.cost = cost;
            return this;
        }

        public Meal build() {
            if (main == null) throw new IllegalStateException("Main course is required");
            return new Meal(this);
        }
    }
}
\`\`\`

---

## 🧪 Usage

\`\`\`java
Meal m = new Meal.MealBuilder()
    .main("Burger")
    .drink("Soda")
    .takeOut(true)
    .cost(9.99)
    .build();
\`\`\`

---

## 🧠 Benefits

- Improves code readability
- Enables immutability
- Separates construction logic from the object itself
- Supports validation and defaults

---

## ⚠️ Common Mistake

Just wrapping `setX()` in `addX()` methods doesn’t make it a proper Builder.
> A Builder should meaningfully control the creation process — not just rename setters.

---

## 📌 Summary

- Use Builder for **complex objects with optional parameters**
- Avoid it for **simple data structures**
- Prefer immutability, fluent syntax, and encapsulated logic