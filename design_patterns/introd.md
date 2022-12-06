# DESIGN PATTERNS

# Introduction
- reusable and named solutions to recurring problems in a context.

# SOLID Principles (Oop principles)
- `Single responsibility`: 
    - each class has a single responsibility
- `Open-closed`:
    - classes will be open for extension and closed for modification; use inheritance.
- `Liskov subsitution`:
    - when you inherit from the class, you ust be able to substitute the subclassfor the baseclass without things going wrong.
- `Interface segregation`:
    - you should define fine-grained interfaces as specific to the client that is going to use them.
- `Dependency injection`:
    - high level modules should not depend on low-level modules; however both should depend upon abstraction, which could be interfaces or abstract classes.

# Principles vs Patterns
- you don't have to start with principles
- Principles - Low level knowledge
- Patterns - High level knowledge - Proven solutions

# Pattern classification
- Purpose [creational] = related to object instanciation, providing a way to decouple the code that creates the object from the object itself ( Builder, Factory, Absract factory, Prototype, Singleton ); abstracts the process of creating an object, hiding how objects are created.
- Purpose [behavioral] = concerned about how object interact and distribute responsibility ( Visitor, strategy, observer, chain of responsibility, interpreter, template, iterator, Mediator, Memento, State, command)
- Purpose [structural] = describe how classes and objects are composed to create new functionality ( decorator, bridge, facade, adapter, composite, proxy, flyweight )

# ------- Behavioral Pattern ------------
## Strategy Pattern
- defines a family of algorithms, encapsulates each one and makes them interchangeable.
- Strategy lets the algorithm vary independently from clients that use it.
- change a part of a system independently of all other parts; swap behavior at run time.
- encapsulating what changes; favoring composition over inheritance; open-close principle; programming to interfaces;
- strategies are like algorithms, can have same inputs and outputs but different implementations.
- add alt url image.
- payment system

## State Pattern
- models a state as object encapsulating a state as specific methods in separate classes. So when the object changes its state the functionality of the method also changes

## Command Pattern 
encapsulates method invocations as objects allowing clients to execute different operations without knowing anything about them

## Observer Pattern
- notifie when the state of an object changes, minimizing the interdependency between them.

## Template method Pattern
- defines an algorithm in a method, leaving some steps to be redefined by subsclasses.
- In Template pattern, an abstract class exposes defined way(s)/template(s) to execute its methods. Its subclasses can override the method implementation as per need but the invocation is to be in the same way as defined by an abstract class. This pattern comes under behavior pattern category.

## Bonus tip
- Template method Pattern is an alternative to the strategy method. TMP uses inheritance to change part of the algorithm, and the strategy pattern uses composition to change the entire algorithm.

# ----------- Creational Patterns ---------
## Singleton Pattern
- assure a class has only one instance, providing a global point to access to it.
- problem occures in multithreading environment; so we should synchronize access to the static method getInstance.

## Factory and Abstract Factory

## Builder Pattern
- builds a complex object using simple objects, and with a step by step approach;
- use public static nested class: User { public static UserBuilder}. 
    - eg. User has private cstor its argument is UserBuilder with only getter methods,
    - UserBuilder has only setter methods.
- https://www.digitalocean.com/community/tutorials/builder-design-pattern-in-java

# ---------- Structural Patterns ------------

## Facade Pattern
- simplifies an interface to a subsytem, decoupling a client from it; 

## Decorator Pattern
- attach additional responsibilities to an object dynamically instead of adding them via inheritance.

## Adapter Pattern
- it is used so that two unrelated interfaces can work together. The object that joins these unrelated interface is called an Adapter.
- eg. Mobile Charger;
    - Define class Volt,
    - Class Socket with one getVolt() that return a Voltage of 120V;
    - Define SocketAdapter interface with all getVoltX() adapters;
    - then the concreteSocketAdapter will override these methods by implementing SocketAdapter and extending Socket;
    - or by implementing SocketAdapter with private field Socket

## Proxy Pattern
- provides a surrogate for another object to control access to it.
- common uses of a proxy: 
    - Remote calls
    - Security
    - Cache
    - Virtual

# Comparisons
- deco adds one or more respo to an object
- proxy controls access to object
- proxy creates the instance, but decorator takes an instance in the constructor.
- Decorator and Adapters wrap an existing object, but Adapters changes the object interface.
- Decorator adds responsibilities to an object.
- Proxy provides the same interface of the object it grabs. 
- Decorator provides the same interface, but in an enhanced way.
- An adapter provides a different interface to its subject

# Other Patterns

## Enterprise Development Patterns
## Functional Programming Pattern
## Reactive Programming Pattern
- non-blocking
- asynchronous
- declarative
