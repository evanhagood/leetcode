# 🧬 Prototype Design Pattern

## 🔍 What is it?

The **Prototype Pattern** is a *creational* design pattern used to create new objects by **cloning an existing object**, rather than instantiating new ones from scratch.

This is especially useful when:
- Object creation is **expensive** (e.g., involves I/O, complex calculations)
- You want to avoid **subclassing** just to vary a few fields
- You need many copies of objects with similar configurations

---

## ✅ When to Use

- The cost of creating a new object is **higher** than copying
- You have a set of **default or preconfigured** objects to use as prototypes
- You want to avoid writing **many subclasses** for minor variations
- You need to **decouple object creation from concrete classes**

---

## 🚫 When *Not* to Use

- Objects are simple and cheap to construct
- The system doesn’t require a large number of similar objects
- Cloning leads to complexity (e.g., deep vs shallow copy, cyclic references)

---

## 📎 Key Concept

Each prototype object implements a `clone()` or `copy()` method, allowing clients to create duplicates without knowing their concrete class.

---

## 💻 Java Example
```java
interface Shape extends Cloneable {
    Shape clone();
    void draw();
}

class Circle implements Shape {
    private int radius;

    public Circle(int radius) {
        this.radius = radius;
    }

    public Shape clone() {
        return new Circle(this.radius); // shallow copy
    }

    public void draw() {
        System.out.println("Drawing a circle with radius " + radius);
    }
}

class Rectangle implements Shape {
    private int width, height;

    public Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }

    public Shape clone() {
        return new Rectangle(this.width, this.height);
    }

    public void draw() {
        System.out.println("Drawing a rectangle " + width + "x" + height);
    }
}
```

---

## 🧪 Usage

```java
Shape original = new Circle(10);
Shape copy = original.clone();

original.draw(); // Drawing a circle with radius 10
copy.draw();     // Drawing a circle with radius 10
```

You can also store a map of prototypes for reuse:

```java
Map<String, Shape> prototypeCache = new HashMap<>();
prototypeCache.put("circle", new Circle(5));
prototypeCache.put("rectangle", new Rectangle(4, 6));

Shape newCircle = prototypeCache.get("circle").clone();
Shape newRectangle = prototypeCache.get("rectangle").clone();
```

---

## 🧠 Deep vs Shallow Copy

- **Shallow copy**: Fields are copied by reference. Use cautiously for mutable fields.
- **Deep copy**: Entire object graph is duplicated. More complex but safer.

Java’s `Object.clone()` does a shallow copy by default. For deep copies, you often need to implement `clone()` manually or use copy constructors/serialization.

---

## 🧠 Benefits

- Avoids expensive instantiation
- Simplifies object creation for complex configurations
- Promotes flexibility without relying on subclasses
- Enables runtime object duplication

---

## ⚠️ Pitfalls

- Cloning can be error-prone (especially deep cloning)
- Requires all fields and nested objects to be cloneable
- Mutable shared state can lead to bugs if not handled properly

---

## 📌 Summary

- Prototype creates new objects by copying existing ones
- Best for situations with expensive or complex object creation
- Be mindful of deep vs shallow copy
- Often used with a **Prototype Registry** for object reuse

```java
// Instead of: new Circle(10)
// Use: prototype.clone()
```
