# 📝 Java vs Python — Coding Style Cheat Sheet

Comparison of coding conventions, naming standards, and style guidelines between Java and Python

---

<table>
<tr>
<th>Style Aspect</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Naming Conventions</strong></td>
<td>

```java
// camelCase for variables and methods
String userName = "john";
int maxRetries = 3;

// PascalCase for classes
public class UserService {
    public void getUserData() {
        // method body
    }
}

// UPPER_SNAKE_CASE for constants
public static final int MAX_CONNECTIONS = 100;
```

</td>
<td>

```python
# snake_case for variables and functions
user_name = "john"
max_retries = 3

# PascalCase for classes
class UserService:
    def get_user_data(self):
        # method body
        pass

# UPPER_SNAKE_CASE for constants
MAX_CONNECTIONS = 100
```

</td>
</tr>
<tr>
<td><strong>Indentation</strong></td>
<td>

```java
// Uses braces {} for code blocks
public class Example {
    public void method() {
        if (condition) {
            // 4 spaces or 1 tab
            System.out.println("Hello");
        }
    }
}
```

</td>
<td>

```python
# Uses indentation (4 spaces recommended)
class Example:
    def method(self):
        if condition:
            # 4 spaces (PEP 8 standard)
            print("Hello")
```

</td>
</tr>
<tr>
<td><strong>Line Length</strong></td>
<td>

```java
// Generally 80-120 characters
// Can break long lines with proper formatting
String longString = "This is a very long string that " +
                   "continues on the next line";

// Method chaining
object.method1()
      .method2()
      .method3();
```

</td>
<td>

```python
# 79 characters (PEP 8 standard)
# Use parentheses for line continuation
long_string = ("This is a very long string that "
               "continues on the next line")

# Method chaining with backslash
result = (object.method1()
          .method2()
          .method3())
```

</td>
</tr>
<tr>
<td><strong>Imports Organization</strong></td>
<td>

```java
// Standard library first
import java.util.List;
import java.util.ArrayList;

// Third-party libraries
import org.springframework.stereotype.Service;

// Local imports last
import com.example.service.UserService;
```

</td>
<td>

```python
# Standard library first
import os
import sys

# Third-party libraries
import requests
import pandas as pd

# Local imports last
from .models import User
from .services import UserService
```

</td>
</tr>
<tr>
<td><strong>Comments</strong></td>
<td>

```java
// Single line comment
/* Multi-line comment
   for longer explanations */

/**
 * JavaDoc comment for classes and methods
 * @param name the user's name
 * @return formatted greeting
 */
public String greet(String name) {
    return "Hello, " + name;
}
```

</td>
<td>

```python
# Single line comment
# Multi-line comment
# for longer explanations

def greet(name):
    """
    Docstring for functions and classes
    Args:
        name: the user's name
    Returns:
        formatted greeting
    """
    return f"Hello, {name}"
```

</td>
</tr>
<tr>
<td><strong>String Formatting</strong></td>
<td>

```java
// String concatenation
String result = "Hello " + name + "!";

// String.format()
String formatted = String.format("Hello %s! You have %d messages", 
                                name, count);

// StringBuilder for performance
StringBuilder sb = new StringBuilder();
sb.append("Hello ").append(name).append("!");
```

</td>
<td>

```python
# f-strings (Python 3.6+)
result = f"Hello {name}!"

# .format() method
formatted = "Hello {}! You have {} messages".format(name, count)

# % formatting (older style)
formatted = "Hello %s! You have %d messages" % (name, count)
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use meaningful variable and method names
- Follow camelCase convention consistently
- Use JavaDoc for public APIs
- Keep methods under 20 lines when possible
- Use final for immutable variables

### 🐍 Python
- Follow PEP 8 style guide religiously
- Use snake_case for everything except classes
- Write docstrings for all public functions
- Keep lines under 79 characters
- Use type hints for better code documentation

---

💡 **Extra Examples**

```java
// Java - Good style example
public class UserManager {
    private static final int MAX_LOGIN_ATTEMPTS = 3;
    
    private final UserRepository userRepository;
    
    public UserManager(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
    
    /**
     * Authenticates user with given credentials
     * @param username the username
     * @param password the password
     * @return true if authentication successful
     */
    public boolean authenticateUser(String username, String password) {
        if (username == null || password == null) {
            return false;
        }
        
        User user = userRepository.findByUsername(username);
        return user != null && user.getPassword().equals(password);
    }
}
```

```python
# Python - Good style example
from typing import Optional
from dataclasses import dataclass

MAX_LOGIN_ATTEMPTS = 3

@dataclass
class User:
    username: str
    password: str

class UserManager:
    def __init__(self, user_repository):
        self.user_repository = user_repository
    
    def authenticate_user(self, username: str, password: str) -> bool:
        """
        Authenticates user with given credentials
        
        Args:
            username: the username
            password: the password
            
        Returns:
            True if authentication successful
        """
        if not username or not password:
            return False
            
        user = self.user_repository.find_by_username(username)
        return user is not None and user.password == password
```
