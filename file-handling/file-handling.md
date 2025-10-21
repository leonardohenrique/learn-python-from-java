# 📁 Java vs Python — File Handling Cheat Sheet

Basic file operations comparison between Java and Python for reading, writing, and managing files.

---

<table>
<tr>
<th>Operation</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Reading Text File</strong></td>
<td>

```java
// Using try-with-resources
try (BufferedReader reader = Files.newBufferedReader(Paths.get("file.txt"))) {
    String line;
    while ((line = reader.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

</td>
<td>

```python
# Simple file reading
with open('file.txt', 'r') as file:
    for line in file:
        print(line.strip())
```

</td>
</tr>
<tr>
<td><strong>Writing Text File</strong></td>
<td>

```java
// Using try-with-resources
try (BufferedWriter writer = Files.newBufferedWriter(Paths.get("output.txt"))) {
    writer.write("Hello, World!");
    writer.newLine();
    writer.write("Second line");
} catch (IOException e) {
    e.printStackTrace();
}
```

</td>
<td>

```python
# Simple file writing
with open('output.txt', 'w') as file:
    file.write("Hello, World!\n")
    file.write("Second line")
```

</td>
</tr>
<tr>
<td><strong>Appending to File</strong></td>
<td>

```java
// Append mode
try (BufferedWriter writer = Files.newBufferedWriter(
        Paths.get("log.txt"), 
        StandardOpenOption.APPEND,
        StandardOpenOption.CREATE)) {
    writer.write("New log entry");
    writer.newLine();
} catch (IOException e) {
    e.printStackTrace();
}
```

</td>
<td>

```python
# Append mode
with open('log.txt', 'a') as file:
    file.write("New log entry\n")
```

</td>
</tr>
<tr>
<td><strong>Reading Binary File</strong></td>
<td>

```java
// Reading binary data
try {
    byte[] data = Files.readAllBytes(Paths.get("image.jpg"));
    // Process binary data
} catch (IOException e) {
    e.printStackTrace();
}
```

</td>
<td>

```python
# Reading binary data
with open('image.jpg', 'rb') as file:
    data = file.read()
    # Process binary data
```

</td>
</tr>
<tr>
<td><strong>File Existence Check</strong></td>
<td>

```java
// Check if file exists
Path path = Paths.get("file.txt");
if (Files.exists(path)) {
    System.out.println("File exists");
} else {
    System.out.println("File not found");
}
```

</td>
<td>

```python
# Check if file exists
import os
if os.path.exists('file.txt'):
    print("File exists")
else:
    print("File not found")
```

</td>
</tr>
<tr>
<td><strong>Directory Operations</strong></td>
<td>

```java
// Create directory
try {
    Files.createDirectories(Paths.get("new/folder/path"));
} catch (IOException e) {
    e.printStackTrace();
}

// List directory contents
try (Stream<Path> paths = Files.list(Paths.get("."))) {
    paths.forEach(System.out::println);
} catch (IOException e) {
    e.printStackTrace();
}
```

</td>
<td>

```python
# Create directory
import os
os.makedirs('new/folder/path', exist_ok=True)

# List directory contents
for item in os.listdir('.'):
    print(item)
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Always use try-with-resources for automatic resource management
- Use `Files` class for modern file operations (Java 7+)
- `BufferedReader`/`BufferedWriter` for efficient text I/O
- Handle `IOException` properly in file operations

### 🐍 Python
- Use `with` statement for automatic file closing
- Specify encoding explicitly: `open('file.txt', 'r', encoding='utf-8')`
- Use `pathlib.Path` for modern path operations (Python 3.4+)
- `'r'`, `'w'`, `'a'` modes for read, write, append

---

💡 **Extra Examples**

```java
// Java - Reading all lines at once
try {
    List<String> lines = Files.readAllLines(Paths.get("file.txt"));
    lines.forEach(System.out::println);
} catch (IOException e) {
    e.printStackTrace();
}
```

```python
# Python - Reading all lines at once
with open('file.txt', 'r') as file:
    lines = file.readlines()
    for line in lines:
        print(line.strip())
```
