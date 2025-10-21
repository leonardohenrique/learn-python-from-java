# 🏗️ Java vs Python — Classes and Objects Cheat Sheet

Comparison of object-oriented programming concepts between Java and Python, focusing on class definition, object creation, and basic OOP principles.

---

<table>
<tr>
<th>Concept</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Class Definition</strong></td>
<td>

```java
public class Person {
    private String name;
    private int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

</td>
<td>

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
```

</td>
</tr>
<tr>
<td><strong>Object Creation</strong></td>
<td>

```java
Person person = new Person("Alice", 30);
```

</td>
<td>

```python
person = Person("Alice", 30)
```

</td>
</tr>

<tr>
<td><strong>Instance Attribute</strong></td>
<td>

```java
public class Person {
    private String name;
    private int age;
    
    public Person(String name, int age) {
        this.name = name;  // Instance attribute
        this.age = age;    // Instance attribute
    }
    
    public void setName(String name) {
        this.name = name;  // Modifying instance attribute
    }
}
```

</td>
<td>

```python
class Person:
    def __init__(self, name, age):
        self.name = name  # Instance attribute
        self.age = age    # Instance attribute
    
    def set_name(self, name):
        self.name = name  # Modifying instance attribute
```

</td>
</tr>
<tr>
<td><strong>Class Attribute</strong></td>
<td>

```java
public class Person {
    private static int totalPersons = 0;
    
    public Person() {
        totalPersons++;
    }
    
    public static int getTotalPersons() {
        return totalPersons;
    }
}
```

</td>
<td>

```python
class Person:
    total_persons = 0
    
    def __init__(self):
        Person.total_persons += 1
    
    @classmethod
    def get_total_persons(cls):
        return cls.total_persons
```

</td>
</tr>

<tr>
<td><strong>Methods</strong></td>
<td>

```java
public class Person {
    public void greet() {
        System.out.println("Hello, I'm " + name);
    }
    
    public void greet(String greeting) {
        System.out.println(greeting + ", I'm " + name);
    }
    
    public String getName() {
        return name;
    }
}
```

</td>
<td>

```python
class Person:
    def greet(self):
        print(f"Hello, I'm {self.name}")
    
    def greet(self, greeting):
        print(f"{greeting}, I'm {self.name}")
    
    def get_name(self):
        return self.name
```

</td>
</tr>

<tr>
<td><strong>Constructor Overloading</strong></td>
<td>

```java
public class Person {
    public Person() {
        this("Unknown", 0);
    }
    
    public Person(String name) {
        this(name, 0);
    }
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

</td>
<td>

```python
class Person:
    def __init__(self, name="Unknown", age=0):
        self.name = name
        self.age = age
```

</td>
</tr>
<tr>
<td><strong>Access and Modify Attributes</strong></td>
<td>

```java
public class Person {
    private String name;
    private int age;
    
    // Getter methods
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
    
    // Setter methods
    public void setName(String name) {
        this.name = name;
    }
    
    public void setAge(int age) {
        this.age = age;
    }
}

// Usage
Person person = new Person("Alice", 30);
String name = person.getName();  // Access
person.setAge(31);               // Modify
```

</td>
<td>

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

# Usage
person = Person("Alice", 30)
name = person.name        # Direct access
person.age = 31           # Direct modification

# Or with methods
def get_name(self):
    return self.name

def set_age(self, age):
    self.age = age
```

</td>
</tr>
<tr>
<td><strong>Delete Attributes and Objects</strong></td>
<td>

```java
public class Person {
    private String name;
    private int age;
    
    public void deleteName() {
        this.name = null;  // Set to null
    }
    
    public void deleteAge() {
        this.age = 0;  // Reset to default
    }
}

// Usage
Person person = new Person("Alice", 30);
person.deleteName();  // Delete attribute
person = null;        // Delete object (garbage collected)
```

</td>
<td>

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

# Usage
person = Person("Alice", 30)
del person.name        # Delete attribute
del person             # Delete object

# Or set to None
person = Person("Alice", 30)
person.name = None     # Set attribute to None
person = None          # Set object to None
```

</td>
</tr>
<tr>
<td><strong>String Representation</strong></td>
<td>

```java
public class Person {
    @Override
    public String toString() {
        return "Person{name='" + name + 
               "', age=" + age + "}";
    }
}
```

</td>
<td>

```python
class Person:
    def __str__(self):
        return f"Person(name='{self.name}', age={self.age})"
    
    def __repr__(self):
        return f"Person('{self.name}', {self.age})"
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `private` for encapsulation, `public` for interface
- Constructor name must match class name exactly
- Use `this` keyword to refer to current object
- Static methods belong to class, not instances

### 🐍 Python
- Use `self` as first parameter in instance methods
- `__init__` is the constructor method
- No explicit access modifiers (convention: underscore prefix for private)
- `__str__` for user-friendly output, `__repr__` for developer output

---

💡 **Extra Examples**

```java
// Java - Multiple constructors
public class Student extends Person {
    private String studentId;
    
    public Student(String name, int age, String studentId) {
        super(name, age);
        this.studentId = studentId;
    }
}
```

```python
# Python - Multiple inheritance
class Student(Person):
    def __init__(self, name, age, student_id):
        super().__init__(name, age)
        self.student_id = student_id
```
