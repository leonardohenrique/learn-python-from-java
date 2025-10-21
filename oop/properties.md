# 🔧 Java vs Python — Properties Cheat Sheet

Comparison of property management between Java and Python, covering getters, setters, encapsulation, and property decorators.

---

<table>
<tr>
<th>Concept</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Basic Getters and Setters</strong></td>
<td>

```java
public class Person {
    private String name;
    private int age;
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        if (name != null && !name.trim().isEmpty()) {
            this.name = name;
        }
    }
    
    public int getAge() {
        return age;
    }
    
    public void setAge(int age) {
        if (age >= 0 && age <= 150) {
            this.age = age;
        }
    }
}
```

</td>
<td>

```python
class Person:
    def __init__(self, name, age):
        self._name = name
        self._age = age
    
    def get_name(self):
        return self._name
    
    def set_name(self, name):
        if name and name.strip():
            self._name = name
    
    def get_age(self):
        return self._age
    
    def set_age(self, age):
        if 0 <= age <= 150:
            self._age = age
```

</td>
</tr>
<tr>
<td><strong>Property Decorator</strong></td>
<td>

```java
// Java doesn't have property decorators
// Use getters/setters or records (Java 14+)
public record PersonRecord(String name, int age) {
    public PersonRecord {
        if (name == null || name.trim().isEmpty()) {
            throw new IllegalArgumentException("Name cannot be empty");
        }
        if (age < 0 || age > 150) {
            throw new IllegalArgumentException("Invalid age");
        }
    }
}
```

</td>
<td>

```python
class Person:
    def __init__(self, name, age):
        self._name = name
        self._age = age
    
    @property
    def name(self):
        return self._name
    
    @name.setter
    def name(self, value):
        if not value or not value.strip():
            raise ValueError("Name cannot be empty")
        self._name = value
    
    @property
    def age(self):
        return self._age
    
    @age.setter
    def age(self, value):
        if not (0 <= value <= 150):
            raise ValueError("Invalid age")
        self._age = value
```

</td>
</tr>
<tr>
<td><strong>Read-Only Properties</strong></td>
<td>

```java
public class Circle {
    private final double radius;
    
    public Circle(double radius) {
        this.radius = radius;
    }
    
    public double getRadius() {
        return radius;
    }
    
    public double getArea() {
        return Math.PI * radius * radius;
    }
    
    public double getCircumference() {
        return 2 * Math.PI * radius;
    }
}
```

</td>
<td>

```python
class Circle:
    def __init__(self, radius):
        self._radius = radius
    
    @property
    def radius(self):
        return self._radius
    
    @property
    def area(self):
        import math
        return math.pi * self._radius ** 2
    
    @property
    def circumference(self):
        import math
        return 2 * math.pi * self._radius
```

</td>
</tr>
<tr>
<td><strong>Computed Properties</strong></td>
<td>

```java
public class Rectangle {
    private double width;
    private double height;
    
    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }
    
    public double getArea() {
        return width * height;
    }
    
    public double getPerimeter() {
        return 2 * (width + height);
    }
    
    public double getDiagonal() {
        return Math.sqrt(width * width + height * height);
    }
}
```

</td>
<td>

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    @property
    def area(self):
        return self.width * self.height
    
    @property
    def perimeter(self):
        return 2 * (self.width + self.height)
    
    @property
    def diagonal(self):
        import math
        return math.sqrt(self.width ** 2 + self.height ** 2)
```

</td>
</tr>
<tr>
<td><strong>Property with Validation</strong></td>
<td>

```java
public class Email {
    private String address;
    
    public Email(String address) {
        setAddress(address);
    }
    
    public String getAddress() {
        return address;
    }
    
    public void setAddress(String address) {
        if (address == null || !address.contains("@")) {
            throw new IllegalArgumentException("Invalid email address");
        }
        this.address = address;
    }
}
```

</td>
<td>

```python
class Email:
    def __init__(self, address):
        self.address = address
    
    @property
    def address(self):
        return self._address
    
    @address.setter
    def address(self, value):
        if not value or "@" not in value:
            raise ValueError("Invalid email address")
        self._address = value
```

</td>
</tr>
<tr>
<td><strong>property() Function</strong></td>
<td>

```java
// Java doesn't have property() function
// Use getters/setters or records
public record PersonRecord(String name, int age) {
    public PersonRecord {
        if (name == null || name.trim().isEmpty()) {
            throw new IllegalArgumentException("Name cannot be empty");
        }
    }
}
```

</td>
<td>

```python
class Person:
    def __init__(self, name, age):
        self._name = name
        self._age = age
    
    def get_name(self):
        return self._name
    
    def set_name(self, value):
        if not value or not value.strip():
            raise ValueError("Name cannot be empty")
        self._name = value
    
    def del_name(self):
        del self._name
    
    # Using property() function
    name = property(get_name, set_name, del_name, "Name property")
    
    # Or with lambda functions
    age = property(
        lambda self: self._age,
        lambda self, value: setattr(self, '_age', value) if 0 <= value <= 150 else None,
        lambda self: delattr(self, '_age'),
        "Age property"
    )
```

</td>
</tr>
<tr>
<td><strong>Lazy Properties</strong></td>
<td>

```java
public class ExpensiveCalculation {
    private String data;
    private String cachedResult;
    
    public ExpensiveCalculation(String data) {
        this.data = data;
    }
    
    public String getResult() {
        if (cachedResult == null) {
            cachedResult = performExpensiveCalculation(data);
        }
        return cachedResult;
    }
    
    private String performExpensiveCalculation(String data) {
        // Simulate expensive operation
        return "Processed: " + data;
    }
}
```

</td>
<td>

```python
class ExpensiveCalculation:
    def __init__(self, data):
        self.data = data
        self._cached_result = None
    
    @property
    def result(self):
        if self._cached_result is None:
            self._cached_result = self._perform_expensive_calculation()
        return self._cached_result
    
    def _perform_expensive_calculation(self):
        # Simulate expensive operation
        return f"Processed: {self.data}"
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `private` fields with public getters/setters
- `final` keyword makes fields immutable
- Records (Java 14+) provide automatic getters
- Validation in setters for data integrity
- Use `@Override` for method overriding

### 🐍 Python
- `@property` decorator for getter-like access
- `@property.setter` for setter-like access
- Underscore prefix (`_`) indicates private by convention
- Properties can be computed on-the-fly
- Use `property()` function for dynamic properties

---

💡 **Extra Examples**

```java
// Java - Builder pattern with properties
public class Person {
    private String name;
    private int age;
    private String email;
    
    private Person() {}
    
    public static class Builder {
        private Person person = new Person();
        
        public Builder name(String name) {
            person.name = name;
            return this;
        }
        
        public Builder age(int age) {
            person.age = age;
            return this;
        }
        
        public Person build() {
            return person;
        }
    }
}
```

```python
# Python - Property with custom getter/setter
class Temperature:
    def __init__(self, celsius=0):
        self._celsius = celsius
    
    @property
    def celsius(self):
        return self._celsius
    
    @celsius.setter
    def celsius(self, value):
        self._celsius = value
    
    @property
    def fahrenheit(self):
        return self._celsius * 9/5 + 32
    
    @fahrenheit.setter
    def fahrenheit(self, value):
        self._celsius = (value - 32) * 5/9
```
