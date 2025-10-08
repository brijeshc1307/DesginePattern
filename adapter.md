# 🔗 Topic 8: Adapter Pattern (Structural Design Pattern)

## 🧠 Overview

The **Adapter Pattern** is a *Structural Design Pattern* that allows **incompatible interfaces to work together**.

In simple words:
➡️ “It acts as a bridge between two classes that otherwise cannot communicate.”

---

## 🎯 Real-Life Example

Imagine you have a **USB device** and a **power socket**.
The USB plug doesn’t fit the socket directly — you need an **adapter**.
Similarly, in C++, an Adapter **translates one interface to another** so classes can work together.

---

## ⚙️ Key Idea

1. Adapter wraps an **existing class** with a new interface.
2. Client code interacts with the **expected interface**, not the adaptee.
3. Helps integrate **legacy or third-party code** without modification.

---

## 🧩 C++ Example (Simple and Clear)

```cpp
#include <iostream>
using namespace std;

// Step 1: Target interface (what client expects)
class Target {
public:
    virtual void request() = 0;
};

// Step 2: Adaptee (existing class with incompatible interface)
class Adaptee {
public:
    void specificRequest() {
        cout << "Specific request from Adaptee class 🔧" << endl;
    }
};

// Step 3: Adapter class (makes Adaptee compatible with Target)
class Adapter : public Target {
private:
    Adaptee* adaptee;
public:
    Adapter(Adaptee* a) : adaptee(a) {}
    void request() override {
        // Translate request to adaptee’s method
        adaptee->specificRequest();
    }
};

// Step 4: Client code
int main() {
    Adaptee* oldSystem = new Adaptee();
    Target* adapter = new Adapter(oldSystem);

    // Client calls request() on Target
    adapter->request();

    delete oldSystem;
    delete adapter;
    return 0;
}
```

---

## 🧾 Output

```
Specific request from Adaptee class 🔧
```

---

## 🔍 Explanation (In Simple Words)

* `Adaptee` has a method (`specificRequest`) that client **cannot use directly**.
* `Target` defines the **interface the client expects**.
* `Adapter` **wraps Adaptee** and makes it compatible with Target.
* Client code works with **Target interface only**, no changes needed to Adaptee.

---

## 🧠 When to Use Adapter Pattern

* You have **existing classes** with incompatible interfaces.
* You want to **reuse legacy or third-party code** without modification.
* You want to provide a **common interface** to different implementations.

---

## 🏁 Summary

| **Concept**  | **Description**                                                         |
| ------------ | ----------------------------------------------------------------------- |
| Purpose      | Allows incompatible interfaces to work together.                        |
| Key Feature  | Adapter converts interface of a class into another expected by clients. |
| Benefit      | Reuse existing code without changing it.                                |
| Example      | USB-to-socket adapter, legacy code integration.                         |
| Pattern Type | Structural Design Pattern                                               |

---

✅ **Quick Comparison with Structural Patterns**

| Pattern   | Purpose                                     |
| --------- | ------------------------------------------- |
| Adapter   | Convert interface to expected one           |
| Bridge    | Separate abstraction and implementation     |
| Composite | Treat group of objects like a single object |
| Decorator | Add functionality to objects dynamically    |
| Facade    | Provide simple interface to complex system  |
| Flyweight | Reduce memory usage by sharing objects      |
| Proxy     | Control access to objects                   |

---

Do you want me to **continue next with Topic 9: Bridge Pattern (Structural Design Pattern)** in the same simple + C++ code style?
