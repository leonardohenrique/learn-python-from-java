# 🎨 Java vs Python — Decorators Cheat Sheet

Comparison of decorator patterns and annotations between Java and Python for cross-cutting concerns

---

<table>
<tr>
<th>Concept</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Basic Decorator/Annotation</strong></td>
<td>

```java
// Custom annotation
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface LogExecution {
    String value() default "";
}

// Usage
@LogExecution("User login")
public void login(String username) {
    // login logic
}
```

</td>
<td>

```python
def log_execution(func):
    def wrapper(*args, **kwargs):
        print(f"Executing {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

# Usage
@log_execution
def login(username):
    # login logic
    pass
```

</td>
</tr>
<tr>
<td><strong>Timing Decorator</strong></td>
<td>

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface Timed {
}

// AspectJ or Spring AOP for implementation
@Timed
public void slowOperation() {
    // operation logic
}
```

</td>
<td>

```python
import time
from functools import wraps

def timed(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} took {end - start:.2f} seconds")
        return result
    return wrapper

@timed
def slow_operation():
    time.sleep(1)
```

</td>
</tr>
<tr>
<td><strong>Parameterized Decorator</strong></td>
<td>

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface Retry {
    int maxAttempts() default 3;
    long delay() default 1000;
}

@Retry(maxAttempts = 5, delay = 2000)
public void unreliableOperation() {
    // operation logic
}
```

</td>
<td>

```python
def retry(max_attempts=3, delay=1):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(max_attempts):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == max_attempts - 1:
                        raise e
                    time.sleep(delay)
            return None
        return wrapper
    return decorator

@retry(max_attempts=5, delay=2)
def unreliable_operation():
    # operation logic
    pass
```

</td>
</tr>
<tr>
<td><strong>Class Decorator</strong></td>
<td>

```java
// Using Spring's @Component
@Component
@Scope("singleton")
public class UserService {
    // class implementation
}

// Custom annotation
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface Service {
    String value() default "";
}
```

</td>
<td>

```python
def singleton(cls):
    instances = {}
    def get_instance(*args, **kwargs):
        if cls not in instances:
            instances[cls] = cls(*args, **kwargs)
        return instances[cls]
    return get_instance

@singleton
class UserService:
    def __init__(self):
        self.users = []
```

</td>
</tr>
<tr>
<td><strong>Built-in Decorators</strong></td>
<td>

```java
// Spring Framework annotations
@RestController
@RequestMapping("/api")
public class UserController {
    
    @GetMapping("/users")
    @PreAuthorize("hasRole('USER')")
    public List<User> getUsers() {
        return userService.findAll();
    }
}
```

</td>
<td>

```python
from functools import lru_cache, wraps

# Built-in decorators
@lru_cache(maxsize=128)
def expensive_calculation(n):
    return sum(i * i for i in range(n))

# Property decorator
class Circle:
    def __init__(self, radius):
        self._radius = radius
    
    @property
    def area(self):
        return 3.14159 * self._radius ** 2
```

</td>
</tr>
<tr>
<td><strong>Multiple Decorators</strong></td>
<td>

```java
@RestController
@RequestMapping("/api")
@Validated
@Transactional
public class UserController {
    
    @GetMapping("/users/{id}")
    @Cacheable("users")
    @PreAuthorize("hasRole('ADMIN')")
    public User getUser(@PathVariable Long id) {
        return userService.findById(id);
    }
}
```

</td>
<td>

```python
@timed
@retry(max_attempts=3)
@log_execution
def complex_operation():
    # operation logic
    pass

# Equivalent to:
# complex_operation = timed(retry(log_execution(complex_operation)))
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use annotations for metadata and cross-cutting concerns
- Spring Framework provides many built-in annotations
- AspectJ enables true AOP functionality
- Annotations are processed at compile-time or runtime

### 🐍 Python
- Decorators are functions that modify other functions
- Use `@wraps` to preserve function metadata
- Decorators are applied bottom-up (closest to function first)
- Can be used on functions, methods, and classes

---

💡 **Extra Examples**

```java
// Java - Custom validation annotation
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.PARAMETER)
public @interface ValidEmail {
    String message() default "Invalid email format";
}

public void sendEmail(@ValidEmail String email, String message) {
    // email sending logic
}

// Spring Security
@PreAuthorize("hasRole('ADMIN') or #user.id == authentication.principal.id")
public void updateUser(@P("user") User user) {
    // update logic
}
```

```python
# Python - Decorator with arguments and class-based decorator
class CountCalls:
    def __init__(self, func):
        self.func = func
        self.count = 0
    
    def __call__(self, *args, **kwargs):
        self.count += 1
        print(f"Call {self.count} of {self.func.__name__}")
        return self.func(*args, **kwargs)

@CountCalls
def say_hello(name):
    return f"Hello, {name}!"

# Flask route decorator
from flask import Flask
app = Flask(__name__)

@app.route('/users/<int:user_id>')
def get_user(user_id):
    return f"User {user_id}"
```
