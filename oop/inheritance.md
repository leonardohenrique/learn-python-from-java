# 🧬 Java vs Python — Inheritance Cheat Sheet

Comparison of inheritance concepts between Java and Python, covering single inheritance, multiple inheritance, method overriding, and polymorphism.

---

<table>
<tr>
<th>Concept</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Single Inheritance</strong></td>
<td>

```java
public class Animal {
    protected String name;
    
    public Animal(String name) {
        this.name = name;
    }
    
    public void makeSound() {
        System.out.println("Some sound");
    }
}

public class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }
    
    @Override
    public void makeSound() {
        System.out.println("Woof!");
    }
}
```

</td>
<td>

```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def make_sound(self):
        print("Some sound")

class Dog(Animal):
    def __init__(self, name):
        super().__init__(name)
    
    def make_sound(self):
        print("Woof!")
```

</td>
</tr>
<tr>
<td><strong>Multiple Inheritance</strong></td>
<td>

```java
// Java doesn't support multiple inheritance
// Use interfaces instead
public interface Flyable {
    void fly();
}

public interface Swimmable {
    void swim();
}

public class Duck extends Animal 
    implements Flyable, Swimmable {
    
    @Override
    public void fly() {
        System.out.println("Flying");
    }
    
    @Override
    public void swim() {
        System.out.println("Swimming");
    }
}
```

</td>
<td>

```python
class Flyable:
    def fly(self):
        print("Flying")

class Swimmable:
    def swim(self):
        print("Swimming")

class Duck(Animal, Flyable, Swimmable):
    def __init__(self, name):
        super().__init__(name)
    
    def make_sound(self):
        print("Quack!")
```

</td>
</tr>
<tr>
<td><strong>Method Overriding</strong></td>
<td>

```java
public class Shape {
    public double getArea() {
        return 0;
    }
}

public class Circle extends Shape {
    private double radius;
    
    public Circle(double radius) {
        this.radius = radius;
    }
    
    @Override
    public double getArea() {
        return Math.PI * radius * radius;
    }
}
```

</td>
<td>

```python
class Shape:
    def get_area(self):
        return 0

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def get_area(self):
        import math
        return math.pi * self.radius ** 2
```

</td>
</tr>
<tr>
<td><strong>Abstract Classes</strong></td>
<td>

```java
public abstract class Vehicle {
    protected String brand;
    
    public Vehicle(String brand) {
        this.brand = brand;
    }
    
    public abstract void start();
    
    public void stop() {
        System.out.println("Vehicle stopped");
    }
}

public class Car extends Vehicle {
    public Car(String brand) {
        super(brand);
    }
    
    @Override
    public void start() {
        System.out.println("Car engine started");
    }
}
```

</td>
<td>

```python
from abc import ABC, abstractmethod

class Vehicle(ABC):
    def __init__(self, brand):
        self.brand = brand
    
    @abstractmethod
    def start(self):
        pass
    
    def stop(self):
        print("Vehicle stopped")

class Car(Vehicle):
    def __init__(self, brand):
        super().__init__(brand)
    
    def start(self):
        print("Car engine started")
```

</td>
</tr>
<tr>
<td><strong>Polymorphism</strong></td>
<td>

```java
public class Animal {
    public void makeSound() {
        System.out.println("Animal sound");
    }
}

public class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Meow");
    }
}

// Usage
Animal[] animals = {
    new Animal(),
    new Cat(),
    new Dog("Buddy")
};

for (Animal animal : animals) {
    animal.makeSound(); // Polymorphic call
}
```

</td>
<td>

```python
class Animal:
    def make_sound(self):
        print("Animal sound")

class Cat(Animal):
    def make_sound(self):
        print("Meow")

# Usage
animals = [
    Animal(),
    Cat(),
    Dog("Buddy")
]

for animal in animals:
    animal.make_sound()  # Polymorphic call
```

</td>
</tr>
<tr>
<td><strong>Super Keyword</strong></td>
<td>

```java
public class Parent {
    protected String name;
    
    public Parent(String name) {
        this.name = name;
    }
    
    public void display() {
        System.out.println("Parent: " + name);
    }
}

public class Child extends Parent {
    private int age;
    
    public Child(String name, int age) {
        super(name);  // Call parent constructor
        this.age = age;
    }
    
    @Override
    public void display() {
        super.display();  // Call parent method
        System.out.println("Child age: " + age);
    }
}
```

</td>
<td>

```python
class Parent:
    def __init__(self, name):
        self.name = name
    
    def display(self):
        print(f"Parent: {self.name}")

class Child(Parent):
    def __init__(self, name, age):
        super().__init__(name)  # Call parent constructor
        self.age = age
    
    def display(self):
        super().display()  # Call parent method
        print(f"Child age: {self.age}")
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `extends` for single inheritance
- Use `implements` for multiple interfaces
- `@Override` annotation for method overriding
- `super()` must be first statement in constructor
- `protected` allows access in subclasses

### 🐍 Python
- Multiple inheritance supported natively
- Method Resolution Order (MRO) determines method lookup
- `super()` works with multiple inheritance
- No explicit access modifiers
- `ABC` and `@abstractmethod` for abstract classes

---

💡 **Extra Examples**

```java
// Java - Interface inheritance
public interface Drawable {
    void draw();
}

public interface Resizable {
    void resize(double factor);
}

public class Rectangle implements Drawable, Resizable {
    @Override
    public void draw() {
        System.out.println("Drawing rectangle");
    }
    
    @Override
    public void resize(double factor) {
        System.out.println("Resizing by " + factor);
    }
}
```

```python
# Python - Method Resolution Order
class A:
    def method(self):
        print("A")

class B(A):
    def method(self):
        print("B")

class C(A):
    def method(self):
        print("C")

class D(B, C):
    pass

d = D()
d.method()  # Prints "B" (MRO: D -> B -> C -> A)
print(D.__mro__)  # Shows method resolution order
```
