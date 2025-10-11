# Singleton Pattern (Creational Design Pattern)

The **Singleton Pattern** is one of the most commonly used *Creational Design Patterns*.
Its main goal is to **ensure that only one object (instance)** of a class is created and that it is **accessible globally** throughout the program.

You can think of it like a **single manager** in a company — only one manager exists, and everyone uses the same manager for communication.

---

##  Why Use Singleton?

We use a Singleton when:

* Only **one instance** of a class should exist.
* You need **a global access point** to that instance.
* Useful for things like:

  * Logging
  * Database connection
  * Configuration manager
  * Thread pool
  * Printer spooler

---

## Key Features

1. **Private constructor** → Prevents direct object creation using `new`.
2. **Static instance pointer** → Holds the single object of the class.
3. **Public static method (`getInstance`)** → Gives access to that one instance.

---

## C++ Example (Simple and Clear)

```cpp
#include <iostream>
using namespace std;

class Singleton {
private:
    // Step 1: Create a static pointer to hold one instance
    static Singleton* instance;

    // Step 2: Make constructor private so no one can create object directly
    Singleton() {
        cout << "Singleton instance created!" << endl;
    }

public:
    // Step 3: Delete copy constructor and assignment operator
    Singleton(const Singleton&) = delete;
    Singleton& operator=(const Singleton&) = delete;

    // Step 4: Public method to access the single instance
    static Singleton* getInstance() {
        if (instance == nullptr) {
            instance = new Singleton(); // create only once
        }
        return instance;
    }

    void showMessage() {
        cout << "Hello from Singleton object!" << endl;
    }
};

// Step 5: Initialize static instance to NULL
Singleton* Singleton::instance = nullptr;

// Step 6: Main function
int main() {
    Singleton* s1 = Singleton::getInstance();
    Singleton* s2 = Singleton::getInstance();

    s1->showMessage();

    if (s1 == s2) {
        cout << "Both pointers point to the same instance!" << endl;
    } else {
        cout << "Different instances!" << endl;
    }

    return 0;
}
```

---

## Output

```
Singleton instance created!
Hello from Singleton object!
Both pointers point to the same instance!
```

---

## Explanation (In Simple Words)

* When `getInstance()` is called the first time → it creates one object.
* The next time you call `getInstance()` → it returns the **same old object**.
* This way, **only one object** ever exists in the entire program.

---

## Thread-Safe Singleton (Modern C++11 version)

```cpp
#include <iostream>
#include <mutex>
using namespace std;

class Singleton {
private:
    static Singleton* instance;
    static mutex mtx;

    Singleton() { cout << "Thread-safe Singleton created!" << endl; }

public:
    static Singleton* getInstance() {
        lock_guard<mutex> lock(mtx);
        if (instance == nullptr)
            instance = new Singleton();
        return instance;
    }
};

Singleton* Singleton::instance = nullptr;
mutex Singleton::mtx;

int main() {
    Singleton* s1 = Singleton::getInstance();
    Singleton* s2 = Singleton::getInstance();
    return 0;
}
```

---

## Summary

| **Concept** | **Description**                                     |
| ----------- | --------------------------------------------------- |
| Purpose     | Ensure only one instance of a class exists.         |
| Constructor | Private (no direct creation).                       |
| Access      | Through a static method (`getInstance()`).          |
| Common Uses | Database connection, logger, configuration manager. |
| Benefit     | Saves memory, ensures consistency, central control. |

---

Would you like me to continue next with **Topic 4: Factory Method Pattern (Creational Design Pattern)** in the same simple style (with explanation + C++ code)?
