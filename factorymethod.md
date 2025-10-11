# Factory Method Pattern (Creational Design Pattern)


The **Factory Method Pattern** is another *Creational Design Pattern* that provides an **interface for creating objects**, but **lets subclasses decide which class to instantiate**.

In simple words:
➡️ Instead of creating objects directly using `new`, you use a **factory** (a special function or class) that decides **which object to create** based on input or logic.

---

## Real-Life Example

Imagine a **vehicle factory**.
You ask the factory for a vehicle type (like *Car* or *Bike*).
You don’t care *how* it’s made — you just get the right object.

Similarly, in C++, a Factory Method hides object creation details and provides flexibility.

---

##  Key Idea

* Define an **interface (base class)** for creating objects.
* Let **derived classes** decide which object to create.
* The **client code** uses only the base class — not the concrete classes.

---

##  C++ Example (Simple and Clear)

```cpp
#include <iostream>
using namespace std;

// Step 1: Create an interface (abstract base class)
class Vehicle {
public:
    virtual void start() = 0; // pure virtual function
};

// Step 2: Create concrete classes
class Car : public Vehicle {
public:
    void start() override {
        cout << "Car started 🚗" << endl;
    }
};

class Bike : public Vehicle {
public:
    void start() override {
        cout << "Bike started 🏍️" << endl;
    }
};

// Step 3: Create a Factory class
class VehicleFactory {
public:
    static Vehicle* createVehicle(string type) {
        if (type == "car")
            return new Car();
        else if (type == "bike")
            return new Bike();
        else
            return nullptr;
    }
};

// Step 4: Client code
int main() {
    Vehicle* v1 = VehicleFactory::createVehicle("car");
    Vehicle* v2 = VehicleFactory::createVehicle("bike");

    if (v1) v1->start();
    if (v2) v2->start();

    // Clean up
    delete v1;
    delete v2;

    return 0;
}
```

---

## 🧾 Output

```
Car started 🚗
Bike started 🏍️
```

---

## 🔍 Explanation (In Simple Words)

* The **`Vehicle`** class defines a common interface.
* The **`Car`** and **`Bike`** classes implement it differently.
* The **`VehicleFactory`** decides which object to create based on input.
* The **main()** function only calls `createVehicle()` — it doesn’t care how the objects are made.

So, if tomorrow you add a **Truck** class, you can just update the factory — not the client code.
✅ That’s flexibility and maintainability in action!

---

## When to Use Factory Method

* When the exact type of object to create is **determined at runtime**.
* When you want to **avoid tight coupling** between code and object creation.
* When creating an object involves **complex logic**.

---

## 🏁 Summary

| **Concept**  | **Description**                                                    |
| ------------ | ------------------------------------------------------------------ |
| Purpose      | Creates objects without exposing the creation logic to the client. |
| Key Feature  | Uses a common interface, returns derived class instances.          |
| Benefit      | Promotes loose coupling and flexibility.                           |
| Example      | VehicleFactory creating Car or Bike.                               |
| Pattern Type | Creational Design Pattern                                          |

---

Would you like me to continue with **Topic 5: Abstract Factory Pattern** next — explained in the same simple English + C++ code format?
