# ⚠️ Java vs Python — Errors and Exceptions Cheat Sheet

Comparison of error handling and exception management between Java and Python

---

<table>
<tr>
<th>Concept</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Basic Exception Handling</strong></td>
<td>

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Error: " + e.getMessage());
} finally {
    System.out.println("Cleanup code");
}
```

</td>
<td>

```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(f"Error: {e}")
finally:
    print("Cleanup code")
```

</td>
</tr>
<tr>
<td><strong>Multiple Exception Handling</strong></td>
<td>

```java
try {
    // risky code
} catch (ArithmeticException e) {
    System.out.println("Math error");
} catch (NullPointerException e) {
    System.out.println("Null pointer");
} catch (Exception e) {
    System.out.println("General error");
}
```

</td>
<td>

```python
try:
    # risky code
except ZeroDivisionError:
    print("Math error")
except AttributeError:
    print("Attribute error")
except Exception as e:
    print("General error")
```

</td>
</tr>
<tr>
<td><strong>Custom Exception</strong></td>
<td>

```java
class CustomException extends Exception {
    public CustomException(String message) {
        super(message);
    }
}

// Usage
throw new CustomException("Something went wrong");
```

</td>
<td>

```python
class CustomException(Exception):
    def __init__(self, message):
        self.message = message
        super().__init__(self.message)

# Usage
raise CustomException("Something went wrong")
```

</td>
</tr>
<tr>
<td><strong>Exception Propagation</strong></td>
<td>

```java
public void method1() throws CustomException {
    method2();
}

public void method2() throws CustomException {
    throw new CustomException("Error in method2");
}
```

</td>
<td>

```python
def method1():
    method2()

def method2():
    raise CustomException("Error in method2")
```

</td>
</tr>
<tr>
<td><strong>Resource Management</strong></td>
<td>

```java
try (FileInputStream fis = new FileInputStream("file.txt")) {
    // use resource
} catch (IOException e) {
    System.out.println("IO Error: " + e.getMessage());
}
```

</td>
<td>

```python
try:
    with open("file.txt", "r") as file:
        # use resource
        pass
except IOError as e:
    print(f"IO Error: {e}")
```

</td>
</tr>
<tr>
<td><strong>Assertions</strong></td>
<td>

```java
assert x > 0 : "x must be positive";
// Enable with: java -ea MyClass
```

</td>
<td>

```python
assert x > 0, "x must be positive"
# Enable with: python -O (disables assertions)
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Always catch specific exceptions before general ones
- Use try-with-resources for automatic resource management
- Checked exceptions must be handled or declared in method signature
- Use `@SuppressWarnings` to suppress specific warnings

### 🐍 Python
- Use `except` without specifying exception type sparingly
- Context managers (`with` statement) are preferred for resource management
- All exceptions inherit from `BaseException`
- Use `raise ... from ...` for exception chaining

---

💡 **Extra Examples**

```java
// Java - Exception chaining
try {
    // some operation
} catch (IOException e) {
    throw new CustomException("Failed to process file").initCause(e);
}

// Java - Multiple resources
try (FileInputStream fis = new FileInputStream("input.txt");
     FileOutputStream fos = new FileOutputStream("output.txt")) {
    // process files
}
```

```python
# Python - Exception chaining
try:
    # some operation
except IOError as e:
    raise CustomException("Failed to process file") from e

# Python - Multiple context managers
with open("input.txt", "r") as infile, open("output.txt", "w") as outfile:
    # process files
    pass
```
