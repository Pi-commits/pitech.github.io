---
layout: post
title: "Design Patterns"
comments: true
keywords: "design patterns, system design"
date: 2023-10-26 23:41:00 +05:30
tags: SystemDesign chapter1
---

### Creational patterns

These patterns provide various object creation mechanisms, which increase flexibility and reuse of existing code.
<br/>

#### Singleton

**Singleton** is a creational design pattern that lets you ensure that a class has only one instance, while providing a global access point to this instance.

##### How it's Done
<br/>
All implementations of the Singleton have these two steps in common:

* Make the default constructor private, to prevent other objects from using the new operator with the Singleton class.
* Create a static creation method that acts as a constructor. Under the hood, this method calls the private constructor to create an object and saves it in a static field. All following calls to this method return the cached object.
<br/>
If your code has access to the Singleton class, then it’s able to call the Singleton’s static method. So whenever that method is called, the same object is always returned.
<br/>

```java
// Classical Java implementation of singleton 
// design pattern
class Singleton
{
    private static Singleton obj;
 
    // private constructor to force use of
    // getInstance() to create Singleton object
    private Singleton() {}
 
    public static Singleton getInstance()
    {
        if (obj==null)
            obj = new Singleton();
        return obj;
    }
}
```

##### Examples
* Hardware access
* Database connections
* Config files
<br/>

#### Factory Method

**Factory Method** is a creational design pattern that provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.


##### How it's Done
<br/>


```python
# Python Code for factory method 
# it comes under the creational 
# Design Pattern
 
class FrenchLocalizer:
 
    """ it simply returns the french version """
 
    def __init__(self):
 
        self.translations = {"car": "voiture", "bike": "bicyclette",
                             "cycle":"cyclette"}
 
    def localize(self, msg):
 
        """change the message using translations"""
        return self.translations.get(msg, msg)
 
class SpanishLocalizer:
    """it simply returns the spanish version"""
 
    def __init__(self):
        self.translations = {"car": "coche", "bike": "bicicleta",
                             "cycle":"ciclo"}
 
    def localize(self, msg):
 
        """change the message using translations"""
        return self.translations.get(msg, msg)
 
class EnglishLocalizer:
    """Simply return the same message"""
 
    def localize(self, msg):
        return msg
 
def Factory(language ="English"):
 
    """Factory Method"""
    localizers = {
        "French": FrenchLocalizer,
        "English": EnglishLocalizer,
        "Spanish": SpanishLocalizer,
    }
 
    return localizers[language]()
 
if __name__ == "__main__":
 
    f = Factory("French")
    e = Factory("English")
    s = Factory("Spanish")
 
    message = ["car", "bike", "cycle"]
 
    for msg in message:
        print(f.localize(msg))
        print(e.localize(msg))
        print(s.localize(msg))
```

##### Advantages of using Factory method: 
1. We can easily add new types of products without disturbing the existing client code.
2. Generally, tight coupling is being avoided between the products and the creator classes and objects.

##### Examples
* Notification System (Email, MSG, Call, Etc.)
* Language Translation App
* Ridesharing App
<br/>




#### Builder


### Structural patterns

These patterns explain how to assemble objects and classes into larger structures while keeping these structures flexible and efficient.
<br/>

#### Adapter

### Behavioral patterns

These patterns are concerned with algorithms and the assignment of responsibilities between objects.

<br/>

#### Strategu
#### Observer
#### State