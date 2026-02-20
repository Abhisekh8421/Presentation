#  Foundations of OOP – Classes and Objects in Python


# Understanding Why We Need Class & Object


Before jumping into definitions,

Let’s first understand:

* Why do we need Class?
* What problem is it solving?
* What was used before?
* What is it replacing?

Because programming concepts exist to solve real problems.

---

#  Step 1: Building a Game Without Classes

Imagine we are building a shooting game.

Each enemy has:

* name
* health
* power
* level

We create enemies using dictionaries.

```python
enemy1 = {
    "name": "Zombie",
    "health": 100,
    "power": 10,
    "level": 1
}

enemy2 = {
    "name": "Zombie",
    "health": 100,
    "power": 10,
    "level": 1
}
```

At first, this looks fine.

But let’s see what happens when the game grows.

---

#  Problems With Dictionary Approach

---

##  1. Repetition

We repeat the same structure again and again.

If we create 100 enemies → we repeat 100 times.

---

##  2. Not Modular

If we want to add a new field like `"speed"`:

```python
enemy1["speed"] = 5
enemy2["speed"] = 5
```

We must manually update every dictionary.

There is no central structure.

---

##  3. Hard to Scale

If player reaches Level 10:

* Bigger enemies
* Boss enemies
* More health
* More power

We copy and modify dictionaries again.

This creates messy and hard-to-maintain code.

---

#  But Wait… Can’t We Add Functions in Dictionary?

Yes, we can.

Example:

```python
def shoot():
    print("Shooting")

enemy1 = {
    "name": "Zombie",
    "health": 100,
    "power": 10,
    "level": 1,
    "shoot": shoot
}

enemy1["shoot"]()
```

So yes, dictionary can store functions.

---

#  But Still Problems Exist

Even if we add methods:

* Behavior is not tightly connected to structure
* Code looks unorganized
* No clear blueprint
* Hard to manage when project becomes large


We are just managing everything manually.

---

#  So What Do We Need?

We need:

* One central blueprint
* Clean structure
* Reusable code
* Data + behavior together
* Easy scaling for large systems

That is where **Class & Object** come in.

---



#  Class – The Blueprint

###  What is a Class?

> A class is a blueprint or template used to create objects.
> It defines the structure (data) and behavior (methods).

Just like a building blueprint defines:

* number of rooms
* size
* structure

A class defines:

* attributes (variables)
* methods (functions)

---

```python
class Enemy:
    def __init__(self, name, health, power, level):
        self.name = name
        self.health = health
        self.power = power
        self.level = level

    def shoot(self):
        print(self.name, "shoots with power", self.power)
```

Now everything is organized:

* Structure is defined once
* Behavior is defined once
* No repetition
* Centralized control

---

#  Object – Real Enemy Created From Blueprint

###  What is an Object?

> An object is an instance of a class.
> It is the real entity created using the class blueprint.

If class is blueprint of enemy,
object is the actual enemy inside the game.

---

```python
enemy1 = Enemy("Zombie", 100, 10, 1)
enemy2 = Enemy("Big Zombie", 300, 50, 5)

enemy1.shoot()
enemy2.shoot()
```

---

###  Important Concept

> Every time we create a new instance, a new object is created in memory.
> Each object is independent of other objects.

That means:

* `enemy1` and `enemy2` are separate
* Changing one does not affect the other

Example:

```python
enemy1.health = 50
print(enemy1.health)   # 50
print(enemy2.health)   # 300 (unchanged)
```

Each object manages its own data.

---

#  What Class Replaces

| Without Class (Dictionary) | With Class            |
| -------------------------- | --------------------- |
| Repetition                 | Reusable Blueprint    |
| Manual updates             | Central structure     |
| Separate functions         | Behavior inside class |
| Hard to scale              | Easy to extend        |
| Unorganized                | Structured            |

---







#  Instance Variables vs Class Attributes

Before understanding this, remember:

* Every object is independent.
* But sometimes some data is common for all objects.

Let’s understand this using a **Student Database Example**.

---

#  Student Example

Imagine we are storing student information in a school database.

Each student has:

* name
* roll number
* marks

But all students belong to the **same school**.

Now the question is:

Should we store school name inside every student object?

---

# Without Class Attribute 

```python
class Student:
    def __init__(self, name, roll, marks, school):
        self.name = name
        self.roll = roll
        self.marks = marks
        self.school = school


s1 = Student("Rahul", 1, 85, "ABC Public School")
s2 = Student("Anita", 2, 90, "ABC Public School")
```

Problem:

* We are repeating `"ABC Public School"` again and again.
* If school name changes → we must update everywhere.

This is not efficient.

---

# Using Class Attribute 

```python
class Student:
    school = "ABC Public School"   # Class Attribute (Common for all)

    def __init__(self, name, roll, marks):
        self.name = name            # Instance Variable
        self.roll = roll            # Instance Variable
        self.marks = marks          # Instance Variable


s1 = Student("Rahul", 1, 85)
s2 = Student("Anita", 2, 90)

print(s1.school)
print(s2.school)
```

Now:

* `school` is stored only once in the class.
* All students automatically get it.
* No need to pass it every time.

---

# What is Instance Variable?

> Instance variables are variables that belong to each object separately.

Example:

* name
* roll
* marks

Each student has different values.

---

# What is Class Attribute?

> Class attribute is a variable that belongs to the class itself.
> It is shared by all objects.

Example:

* school name

All students share the same school.

---

#  Important Concept

If we change class attribute:

```python
Student.school = "XYZ International School"
```

Now all students automatically see updated value.



---

#  Types of Methods in Python OOP

In Python classes, we mainly have:

1. Instance Methods
2. Class Methods
3. Static Methods
4. Abstract Methods

Let’s understand each one simply.

---

# Instance Method

###  What is it?

> Instance method works with object data (instance variables).

It needs access to object values.

That’s why we pass `self`.

---

###  Why Do We Pass `self`?

When we call:

```python
s1.display()
```

Internally Python converts it like this:

```python
Student.display(s1)
```

It automatically passes the object as the first argument.

That object is received as `self`.

So:

> `self` refers to the current object.

---

### Example

```python
class Student:
    def __init__(self, name):
        self.name = name

    def display(self):
        print("Student Name:", self.name)


s1 = Student("Rahul")
s1.display()
```

Here:

* `self.name` refers to `s1.name`
* Each object uses its own data

---

#  Class Method

### What is it?

> Class method works with class attributes, not object data.

It uses `cls` instead of `self`.

We use `@classmethod` decorator.

---

### Example

```python
class Student:
    school = "ABC Public School"

    @classmethod
    def change_school(cls, new_name):
        cls.school = new_name


Student.change_school("XYZ School")
```

Here:

* `cls` refers to the class itself
* It changes class-level data

---

#  Static Method

### What is it?

> Static method does not use instance data or class data.

It behaves like a normal function,
but stays inside the class for organization.

We use `@staticmethod`.

---

### Example

```python
class Student:

    @staticmethod
    def greet():
        print("Welcome to the School System")


Student.greet()
```

No `self`
No `cls`

Just a utility function inside class.


---

# Abstract Method

###  What is an Abstract Method?

> An abstract method is a method that is declared but not implemented.
> It forces child classes to provide their own implementation.

We use:

* `ABC` (Abstract Base Class)
* `@abstractmethod` decorator

---

#  Shape Example

Imagine we are building a system for different shapes.

Every shape must have an `area()` method.

But area formula is different for each shape.

So we create a common blueprint.

---

##  Abstract Base Class

```python
from abc import ABC, abstractmethod

class Shape(ABC):

    @abstractmethod
    def area(self):
        pass
```

Here:

* `Shape` is an abstract class.
* `area()` is abstract.
* It has no implementation.
* Any child class must define `area()`.

---

# Rectangle Class (Child Class)

```python
class Rectangle(Shape):

    def __init__(self, length, width):
        self.length = length
        self.width = width

    def area(self):
        return self.length * self.width
```

Now Rectangle provides its own area formula.

---

#  Circle Class 

```python
class Circle(Shape):

    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14 * self.radius * self.radius
```

Circle also implements `area()` in its own way.

---

#  Important Rule

If a child class does not implement `area()`:

```python
class Triangle(Shape):
    pass
```

Creating object of Triangle will give error 

Because abstract method must be implemented.

---

# 














Why Do We Use Abstract Methods?

* To define a common structure
* To force child classes to implement required methods
* To maintain consistency in large projects
* Abstract classes help us catch errors early
* ensure every required method is properly implemented.
---













