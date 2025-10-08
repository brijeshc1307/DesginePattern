# ⚙️ **2. SOLID Principles**

## 📘 **Overview**

The **SOLID principles** are **five key rules** in object-oriented programming that make your code:

* **Easier to understand**
* **Easier to maintain**
* **Easier to extend** without breaking existing code

They act as a **guideline** for writing clean and reliable software — and are the **base for many design patterns**.

---

## 🔠 **What Does SOLID Stand For?**

| **Letter** | **Principle**                         | **Meaning**                                                                 |
| ---------- | ------------------------------------- | --------------------------------------------------------------------------- |
| **S**      | Single Responsibility Principle (SRP) | A class should have only **one reason to change**.                          |
| **O**      | Open/Closed Principle (OCP)           | Classes should be **open for extension**, but **closed for modification**.  |
| **L**      | Liskov Substitution Principle (LSP)   | Subclasses should be usable **without breaking** the parent class behavior. |
| **I**      | Interface Segregation Principle (ISP) | Don’t force a class to implement **unused interfaces**.                     |
| **D**      | Dependency Inversion Principle (DIP)  | Depend on **abstractions**, not concrete implementations.                   |

---

## 🧩 **1. Single Responsibility Principle (SRP)**

> A class should do **only one job** and have **one reason to change**.

### ❌ Bad Example

```cpp
#include <iostream>
#include <fstream>
using namespace std;

class Report {
public:
    void generateReport() {
        cout << "Report generated\n";
    }
    void saveToFile() {
        ofstream file("report.txt");
        file << "Saving report to file...";
    }
};
```

➡️ The class `Report` is doing **two jobs**:

* Generating a report
* Saving it to a file

If file-saving logic changes, this class must also change — violating SRP.

---

### ✅ Good Example (SRP Applied)

```cpp
#include <iostream>
#include <fstream>
using namespace std;

class Report {
public:
    void generateReport() {
        cout << "Report generated\n";
    }
};

class FileSaver {
public:
    void saveReport() {
        ofstream file("report.txt");
        file << "Saving report to file...";
    }
};
```

➡️ Each class now has a **single responsibility**.

---

## 🧩 **2. Open/Closed Principle (OCP)**

> Classes should be **open for extension** but **closed for modification**.

### ❌ Bad Example

```cpp
class AreaCalculator {
public:
    double area(string shape, double a, double b) {
        if (shape == "rectangle") return a * b;
        if (shape == "triangle") return 0.5 * a * b;
        return 0;
    }
};
```

➡️ If we add a new shape (circle, hexagon), we must **modify** this class — breaking OCP.

---

### ✅ Good Example (OCP Applied)

```cpp
#include <iostream>
using namespace std;

class Shape {
public:
    virtual double area() = 0;  // abstract method
};

class Rectangle : public Shape {
    double w, h;
public:
    Rectangle(double w, double h): w(w), h(h) {}
    double area() override { return w * h; }
};

class Triangle : public Shape {
    double b, h;
public:
    Triangle(double b, double h): b(b), h(h) {}
    double area() override { return 0.5 * b * h; }
};

void printArea(Shape* s) {
    cout << "Area: " << s->area() << endl;
}
```

➡️ To add a new shape (like Circle), you **extend** the code (create a new class) without modifying existing ones.

---

## 🧩 **3. Liskov Substitution Principle (LSP)**

> Subclasses should **replace** their base classes **without breaking** functionality.

### ❌ Bad Example

```cpp
class Bird {
public:
    virtual void fly() { cout << "Flying\n"; }
};

class Penguin : public Bird {
public:
    void fly() override { cout << "Penguins can’t fly!\n"; }  // Wrong behavior
};
```

➡️ `Penguin` violates LSP — it **can’t fly**, so substituting it for a `Bird` breaks the program logic.

---

### ✅ Good Example (LSP Applied)

```cpp
class Bird { public: virtual void eat() = 0; };
class FlyingBird : public Bird { public: virtual void fly() = 0; };

class Sparrow : public FlyingBird {
public:
    void eat() override { cout << "Sparrow eating\n"; }
    void fly() override { cout << "Sparrow flying\n"; }
};

class Penguin : public Bird {
public:
    void eat() override { cout << "Penguin eating\n"; }
};
```

➡️ Now, `Penguin` doesn’t break anything — it doesn’t belong to `FlyingBird`.

---

## 🧩 **4. Interface Segregation Principle (ISP)**

> Don’t force a class to **implement interfaces it doesn’t use**.

### ❌ Bad Example

```cpp
class IWorker {
public:
    virtual void work() = 0;
    virtual void eat() = 0;
};

class Robot : public IWorker {
public:
    void work() override { cout << "Robot working\n"; }
    void eat() override { cout << "Robot doesn't eat!\n"; } // unnecessary
};
```

---

### ✅ Good Example (ISP Applied)

```cpp
class IWorkable { public: virtual void work() = 0; };
class IEatable { public: virtual void eat() = 0; };

class Human : public IWorkable, public IEatable {
public:
    void work() override { cout << "Human working\n"; }
    void eat() override { cout << "Human eating\n"; }
};

class Robot : public IWorkable {
public:
    void work() override { cout << "Robot working\n"; }
};
```

➡️ Interfaces are now **segregated** — no unnecessary methods.

---

## 🧩 **5. Dependency Inversion Principle (DIP)**

> High-level modules should not depend on low-level modules;
> both should depend on **abstractions**.

### ❌ Bad Example

```cpp
class LightBulb {
public:
    void turnOn() { cout << "Light ON\n"; }
};

class Switch {
    LightBulb bulb;
public:
    void operate() { bulb.turnOn(); }
};
```

➡️ `Switch` is tightly coupled to `LightBulb`.
If we add a `Fan`, we must modify the `Switch` class.

---

### ✅ Good Example (DIP Applied)

```cpp
#include <iostream>
using namespace std;

class Device {
public:
    virtual void turnOn() = 0;
};

class LightBulb : public Device {
public:
    void turnOn() override { cout << "Light ON\n"; }
};

class Fan : public Device {
public:
    void turnOn() override { cout << "Fan ON\n"; }
};

class Switch {
    Device* device;
public:
    Switch(Device* dev): device(dev) {}
    void operate() { device->turnOn(); }
};

int main() {
    LightBulb bulb;
    Fan fan;
    Switch s1(&bulb);
    Switch s2(&fan);

    s1.operate();
    s2.operate();
}
```

➡️ Now the `Switch` depends on the **abstract interface**, not a specific class — it can work with any `Device`.

---

## 🏁 **Summary Table**

| **Principle** | **Key Idea**          | **Example Concept**                           |
| ------------- | --------------------- | --------------------------------------------- |
| **S**         | Single Responsibility | One class → one job                           |
| **O**         | Open/Closed           | Extend, don’t modify                          |
| **L**         | Liskov Substitution   | Derived classes shouldn’t break base behavior |
| **I**         | Interface Segregation | Small, specific interfaces                    |
| **D**         | Dependency Inversion  | Depend on abstractions, not concrete classes  |

---

Would you like me to continue with
**Topic 3: Singleton Pattern (Creational Design Pattern)** — the first real design pattern in the list, explained in simple English with C++ code?
