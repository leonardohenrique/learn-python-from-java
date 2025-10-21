# 🔧 Java vs Python — Functions Cheat Sheet

Comparison of function definitions, parameters, return values, and method overloading between Java and Python

---

<table>
<tr>
<th>Concept</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Basic Function Definition</strong></td>
<td>

```java
public static int add(int a, int b) {
    return a + b;
}
```

</td>
<td>

```python
def add(a, b):
    return a + b
```

</td>
</tr>
<tr>
<td><strong>Function with Default Parameters</strong></td>
<td>

```java
// Java doesn't support default parameters
// Use method overloading instead
public static int multiply(int a, int b) {
    return multiply(a, b, 1);
}

public static int multiply(int a, int b, int c) {
    return a * b * c;
}
```

</td>
<td>

```python
def multiply(a, b, c=1):
    return a * b * c
```

</td>
</tr>
<tr>
<td><strong>Variable Arguments</strong></td>
<td>

```java
public static int sum(int... numbers) {
    int total = 0;
    for (int num : numbers) {
        total += num;
    }
    return total;
}
```

</td>
<td>

```python
def sum(*numbers):
    return sum(numbers)
```

</td>
</tr>
<tr>
<td><strong>Keyword Arguments</strong></td>
<td>

```java
// Java doesn't support keyword arguments
// Use method overloading or builder pattern
public static void greet(String name, int age) {
    System.out.println("Hello " + name + ", age " + age);
}
```

</td>
<td>

```python
def greet(name, age):
    print(f"Hello {name}, age {age}")

# Can be called with keyword arguments
greet(age=25, name="Alice")
```

</td>
</tr>
<tr>
<td><strong>Return Multiple Values</strong></td>
<td>

```java
// Java doesn't support multiple return values
// Use custom class or array
public static int[] divide(int a, int b) {
    return new int[]{a / b, a % b};
}
```

</td>
<td>

```python
def divide(a, b):
    return a // b, a % b

# Unpacking
quotient, remainder = divide(10, 3)
```

</td>
</tr>
<tr>
<td><strong>Documentation</strong></td>
<td>

```java
/**
 * Calculates the factorial of a given number.
 * 
 * @param n the non-negative integer to calculate factorial for
 * @return the factorial of n
 * @throws IllegalArgumentException if n is negative
 */public static int factorial(int n) {
    if (n < 0) {
        throw new IllegalArgumentException("n must be non-negative");
    }
    if (n <= 1) {
        return 1;
    }
    return n * factorial(n - 1);
}
```

</td>
<td>

```python
def factorial(n: int) -> int:
    """
    Calculate factorial of n.
    
    Args:
        n: Non-negative integer
        
    Returns:
        Factorial of n
        
    Raises:
        ValueError: If n is negative
    """
    if n < 0:
        raise ValueError("n must be non-negative")
    if n <= 1:
        return 1
    return n * factorial(n - 1)
```

</td>
</tr>
<tr>
<td><strong>Function as Parameter</strong></td>
<td>

```java
// Using functional interfaces
@FunctionalInterface
interface Operation {
    int apply(int a, int b);
}

public static int calculate(int a, int b, Operation op) {
    return op.apply(a, b);
}

// Usage
int result = calculate(5, 3, (x, y) -> x + y);
```

</td>
<td>

```python
def calculate(a, b, operation):
    return operation(a, b)

# Usage
result = calculate(5, 3, lambda x, y: x + y)
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `public static` for utility functions
- Method overloading allows multiple signatures
- Use `@FunctionalInterface` for function parameters
- Return types must be explicitly declared
- Use JavaDoc comments (`/** */`) for method documentation

### 🐍 Python
- Functions are first-class objects
- Default parameters must come after required ones
- Use `*args` for variable arguments, `**kwargs` for keyword arguments
- Functions can return multiple values as tuples
- Use docstrings (`""" """`) for function documentation

---

💡 **Extra Examples**

```java
// Java - Method overloading
public class Calculator {
    public static int add(int a, int b) {
        return a + b;
    }
    
    public static double add(double a, double b) {
        return a + b;
    }
    
    public static int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

```python
# Python - Function with type hints
from typing import List, Tuple

def process_data(data: List[int]) -> Tuple[int, float]:
    total = sum(data)
    average = total / len(data)
    return total, average

# Function with docstring
def factorial(n: int) -> int:
    """
    Calculate factorial of n.
    
    Args:
        n: Non-negative integer
        
    Returns:
        Factorial of n
    """
    if n <= 1:
        return 1
    return n * factorial(n - 1)
```
