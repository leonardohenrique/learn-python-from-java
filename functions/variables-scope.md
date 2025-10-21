# 🎯 Java vs Python — Variable Scope Cheat Sheet

Comparison of variable scope, lifetime, and access modifiers between Java and Python

---

<table>
<tr>
<th>Concept</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Local Variables</strong></td>
<td>

```java
public class ScopeExample {
    public void method() {
        int localVar = 10;  // Local to method
        if (true) {
            int blockVar = 20;  // Local to block
            System.out.println(localVar);  // OK
        }
        // System.out.println(blockVar);  // Error!
    }
}
```

</td>
<td>

```python
def method():
    local_var = 10  # Local to function
    if True:
        block_var = 20  # Local to function (not block)
        print(local_var)  # OK
    print(block_var)  # OK - Python has function scope
```

</td>
</tr>
<tr>
<td><strong>Global Variables</strong></td>
<td>

```java
public class GlobalExample {
    private static int globalVar = 100;  // Class-level global
    
    public void method() {
        System.out.println(globalVar);  // Access global
        // globalVar = 200;  // Can modify
    }
    
    public static void staticMethod() {
        System.out.println(globalVar);  // Access from static
    }
}
```

</td>
<td>

```python
global_var = 100  # Module-level global

def method():
    global global_var
    print(global_var)  # Access global
    global_var = 200   # Modify global (requires 'global')

def another_method():
    print(global_var)  # Access global (read-only)
```

</td>
</tr>
<tr>
<td><strong>Modifying Globals Inside a Function</strong></td>
<td>

```java
public class GlobalModification {
    private static int counter = 0;
    
    public static void incrementCounter() {
        counter++;  // Can modify static variable directly
        System.out.println("Counter: " + counter);
    }
    
    public static void resetCounter() {
        counter = 0;  // Direct modification
    }
    
    public static int getCounter() {
        return counter;
    }
}
```

</td>
<td>

```python
counter = 0  # Global variable

def increment_counter():
    global counter
    counter += 1  # Must use 'global' keyword
    print(f"Counter: {counter}")

def reset_counter():
    global counter
    counter = 0  # Must use 'global' keyword

def get_counter():
    return counter  # Read-only access doesn't need 'global'

# Without 'global' keyword (creates local variable)
def bad_increment():
    counter = counter + 1  # UnboundLocalError!
```

</td>
</tr>
<tr>
<td><strong>Enclosing Scope</strong></td>
<td>

```java
// Java doesn't have enclosing scope concept
// Use anonymous inner classes or lambda expressions instead
```

</td>
<td>

```python
def outer_function(x):
    def inner_function(y):
        return x + y  # x is from enclosing scope
    return inner_function

# Create closure
add_five = outer_function(5)
result = add_five(3)  # Returns 8

# Another example
def create_multiplier(n):
    def multiplier(x):
        return x * n  # n is from enclosing scope
    return multiplier

double = create_multiplier(2)
triple = create_multiplier(3)
print(double(5))  # 10
print(triple(5))  # 15
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Variables have block scope (curly braces define scope)
- Use `this` to access instance variables when shadowed
- Static variables belong to the class, not instances
- Access modifiers control visibility at compile time
- Static variables can be modified directly within static methods
- No enclosing scope concept (use anonymous classes or lambdas)

### 🐍 Python
- Variables have function scope (entire function is scope)
- Use `global` keyword to modify global variables
- Use `nonlocal` to modify variables in enclosing scope
- Access control is by convention (single/double underscores)
- Without `global`, assignment creates a local variable
- Functions can access variables from enclosing scope (closures)

---

💡 **Extra Examples**

```java
// Java - Complex scope example
public class ScopeDemo {
    private static int classVar = 0;
    private int instanceVar = 0;
    
    public void demonstrateScope() {
        int localVar = 0;
        
        for (int i = 0; i < 3; i++) {
            int loopVar = i;  // Block scope
            localVar += loopVar;
            instanceVar += loopVar;
            classVar += loopVar;
        }
        
        // System.out.println(loopVar);  // Error - out of scope
        System.out.println("Local: " + localVar);
        System.out.println("Instance: " + instanceVar);
        System.out.println("Class: " + classVar);
    }
    
    public static void staticMethod() {
        // System.out.println(instanceVar);  // Error - can't access instance
        System.out.println("Class var: " + classVar);
    }
}
```

```python
# Python - Complex scope example
class_var = 0

class ScopeDemo:
    def __init__(self):
        self.instance_var = 0
    
    def demonstrate_scope(self):
        local_var = 0
        
        for i in range(3):
            loop_var = i  # Function scope
            local_var += loop_var
            self.instance_var += loop_var
            global class_var
            class_var += loop_var
        
        print(f"Local: {local_var}")
        print(f"Instance: {self.instance_var}")
        print(f"Class: {class_var}")
        print(f"Loop var: {loop_var}")  # OK - function scope
    
    @classmethod
    def class_method(cls):
        print(f"Class var: {class_var}")
    
    def nested_function_example(self):
        outer_var = 10
        
        def inner_function():
            nonlocal outer_var
            outer_var = 20  # Modify outer function's variable
            print(f"Inner: {outer_var}")
        
        inner_function()
        print(f"Outer: {outer_var}")  # 20
```
