# ⚡ Java vs Python — Async/Await Cheat Sheet

Comparison of asynchronous programming patterns between Java and Python

---

<table>
<tr>
<th>Concept</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Basic Async Function</strong></td>
<td>

```java
// Java CompletableFuture
public CompletableFuture<String> fetchData() {
    return CompletableFuture.supplyAsync(() -> {
        // Simulate async work
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
        return "Data from Java";
    });
}
```

</td>
<td>

```python
# Python async/await
import asyncio

async def fetch_data():
    # Simulate async work
    await asyncio.sleep(1)
    return "Data from Python"
```

</td>
</tr>
<tr>
<td><strong>Calling Async Function</strong></td>
<td>

```java
// Java - blocking call
CompletableFuture<String> future = fetchData();
String result = future.get(); // blocks

// Java - non-blocking with callback
fetchData().thenAccept(result -> {
    System.out.println("Result: " + result);
});
```

</td>
<td>

```python
# Python - blocking call
result = asyncio.run(fetch_data())

# Python - non-blocking in async context
async def main():
    result = await fetch_data()
    print(f"Result: {result}")

asyncio.run(main())
```

</td>
</tr>
<tr>
<td><strong>Multiple Async Calls</strong></td>
<td>

```java
// Java - parallel execution
CompletableFuture<String> future1 = fetchData();
CompletableFuture<String> future2 = fetchData();

CompletableFuture<Void> allFutures = 
    CompletableFuture.allOf(future1, future2);

allFutures.thenRun(() -> {
    String result1 = future1.join();
    String result2 = future2.join();
    System.out.println("Both completed");
});
```

</td>
<td>

```python
# Python - parallel execution
async def main():
    # Run concurrently
    result1, result2 = await asyncio.gather(
        fetch_data(),
        fetch_data()
    )
    print("Both completed")

asyncio.run(main())
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `CompletableFuture` for async operations
- Chain operations with `thenApply()`, `thenAccept()`, `thenRun()`
- Handle exceptions with `handle()` or `exceptionally()`

### 🐍 Python
- Use `async def` to define async functions
- Use `await` to call async functions
- Use `asyncio.gather()` for parallel execution

---

💡 **Extra Examples**

```java
// Java - Exception handling
CompletableFuture<String> future = fetchData()
    .handle((result, throwable) -> {
        if (throwable != null) {
            return "Error occurred: " + throwable.getMessage();
        }
        return result;
    });
```

```python
# Python - Exception handling
async def safe_fetch():
    try:
        result = await fetch_data()
        return result
    except Exception as e:
        return f"Error occurred: {e}"

result = asyncio.run(safe_fetch())
```
