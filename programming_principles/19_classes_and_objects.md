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

Encapsulation is one of the three main principles of the OOP. Encapsulation in OOP is the concept of bundling data (attributes of an object) and methods (behavior of an object) that operate on that data into a single unit, usually called a class, and restricting direct access to some of the object's components. In short: Encapsulation is about protecting data inside a class, or an object.

To understand completely the encapsulation principles, let's analyze the three its main concepts:

- Data hiding: all object attributes, in a class, should be accessible by only the object. This concepts means attributes and methods should be private, or protected, when they're cannot be exposed outside from the class where they're defined.
- Public interface: you interact with the object through specific methods (like getters/setters). These methods are called access methods (or, sometimes, accessors also). The set methods can set the value of a specific attribute; the get methods can return the value of a specific attribute.
- Access control: an attribute, or a method of a class can be qualified by one of three access level: public (member accessible from the outside of the class), protected (member accessible from the same module where the class is defined), or private (member not accessible from the outside of the class).

Previously, we've defined a class called `Shape` representing a generic geometric shape. Previously, we've defined two attributes for the `Shape` objects: `x` and `y`, the coords where the shape is located in a bidimensional plane. Encapsulation involves not making these attributes visible outside the class. So, we modify the `Shape` class in this way:

```python
class Shape:
    DEFAULT_X_POSITION = 0
    DEFAULT_Y_POSITION = 0

    def __init__(self, x = 0, y = 0):
        self.__x = 0
        self.__y = 0
    
    def to_center(self):
        self.__x = 0
        self.__y = 0
    
    def move(self, x, y):
        self.__x = x
        self.__y = y
```

Note that we've specified the double-underscore prefix (`__`) before each `x` and `y` identifiers. In Python, the double-underscore prefix has a specific meaning: it makes an attribute a private attribute, that cannot be accessible from the outside of the class. If you try to write something like this:

```python
s = Shape()
print(s.__x) # ERROR! AttributeError: 'Shape' object has no attribute '__x'
```

Python interpreter returns an `AttributeError`, explaining you're trying to access to a non-existing property. If you want to access the `__x`, or the `__y` properties, you need to create the appropriate methods, called access methods (or accessors). The `Shape` class becomes this:

```python
class Shape:

    # Class Attributes
    DEFAULT_X_POSITION = 0
    DEFAULT_Y_POSITION = 0

    # Init Method
    def __init__(self, x = 0, y = 0):
        self.__x = 0
        self.__y = 0
    
    # Getters
    def get_x(self):
        return self.__x
    
    def get_y(self):
        return self.__y
    
    # Setter
    def set_x(self, x):
        self.__x = x
    
    def set_y(self, y):
        self.__y = y

    # Methods
    def to_center(self):
        self.__x = 0
        self.__y = 0
    
    def move(self, x, y):
        self.__x = x
        self.__y = y
```

Now, you can use the `get_x()` and `get_y()` methods to get the `x` and `y` attributes. You can also use the `set_x()` and `set_y()` methods to set the `x` and `y` attributes. As all other methods, the first argument accepted by the accessors (both getters and setters) are the `self` argument. If you need to add business logic, or checks to ensure the value is correct (for both `__x` and `__y`), you can implement the needed code in the setters methods. If you need to format appropriately the `__x`, or `__y` attribute, you can write this code in the getters methods. This is the best way in Python to respect the principle of encapsulation.

Python allows the developer to specify protected attributes also. Meanwhile the double-underscore prefix indicates a private attribute, or method, the single-underscore prefix indicates a protected attribute, or method. Although the protected attributes are effectively a convention in Python, the single-underscore prefix indicates that the attribute, or the method must be used carefully by other member of the class and its subclasses (yes, in Python you can define nested classes!).

The `Shape` class with protected attributes is:

```python
class Shape:

    # Class Attributes
    DEFAULT_X_POSITION = 0
    DEFAULT_Y_POSITION = 0

    # Init Method
    def __init__(self, x = 0, y = 0):
        self._x = 0
        self._y = 0
    
    # Getters
    def get_x(self):
        return self._x
    
    def get_y(self):
        return self._y
    
    # Setter
    def set_x(self, x):
        self._x = x
    
    def set_y(self, y):
        self._y = y

    # Methods
    def to_center(self):
        self._x = 0
        self._y = 0
    
    def move(self, x, y):
        self._x = x
        self._y = y
```

And the following code is perfectly interpreted by Python:

```python
s = Shape(10, 20)
print(s._x) # 10
print(s._y) # 20
```

### 19.10. Class Methods with `@classmethod`

So far we have seen instance methods, that is, methods that can be called using an identifier of an object and that modify the state of the object, or perform some operation that has to do with the single instance of the class.

There is another category of methods, called class methods, that cannot be directly binded to a specific instance of the class, but  to the class itself. The class methods can be invoked by specifying the class name, the dot operator and, finally, the identifier of the class method. This is the syntaxt:

```python
MyClass.classMethodName(parameters)
```

A class method receives the class itself as the first argument (by convention called `cls`). The `cls` parameter is very similar to the `self` parameter:

- The `cls` parameter is the first argument of a class method and it means "this class".
- The `self` paramter is the first argument of an instance method, but it means "this object", or "this current instance".

You can use the class methods when you need to modify class attributes, or when you need to execute a task independent of any created object. A class method is decorated by `@classmethod`: it's called decorator, cause it's written immediately before the header of the class method.

For example, the following example shows the `Shape` class with a class method called `from_string()`:

```python
class Shape:

    # Class Attributes
    DEFAULT_X_POSITION = 0
    DEFAULT_Y_POSITION = 0

    # Class Methods
    @classmethod
    def from_string(cls, shape_str):
        x, y = shape_str.split(":")
        return cls(int(x), int(y))
    
    # ... other code of the class ...
```

The method called `from_str()` takes a string as second argument and `cls` as first argument. It's decorated by the `@classmethod` decorator, so it's a class method. Into this method, we split a string `shape_str` by using the `:` character, so we can have the `x` and the `y` coords stored in two different variables. Made this, we invoke the class's `__init__()` method with the following expression:

```python
cls(int(x), int(y))
```

Remember that the `split()` method returns a list of strings, so to invoke the `__init__()` method without any type issues, or problem, we've made a string-to-integer conversion by the `int()` built-in function. You can use this function in this way:

```python
s = Shape.from_string("10:-10")
print(s._x) # 10
print(s._y) # -10
```

`from_string()` returns an instance of the `Shape` class. Writing `cls()`, or `Shape()` is the same.

### 19.11. Static Methods with `@staticmethod`

Differently from a class method, a static method doesn't receive any parameters (`self`, or `cls`). It behaves like a regular function, but lives inside the class where it's defined. A static method is decorated by the `@staticmethod` decorator, located immediately before the header of the method. It's declared and implemented in the class; moreover, it can be called via the `MyClass.staticMethodName(arguments)` syntaxt.

For example, in the `Shape` class we want to track the number of instances created from the start of the Python program. We can use a class attribute to track the instances created and two static methods (both decorated with `@staticmethod`) to increment the counter, or decrement it. Here's an example:

```python
class Shape:
    
    # Class Attributes
    instances = 0
    DEFAULT_X_POSITION = 0
    DEFAULT_Y_POSITION = 0

    # Static Methods
    @staticmethod
    def increment_instances():
        Shape.instances += 1

    @staticmethod
    def decrement_instances():
        Shape.instances -= 0 if Shape.instance == 0 else 1

    # ... other code of the class ...
```

In the previous example, we've defined two static methods: `increment_instances()` and `decrement_instances()`. Both use the `Shape.instances` counter to track the number of the created instances of the class `Shape`. Both are decorated with the `@staticmethod` decorator. Both haven't any argument.

If you write something like this:

```python
print(Shape.instances) # 0

s1 = Shape()
Shape.increment_instances()

s2 = Shape()
Shape.increment_instances()

print(Shape.instances) # 2
```

the first invocation of the `print()` function prints `0`, the second prints `2`, cause `increment_instances()` has been called two times (and `Shape.instances` is incremented two times).

### 19.12. Magic Methods: `__str__()`, `__eq__()` and `__repr__()`

Python uses the double-underscore as both prefix and postfix to specify a "special" method (usually called magic method). Three are the most common magic methods you'll implement in your classes:

The `__str__()` method is a special method that controls what is returned when the object is printed. We can add the `__str__()` method to the `Shape` class:

```python
class Shape:
    # ... code before __str__() ...

    def __str__(self):
        return f"x: {self.x}\ny: {self.y}\n"

    # ... code after __str__() ...
```

The `__str__()` magic method returns a human-readable string of the object. In our case, we use an f-string to print the `x` and `y` properties of the current instance.

Another common used magic method is `__eq__()`. This magic method defines how two objects are compared using the comparator operator (`==`) and it should return a boolean value: `True` if the two compared instance are considered equal, `False` otherwise. The `__eq__()` magic method is used to compare the object content, not identity. Let's add the `__eq__()` magic method in the `Shape` class:

```python
class Shape:
    # ... code before __eq__() ...

    def __eq__(self, shape):
        return isinstance(shape, Shape) and self.x == shape.x and self.y == shape.y

    # ... code after __eq__() ...
```

The `__eq__()` method accepts another instance of the same class (`Shape` in our case) to compare the current instance with it. Note that the return value of the `__eq__()` magic method is determined by three subconditions, linked by the `and` logical operator:

- First of all, the `shape` parameter must be an instance of the `Shape` class.
- Second, the `x` attribute of the current instance (`self.x`) must be equal to the `x` attribute of the other instance (`shape.x`).
- Third, the `y` attribute of the current instance (`self.y`) must be equal to the `y` attribute of the other instance (`shape.y`).

A third magic method is `__repr__()` (a contraction of "representation"). Differently from `__str__()`, the `__repr__()` magic method is used to return a detailed representation of the current instance. We can define the `__repr__()` magic method in the `Shape` class in this way:

```python
class Shape:
    # ... code before __repr__() ...

    def __repr__(self):
        return f"Shape({self.x}, {self.y})"

    # ... code after __repr__() ...
```

As you can see, the `__repr__()` defines the official string representation of an object. Now, when you use the `repr()` built-in function of Python by passing an instance of the `Shape` class, for debugging and other things, you can see the output returned by the `__repr__()` magic method. The string returned by the `__repr__()` magic method should be clear and unambiguous. You can see the output of the `__repr__()` magic method as a developer-level representation of the object, useful for documentation.

### 19.13. Getters and Setters with `@property`

Previously, we've used the setters and getters method for both `x` and `y` instance attributes in the definition of the class `Shape`. Python has a built-in decorator, called `@property`, allows you to access methods like attributes. It is used to create controlled access (getter/setter) for class attributes and you can see it as a syntactic sugar for getter and setter methods of a particular instance attribute. This decorator helps encapsulate logic while keeping a clean interface.

For example, if we've a class called `Person`:

```python
class Person:
    def __init__(self):
        # to do
        pass
```

we can add two private attributes: `__fullName` and `__age`.

```python
class Person:
    def __init__(self, fullName = "Bob Parker", age = 18):
        self.__fullName = fullName
        self.__age = age
```

These attributes aren't accessible from the outside of the `Person` class. So, we can use the `@property` decorator to create the getters methods for the `__fullName` and `__age` attributes in thiis way:

```python
class Person:
    def __init__(self, fullName = "Bob Parker", age = 18):
        self.__fullName = fullName
        self.__age = age
    
    @property
    def fullName(self):
        return self.__fullName
    
    @property
    def age(self):
        return self.__age
```

Note that we've specified two methods: `fullName()` and `age()` and, thanks to the `@property` decorator, we can access indirectly to the `__fullName` and `__age` properties in this way:

```python
p = Person("Christian Alessandro Atzeni", 25)
print(p.fullName) # "Christian Alessandro Atzeni"
print(p.age) # 25
```

As you can see, we used the fullName and age methods of an instance of type Person as if they were directly accessible properties (but in reality they are still methods).

And for setters? For the setter, Python provides the following syntaxt: `@propertyName.setter`, where the part `propertyName` of the decorator is the same name of the method decorated with the `@property` decorator. For example, if we want to add two setters to the `Person` class, one for the `fullName` property (`__fullName` private attribute) and another for the `age` property (`__age` private attribute), we can write something like this:

```python
class Person:
    def __init__(self, fullName = "Bob Parker", age = 18):
        self.__fullName = fullName
        self.__age = age
    
    @property
    def fullName(self):
        return self.__fullName
    
    @fullName.setter
    def fullName(self, fullName):
        self.__fullName = fullName
    
    @property
    def age(self):
        return self.__age

    @age.setter
    def age(self, age):
        self.__age = age
```

Note that both getter and setter methods of a property have the same name. You can use the setters methods simply by using `p.fullName` and `p.age` on the left side of the assignment operator, like this:

```python
p = Person("Christian Alessandro Atzeni", 25)

print(p.fullName) # "Christian Alessandro Atzeni"
print(p.age) # 25

p.fullName = "Maristella Rossi" # using the setter method for __fullName
p.age = 29 # using the setter method for __age

print(p.fullName) # "Maristella Rossi"
print(p.age) # 29
```

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

Reflection is the ability of a program to inspect and modify its own structure and behavior at runtime. In Python, this includes dynamically accessing attributes or methods using functions like `getattr()` and `setattr()`. It enables flexible and dynamic code, often used in frameworks and metaprogramming.

The most common reflection functions (all built-in functions) used in Python are:

- `getattr(obj, name)`: return the `name` attribute of the `obj` instance.
- `setattr(obj, name, value)`: set the `name` attribute to the `value` value of the `obj` instance.
- `hasattr(obj, name)`: return `True` if the `obj` instance has the `name` attribute, `False` otherwise.
- `delattr(obj, name)`: deletes the `name` attribute of the `obj` instance.

You can use `getattr()` to call method dynamically, for example:

```python
method_to_call = getattr(Shape(), "move")
method_to_call(10, 5) # it calls the move() method defined in the Shape class
```

The `__dir__` attribute returns a dictionary of the instance where the keys are all the attributes of the instance, meanwhile the values are the value of each key. The same dictionary can be obtained by using the `vars()` built-in function.

### 19.24. Introspection

Introspection is the ability to examine objects, types, and their properties at runtime. Python provides tools like `type()`, `dir()`, and `help()` to inspect objects. It is mainly used for debugging, exploration, and understanding code structure.

- `type()` accepts one argument and it returns the type of the accepted argument at runtime.
- `dir()`: accepts one argument and it returns a list of all the attributes and methods accessible of that argument.
- `help()`: accepts one argument and it returns some info about the argument.

### 19.25. Singleton

A Singleton is a design pattern that ensures a class has only one instance throughout the program. All parts of the code share the same instance, providing a single point of access. It is commonly used for shared resources like configuration, or logging systems. Singleton are particularly used with the OOP languages, like Python, cause it allows the system to save memory and optimize performances during the program execution.
