# 19. Classes and Objects

### 19.01. Object-Oriented Programming Overview: OO, OOD and OOP

The OOP (Object-Oriented Programming) is a programming language paradigm you can use to model the reality in a simpliest way than using only the functions. There OO (Object-Oriented) is the philosophy behind the OOP paradigm and the OOD (Object-Oriented Design) indicates the art of modeling the reality by exploiting the rules of the OO.

In the OO philosophy, each acton, or process, or objects of the real world is an independent entity that has the own lifecycle and the own behaviors, moreover the own interactions with the other things of the world. For example, if you are modeling a company, you may have an entity called "Person", that represents a person in the real world. A person has securely a first name, a last name, a date of birth and so many other informations. If the focus is on the business car that a person can use, you can create a second entity called "Business Car" (with common attributes like brand, color, model, year and so on). You can create a relationship between the entity "Person" and the entity "Business Car": a person can use zero, one, or more business car in a company.

Python conforms perfectly to the OOP paradigm and you can use classes and objects to model the part of the real world you considering for your software. Python is an OOP language, allowing you to structure your code using classes and objects for better organization and reusability. Some advantages of the OOP paradigm are:

- Provides a clear structure to programs.
- Makes code easier to maintain, reuse, and debug.
- Helps keep your code DRY (Don't Repeat Yourself).
- Allows you to build reusable applications with less code.

The DRY principle means you should avoid writing the same code more than once. Move repeated code into functions, or classes and reuse it.

In the OOD, the entioties are called ADTs (Abstract Data Types).

### 19.02. What is a Class?

Classes and objects are the two core concepts in object-oriented programming. A class defines what an object should look like, and an object is created based on that class. For example:

- A class called `Fruit`, in a food world, models the fruit entity, like: apples, bananas, kiwis, mangos and so on.
- A class called `Emplyee`, in a company world, models an employee: managers, developers, assistants and so on.
- A class called `Car`, in a car racing world, models a car of specific model: Audi, Peugeot, Toyota, Volvo, Fiat and so on.
 
A class is a blueprint from which you can create various (theoretically infinite) instances in a pragmatic way and according to certain rules.

### 19.03. What is an Object?

An object (or instance) in Python OOP is a concrete realization of a class. Cuase a class defines a blueprint to create objects, an object is a specific element created from that blueprint. Each object has its own attributes (data) and can use the methods (functions) defined in the class.

For example, if you consider a class called `Fruit`, you can create these objects from this: `apple`, `banana`, `kiwi`, `mango` and so on. Each instance has the own lifecycle: you can create an object in different moment of the program execution. Moreover, an object can be deallocated (removed) from the main memory directly by the Python interpreter at any time. Each object has the own state, represented by all attributes.

To summarize: an object (instance) is a specific instance of a class that contains its own data and can use the methods declared and defined in the class.

### 19.04. Class Definition

You can define a class by using the `class` keyword. A class has an own name, in the following code we defines the class `Shape`, that represents a geometric shape (like circles, triangles, rectangles and so on):

```python
class Shape:
    pass
```

We use the `pass` keyword when we don't say nothing about the class implementation (its attributes and its methods). You can access to the name of the class, in our case `Shape`, by using the `__name__` attribute in this way:

```python
print(Shape.__name__) # "Shape"
```

In general the syntaxt to define a class is:

```python
class ClassName:
    implementation
```

### 19.05. Object Creation

You can create an object (or instance) of the class `Shape` we've defined in the previous paragraph by using the following syntaxt:

```python
shape = Shape()
```

Cause a class is a blueprint, you can create as many objects as you want by using `Shape()`:

```python
a = Shape()
b = Shape()
c = Shape()
```

In the previous code, we've created three instances: `a`, `b` and `c`. Both these three instances have the own allocated memory, necessary to contain all attributes defined in the blueprint (the `Shape` class). The expression `Shape()`, as we will see in the next paragraph, represents the constructor invocation of the `Shape()` class. A constructor is a special method of a class that has the main purpose to set all attributes.

In general, the basic syntaxt to create an instance is:

```python
instance_name = ClassName(arguments)
```

In the next paragraph we'll see the meaning of the `arguments` inside the round brackets.

You can delete explicitly an object by using the `del` keyword:

```python
del a
```

When the Python interpreter reads this line of code, it deallocates all memory about the `a` instance and the object doesn't exist after this operation.

### 19.07. `__init__()` Method and `self` Argument
<!-- to do -->

### 19.06. Object Attributes
<!-- to do -->

### 19.07. Object Methods
<!-- to do -->

### 19.08. Class Attributes
<!-- to do -->

### 19.09. Encapsulation: Protected Attributes and Methods with `_` and Private Attributes and Methods with `__`
<!-- to do -->

### 19.10. Class Methods with `@classmethod`
<!-- to do -->

### 19.11. Static Methods with `@staticmethod`
<!-- to do -->

### 19.12. Magic Methods: `__str__()`, `__eq__()` and `__repr__()`
<!-- to do -->

### 19.13. Getters and Setters with `@property`
<!-- to do -->

### 19.14. Inheritance and the `super()` Method
<!-- to do -->

### 19.15. Multiple Inheritance
<!-- to do -->

### 19.16. Method Overriding with `@override`
<!-- to do -->

### 19.17. MRO (Method Resolution Order)
<!-- to do -->

### 19.18. Polymorphism
<!-- to do -->

### 19.19. Abstract Classes and `@abstractmethod` 
<!-- to do -->

### 19.20. Dataclasses with `@dataclass`
<!-- to do -->

### 19.21. Aggregation Relationship
<!-- to do -->

### 19.22. Composition Relationship
<!-- to do -->

### 19.23. Reflection
<!-- to do -->

### 19.24. Introspection
<!-- to do -->

### 19.25. Singleton
<!-- to do -->
