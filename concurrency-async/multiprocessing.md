# 🔄 Java vs Python — Multiprocessing Cheat Sheet

Comparison of multiprocessing approaches between Java and Python

---

<table>
<tr>
<th>Concept</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Creating Processes</strong></td>
<td>

```java
// Java - ProcessBuilder
ProcessBuilder pb = new ProcessBuilder("java", "-version");
Process process = pb.start();

// Java - Fork/Join Framework
public class Task extends RecursiveTask<Integer> {
    private final int[] array;
    private final int start, end;
    
    public Task(int[] array, int start, int end) {
        this.array = array;
        this.start = start;
        this.end = end;
    }
    
    @Override
    protected Integer compute() {
        if (end - start <= 10) {
            // Base case
            return Arrays.stream(array, start, end).sum();
        } else {
            // Split task
            int mid = (start + end) / 2;
            Task left = new Task(array, start, mid);
            Task right = new Task(array, mid, end);
            left.fork();
            return right.compute() + left.join();
        }
    }
}
```

</td>
<td>

```python
# Python - multiprocessing module
import multiprocessing

def worker(name):
    print(f"Worker {name} running")

if __name__ == "__main__":
    process = multiprocessing.Process(target=worker, args=("Process1",))
    process.start()
    process.join()
```

</td>
</tr>
<tr>
<td><strong>Process Communication</strong></td>
<td>

```java
// Java - Shared memory with synchronized collections
import java.util.concurrent.ConcurrentHashMap;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.ArrayBlockingQueue;

// Shared map
ConcurrentHashMap<String, String> sharedMap = 
    new ConcurrentHashMap<>();

// Message passing with queues
BlockingQueue<String> queue = new ArrayBlockingQueue<>(10);

// Producer
queue.put("Message from producer");

// Consumer
String message = queue.take();
```

</td>
<td>

```python
# Python - multiprocessing.Queue
import multiprocessing

def producer(queue):
    queue.put("Message from producer")

def consumer(queue):
    message = queue.get()
    print(f"Received: {message}")

if __name__ == "__main__":
    queue = multiprocessing.Queue()
    
    p1 = multiprocessing.Process(target=producer, args=(queue,))
    p2 = multiprocessing.Process(target=consumer, args=(queue,))
    
    p1.start()
    p2.start()
    p1.join()
    p2.join()
```

</td>
</tr>
<tr>
<td><strong>Process Pool</strong></td>
<td>

```java
// Java - ExecutorService with multiple threads
ExecutorService executor = Executors.newFixedThreadPool(
    Runtime.getRuntime().availableProcessors()
);

List<Future<Integer>> futures = new ArrayList<>();
for (int i = 0; i < 10; i++) {
    final int taskId = i;
    Future<Integer> future = executor.submit(() -> {
        // CPU-intensive task
        return taskId * taskId;
    });
    futures.add(future);
}

// Collect results
for (Future<Integer> future : futures) {
    System.out.println("Result: " + future.get());
}

executor.shutdown();
```

</td>
<td>

```python
# Python - multiprocessing.Pool
import multiprocessing

def cpu_intensive_task(n):
    return n * n

if __name__ == "__main__":
    with multiprocessing.Pool() as pool:
        results = pool.map(cpu_intensive_task, range(10))
        print(f"Results: {results}")
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `ProcessBuilder` for external process execution
- Use `ForkJoinPool` for CPU-intensive parallel tasks
- Use `ConcurrentHashMap` and `BlockingQueue` for inter-process communication

### 🐍 Python
- Use `multiprocessing.Process` for separate processes
- Use `multiprocessing.Pool` for parallel execution
- Use `multiprocessing.Queue` for process communication

---

💡 **Extra Examples**

```java
// Java - Parallel streams
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
int sum = numbers.parallelStream()
    .mapToInt(n -> n * n)
    .sum();
System.out.println("Sum: " + sum);
```

```python
# Python - multiprocessing.Manager for shared state
import multiprocessing

def worker(shared_list, index):
    shared_list[index] = index * index

if __name__ == "__main__":
    with multiprocessing.Manager() as manager:
        shared_list = manager.list([0] * 5)
        processes = []
        
        for i in range(5):
            p = multiprocessing.Process(target=worker, args=(shared_list, i))
            processes.append(p)
            p.start()
        
        for p in processes:
            p.join()
        
        print(f"Shared list: {list(shared_list)}")
```
