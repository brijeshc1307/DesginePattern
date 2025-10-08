# 🌀 Topic 7: Prototype Pattern (Creational Design Pattern)

## 🧠 Overview

The **Prototype Pattern** is a *Creational Design Pattern* that allows you to **create new objects by copying (cloning) an existing object**, rather than creating a new instance from scratch.

In simple words:
➡️ “If creating a new object is expensive, just clone an existing one.”

---

## 🎯 Real-Life Example

Imagine you’re designing a **video game** 🕹️.
You have a **monster object** with health, weapons, and skills.
Instead of creating every monster from scratch, you can **clone an existing monster** and make small modifications.

This saves time and resources, especially when object creation is costly.

---

## ⚙️ Key Idea

1. A class provides a **clone method**.
2. New objects are created by **copying the existing object**.
3. Useful when **creating a new object is heavy** (like database, files, network, or large objects).

---

## 🧩 C++ Example (Simple and Clear)

```cpp
#include <iostream>
#include <string>
using namespace std;

// Step 1: Prototype class
class Monster {
public:
    string type;
    int health;
    string weapon;

    Monster(string t, int h, string w) : type(t), health(h), weapon(w) {}

    // Step 2: Clone method
    Monster* clone() {
        return new Monster(type, health, weapon);
    }

    void showInfo() {
        cout << "Monster Type: " << type
             << ", Health: " << health
             << ", Weapon: " << weapon << endl;
    }
};

int main() {
    // Step 3: Original object
    Monster* dragon = new Monster("Dragon", 500, "Fire Breath");
    dragon->showInfo();

    // Step 4: Cloned object
    Monster* dragonClone = dragon->clone();
    dragonClone->weapon = "Ice Breath";  // modify cloned object
    dragonClone->showInfo();

    delete dragon;
    delete dragonClone;
    return 0;
}
```

---

## 🧾 Output

```
Monster Type: Dragon, Health: 500, Weapon: Fire Breath
Monster Type: Dragon, Health: 500, Weapon: Ice Breath
```

---

## 🔍 Explanation (In Simple Words)

* `Monster` is our **prototype object**.
* `clone()` method **creates a copy** of the object.
* We can **modify the cloned object** without affecting the original.
* This pattern is **very useful** when creating an object is expensive or complex.

---

## 🧠 When to Use Prototype Pattern

* When object creation is **time-consuming or costly**.
* When you want to **avoid repeated initialization code**.
* When you need **many similar objects** with minor differences.

---

## 🏁 Summary

| **Concept**  | **Description**                               |
| ------------ | --------------------------------------------- |
| Purpose      | Create new objects by cloning existing ones.  |
| Key Feature  | `clone()` method duplicates the object.       |
| Benefit      | Saves resources, avoids heavy initialization. |
| Example      | Video game monsters, document templates.      |
| Pattern Type | Creational Design Pattern                     |

---

✅ **Quick Comparison with Other Creational Patterns**

| Pattern          | Focus                     | Example                  |
| ---------------- | ------------------------- | ------------------------ |
| Singleton        | Only one object           | Logger, DB Connection    |
| Factory Method   | One type of object        | Car or Bike              |
| Abstract Factory | Families of objects       | Windows UI or Mac UI     |
| Builder          | Step-by-step construction | SportsCar or SUVCar      |
| Prototype        | Clone existing object     | Game monsters, templates |

---

Do you want me to **continue next with Topic 8: Adapter Pattern (Structural Design Pattern)** in the same style?
