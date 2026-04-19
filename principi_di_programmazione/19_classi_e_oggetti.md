# 19. Classi e oggetti

### 19.01. Panoramica sulla programmazione a oggetti

La OOP (Object-Oriented Programming) e' un paradigma di programmazione che permette di modellare la realta' in modo piu' naturale rispetto all'uso esclusivo di funzioni. In questo contesto:

- OO (Object-Oriented) indica la filosofia,
- OOD (Object-Oriented Design) indica l'arte di progettare il dominio del problema,
- OOP indica il paradigma di programmazione vero e proprio.

Nella filosofia object-oriented, azioni, processi e oggetti del mondo reale possono essere rappresentati come entita' indipendenti, con un proprio ciclo di vita, uno stato e dei comportamenti. Per esempio, in un'azienda potresti modellare una classe `Person` e una classe `BusinessCar`, con una relazione tra una persona e una o piu' auto aziendali.

Python supporta molto bene la programmazione a oggetti. Alcuni vantaggi della OOP sono:

- fornisce una struttura piu' chiara ai programmi,
- rende il codice piu' semplice da mantenere, riusare e debuggare,
- aiuta a rispettare il principio DRY,
- permette di costruire applicazioni riusabili con meno duplicazione.

### 19.02. Che cos'e' una classe?

Classi e oggetti sono i due concetti centrali della programmazione a oggetti. Una classe definisce come deve essere fatto un oggetto. Per esempio:

- una classe `Fruit` modella la nozione di frutto,
- una classe `Employee` modella un dipendente,
- una classe `Car` modella un'auto.

Una classe e' un modello, o blueprint, da cui puoi creare molte istanze concrete.

### 19.03. Che cos'e' un oggetto?

Un oggetto, o istanza, e' una realizzazione concreta di una classe. Se la classe definisce il blueprint, l'oggetto e' il singolo elemento creato da quel blueprint.

Ogni oggetto:

- ha i propri attributi, cioe' i dati,
- puo' usare i metodi definiti dalla classe,
- ha un proprio ciclo di vita,
- possiede uno stato, rappresentato dai valori dei suoi attributi.

### 19.04. Definizione di una classe

Puoi definire una classe usando la parola chiave `class`:

```python
class Shape:
    pass
```

La parola chiave `pass` indica che, per il momento, non stiamo specificando implementazione. Puoi accedere al nome della classe tramite `__name__`:

```python
print(Shape.__name__)  # "Shape"
```

### 19.05. Creazione di oggetti

Puoi creare un oggetto della classe `Shape` in questo modo:

```python
shape = Shape()
```

Dato che una classe e' un blueprint, puoi creare tutte le istanze che vuoi:

```python
a = Shape()
b = Shape()
c = Shape()
```

In generale, la sintassi di base e':

```python
instance_name = ClassName(arguments)
```

Puoi anche eliminare esplicitamente un oggetto con `del`:

```python
del a
```

### 19.06. `__init__()` e argomento `self`

Ogni classe puo' definire un metodo speciale chiamato `__init__()`, eseguito quando l'oggetto viene creato. Questo metodo viene usato per inizializzare lo stato dell'istanza.

```python
class Shape:
    def __init__(self):
        print("Object created!")
```

L'argomento `self` rappresenta l'istanza corrente. E' l'equivalente concettuale di `this` in altri linguaggi.

Puoi usare `self` per assegnare valori agli attributi:

```python
class Shape:
    def __init__(self, x=0, y=0):
        self.x = x
        self.y = y
```

Ora puoi creare oggetti cosi':

```python
s1 = Shape(10, 20)
s2 = Shape(-10, -5)

print(s1.x)  # 10
print(s2.y)  # -5
```

### 19.07. Attributi degli oggetti

Gli attributi rappresentano lo stato dell'oggetto. Nell'esempio precedente, `x` e `y` sono attributi dell'istanza. La sintassi per accedere a un attributo e' `identifier.attribute`:

```python
s1.x
s1.y
```

Gli attributi possono essere impostati in `__init__()` oppure assegnati successivamente. Tuttavia, inizializzarli in `__init__()` e' una buona pratica, perche' garantisce che tutte le istanze abbiano la stessa struttura di base.

### 19.08. Metodi degli oggetti

Un metodo di istanza e' un comportamento definito all'interno della classe e invocabile sugli oggetti creati da quella classe.

```python
class Shape:
    def __init__(self, x=0, y=0):
        self.x = x
        self.y = y

    def move(self, x, y):
        self.x = x
        self.y = y
```

Puoi usare il metodo `move()` cosi':

```python
s = Shape(10, 20)
s.move(100, -50)
print(s.x)  # 100
print(s.y)  # -50
```

Un metodo puo' avere anche zero argomenti oltre a `self`, come nel caso di `to_center()`.

### 19.09. Attributi di classe

Oltre agli attributi di istanza, Python permette di definire attributi di classe, condivisi da tutte le istanze:

```python
class Shape:
    DEFAULT_X_POSITION = 0
    DEFAULT_Y_POSITION = 0
```

Puoi accedervi tramite il nome della classe:

```python
print(Shape.DEFAULT_X_POSITION)
```

oppure, anche se meno consigliato, tramite un'istanza.

Gli attributi di classe sono utili per costanti e valori condivisi.

### 19.10. Incapsulamento: membri protetti e privati

L'incapsulamento e' uno dei principi fondamentali della OOP. Consiste nel proteggere i dati interni della classe e nel controllare come vengono letti o modificati.

In Python:

- il prefisso `_` indica convenzionalmente un membro protetto,
- il prefisso `__` indica un membro privato.

Per esempio:

```python
class Shape:
    def __init__(self, x=0, y=0):
        self.__x = x
        self.__y = y
```

In questo caso `__x` e `__y` non sono pensati per l'accesso diretto dall'esterno. Il modo corretto per esporli e' tramite metodi di accesso.

### 19.11. Getter e setter

Per leggere o modificare attributi privati puoi definire getter e setter:

```python
class Shape:
    def __init__(self, x=0, y=0):
        self.__x = x
        self.__y = y

    def get_x(self):
        return self.__x

    def get_y(self):
        return self.__y

    def set_x(self, x):
        self.__x = x

    def set_y(self, y):
        self.__y = y
```

Questo approccio permette anche di aggiungere controlli o logica aggiuntiva prima di aggiornare lo stato dell'oggetto.

### 19.12. Metodi di classe con `@classmethod`

Un class method e' un metodo legato alla classe, non alla singola istanza. Riceve come primo argomento la classe stessa, per convenzione chiamata `cls`.

```python
class Shape:
    @classmethod
    def from_string(cls, shape_str):
        x, y = shape_str.split(":")
        return cls(int(x), int(y))
```

Un metodo come `from_string()` e' utile, per esempio, come costruttore alternativo.

### 19.13. Metodi statici con `@staticmethod`

Un metodo statico non riceve ne' `self` ne' `cls`. Si comporta come una funzione normale, ma viene definito dentro la classe.

```python
class Shape:
    instances = 0

    @staticmethod
    def increment_instances():
        Shape.instances += 1
```

I metodi statici sono utili quando l'operazione non dipende dallo stato dell'istanza o della classe, ma ha comunque senso logico dentro quella classe.

### 19.14. Metodi magici: `__str__()`, `__eq__()` e `__repr__()`

Python usa metodi speciali, spesso chiamati magic methods, per definire comportamenti standard degli oggetti.

`__str__()` definisce la rappresentazione leggibile dell'oggetto:

```python
def __str__(self):
    return f"x: {self.x}, y: {self.y}"
```

`__eq__()` definisce il confronto con `==`:

```python
def __eq__(self, shape):
    return isinstance(shape, Shape) and self.x == shape.x and self.y == shape.y
```

`__repr__()` definisce una rappresentazione piu' precisa, utile per debugging:

```python
def __repr__(self):
    return f"Shape({self.x}, {self.y})"
```

### 19.15. Proprieta' con `@property`

Python offre il decoratore `@property`, che consente di esporre metodi come se fossero attributi.

```python
class Person:
    def __init__(self, fullName="Bob Parker", age=18):
        self.__fullName = fullName
        self.__age = age

    @property
    def fullName(self):
        return self.__fullName

    @fullName.setter
    def fullName(self, fullName):
        self.__fullName = fullName
```

Questo approccio mantiene una sintassi semplice verso l'esterno, ma consente comunque di applicare logica di validazione o trasformazione.

### 19.16. Ereditarieta' e metodo `super()`

L'ereditarieta' permette di definire una classe che eredita metodi e attributi da un'altra classe. E' una relazione di tipo is-a.

Per esempio, se `Circle` eredita da `Shape`, allora un `Circle` e' anche uno `Shape`.

```python
class Shape:
    def __init__(self, x=0, y=0):
        self.__x = x
        self.__y = y

class Circle(Shape):
    def __init__(self, x=0, y=0, radius=0):
        super().__init__(x, y)
        self.__radius = radius
```

Il metodo `super()` permette di richiamare il comportamento della superclasse, evitando duplicazione di codice.

### 19.17. Override dei metodi

Quando una sottoclasse ridefinisce un metodo gia' presente nella superclasse, si parla di overriding.

Per esempio, `Circle` puo' ridefinire `__str__()` e `__eq__()` per includere anche il raggio:

```python
class Circle(Shape):
    def __str__(self):
        return f"{super().__str__()}, radius: {self.__radius}"

    def __eq__(self, circle):
        return super().__eq__(circle) and isinstance(circle, Circle) and self.__radius == circle.radius
```

L'override permette di specializzare il comportamento ereditato.

### 19.18. Ereditarieta' multipla e MRO

Python supporta anche l'ereditarieta' multipla: una classe puo' ereditare da piu' superclassi.

```python
class A:
    pass

class B:
    pass

class C(A, B):
    pass
```

Quando esiste ereditarieta' multipla, Python usa la MRO (Method Resolution Order) per decidere in quale ordine cercare metodi e attributi.

Puoi ispezionare la MRO con:

```python
print(C.mro())
```

Questo ordine e' fondamentale per capire quale implementazione verra' usata quando lo stesso metodo e' definito in piu' punti della gerarchia.

### 19.19. Polimorfismo, classi astratte e aggregazione

Il polimorfismo significa che oggetti diversi possono esporre la stessa interfaccia ed essere usati in modo intercambiabile.

```python
class Cat:
    def speak(self):
        return "meow"

class Dog:
    def speak(self):
        return "woof"
```

Le classi astratte, invece, permettono di definire interfacce comuni che le sottoclassi devono implementare. In Python puoi crearle con il modulo `abc` e il decoratore `@abstractmethod`.

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass
```

Infine, l'aggregazione e' una relazione di tipo has-a. Per esempio, un'auto puo' avere un motore, ma i due oggetti possono esistere indipendentemente:

```python
class Engine:
    def start(self):
        return "Engine started"

class Car:
    def __init__(self, engine=None):
        self.engine = engine
```

A differenza dell'ereditarieta', l'aggregazione non rappresenta una relazione is-a, ma una relazione di composizione debole tra oggetti.
