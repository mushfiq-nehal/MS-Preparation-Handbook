# 📘 MSc Admission Prep — Subject 09: Object Oriented Programming
### 🎯 JUST-Style Exam Handbook | Fast Revision Edition

> **Goal:** Deep, visual, exam-focused revision of OOP concepts. Every topic includes intuition, code examples, diagrams, comparisons, and exam tips.

---

## 📋 Table of Contents

| # | Topic | Tier |
|---|-------|------|
| 1 | [Encapsulation](#1-encapsulation) | 🔴 Must Master |
| 2 | [Inheritance](#2-inheritance) | 🔴 Must Master |
| 3 | [Polymorphism](#3-polymorphism) | 🔴 Must Master |
| 4 | [Abstraction](#4-abstraction) | 🔴 Must Master |
| 5 | [Overloading vs Overriding](#5-overloading-vs-overriding) | 🔴 Must Master |
| 6 | [Abstract Class vs Interface](#6-abstract-class-vs-interface) | 🔴 Must Master |
| 7 | [Exception Handling](#7-exception-handling) | 🔴 Must Master |

---

---

# 1. Encapsulation

## 💡 Intuition First

> **Encapsulation** is the practice of **bundling data (attributes) and the methods that operate on that data into a single unit (class)**, and **restricting direct access** to some of the object's components.

**Real-world analogy:** A TV remote — you press buttons (public interface) without knowing the internal circuitry (private implementation). The internals are hidden; you interact only through the provided interface.

**Why it matters:** Protects data integrity, reduces complexity, makes code maintainable. Change the internal implementation without breaking external code.

---

## 📐 Access Modifiers

```
Access levels (Java/C++ style):

private:    Accessible only within the same class
protected:  Accessible within class + subclasses + same package
public:     Accessible from anywhere
(default):  Accessible within same package (Java)

Visibility:
            Same Class  Subclass  Same Package  Other
private         ✅         ❌          ❌          ❌
protected       ✅         ✅          ✅          ❌
public          ✅         ✅          ✅          ✅
```

---

## 📐 Encapsulation in Code

```java
// BAD — No encapsulation
class BankAccount {
    public double balance;  // anyone can change this directly!
}

// Usage (dangerous):
account.balance = -1000;  // invalid state!

// GOOD — With encapsulation
class BankAccount {
    private double balance;    // hidden
    private String owner;      // hidden

    // Constructor
    public BankAccount(String owner, double initialBalance) {
        this.owner = owner;
        if (initialBalance >= 0) {
            this.balance = initialBalance;
        }
    }

    // Getter (read access)
    public double getBalance() {
        return balance;
    }

    // Setter with validation (controlled write access)
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        } else {
            throw new IllegalArgumentException("Amount must be positive");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
        } else {
            throw new IllegalArgumentException("Invalid withdrawal");
        }
    }
}

// Usage (safe):
BankAccount acc = new BankAccount("Alice", 1000);
acc.deposit(500);      // ✅ controlled
acc.withdraw(200);     // ✅ validated
// acc.balance = -1000; // ❌ compile error — private!
```

---

## 📐 Getters and Setters

```java
class Student {
    private String name;
    private int age;
    private double gpa;

    // Getter
    public String getName() { return name; }

    // Setter with validation
    public void setAge(int age) {
        if (age > 0 && age < 150) {
            this.age = age;
        }
    }

    public void setGpa(double gpa) {
        if (gpa >= 0.0 && gpa <= 4.0) {
            this.gpa = gpa;
        }
    }
}
```

---

## 📐 Benefits of Encapsulation

```
1. Data hiding:
   Internal state protected from invalid modifications

2. Flexibility:
   Change internal implementation without affecting external code
   Example: Change balance from double to BigDecimal internally
            External code still calls getBalance() — no change needed

3. Reusability:
   Well-encapsulated classes are easier to reuse

4. Testability:
   Controlled interface makes unit testing easier

5. Maintainability:
   Changes localized to one class
```

---

## ⚖️ Encapsulation vs Information Hiding

```
Encapsulation:    Bundling data + methods into a class
Information Hiding: Restricting access to internal details

They are related but distinct:
  Encapsulation is the MECHANISM
  Information hiding is the PRINCIPLE/GOAL

You can have encapsulation without information hiding
(all public fields in a class — bundled but not hidden)
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Making all fields public defeats encapsulation — always use private fields.
> 🚫 **Mistake 2:** Providing getters/setters for ALL fields is lazy encapsulation — only expose what's needed.
> 🚫 **Mistake 3:** Returning mutable objects from getters breaks encapsulation — return copies or use immutable types.
> 🚫 **Mistake 4:** Encapsulation ≠ security — it's about design, not preventing hacking.

---

## ⚡ One-Minute Recap

- Encapsulation: bundle data + methods, restrict access
- Private fields + public methods = proper encapsulation
- Getters: read access | Setters: controlled write access with validation
- Benefits: data integrity, flexibility, maintainability
- Access modifiers: private < protected < public

---

## 📝 Probable Exam Questions

> **5-mark:** Explain encapsulation with a code example. What are its benefits?
> **Short note:** What are access modifiers in OOP? Explain private, protected, and public.
> **Code:** Write a Java class `BankAccount` demonstrating encapsulation with deposit and withdraw methods.
> **Conceptual:** Why should class fields be private? What problem does it solve?

---

---

# 2. Inheritance

## 💡 Intuition First

> **Inheritance** allows a class (child/subclass) to **acquire properties and behaviors** of another class (parent/superclass). The child gets everything the parent has, and can add more or change some behaviors.

**Real-world analogy:** A child inherits traits from parents — eye color, height tendencies. But the child also has their own unique traits and can behave differently in some situations.

**Why it matters:** Promotes code reuse. Instead of rewriting common code, inherit it. Establishes "is-a" relationships.

---

## 📐 Inheritance Hierarchy

```
Animal (parent/superclass)
├── Dog (child/subclass)
│   ├── Labrador (grandchild)
│   └── Poodle
└── Cat (child/subclass)
    └── Persian

"Dog IS-A Animal" ✅
"Labrador IS-A Dog" ✅
"Labrador IS-A Animal" ✅ (transitive)
```

---

## 📐 Inheritance in Code

```java
// Parent class
class Animal {
    protected String name;
    protected int age;

    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void eat() {
        System.out.println(name + " is eating");
    }

    public void sleep() {
        System.out.println(name + " is sleeping");
    }

    public String toString() {
        return "Animal: " + name + ", Age: " + age;
    }
}

// Child class — inherits from Animal
class Dog extends Animal {
    private String breed;

    public Dog(String name, int age, String breed) {
        super(name, age);    // call parent constructor
        this.breed = breed;
    }

    // New method (not in Animal)
    public void bark() {
        System.out.println(name + " says: Woof!");
    }

    // Override parent method
    @Override
    public String toString() {
        return "Dog: " + name + ", Breed: " + breed;
    }
}

// Usage:
Dog d = new Dog("Rex", 3, "Labrador");
d.eat();        // inherited from Animal ✅
d.sleep();      // inherited from Animal ✅
d.bark();       // Dog's own method ✅
System.out.println(d);  // uses Dog's toString ✅
```

---

## 📐 Types of Inheritance

```
1. Single Inheritance:
   A → B (B inherits from A)
   Java supports this ✅

2. Multilevel Inheritance:
   A → B → C (C inherits from B, which inherits from A)
   Java supports this ✅

3. Hierarchical Inheritance:
   A → B, A → C (B and C both inherit from A)
   Java supports this ✅

4. Multiple Inheritance (classes):
   B, C → D (D inherits from both B and C)
   Java does NOT support this for classes ❌
   (Diamond problem!)
   Java supports multiple inheritance through INTERFACES ✅

5. Hybrid Inheritance:
   Combination of above types
   Java supports via interfaces ✅

Diamond Problem:
  class A { void show() { "A" } }
  class B extends A { void show() { "B" } }
  class C extends A { void show() { "C" } }
  class D extends B, C { }  // Which show() does D inherit? AMBIGUOUS!
  → Java prevents this with classes, allows with interfaces (default methods)
```

---

## 📐 `super` Keyword

```java
class Vehicle {
    protected int speed;
    public Vehicle(int speed) { this.speed = speed; }
    public void display() { System.out.println("Speed: " + speed); }
}

class Car extends Vehicle {
    private String brand;

    public Car(int speed, String brand) {
        super(speed);          // call parent constructor
        this.brand = brand;
    }

    @Override
    public void display() {
        super.display();       // call parent method
        System.out.println("Brand: " + brand);
    }
}
```

---

## ⚖️ Inheritance vs Composition

```
Inheritance ("is-a"):
  Dog IS-A Animal → use inheritance
  class Dog extends Animal { }

Composition ("has-a"):
  Car HAS-A Engine → use composition
  class Car {
      private Engine engine;  // composition
  }

Rule of thumb: "Favor composition over inheritance"
  Inheritance creates tight coupling
  Composition is more flexible

When to use inheritance:
  ✅ True "is-a" relationship
  ✅ Want to reuse and extend parent behavior
  ✅ Polymorphism needed

When to use composition:
  ✅ "has-a" relationship
  ✅ Want to reuse without inheriting all parent behavior
  ✅ Need more flexibility
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Java doesn't support multiple inheritance with classes — use interfaces instead.
> 🚫 **Mistake 2:** `super()` must be the FIRST statement in a constructor.
> 🚫 **Mistake 3:** Private members of parent are NOT inherited (not accessible in child).
> 🚫 **Mistake 4:** Overusing inheritance — not every relationship is "is-a". Use composition for "has-a".

---

## ⚡ One-Minute Recap

- Inheritance: child class acquires parent's properties and methods
- `extends` keyword in Java | `:` in C++
- `super` calls parent constructor/method
- Types: single, multilevel, hierarchical, multiple (via interfaces)
- Diamond problem: why Java doesn't allow multiple class inheritance
- Prefer composition over inheritance for "has-a" relationships

---

## 📝 Probable Exam Questions

> **5-mark:** Explain inheritance with a code example. What is the diamond problem?
> **Short note:** What is the difference between inheritance and composition?
> **Code:** Write a Java class hierarchy: Shape → Circle, Rectangle. Each has area() method.
> **Explain:** What does the `super` keyword do in Java?

---

---

# 3. Polymorphism

## 💡 Intuition First

> **Polymorphism** means "many forms." The same method name behaves differently depending on the object it's called on. Like the word "open" — open a door, open a file, open a bank account — same word, different behavior depending on context.

**Real-world analogy:** A universal remote control — the "volume up" button works on a TV, a soundbar, or a projector. Same button, different behavior per device.

---

## 📐 Types of Polymorphism

```
Polymorphism
├── Compile-time (Static) Polymorphism
│   └── Method Overloading
│       (same name, different parameters, resolved at compile time)
│
└── Runtime (Dynamic) Polymorphism
    └── Method Overriding
        (same name + signature, different class, resolved at runtime)
```

---

## 📐 Runtime Polymorphism (Method Overriding)

```java
class Shape {
    public double area() {
        return 0;
    }

    public void draw() {
        System.out.println("Drawing a shape");
    }
}

class Circle extends Shape {
    private double radius;

    public Circle(double radius) { this.radius = radius; }

    @Override
    public double area() {
        return Math.PI * radius * radius;
    }

    @Override
    public void draw() {
        System.out.println("Drawing a circle");
    }
}

class Rectangle extends Shape {
    private double width, height;

    public Rectangle(double w, double h) {
        this.width = w; this.height = h;
    }

    @Override
    public double area() {
        return width * height;
    }

    @Override
    public void draw() {
        System.out.println("Drawing a rectangle");
    }
}

// POLYMORPHISM IN ACTION:
Shape[] shapes = {
    new Circle(5),
    new Rectangle(4, 6),
    new Circle(3)
};

for (Shape s : shapes) {
    s.draw();        // calls the RIGHT draw() at runtime!
    System.out.println("Area: " + s.area());
}

// Output:
// Drawing a circle      ← Circle's draw()
// Area: 78.54
// Drawing a rectangle   ← Rectangle's draw()
// Area: 24.0
// Drawing a circle      ← Circle's draw()
// Area: 28.27
```

---

## 📐 Dynamic Dispatch

```
How does Java know which method to call at runtime?

Shape s = new Circle(5);  // reference type = Shape, object type = Circle

s.draw();  // Which draw() is called?

At compile time: compiler sees Shape reference → checks Shape has draw() ✅
At runtime:      JVM sees actual object is Circle → calls Circle's draw()

This is called DYNAMIC DISPATCH or LATE BINDING.

Key rule: Method resolution is based on the ACTUAL OBJECT TYPE,
          not the reference type.
```

---

## 📐 Upcasting and Downcasting

```java
// Upcasting (implicit, safe):
Shape s = new Circle(5);   // Circle → Shape (upcast)
// s can only access Shape methods (even though it's a Circle)

// Downcasting (explicit, may throw ClassCastException):
Circle c = (Circle) s;     // Shape → Circle (downcast)
// Now c can access Circle-specific methods

// Safe downcasting with instanceof:
if (s instanceof Circle) {
    Circle c = (Circle) s;
    System.out.println("Radius: " + c.getRadius());
}
```

---

## 📐 Polymorphism with Interfaces

```java
interface Drawable {
    void draw();
    default void display() {
        System.out.println("Displaying...");
    }
}

class Circle implements Drawable {
    @Override
    public void draw() { System.out.println("Drawing circle"); }
}

class Triangle implements Drawable {
    @Override
    public void draw() { System.out.println("Drawing triangle"); }
}

// Polymorphism via interface:
Drawable[] items = { new Circle(), new Triangle() };
for (Drawable d : items) {
    d.draw();  // runtime polymorphism!
}
```

---

## ⚖️ Compile-time vs Runtime Polymorphism

| Feature | Compile-time (Overloading) | Runtime (Overriding) |
|---------|---------------------------|----------------------|
| Also called | Static polymorphism | Dynamic polymorphism |
| Resolved | At compile time | At runtime |
| Mechanism | Method overloading | Method overriding |
| Inheritance | Not required | Required |
| Return type | Can differ | Must be same (or covariant) |
| Performance | Faster | Slightly slower (dynamic dispatch) |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Static methods are NOT polymorphic — they're resolved at compile time based on reference type.
> 🚫 **Mistake 2:** Private methods cannot be overridden — they're not inherited.
> 🚫 **Mistake 3:** Overriding requires SAME method signature. Different parameters = overloading, not overriding.
> 🚫 **Mistake 4:** `@Override` annotation is optional but strongly recommended — catches errors at compile time.

---

## ⚡ One-Minute Recap

- Polymorphism: same interface, different behavior
- Compile-time: overloading (same name, different params)
- Runtime: overriding (same name+params, different class)
- Dynamic dispatch: JVM calls method based on actual object type
- Upcasting: safe (child → parent) | Downcasting: risky (parent → child)

---

## 📝 Probable Exam Questions

> **5-mark:** Explain runtime polymorphism with a code example. What is dynamic dispatch?
> **Code:** Write a Java program demonstrating polymorphism with Shape, Circle, and Rectangle classes.
> **Short note:** What is the difference between compile-time and runtime polymorphism?
> **Explain:** What is upcasting and downcasting? When would you use each?

---

---

# 4. Abstraction

## 💡 Intuition First

> **Abstraction** means **hiding complex implementation details and showing only the essential features**. You interact with a simplified interface without needing to know how it works internally.

**Real-world analogy:** Driving a car — you use the steering wheel, accelerator, and brakes (abstract interface) without knowing how the engine, transmission, or braking system work internally.

**Abstraction vs Encapsulation:**
- Encapsulation = HOW you hide (using access modifiers, bundling)
- Abstraction = WHAT you hide (hiding complexity, showing only essentials)

---

## 📐 Abstraction in OOP

> Achieved through **abstract classes** and **interfaces**.

```java
// Abstract class — partial abstraction
abstract class Vehicle {
    protected String brand;

    public Vehicle(String brand) {
        this.brand = brand;
    }

    // Abstract method — no implementation, MUST be overridden
    public abstract void startEngine();

    // Concrete method — has implementation
    public void stop() {
        System.out.println(brand + " stopped");
    }
}

class Car extends Vehicle {
    public Car(String brand) { super(brand); }

    @Override
    public void startEngine() {
        System.out.println(brand + ": Vroom! Engine started");
    }
}

class ElectricCar extends Vehicle {
    public ElectricCar(String brand) { super(brand); }

    @Override
    public void startEngine() {
        System.out.println(brand + ": Silent electric motor started");
    }
}

// Usage:
Vehicle v1 = new Car("Toyota");
Vehicle v2 = new ElectricCar("Tesla");
v1.startEngine();  // Toyota: Vroom!
v2.startEngine();  // Tesla: Silent electric motor started
v1.stop();         // Toyota stopped (inherited)
```

---

## 📐 Levels of Abstraction

```
High-level abstraction:
  User sees: "Send email"
  Doesn't know: SMTP protocol, TCP/IP, network routing

Medium-level abstraction:
  Developer sees: EmailService.send(to, subject, body)
  Doesn't know: SMTP handshake details

Low-level abstraction:
  Library developer sees: SMTP commands, socket connections
  Doesn't know: TCP packet structure

Each level hides complexity from the level above.
```

---

## ⚖️ Abstraction vs Encapsulation

| Aspect | Abstraction | Encapsulation |
|--------|-------------|---------------|
| Focus | What to show | How to hide |
| Goal | Reduce complexity | Protect data |
| Achieved by | Abstract classes, interfaces | Access modifiers |
| Design level | High-level (design) | Implementation level |
| Example | `abstract void startEngine()` | `private double balance` |
| Analogy | Car dashboard (shows controls) | Car hood (hides engine) |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Abstract classes CAN have concrete methods — not everything must be abstract.
> 🚫 **Mistake 2:** You CANNOT instantiate an abstract class directly: `new Vehicle()` → error.
> 🚫 **Mistake 3:** Abstraction is a design concept; encapsulation is an implementation technique.
> 🚫 **Mistake 4:** A class with even ONE abstract method must be declared abstract.

---

## ⚡ One-Minute Recap

- Abstraction: hide complexity, show only essentials
- Abstract class: can have abstract + concrete methods, cannot be instantiated
- Interface: 100% abstract (traditionally), defines a contract
- Abstraction = WHAT to hide | Encapsulation = HOW to hide
- Achieved through: abstract classes and interfaces

---

## 📝 Probable Exam Questions

> **5-mark:** Explain abstraction in OOP. How is it different from encapsulation?
> **Code:** Write an abstract class `Shape` with abstract method `area()`. Implement it in `Circle` and `Triangle`.
> **Short note:** What is an abstract method? Can an abstract class have concrete methods?

---

---

# 5. Overloading vs Overriding

## 💡 Intuition First

> **Overloading** = same method name, different parameters, SAME class. Like a restaurant with a "serve" function — serve(coffee), serve(tea), serve(juice) — same action, different inputs.
>
> **Overriding** = same method name AND parameters, DIFFERENT class (child overrides parent). Like a child doing the same task as the parent but in their own way.

---

## 📐 Method Overloading

> Multiple methods with the **same name** but **different parameter lists** in the **same class**.

```java
class Calculator {

    // Overloaded add() methods
    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }

    public int add(int a, int b, int c) {
        return a + b + c;
    }

    public String add(String a, String b) {
        return a + b;  // string concatenation
    }
}

// Usage:
Calculator calc = new Calculator();
calc.add(2, 3);           // calls int version → 5
calc.add(2.5, 3.5);       // calls double version → 6.0
calc.add(1, 2, 3);        // calls 3-param version → 6
calc.add("Hello", " World"); // calls String version → "Hello World"
```

### Overloading Rules

```
✅ Different number of parameters
✅ Different types of parameters
✅ Different order of parameter types

❌ Return type alone CANNOT differentiate overloaded methods
   int add(int a, int b)     ← same params
   double add(int a, int b)  ← COMPILE ERROR (ambiguous)
```

---

## 📐 Method Overriding

> Child class provides a **specific implementation** of a method already defined in the parent class. Same name, same parameters, same return type.

```java
class Animal {
    public void makeSound() {
        System.out.println("Some generic animal sound");
    }

    public String toString() {
        return "I am an Animal";
    }
}

class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Woof! Woof!");
    }
}

class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Meow!");
    }
}

// Usage:
Animal a = new Animal();
Animal d = new Dog();    // upcasting
Animal c = new Cat();    // upcasting

a.makeSound();  // "Some generic animal sound"
d.makeSound();  // "Woof! Woof!"  ← Dog's version (runtime polymorphism)
c.makeSound();  // "Meow!"        ← Cat's version
```

### Overriding Rules

```
✅ Same method name
✅ Same parameter list
✅ Same or covariant return type
✅ Access modifier can be same or LESS restrictive (not more)
   Parent: public → Child: public ✅
   Parent: protected → Child: public ✅
   Parent: public → Child: private ❌

❌ Cannot override static methods (they're hidden, not overridden)
❌ Cannot override final methods
❌ Cannot override private methods (not inherited)
```

---

## ⚖️ Overloading vs Overriding — Master Comparison

| Feature | Overloading | Overriding |
|---------|-------------|------------|
| Also called | Compile-time polymorphism | Runtime polymorphism |
| Location | Same class | Parent + Child class |
| Method name | Same | Same |
| Parameters | DIFFERENT | SAME |
| Return type | Can differ | Must be same (or covariant) |
| Inheritance | Not required | Required |
| Resolved | At compile time | At runtime |
| `@Override` | Not applicable | Recommended |
| Static methods | Can be overloaded | Cannot be overridden |
| Access modifier | Can be anything | Cannot be more restrictive |

---

## ✏️ Tricky Example

```java
class Parent {
    public void show(int x) {
        System.out.println("Parent: " + x);
    }
}

class Child extends Parent {
    // This is OVERLOADING (different parameter type)
    public void show(double x) {
        System.out.println("Child double: " + x);
    }

    // This is OVERRIDING (same parameter type)
    @Override
    public void show(int x) {
        System.out.println("Child int: " + x);
    }
}

Child c = new Child();
c.show(5);      // "Child int: 5"    ← overriding
c.show(5.0);    // "Child double: 5.0" ← overloading

Parent p = new Child();
p.show(5);      // "Child int: 5"    ← runtime polymorphism (overriding)
p.show(5.0);    // COMPILE ERROR — Parent doesn't have show(double)
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Changing only the return type is NOT overloading — it's a compile error.
> 🚫 **Mistake 2:** Overriding requires EXACT same parameter list. Different params = overloading.
> 🚫 **Mistake 3:** Static methods can be hidden (not overridden) — `@Override` on static method → error.
> 🚫 **Mistake 4:** Overriding with more restrictive access (public → private) is NOT allowed.

---

## 🎯 Exam Tips

> 💡 **The key difference:** Overloading = same class, different params | Overriding = different class, same params.
> 💡 Overloading is resolved at **compile time** (static binding).
> 💡 Overriding is resolved at **runtime** (dynamic binding).
> 💡 `@Override` annotation helps catch overriding mistakes at compile time — always use it.

---

## ⚡ One-Minute Recap

- Overloading: same name, different params, same class, compile-time
- Overriding: same name, same params, child class, runtime
- Overloading: return type can differ | Overriding: return type must match
- Cannot override: static, final, private methods
- Overriding enables runtime polymorphism

---

## 📝 Probable Exam Questions

> **5-mark:** Explain method overloading and overriding with code examples. How do they differ?
> **Code:** Write a Java program showing both overloading and overriding in the same hierarchy.
> **Short note:** Can you override a static method in Java? Why or why not?
> **Identify:** Given code snippets, identify whether each is overloading or overriding.

---

---

# 6. Abstract Class vs Interface

## 💡 Intuition First

> **Abstract class** is like a **partial blueprint** — it defines some things completely and leaves others for subclasses to fill in. Like a house blueprint with the foundation drawn but rooms left to the builder.
>
> **Interface** is like a **contract** — it says "you MUST implement these methods" but doesn't tell you how. Like a job description — "must be able to drive, speak English" — doesn't say how you learned.

---

## 📐 Abstract Class

```java
abstract class Animal {
    // Instance variables (state)
    protected String name;
    protected int age;

    // Constructor
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Abstract method — MUST be implemented by subclasses
    public abstract void makeSound();

    // Concrete method — inherited as-is
    public void eat() {
        System.out.println(name + " is eating");
    }

    public void sleep() {
        System.out.println(name + " is sleeping");
    }
}

class Dog extends Animal {
    public Dog(String name, int age) {
        super(name, age);
    }

    @Override
    public void makeSound() {
        System.out.println("Woof!");
    }
}

// Animal a = new Animal("X", 1);  // ❌ CANNOT instantiate abstract class
Dog d = new Dog("Rex", 3);
d.makeSound();  // Woof!
d.eat();        // Rex is eating (inherited)
```

---

## 📐 Interface

```java
interface Flyable {
    // Constants (implicitly public static final)
    int MAX_ALTITUDE = 10000;

    // Abstract methods (implicitly public abstract)
    void fly();
    void land();

    // Default method (Java 8+) — has implementation
    default void takeOff() {
        System.out.println("Taking off...");
    }

    // Static method (Java 8+)
    static void checkWeather() {
        System.out.println("Checking weather...");
    }
}

interface Swimmable {
    void swim();
}

// A class can implement MULTIPLE interfaces
class Duck extends Animal implements Flyable, Swimmable {
    public Duck(String name) { super(name, 1); }

    @Override
    public void makeSound() { System.out.println("Quack!"); }

    @Override
    public void fly() { System.out.println(name + " is flying"); }

    @Override
    public void land() { System.out.println(name + " landed"); }

    @Override
    public void swim() { System.out.println(name + " is swimming"); }
}

// Usage:
Duck duck = new Duck("Donald");
duck.fly();      // Donald is flying
duck.swim();     // Donald is swimming
duck.takeOff();  // Taking off... (default method)
Flyable.checkWeather();  // static method
```

---

## ⚖️ Abstract Class vs Interface — Master Comparison

| Feature | Abstract Class | Interface |
|---------|----------------|-----------|
| Keyword | `abstract class` | `interface` |
| Inheritance | `extends` (single) | `implements` (multiple) |
| Methods | Abstract + concrete | Abstract + default + static |
| Variables | Instance variables | Constants only (public static final) |
| Constructor | ✅ Can have | ❌ Cannot have |
| Access modifiers | Any | public (implicitly) |
| Multiple inheritance | ❌ No | ✅ Yes |
| State | ✅ Can maintain state | ❌ No instance state |
| When to use | Shared code + partial implementation | Contract / capability |

---

## 📐 When to Use Which?

```
Use Abstract Class when:
  ✅ Classes share common code (avoid duplication)
  ✅ You want to provide default behavior
  ✅ Classes have common state (instance variables)
  ✅ "Is-a" relationship with shared implementation
  Example: Animal (all animals eat, sleep — common behavior)

Use Interface when:
  ✅ Unrelated classes need same capability
  ✅ Multiple inheritance needed
  ✅ Defining a contract/API
  ✅ "Can-do" relationship
  Example: Flyable (birds, planes, drones — unrelated but all fly)

Real-world example:
  abstract class Shape { ... }  // shapes share area/perimeter concepts
  interface Serializable { }    // any class can be serializable
  interface Comparable { }      // any class can be compared
```

---

## 📐 Java 8+ Interface Features

```java
interface Logger {
    // Abstract method (must implement)
    void log(String message);

    // Default method (can override, has implementation)
    default void logError(String message) {
        log("ERROR: " + message);
    }

    // Static method (called on interface, not instance)
    static Logger getConsoleLogger() {
        return message -> System.out.println(message);
    }
}

// Functional interface (one abstract method) → can use lambda
Logger consoleLogger = message -> System.out.println(message);
consoleLogger.log("Hello");
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Interface variables are implicitly `public static final` — they're constants, not instance variables.
> 🚫 **Mistake 2:** A class can extend only ONE abstract class but implement MULTIPLE interfaces.
> 🚫 **Mistake 3:** Abstract class with no abstract methods is valid — it just can't be instantiated.
> 🚫 **Mistake 4:** Interface methods are implicitly `public` — you can't make them private (except Java 9+ private methods).

---

## 🎯 Exam Tips

> 💡 **The key difference:** Abstract class = partial implementation + state | Interface = pure contract.
> 💡 Java supports multiple interface implementation — this is how Java achieves multiple inheritance.
> 💡 If a class implements an interface but doesn't implement all methods → class must be abstract.
> 💡 Java 8 added default methods to interfaces — this blurred the line between abstract class and interface.

---

## ⚡ One-Minute Recap

- Abstract class: partial blueprint, can have state, single inheritance
- Interface: pure contract, no state, multiple implementation
- Abstract class: use for "is-a" with shared code
- Interface: use for "can-do" capabilities across unrelated classes
- Java 8+: interfaces can have default and static methods

---

## 📝 Probable Exam Questions

> **5-mark:** Compare abstract class and interface in Java. When would you use each?
> **Code:** Write an interface `Drawable` and an abstract class `Shape`. Show a class implementing both.
> **Short note:** Can an interface have a constructor? Can it have instance variables?
> **Explain:** What are default methods in Java interfaces? Why were they introduced?

---

---

# 7. Exception Handling

## 💡 Intuition First

> An **exception** is an unexpected event that disrupts normal program flow — like a car breaking down mid-journey. Exception handling is the plan for what to do when things go wrong — pull over, call for help, fix the problem, continue the journey.

**Real-world analogy:** An ATM transaction — if the network fails (exception), the ATM doesn't crash. It catches the error, shows "Service unavailable," and lets you try again.

---

## 📐 Exception Hierarchy (Java)

```
Throwable
├── Error (serious, don't catch)
│   ├── OutOfMemoryError
│   ├── StackOverflowError
│   └── VirtualMachineError
│
└── Exception
    ├── Checked Exceptions (must handle)
    │   ├── IOException
    │   ├── SQLException
    │   ├── FileNotFoundException
    │   └── ClassNotFoundException
    │
    └── RuntimeException (Unchecked — optional to handle)
        ├── NullPointerException
        ├── ArrayIndexOutOfBoundsException
        ├── ClassCastException
        ├── ArithmeticException (divide by zero)
        └── IllegalArgumentException
```

---

## 📐 try-catch-finally

```java
try {
    // Code that might throw an exception
    int result = 10 / 0;  // ArithmeticException!
    System.out.println("Result: " + result);  // never reached

} catch (ArithmeticException e) {
    // Handle the specific exception
    System.out.println("Error: " + e.getMessage());
    // Output: Error: / by zero

} catch (Exception e) {
    // Catch any other exception (more general)
    System.out.println("General error: " + e.getMessage());

} finally {
    // ALWAYS executes (cleanup code)
    System.out.println("Finally block executed");
    // Close files, release resources, etc.
}
```

### Execution Flow

```
Normal execution:
  try block → finally block → continue

Exception caught:
  try block (exception!) → catch block → finally block → continue

Exception NOT caught:
  try block (exception!) → finally block → propagate up call stack
```

---

## 📐 Multiple Catch Blocks

```java
public void readFile(String filename) {
    try {
        FileReader fr = new FileReader(filename);
        int data = fr.read();
        int result = 100 / data;

    } catch (FileNotFoundException e) {
        System.out.println("File not found: " + filename);

    } catch (IOException e) {
        System.out.println("Error reading file: " + e.getMessage());

    } catch (ArithmeticException e) {
        System.out.println("Math error: " + e.getMessage());

    } catch (Exception e) {
        // Most general — catches anything not caught above
        System.out.println("Unexpected error: " + e.getMessage());

    } finally {
        System.out.println("Cleanup done");
    }
}

// Rule: More specific exceptions BEFORE more general ones
// FileNotFoundException before IOException (FileNotFoundException IS-A IOException)
```

---

## 📐 throw and throws

```java
// throws: declares that method might throw an exception
public void withdraw(double amount) throws InsufficientFundsException {
    if (amount > balance) {
        throw new InsufficientFundsException("Insufficient funds");
    }
    balance -= amount;
}

// throw: actually throws an exception
public void setAge(int age) {
    if (age < 0 || age > 150) {
        throw new IllegalArgumentException("Invalid age: " + age);
    }
    this.age = age;
}

// Custom exception class
class InsufficientFundsException extends Exception {
    public InsufficientFundsException(String message) {
        super(message);
    }
}
```

---

## 📐 Checked vs Unchecked Exceptions

```
Checked Exceptions:
  Must be handled (try-catch) OR declared (throws)
  Compiler enforces this
  Examples: IOException, SQLException, FileNotFoundException

  public void readFile() throws IOException {  // must declare
      FileReader fr = new FileReader("file.txt");
  }

Unchecked Exceptions (RuntimeException):
  Optional to handle
  Compiler doesn't enforce
  Examples: NullPointerException, ArrayIndexOutOfBoundsException

  int[] arr = new int[5];
  arr[10] = 1;  // ArrayIndexOutOfBoundsException — no need to declare
```

---

## 📐 try-with-resources (Java 7+)

```java
// Automatically closes resources (implements AutoCloseable)
try (FileReader fr = new FileReader("file.txt");
     BufferedReader br = new BufferedReader(fr)) {

    String line = br.readLine();
    System.out.println(line);

} catch (IOException e) {
    System.out.println("Error: " + e.getMessage());
}
// fr and br automatically closed — no need for finally!
```

---

## 📐 Exception Propagation

```java
void methodC() {
    int result = 10 / 0;  // ArithmeticException thrown here
}

void methodB() {
    methodC();  // exception propagates up
}

void methodA() {
    try {
        methodB();  // exception caught here
    } catch (ArithmeticException e) {
        System.out.println("Caught in methodA: " + e.getMessage());
    }
}

// Call stack when exception occurs:
// methodA → methodB → methodC (exception!)
// Propagates: methodC → methodB → methodA (caught!)
```

---

## ⚖️ Exception Handling Best Practices

```
✅ Catch specific exceptions (not just Exception)
✅ Don't swallow exceptions (empty catch block)
✅ Use finally for cleanup (or try-with-resources)
✅ Create meaningful custom exceptions
✅ Log exceptions with context information
✅ Don't use exceptions for flow control

❌ Bad:
   try { ... }
   catch (Exception e) { }  // swallowing exception!

❌ Bad:
   try { ... }
   catch (Exception e) {
       if (condition) { ... }  // using exception for flow control
   }

✅ Good:
   try { ... }
   catch (FileNotFoundException e) {
       logger.error("File not found: " + filename, e);
       throw new ServiceException("Cannot load config", e);
   }
```

---

## ⚖️ throw vs throws

| Feature | `throw` | `throws` |
|---------|---------|---------|
| Purpose | Actually throws an exception | Declares possible exceptions |
| Location | Inside method body | Method signature |
| Followed by | Exception object | Exception class name(s) |
| Example | `throw new IOException()` | `void read() throws IOException` |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** `finally` always executes — even if there's a `return` in try or catch.
> 🚫 **Mistake 2:** Catching `Exception` or `Throwable` is too broad — catch specific exceptions.
> 🚫 **Mistake 3:** More specific exceptions must come BEFORE more general ones in catch chain.
> 🚫 **Mistake 4:** `Error` (OutOfMemoryError, StackOverflowError) should NOT be caught — they're unrecoverable.

---

## 🎯 Exam Tips

> 💡 **Exception hierarchy:** Throwable → Error / Exception → RuntimeException
> 💡 Checked = must handle (IOException) | Unchecked = optional (NullPointerException)
> 💡 `finally` always runs — used for resource cleanup.
> 💡 `throw` throws an exception | `throws` declares it in method signature.

---

## ⚡ One-Minute Recap

- Exception: unexpected event disrupting normal flow
- try: risky code | catch: handle exception | finally: always runs
- Checked: must handle (IOException) | Unchecked: optional (RuntimeException)
- throw: throw exception | throws: declare in method signature
- Custom exceptions: extend Exception (checked) or RuntimeException (unchecked)

---

## 📝 Probable Exam Questions

> **5-mark:** Explain exception handling in Java with try-catch-finally. Give an example.
> **Short note:** What is the difference between checked and unchecked exceptions?
> **Code:** Write a Java program that reads a file and handles FileNotFoundException and IOException.
> **Explain:** What is the difference between `throw` and `throws`?

---

---

# 🏁 Master Quick Revision Sheet — Object Oriented Programming

## ⚡ OOP Pillars Summary

```
┌─────────────────┬──────────────────────────────────────────────────┐
│ Pillar          │ Core Idea                                        │
├─────────────────┼──────────────────────────────────────────────────┤
│ Encapsulation   │ Bundle data + methods, hide internals            │
│ Inheritance     │ Child acquires parent's properties (is-a)        │
│ Polymorphism    │ Same interface, different behavior               │
│ Abstraction     │ Hide complexity, show only essentials            │
└─────────────────┴──────────────────────────────────────────────────┘
```

## 🔑 Key Facts to Remember

| Fact | Detail |
|------|--------|
| Encapsulation | Private fields + public methods |
| Inheritance keyword | `extends` (Java), `:` (C++) |
| Multiple inheritance | Not allowed for classes in Java (use interfaces) |
| Diamond problem | Ambiguity in multiple class inheritance |
| Overloading | Same class, different params, compile-time |
| Overriding | Child class, same params, runtime |
| Cannot override | static, final, private methods |
| Abstract class | Can have concrete methods, cannot instantiate |
| Interface | No state, no constructor, multiple implementation |
| Checked exception | Must handle (IOException) |
| Unchecked exception | Optional (RuntimeException) |
| `finally` | Always executes (cleanup) |
| `throw` | Throws exception object |
| `throws` | Declares exception in method signature |
| Dynamic dispatch | Method resolved based on actual object type at runtime |

## 🧠 Memory Tricks

- **OOP pillars:** "**E**very **I**ntelligent **P**rogrammer **A**bstracts" → Encapsulation, Inheritance, Polymorphism, Abstraction
- **Overloading vs Overriding:** "**Load** = same class | **Ride** = child class"
- **Abstract vs Interface:** "**Abstract** = partial blueprint | **Interface** = pure contract"
- **Checked vs Unchecked:** "**Checked** = compiler **checks** you handle it | **Unchecked** = runtime surprise"
- **Exception hierarchy:** "**T**hrowable has **E**rror and **E**xception, **E**xception has **R**untime"

## 🎯 Top 10 Most Probable Exam Questions

1. Explain the four pillars of OOP with examples
2. Explain encapsulation with a BankAccount code example
3. Explain inheritance — types, diamond problem, super keyword
4. Explain runtime polymorphism with Shape/Circle/Rectangle example
5. Compare overloading and overriding in a table
6. Compare abstract class and interface — when to use each
7. Write code demonstrating all four OOP pillars
8. Explain exception handling with try-catch-finally
9. Difference between checked and unchecked exceptions
10. What is dynamic dispatch? How does it enable polymorphism?

## 📊 Quick Comparison Tables

```
Overloading vs Overriding:
┌──────────────┬──────────────────┬──────────────────┐
│ Feature      │ Overloading      │ Overriding       │
├──────────────┼──────────────────┼──────────────────┤
│ Location     │ Same class       │ Parent + Child   │
│ Parameters   │ Different        │ Same             │
│ Resolved     │ Compile time     │ Runtime          │
│ Inheritance  │ Not needed       │ Required         │
└──────────────┴──────────────────┴──────────────────┘

Abstract Class vs Interface:
┌──────────────┬──────────────────┬──────────────────┐
│ Feature      │ Abstract Class   │ Interface        │
├──────────────┼──────────────────┼──────────────────┤
│ Methods      │ Abstract+Concrete│ Abstract+Default │
│ Variables    │ Instance vars    │ Constants only   │
│ Constructor  │ Yes              │ No               │
│ Inheritance  │ Single (extends) │ Multiple (impl.) │
└──────────────┴──────────────────┴──────────────────┘
```

---

> 📌 **End of Subject 09: Object Oriented Programming**
>
> Next: **Subject 10 — Programming Fundamentals** →

---

*Handbook generated for MSc Admission Preparation | JUST-Style Exam Focus*
*Version 1.0 | Object Oriented Programming*
