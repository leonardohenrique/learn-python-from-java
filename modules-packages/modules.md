# 📦 Java vs Python — Modules Cheat Sheet

Comparison of module concepts and organization between Java and Python

---

<table>
<tr>
<th>Concept</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Module Definition</strong></td>
<td>

```java
// A Java file is a compilation unit
// Each .java file can contain multiple classes
// File: Calculator.java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}

public class MathUtils {
    public static double pi = 3.14159;
}
```

</td>
<td>

```python
# A Python file is a module
# File: calculator.py
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

# Module-level variables
PI = 3.14159
```

</td>
</tr>
<tr>
<td><strong>Module Execution</strong></td>
<td>

```java
// Java modules are compiled to .class files
// Execution requires a main method
public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        int result = calc.add(5, 3);
        System.out.println(result);
    }
}
```

</td>
<td>

```python
# Python modules can be executed directly
# File: calculator.py
def add(a, b):
    return a + b

# Module can be run directly
if __name__ == "__main__":
    result = add(5, 3)
    print(result)
```

</td>
</tr>
<tr>
<td><strong>Module Variables</strong></td>
<td>

```java
// Java uses static variables for module-level data
public class Config {
    public static final String APP_NAME = "MyApp";
    public static int instanceCount = 0;
    
    public static void incrementCount() {
        instanceCount++;
    }
}
```

</td>
<td>

```python
# Python module variables are global to the module
# File: config.py
APP_NAME = "MyApp"
instance_count = 0

def increment_count():
    global instance_count
    instance_count += 1
```

</td>
</tr>
<tr>
<td><strong>Module Initialization</strong></td>
<td>

```java
// Java uses static blocks for initialization
public class Database {
    private static Connection connection;
    
    static {
        try {
            connection = DriverManager.getConnection("jdbc:mysql://localhost/db");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

</td>
<td>

```python
# Python modules execute top-level code on import
# File: database.py
import sqlite3

# This runs when module is imported
connection = sqlite3.connect("database.db")

def get_connection():
    return connection
```

</td>
</tr>
<tr>
<td><strong>Module Namespace</strong></td>
<td>

```java
// Java uses packages for namespacing
package com.example.utils;

public class StringHelper {
    public static String capitalize(String str) {
        return str.substring(0, 1).toUpperCase() + 
               str.substring(1).toLowerCase();
    }
}

// Usage: com.example.utils.StringHelper.capitalize("hello")
```

</td>
<td>

```python
# Python modules create their own namespace
# File: string_helper.py
def capitalize(text):
    return text[0].upper() + text[1:].lower()

def reverse(text):
    return text[::-1]

# Usage: string_helper.capitalize("hello")
```

</td>
</tr>
<tr>
<td><strong>Module Reloading</strong></td>
<td>

```java
// Java doesn't support module reloading
// Requires application restart or custom classloader
public class ModuleManager {
    private static ClassLoader customLoader;
    
    public static void reloadModule(String className) {
        // Complex custom implementation needed
        // Usually requires application restart
    }
}
```

</td>
<td>

```python
# Python supports module reloading
import importlib
import my_module

# Reload module during runtime
importlib.reload(my_module)

# Or using imp module (deprecated in Python 3.4+)
import imp
imp.reload(my_module)
```

</td>
</tr>
<tr>
<td><strong>Module Metadata</strong></td>
<td>

```java
// Java uses annotations for metadata
@Deprecated
public class OldCalculator {
    @SuppressWarnings("unchecked")
    public void oldMethod() {
        // Deprecated functionality
    }
}

// Package-info.java for package-level metadata
@PackageAnnotation
package com.example.utils;
```

</td>
<td>

```python
# Python uses module-level variables for metadata
# File: my_module.py
__version__ = "1.0.0"
__author__ = "John Doe"
__all__ = ["public_function", "PublicClass"]

def public_function():
    pass

def _private_function():
    pass

class PublicClass:
    pass
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Each .java file can contain multiple public classes
- Static blocks run when class is first loaded
- Use packages for namespace organization
- Module reloading requires custom implementation

### 🐍 Python
- Each .py file is a module with its own namespace
- Top-level code executes on import
- Use `__all__` to control `from module import *`
- Built-in support for module reloading

---

💡 **Extra Examples**

```java
// Java - Module with multiple classes
public class MathOperations {
    public static int add(int a, int b) { return a + b; }
    public static int multiply(int a, int b) { return a * b; }
}

public class StringOperations {
    public static String reverse(String str) {
        return new StringBuilder(str).reverse().toString();
    }
}

// Java - Static initialization
public class Logger {
    private static final Logger INSTANCE;
    
    static {
        INSTANCE = new Logger();
        System.out.println("Logger initialized");
    }
    
    public static Logger getInstance() {
        return INSTANCE;
    }
}
```

```python
# Python - Module with multiple functions
def add(a, b):
    return a + b

def multiply(a, b):
    return a * b

def reverse(text):
    return text[::-1]

# Python - Module initialization
print("Module is being imported")

# Python - Conditional execution
if __name__ == "__main__":
    print("Module is being run directly")
    print(f"2 + 3 = {add(2, 3)}")
else:
    print("Module is being imported")
```
