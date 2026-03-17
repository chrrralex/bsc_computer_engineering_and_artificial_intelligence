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

Each class has the own built-in method called `__init__()`, which is always executed when the class is being initiated. You can see the `__init__()` as an entrypoint when you create an object by using the `MyClass()` expression. Consider the `Shape` class we've defined in the previous snippets. We can add the `__init__()` method in this way:

```python
class Shape:
    def __init__(self):
        print("Object created!")
```

When you create one, or more objects, you can see the string `"Object created!"` in the standard output (the console, or the monitor):

```python
s1 = Shape() # "Object created!"
s2 = Shape() # "Object created!"
s3 = Shape() # "Object created!"
```

But, wait a scond: what is the argument called `self` accepted by the `__init__()` method? This parameter is the current instance of the object you creating: `self` is like `this` in other OOP programming languages (like Java, or C++, or PHP). Through the `self` argument, you can set one, or more attributes of the object. So, the `__init__()` method is used to assign values to object properties, or to perform operations that are necessary when the object is being created. For example, if the `Shape` has two coords, `x` and `y`, you can set their default values directly into the `__init__()` method by using the `self` argument:

```python
class Shape:
    def __init__(self):
        self.x = 0
        self.y = 0
```

Optionally, you can add one, or more formal parameters to the `__init__()` method, so you can pass the attributes of the object directly when you use the `MyClass()` expression, when you're instatiating an object. In the case of the `Shape` class, you can write something like this:

```python
class Shape:
    def __init__(self, x, y):
        self.x = x
        self.y = y
```

and you can create one, or more instance in this way:

```python
s1 = Shape(10, 20)
s2 = Shape(-10, -5)

print(s1.x) # 10
print(s2.y) # -5
```

You must pay attention: in the previous case, the `x` and `y` arguments are positional arguments, so they're required. Whn you invoke the `Shape`'s `__init__()` method, you must specify both the `x` and the `y` parameters. Note that in the previous example we've created two instances of the `Shape` class: `s1` and `s2`.

A common way to ensure more flexibility of your code is to use the default parameters. For example, for the `x` and `y` coords, we assume that their default values are `0`. You can use the default parameters in the `__init__()` method:

```python
class Shape:
    def __init__(self, x = 0, y = 0):
        self.x = x
        self.y = y
```

in this way, you can create one, or more objects of the `Shape` entity in this way:

```python
s1 = Shape() # both x and y take the default values: x = 0, y = 0
s2 = Shape(100) # only y take the default value: x = 100, y = 0
s3 = Shape(y = 100) # only x take the default value: x = 0, y = 100
s4 = Shape(100, 200) # x = 100, y = 200
s5 = Shape(x = -10, y = -20) # x = -10, y = -20
```

You can use the named parameters also, as you can see in the last line of code of the previous example.

### 19.06. Object Attributes

As we've seen in the previous paragraph, each object has the own state, represented by its attributes and its values. When we have created the five instances (from `s1` to `s5`) in the previous example, each instance has the own lifecycle and the own `x` and `y` attributes. The syntaxt to access to an attribute by the object identifier is `identifier.attribute`. In our case, to access to the `x` and `y` coords of the `s1` instance, you can write:

```python
s1.x
s1.y
```

But what is an object attributes? An object attribute is a variable directly stored in the instance of a class, that represents a property of the object. For example, for an instance of the class `Student`, the `studentiId` could be a valid attrbute of the entity, in the OO phiosophy; for an instance of the class `Car`, the `model` could be a valid attribute of the entity. Attributes are effectively handled into the class from which you create all instances, but each instance has the own values. All the attributes of an instance compose the state of the instance itself. For example, if you have two shapes created from the class `Shape` and called `s1` and `s2`, the state of an instance is normally composed by the following two attributes:

- `x` defines the x coord in a hypothetical cartesian plane (or bidimensional plane).
- `y` defines the y coord in a hypothetical cartesian plane (or bidimensional plane).

An attribute has the own domain: it can be a string, an integer, a floating-point number, or a bytes sequence. Into the `__init__()` method of the class, you can set the object attributes by using the `self.attribute` syntaxt to access to the property `attribute` of the `self` object (an alias standing for "this current object") and the assignment operator (`=`) to assign a value to a specific property in this way:

```python
class Shape:
    def __init__(self, x = 0, y = 0):
        self.x = x
        self.y = y
```

Note that the `__init__()` method is only a way to set values to the attributes. Normally, if you remove the `__init__()` method from the `Shape` class, you must set attributes and values for each object manually, by writing something like this:

```python
class Shape:
    pass

s1 = Shape()
s1.x = 100
s1.y = -20

print(s1.x) # 100
print(s1.y) # -20
```

If you try to create a second object of the class `Shape`, Python interpreter will throw an error:

```python
s2 = Shape()

print(s2.x) # ERROR! AttributeError: 'Shape' object has no attribute 'x'
print(s2.y) # ERROR! AttributeError: 'Shape' object has no attribute 'y'
```

In practice, Python tells you that both the attributes `x` and `y` don't exist for the instance `s2`, cause we've defined a class without the `__init_()` method. Defines attributes and their default values by using the `__init__()` method is a best practice in Python, cause it ensures all instances created from a class have the same attributes and the same default values. The final definition (for now) of the our class `Shape` is this:

```python
class Shape:
    def __init__(self, x = 0, y = 0):
        self.x = x
        self.y = y
```

You can directly modify the value of an attributi in this way:

```python
s = Shape()

s.x = 100
x.y = s.x - 50
```

As we'll see in the next paragraphs, this isn't a good practice: it doesn't respect the principle of the encapsulation, one of the most important principles of the OOP. We'll analyze this principle in the remaining part of this chapter.

### 19.07. Object Methods

An object method (also called instance method) is a specific behavior very similarly to a Python function, but declared and defined into the class, that each object of the class can execute. Similarly to the attribute access, you can call an object method by writing the identifier of the object, the dot operator (`.`, also called member access operator) and the method identifier. For example, the objects created from the class `Shape` can be moved from a position in another by updating the `x` and `y` attributes. So, we can declare and define a method called `move()` in the body of the `Shape` class, like this:

```python
class Shape:
    def __init__(self, x = 0, y = 0):
        self.x = 0
        self.y = 0
    
    def move(self, x, y):
        self.x = x
        self.y = y
```

You can use the `move()` method only after you've created at least one instance of the class `Shape`, for example an object called `s`:

```python
s = Shape(10, 20)
print(s.x) # 10
print(s.y) # 20

s.move(100, -50)
print(s.x) # 100
print(s.y) # -50
```

As you can see, the values of the `x` and `y` attributes are changed in according to the values passed to the positional arguments accepted by the `move()` method. Note that the `move()` (and in general a method of an instance) always accepts the `self` argument as first parameter, but this is completely transparent when you call the method. It means when you call `s.move()`, you can pass only the arguments specified after the `self` argument (the first argument), in this case `x` and `y` positional arguments.

Another method we can add to the `Shape` class is `to_center()`, that moves the shape in the center of the cartesian plane (the point `(0, 0)`):

```python
class Shape:
    def __init__(self, x = 0, y = 0):
        self.x = 0
        self.y = 0
    
    def move(self, x, y):
        self.x = x
        self.y = y
    
    def to_center(self):
        self.x = 0
        self.y = 0

s = Shape(10, 20)
print(s.x) # 10
print(s.y) # 20

s.to_center()
print(s.x) # 0
print(s.y) # 0
```

In this case also, note that when we call the `to_center()` method, we don't specify any argument: the Python interpreter will infer automatically, at runtime, at what the `self` argument refers.

An object method is not different from a normal Python function: it can specify positional parameters, keyword parameters, positional-only parameters with `/`, keyword-only parameters with `*`, positional var-args with `*args` and keyword var-args with `**kwargs`. All the rules we've analyzed in the previous chapters for the function are the same for the object methods. The term "method" is the most correct in the OOP paradigm, meanwhile the term "function", or "procedure" is the most correct in the procedural paradigm.

### 19.08. Class Attributes

An object attribute is a variable stored in each instance of the class, that has the own life and own value. Change a value for an object attribute doesn't interfere with the same attribute, but stored in another object. If you have two instances of the class `Shape`, `s1` and `s2`, the following line of codes:

```python
s1.x = 70
s2.y = -30
```

change only the `x` attribute of `s1` (without modifying the `s2.x` attribute) and the `y` attribute of `s2` (without modifying the `s1.y` attribute).

Python allows another type of attribute in its OOP: the class attribute. A class attribute is an attribute binded and associated to the class. It means that all objects created from the class can see all the class attributes defined at class-level and their values are the same for all instances. For example, for the class `Shape` it's useful to store the default value of `x` and the default value of `y` in two class attributes:

```python
class Shape:
    DEFAULT_X_POSITION = 0
    DEFAULT_Y_POSITION = 0

    # ... other class code ...
```

Meanwhile properties defined in the `__init__()` method are different for each object (instance properties), all the properties defined outside methods at the class-level (tipically at the top of the class, or immediately after the class header) are class attributes. `DEFAULT_X_POSITION` and `DEFAULT_Y_POSITION` are both class attributes. You can access to a class attribute by using the following syntaxt:

```python
MyClass.classAttribute
```

In our case, if you want to print to the standard output the value of `DEFAULT_X_POSITION`, you can write this line of code:

```python
print(Shape.DEFAULT_X_POSITION) # 0
```

Although it is not considered good programming practice in the OOP paradigm, Python also allows you to access class attributes through an instance identifier:

```python
print(s.DEFAULT_Y_POSITION) # 0
```

You can change the value of a class property by using the class name, the dot operator and the name of the class attributes with the assignment operator:

```python
Shape.DEFAULT_X_POSITION = 10
```

But there is a trick in Python! If you try to modify a class attribute by an instance, you're not actually modifying the class variable; rather, the Python interpreter sees the assignment as creating a new property of the object (which will exist only for that object). This is a bad idea:

```python
print(Shape.DEFAULT_X_POSITION) # ok, it takes the value of the class attribute: 0
print(s.DEFAULT_X_POSITION) # ok, it takes the value of the class attribute: 0

Shape.DEFAULT_X_POSITION = 10
print(Shape.DEFAULT_X_POSITION) # ok, it takes the new value of the class attribute: 10
print(s.DEFAULT_X_POSITION) # ok, it takes the new value of the class attribute: 10

s.DEFAULT_X_POSITION = 20
print(Shape.DEFAULT_X_POSITION) # ok, it takes the last value of the class attribute: it's always 10
print(s.DEFAULT_X_POSITION) # bad idea! it takes the value of the object attribute called DEFAULT_X_POSITION: 20
```

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
