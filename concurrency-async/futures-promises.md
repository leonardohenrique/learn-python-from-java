# 🔮 Java vs Python — Futures & Promises Cheat Sheet

Comparison of future and promise patterns between Java and Python

---

<table>
<tr>
<th>Concept</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Basic Future</strong></td>
<td>

```java
// Java - CompletableFuture
CompletableFuture<String> future = CompletableFuture
    .supplyAsync(() -> {
        // Simulate long-running task
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
        return "Task completed";
    });

// Get result (blocking)
String result = future.get();

// Non-blocking with callback
future.thenAccept(result -> 
    System.out.println("Result: " + result)
);
```

</td>
<td>

```python
# Python - concurrent.futures.Future
from concurrent.futures import ThreadPoolExecutor
import time

def long_running_task():
    time.sleep(2)
    return "Task completed"

with ThreadPoolExecutor() as executor:
    future = executor.submit(long_running_task)
    
    # Get result (blocking)
    result = future.result()
    
    # Non-blocking check
    if future.done():
        print(f"Result: {future.result()}")
```

</td>
</tr>
<tr>
<td><strong>Future Chaining</strong></td>
<td>

```java
// Java - CompletableFuture chaining
CompletableFuture<String> future = CompletableFuture
    .supplyAsync(() -> "Hello")
    .thenApply(s -> s + " World")
    .thenApply(String::toUpperCase)
    .thenCompose(s -> 
        CompletableFuture.supplyAsync(() -> s + "!")
    );

String result = future.get(); // "HELLO WORLD!"
```

</td>
<td>

```python
# Python - asyncio with chaining
import asyncio

async def step1():
    return "Hello"

async def step2(text):
    return text + " World"

async def step3(text):
    return text.upper()

async def step4(text):
    return text + "!"

async def main():
    result1 = await step1()
    result2 = await step2(result1)
    result3 = await step3(result2)
    result4 = await step4(result3)
    return result4

result = asyncio.run(main())  # "HELLO WORLD!"
```

</td>
</tr>
<tr>
<td><strong>Exception Handling</strong></td>
<td>

```java
// Java - CompletableFuture exception handling
CompletableFuture<String> future = CompletableFuture
    .supplyAsync(() -> {
        if (Math.random() > 0.5) {
            throw new RuntimeException("Random error");
        }
        return "Success";
    })
    .handle((result, throwable) -> {
        if (throwable != null) {
            return "Error: " + throwable.getMessage();
        }
        return result;
    })
    .exceptionally(throwable -> 
        "Fallback: " + throwable.getMessage()
    );

String result = future.get();
```

</td>
<td>

```python
# Python - Exception handling with futures
from concurrent.futures import ThreadPoolExecutor
import random

def risky_task():
    if random.random() > 0.5:
        raise Exception("Random error")
    return "Success"

with ThreadPoolExecutor() as executor:
    future = executor.submit(risky_task)
    
    try:
        result = future.result()
        print(f"Success: {result}")
    except Exception as e:
        print(f"Error: {e}")
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `CompletableFuture` for async operations and chaining
- Chain operations with `thenApply()`, `thenCompose()`, `thenAccept()`
- Handle exceptions with `handle()` or `exceptionally()`

### 🐍 Python
- Use `concurrent.futures.Future` for thread-based futures
- Use `asyncio` for async/await patterns
- Use `future.result()` to get results or handle exceptions

---

💡 **Extra Examples**

```java
// Java - Combining multiple futures
CompletableFuture<String> future1 = CompletableFuture
    .supplyAsync(() -> "Task 1");
CompletableFuture<String> future2 = CompletableFuture
    .supplyAsync(() -> "Task 2");

CompletableFuture<String> combined = future1
    .thenCombine(future2, (result1, result2) -> 
        result1 + " + " + result2
    );

String result = combined.get(); // "Task 1 + Task 2"
```

```python
# Python - Combining multiple futures
import asyncio

async def task1():
    return "Task 1"

async def task2():
    return "Task 2"

async def main():
    result1, result2 = await asyncio.gather(task1(), task2())
    return f"{result1} + {result2}"

result = asyncio.run(main())  # "Task 1 + Task 2"
```
