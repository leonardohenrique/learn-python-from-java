# 🧵 Java vs Python — Threading Cheat Sheet

Comparison of threading mechanisms between Java and Python

---

<table>
<tr>
<th>Concept</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Creating Threads</strong></td>
<td>

```java
// Java - Thread class
Thread thread = new Thread(() -> {
    System.out.println("Running in thread: " + 
        Thread.currentThread().getName());
});
thread.start();

// Java - Runnable interface
Runnable task = () -> {
    System.out.println("Task running");
};
Thread thread2 = new Thread(task);
thread2.start();
```

</td>
<td>

```python
# Python - threading module
import threading

def worker():
    print(f"Running in thread: {threading.current_thread().name}")

thread = threading.Thread(target=worker)
thread.start()
```

</td>
</tr>
<tr>
<td><strong>Thread Synchronization</strong></td>
<td>

```java
// Java - synchronized keyword
public class Counter {
    private int count = 0;
    
    public synchronized void increment() {
        count++;
    }
    
    public synchronized int getCount() {
        return count;
    }
}

// Java - ReentrantLock
private final ReentrantLock lock = new ReentrantLock();

public void safeIncrement() {
    lock.lock();
    try {
        count++;
    } finally {
        lock.unlock();
    }
}
```

</td>
<td>

```python
# Python - threading.Lock
import threading

class Counter:
    def __init__(self):
        self._count = 0
        self._lock = threading.Lock()
    
    def increment(self):
        with self._lock:
            self._count += 1
    
    def get_count(self):
        with self._lock:
            return self._count
```

</td>
</tr>
<tr>
<td><strong>Thread Communication</strong></td>
<td>

```java
// Java - wait/notify
public class ProducerConsumer {
    private final Object lock = new Object();
    private boolean ready = false;
    
    public void produce() {
        synchronized (lock) {
            // Produce data
            ready = true;
            lock.notify();
        }
    }
    
    public void consume() throws InterruptedException {
        synchronized (lock) {
            while (!ready) {
                lock.wait();
            }
            // Consume data
        }
    }
}
```

</td>
<td>

```python
# Python - threading.Condition
import threading

class ProducerConsumer:
    def __init__(self):
        self._condition = threading.Condition()
        self._ready = False
    
    def produce(self):
        with self._condition:
            # Produce data
            self._ready = True
            self._condition.notify()
    
    def consume(self):
        with self._condition:
            while not self._ready:
                self._condition.wait()
            # Consume data
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `synchronized` for simple synchronization
- Use `ReentrantLock` for more complex locking scenarios
- Use `wait()` and `notify()` for thread communication

### 🐍 Python
- Use `threading.Lock()` for basic synchronization
- Use `threading.Condition()` for complex thread communication
- Python has GIL (Global Interpreter Lock) limitations

---

💡 **Extra Examples**

```java
// Java - Thread pool
ExecutorService executor = Executors.newFixedThreadPool(4);
for (int i = 0; i < 10; i++) {
    executor.submit(() -> {
        System.out.println("Task executed");
    });
}
executor.shutdown();
```

```python
# Python - Thread pool
from concurrent.futures import ThreadPoolExecutor

with ThreadPoolExecutor(max_workers=4) as executor:
    futures = [executor.submit(lambda: print("Task executed")) 
               for _ in range(10)]
    for future in futures:
        future.result()
```
