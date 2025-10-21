# 🔑 Java vs Python — Keywords Cheat Sheet

Comparison of reserved keywords and their usage between Java and Python programming languages

---

<table>
<tr>
<th>Category</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Access Modifiers</strong></td>
<td>

```java
public class MyClass {
    public int publicVar;
    private int privateVar;
    protected int protectedVar;
    int packageVar; // default
}
```

</td>
<td>

```python
class MyClass:
    def __init__(self):
        self.public_var = 1
        self._protected_var = 2
        self.__private_var = 3
```

</td>
</tr>
<tr>
<td><strong>Control Flow</strong></td>
<td>

```java
if (condition) {
    // code
} else if (other) {
    // code
} else {
    // code
}

for (int i = 0; i < 10; i++) {
    // code
}

while (condition) {
    // code
}
```

</td>
<td>

```python
if condition:
    # code
elif other:
    # code
else:
    # code

for i in range(10):
    # code

while condition:
    # code
```

</td>
</tr>
<tr>
<td><strong>Exception Handling</strong></td>
<td>

```java
try {
    // risky code
} catch (ExceptionType e) {
    // handle exception
} finally {
    // cleanup code
}

throw new Exception("Error message");
```

</td>
<td>

```python
try:
    # risky code
except ExceptionType as e:
    # handle exception
finally:
    # cleanup code

raise Exception("Error message")
```

</td>
</tr>
<tr>
<td><strong>Class Definition</strong></td>
<td>

```java
public class MyClass extends ParentClass 
    implements Interface1, Interface2 {
    
    private String name;
    
    public MyClass(String name) {
        this.name = name;
    }
    
    public void method() {
        // code
    }
}
```

</td>
<td>

```python
class MyClass(ParentClass, Interface1, Interface2):
    def __init__(self, name):
        self.name = name
    
    def method(self):
        # code
        pass
```

</td>
</tr>
<tr>
<td><strong>Method/Function Definition</strong></td>
<td>

```java
public static void main(String[] args) {
    // entry point
}

public int calculate(int a, int b) {
    return a + b;
}

private void helper() {
    // helper method
}
```

</td>
<td>

```python
def main():
    # entry point
    pass

def calculate(a, b):
    return a + b

def _helper():
    # helper method
    pass
```

</td>
</tr>
<tr>
<td><strong>Variable Declaration</strong></td>
<td>

```java
int number = 42;
String text = "Hello";
boolean flag = true;
final int CONSTANT = 100;
```

</td>
<td>

```python
number = 42
text = "Hello"
flag = True
CONSTANT = 100  # convention for constants
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `final` for constants and immutable references
- Access modifiers (`public`, `private`, `protected`) control visibility
- `static` methods belong to the class, not instances
- `this` refers to the current object instance

### 🐍 Python
- No explicit access modifiers - use naming conventions (`_` for protected, `__` for private)
- `self` is the first parameter in instance methods
- `pass` is used for empty code blocks
- `None` is Python's equivalent to Java's `null`

---

💡 **Extra Examples**

```java
// Java - Interface and Abstract Class
public interface Drawable {
    void draw();
}

public abstract class Shape implements Drawable {
    protected String color;
    
    public abstract double getArea();
    
    public void setColor(String color) {
        this.color = color;
    }
}
```

```python
# Python - Abstract Base Class
from abc import ABC, abstractmethod

class Drawable(ABC):
    @abstractmethod
    def draw(self):
        pass

class Shape(Drawable):
    def __init__(self, color):
        self.color = color
    
    @abstractmethod
    def get_area(self):
        pass
    
    def set_color(self, color):
        self.color = color
```
