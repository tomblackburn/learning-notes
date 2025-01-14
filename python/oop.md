# Object Orientated Programming

[Object-Oriented Programming](https://en.wikipedia.org/wiki/Object-oriented_programming), or "OOP", is a pattern for writing clean and maintainable code. Not everyone *agrees* that object-oriented principles are the best way to write code, but, to be a good engineer, you should at least understand them.

Paradigms like [object-oriented programming](https://en.wikipedia.org/wiki/Object-oriented_programming) and [functional programming](https://en.wikipedia.org/wiki/Functional_programming) are all about making code easier to work with and understand as the feeble humans we are. Code that's easy for humans to understand is called "clean code".

# Classes

A [class](https://docs.python.org/3/tutorial/classes.html) is a special type of value in an object-oriented programming language like Python. It's similar to a dictionary in that it usually stores other types inside itself.#

```python
# Defines a new class called "Soldier"
class Soldier:
    health = 5
    armor = 3
    damage = 2
```

Just like a string, integer or float, a class is a *type*, but instead of being a built-in type, your classes are custom types that you define.

An object is just an [instance](https://stackoverflow.com/questions/20461907/what-is-meaning-of-instance-in-programming) of a class type. For example:

```python
health = 50
# health is an instance of an integer type
aragorn = Soldier()
# aragorn is an instance of the Soldier type (class)
```

"Classes" are custom new types that we define as the programmer. Each new instance of a class is an "object".

# Methods

After the last exercise, you might be wondering *why* classes are useful, they're like [dictionaries](https://docs.python.org/3/tutorial/datastructures.html#dictionaries)... but worse!

One thing that makes classes cool is that we can define [methods](https://docs.python.org/3/tutorial/classes.html#method-objects) on them. A method is a function that's tied directly to a class and has access to all its properties.

## Self

Methods are nested within the `class` declaration. Their first parameter is always the instance of the class that the method is being called on. By convention, it's called ["self"](https://docs.python.org/3/glossary.html#term-method). Because `self` is a reference to the object, you can use it to read and update the properties of the object.

Notice that methods are called directly on an object using the dot operator.

## Methods return values

If a normal function doesn't return anything, it's typically not a very useful function. In contrast, methods often don't return anything explicitly because they can mutate the properties of the object instead. That's exactly what we did in the last assignment.

However, they *can* return values if you want! They're just functions with access to an object, after all.

```python
class Soldier:
    armor = 2
    num_weapons = 2

    def get_speed(self):
        speed = 10
        speed -= self.armor
        speed -= self.num_weapons
        return speed

soldier_one = Soldier()
print(soldier_one.get_speed())
# prints "6"
```

# **Methods vs Functions**

You know what a [function](https://docs.python.org/3/glossary.html#term-function) is. A method has all the same properties as a function, but it is tied directly to a class and has access to all its properties.

A method *automatically* receives the object it was called on as its first parameter.

```python
class Soldier:
    health = 5

    def take_damage(self, damage, multiplier):
        damage = damage * multiplier
        self.health -= damage

dalinar = Soldier()
damage, multiplier = 30, 3

# Only "damage" and "multiplier" are passed as arguments
# "dalinar" is passed implicitly as the first argument, "self"
dalinar.take_damage(damage, multiplier)
```

A method can operate on data that is contained within the class. In other words, you won't always see all the "outputs" in the `return` statement because the method might just mutate the object's properties directly.

## The OOP debate

Because functions are more explicit, some developers argue that [functional programming](https://blog.boot.dev/clean-code/benefits-of-functional-programming/) is better than object-oriented programming. In reality, neither paradigm is "better", and the best developers learn and understand both styles and use them as they see fit.

For example, while methods are more implicit and often make code more difficult to read, they also make it easier to group a program's data and behavior in one place, which can lead to a more organized codebase.

# **Constructors (or initializers)**

It's rare in the real world to see a class that defines properties the way we've been doing it:

```python
class Soldier:
    name = "Legolas"
    armor = 2
    num_weapons = 2
```

It's more practical to use a [constructor](https://en.wikipedia.org/wiki/Constructor_(object-oriented_programming)). In Python, if you name a method [`__init__`](https://docs.python.org/3/reference/datamodel.html#object.__init__), that's the constructor and it is called when a new object is created.

So, with a constructor, the code would look like this:

```python
class Soldier:
    def __init__(self):
        self.name = "Legolas"
        self.armor = 2
        self.num_weapons = 2
```

Now we can make the starting armor and number of weapons configurable with some parameters!

```python
class Soldier:
    def __init__(self, name, armor, num_weapons):
        self.name = name
        self.armor = armor
        self.num_weapons = num_weapons

soldier = Soldier("Legolas", 5, 10)
print(soldier.name)
# prints "Legolas"
print(soldier.armor)
# prints "5"
print(soldier.num_weapons)
# prints "10"
```

# Class Variables vs Instance Variables

So far we've worked with both class variables and instance variables, but we haven't talked about the difference.

## Instance Variables

Instance variables vary from object to object and are **declared in the constructor.**

```python
class Wall:
    def __init__(self):
        self.height = 10

south_wall = Wall()
south_wall.height = 20 # only updates this instance of a wall
print(south_wall.height)
# prints "20"

north_wall = Wall()
print(north_wall.height)
# prints "10"
```

## Class Variables

Class variables remain the same between instances of the same class and are **declared at the top level of a class definition**.

```python
class Wall:
    height = 10

south_wall = Wall()
print(south_wall.height)
# prints "10"

Wall.height = 20 # updates all instances of a Wall

print(south_wall.height)
# prints "20"
```

In other languages these types of variables are often called [static variables](https://en.wikipedia.org/wiki/Static_variable).

## Variables, fields and properties

The terms instance and class variable, field, property and attribute are used interchangeably and usually refer to the same concept in languages that support some form of object-oriented programming. Here's a quick reference for some popular languages:

| Language | Class variable | Instance variable |
| --- | --- | --- |
| Python | Class variable | Instance variable |
| Go | Field | Field |
| JavaScript | Property | Property |
| C# | Static field | Field |
| Java | Static field | Field |

### Which should I use?

Generally speaking, *stay away from class variables*. Just like global variables, class variables are usually a bad idea because they make it hard to keep track of which parts of your program are making updates. However, it is important to understand how they work because you may see them out in the wild.

# **Encapsulation**

[Encapsulation](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)) is the practice of hiding complexity inside a ["black box"](https://en.wikipedia.org/wiki/Black_box) so that it's easier to focus on the problem at hand.

![image.png](image.png)

The most basic example of encapsulation is a function. The caller of a function doesn't need to worry too much about what happens inside, they just need to understand the inputs and outputs.

```python
acceleration = calc_acceleration(initial_speed, final_speed, time)
```

To use the `calc_acceleration` function, we don't need to think about every individual line of code inside the function. We just need to know that if we give it the inputs:

- `initial_speed`
- `final_speed`
- `time`

Then it will give us the correct `acceleration` as an output.

## Public or Private

By default, all properties and methods in a class are *public*. That means that you can access them with the `.` operator:

```python
wall.height = 10
print(wall.height)
# 10
```

[Private](https://docs.python.org/3/tutorial/classes.html#tut-private) data members are how we encapsulate logic and data within a class. To make a property or method private, you just need to prefix it with two underscores.

```python
class Wall:
    def __init__(self, armor, magic_resistance):
        self.__armor = armor
        self.__magic_resistance = magic_resistance

    def get_defense(self):
        return self.__armor + self.__magic_resistance

front_wall = Wall(10, 20)

# This results in an error
print(front_wall.__armor)

# This works
print(front_wall.get_defense())
# 30
```

We do this because, in this example, `armor` and `magic_resistance` are implementation details. After creating a `Wall`, they don't matter anymore. Now the game developers can just call `get_defense` and not worry about how it's calculated under the hood.

## Encapsulation in Python

Python is a dynamic language, and that makes it difficult for the 
interpreter to enforce some of the safeguards that languages like [Go](https://go.dev/) do. That's why encapsulation in Python is achieved mostly by [convention](https://en.wikipedia.org/wiki/Coding_conventions) rather than by *force*.

Prefixing methods and properties with a double underscore is a *strong* suggestion to the users of your class that they shouldn't be touching that stuff. If a developer wants to break convention, [there are ways to get around](https://stackoverflow.com/questions/3385317/private-variables-and-methods-in-python) the double underscore rule

```python
class Wall:
    def __init__(self, height):
        # the double underscore make this a private property
        # but it's not strictly enforced, there are hacks to get around it
        self.__height = height

    def get_height(self):
        return self.__height
```

# Abstraction

Abstraction helps us handle complexity by hiding unnecessary details. Sounds like encapsulation, right? They're so similar that it's almost not worth worrying about the difference...almost.

## Abstraction vs Encapsulation

- Abstraction is about *creating a simple interface for complex behavior.* It focuses on what's exposed.
- Encapsulation is about *hiding internal state.* It focuses on tucking implementation details away so no one depends on them.

Abstraction is more about reducing complexity, encapsulation is more about maintaining the integrity of system internals.

## Are we encapsulating or abstracting?

Both. Almost always we are doing both. Here's an example of using the `random` library to generate a random number:

```python
import random

attack_damage = random.randrange(5)
```

[Generating random numbers](https://blog.boot.dev/cryptography/what-is-entropy-in-cryptography/) is a *really hard* problem. The operating system uses the physical hardware of the computer to create a [seed](https://en.wikipedia.org/wiki/Random_seed) for the randomness. However, the developers of the `random` library have *abstracted* that complexity away and *encapsulated* it within the simple `randrange` function. We just say "I want a random number from 0 to 4" and the library does it.

When writing libraries for use by other developers, getting the abstractions right is *crucial* because changing them later can be disastrous. Imagine if the maintainers of the `random` module changed the input parameters to the `randrange` function! It would break code all over the world.

## How OOP Developers Think

Classes in object-oriented programming are all about grouping data and behavior *together* in one place: an *object*. Object-oriented programmers tend to think about programming as a modeling problem. They think:

> "How can I write a Human class that holds the data and simulates the behavior of a real human?"
> 

To provide some contrast, functional programmers tend to think of their code as inputs and outputs, and how those inputs and outputs transition the world from one state to the next:

> "When a human takes a step, what's the new state of the game?"
> 

![image.png](image%201.png)

OOP isn't the only pattern for organizing code, but it's one of the more popular ones. If you understand multiple ways of thinking about code, you'll be a much better developer overall.

# Inheritance

Non-OOP languages like Go and Rust allow for encapsulation and abstraction features as nearly *every* language does. Inheritance, on the other hand, tends to be unique to class-based languages like Python, Java, and Ruby.

Inheritance allows one class, the "child" class, to *inherit* the properties and methods of another class, the "parent" class.

This powerful language feature helps us avoid writing a lot of the same code twice. It allows us to [DRY (don't repeat yourself)](https://blog.boot.dev/clean-code/dry-code/) up our code.

Here `Cow` is a "child" class that inherits from the "parent" class `Animal`:

```python
class Animal:
    # parent "Animal" class

class Cow(Animal):
    # child class "Cow" inherits "Animal"
```

The `Cow` class can reuse the `Animal` class's constructor with the [super()](https://docs.python.org/3/library/functions.html#super) method, `super()` allows the child class to call methods and constructors from its parent class, in this case, `__init__()`:

```python
class Animal:
    def __init__(self, num_legs):
        self.num_legs = num_legs

class Cow(Animal):
    def __init__(self, num_udders):
        # call the parent constructor to give the cow some legs
        super().__init__(4)

        # set cow specific properties
        self.num_udders = num_udders
```

## When should Inheritance be used?

Inheritance is a powerful tool, but it is a *really* bad idea to try to overuse it. Inheritance should only be used when all instances of a child class are also instances of the parent class.

When a child class inherits from a parent, it inherits *everything*. If you only want to share *some* functionality, inheritance is probably not the best answer. Better to 
simply share some functions, or maybe make a new parent class that both 
classes can inherit from.

**All cats are animals but not all animals are cats:**

![image.png](image%202.png)

## Inheritance Hierarchy

There is no limit to how deeply we can nest an inheritance tree. For example, a `Cat` can inherit from an `Animal` that inherits from `LivingThing`. That said, be careful! New programmers often get carried away.

You should never think to yourself:

> "Well *most* wizards are elves... so I'll just have wizard inherit from elf"
> 

A good child class is a strict [subset](https://en.wikipedia.org/wiki/Subset) of its parent class.

An example of this with private properties. A child class cannot simply access a private property of its parent class. It has to use a getter. For example:

```python
class Wall:
    def __init__(self, height):
        self.__height = height

    def get_height(self):
        return self.__height

class Castle(Wall):
    def __init__(self, height, towers):
        super().__init__(height)
        self.towers = towers

    def get_tower_height(self):
        return self.get_height() * 2
```

# **Polymorphism**

While inheritance is the most unique trait of object-oriented languages, polymorphism is probably the most powerful. Polymorphism is the ability of a variable, function or object to take on multiple forms.

- "poly"="many"
- "morph"="form".

For example, classes in the same hierarchical tree may have methods with the *same* name but *different* behaviors.

```python
class Creature():
    def move(self):
        print("the creature moves")

class Dragon(Creature):
    def move(self):
        print("the dragon flies")

class Kraken(Creature):
    def move(self):
        print("the kraken swims")

for creature in [Creature(), Dragon(), Kraken()]:
    creature.move()
# prints:
# the creature moves
# the dragon flies
# the kraken swims
```

The `Dragon` and `Kraken` child classes are **overriding** the behavior of their parent class's `move()` method.

Polymorphism in programming is the ability to present the same interface (function or method signatures) for many different underlying forms (data types).

A classic example is a `Shape` class that `Rectangle`, `Circle`, and `Triangle` can inherit from. With polymorphism, each of these classes will have different underlying data. The circle needs its center point coordinates and radius. The rectangle needs two coordinates for the top left and bottom right corners. The triangle needs coordinates for the corners.

By making each class responsible for its data **and** its code, you can achieve polymorphism. In the shapes example, each class would have its own `draw_shape()` method. This allows the code that uses the different shapes to be simple and easy, and more importantly, it can treat shapes as the **same** even though they are **different**. It hides the complexities of the difference behind a clean abstraction.

```python
shapes = [Circle(5, 5, 10), Rectangle(1, 3, 5, 6)]
for shape in shapes:
    print(shape.draw_shape())
```

This is in contrast to the functional way of doing things where you would have had separate functions that have **different** function signatures, like `draw_rectangle(x1, y1, x2, y2)` and `draw_circle(x, y, radius)`.

## Function Signature

A function signature (or method signature) includes the name, inputs, and outputs of a function or method. For example, `hit_by_fire` in the `Human` and `Archer` classes have identical signatures.

```python
class Human:
    def hit_by_fire(self):
        self.health -= 5
        return self.health

class Archer:
    def hit_by_fire(self):
        self.health -= 10
        return self.health
```

Both methods have the same name, take `0` inputs, and return integers. If *any* of those things were different, they would have different function signatures.

Here is an example of different signatures:

```python
class Human:
    def hit_by_fire(self):
        self.health -= 5
        return self.health

class Archer:
    def hit_by_fire(self, dmg):
        self.health -= dmg
        return self.health
```

If you change the function signature of a parent class when overriding a method, it could be a disaster. The whole point of overriding a method is so that the caller of your code *doesn't have to worry* about what different things are going on inside the methods of different object types.

# Operator Overloading

Another kind of built-in polymorphism in Python is the ability to override how an operator works. For example, the `+` operator works for built-in types like integers and strings.

```python
print(3 + 4)
# prints "7"

print("three " + "four")
# prints "three four"
```

Custom classes on the other hand don't have any built-in support for those operators:

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

p1 = Point(4, 5)
p2 = Point(2, 3)
p3 = p1 + p2
# TypeError: unsupported operand type(s) for +: 'Point' and 'Point'
```

However, we can add our own support! If we create an `__add__(self, other)` method on our class, the Python interpreter will use it when instances of the class are being added with the `+` operator. Here's an example:

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, point):
        x = self.x + point.x
        y = self.y + point.y
        return Point(x, y)

p1 = Point(4, 5)
p2 = Point(2, 3)
p3 = p1 + p2
# p3 is (6, 8)
```

Now, when `p1 + p2` is executed, under the hood the Python interpreter just calls `p1.__add__(p2)`

As we discussed in the last assignment, operator overloading is the practice of defining custom behavior for standard Python operators. Here's a list of how the operators translate into method names.

| Operation | Operator | Method |
| --- | --- | --- |
| Addition | + | __add__ |
| Subtraction | - | __sub__ |
| Multiplication | * | __mul__ |
| Power | ** | __pow__ |
| Division | / | __truediv__ |
| Floor Division | // | __floordiv__ |
| Remainder (modulo) | % | __mod__ |
| Bitwise Left Shift | << | __lshift__ |
| Bitwise Right Shift | >> | __rshift__ |
| Bitwise AND | & | __and__ |
| Bitwise OR | | | __or__ |
| Bitwise XOR | ^ | __xor__ |
| Bitwise NOT | ~ | __invert__ |

## Overriding Built-In Methods

While there isn't a default behavior for the arithmetic operators like we just saw, there *is* a default behavior for **printing** a class.

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

p1 = Point(4, 5)
print(p1)
# prints "<Point object at 0xa0acf8>"
```

That's not super useful! Let's teach instances of our `Point` object to print themselves. The [`__str__`](https://docs.python.org/3/reference/datamodel.html#object.__str__) method (short for "string") lets us do just that. It takes no inputs but returns a string that will be printed to the console when someone passes an instance of the class to Python's `print()` function.

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):
        return f"({self.x},{self.y})"

p1 = Point(4, 5)
print(p1)
# prints "(4,5)"
```

*Note: the [`__repr__`](https://docs.python.org/3/reference/datamodel.html#object.__repr__) method works in a similar way, you'll see it from time to time.*