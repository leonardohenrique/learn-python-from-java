# 🖥️ Java vs Python — OS Module Cheat Sheet

Operating system interface and file system operations comparison between Java and Python

---

<table>
<tr>
<th>Operation</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Get Current Directory</strong></td>
<td>

```java
import java.nio.file.Paths;
import java.nio.file.Files;

String currentDir = System.getProperty("user.dir");
// or
String currentDir = Paths.get("").toAbsolutePath().toString();
```

</td>
<td>

```python
import os

current_dir = os.getcwd()
```

</td>
</tr>
<tr>
<td><strong>Change Directory</strong></td>
<td>

```java
import java.nio.file.Paths;

// Java doesn't have direct chdir
// Use ProcessBuilder or System.setProperty
System.setProperty("user.dir", "/new/path");
```

</td>
<td>

```python
import os

os.chdir('/new/path')
```

</td>
</tr>
<tr>
<td><strong>List Directory Contents</strong></td>
<td>

```java
import java.nio.file.Files;
import java.nio.file.Paths;
import java.util.stream.Stream;

try (Stream<Path> paths = Files.list(Paths.get("."))) {
    paths.forEach(System.out::println);
}
```

</td>
<td>

```python
import os

files = os.listdir('.')
# or
for item in os.listdir('.'):
    print(item)
```

</td>
</tr>
<tr>
<td><strong>Check if Path Exists</strong></td>
<td>

```java
import java.nio.file.Files;
import java.nio.file.Paths;

boolean exists = Files.exists(Paths.get("file.txt"));
boolean isFile = Files.isRegularFile(Paths.get("file.txt"));
boolean isDir = Files.isDirectory(Paths.get("dir"));
```

</td>
<td>

```python
import os

exists = os.path.exists('file.txt')
is_file = os.path.isfile('file.txt')
is_dir = os.path.isdir('dir')
```

</td>
</tr>
<tr>
<td><strong>Create Directory</strong></td>
<td>

```java
import java.nio.file.Files;
import java.nio.file.Paths;

Files.createDirectories(Paths.get("new/directory"));
// or
Files.createDirectory(Paths.get("single_dir"));
```

</td>
<td>

```python
import os

os.makedirs('new/directory', exist_ok=True)
# or
os.mkdir('single_dir')
```

</td>
</tr>
<tr>
<td><strong>Get Environment Variables</strong></td>
<td>

```java
String home = System.getenv("HOME");
String path = System.getenv("PATH");
// Get all env vars
Map<String, String> env = System.getenv();
```

</td>
<td>

```python
import os

home = os.environ.get('HOME')
path = os.environ.get('PATH')
# Get all env vars
env_vars = os.environ
```

</td>
</tr>
<tr>
<td><strong>Execute System Commands</strong></td>
<td>

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;

Process process = Runtime.getRuntime().exec("ls -la");
BufferedReader reader = new BufferedReader(
    new InputStreamReader(process.getInputStream())
);
String line;
while ((line = reader.readLine()) != null) {
    System.out.println(line);
}
```

</td>
<td>

```python
import os

result = os.system('ls -la')
# or
import subprocess
result = subprocess.run(['ls', '-la'], 
                       capture_output=True, text=True)
print(result.stdout)
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `java.nio.file` package for modern file operations
- `Files` class provides static methods for common operations
- `Paths` class for path manipulation
- Use try-with-resources for stream operations

### 🐍 Python
- `os.path` module for path operations (legacy)
- `pathlib` is the modern approach (Python 3.4+)
- `os.environ` is a mapping-like object
- Use `subprocess` instead of `os.system()` for better control

---

💡 **Extra Examples**

```java
// Java - Modern path operations
import java.nio.file.*;

Path path = Paths.get("data", "file.txt");
Files.write(path, "Hello World".getBytes());
String content = Files.readString(path);
Files.delete(path);
```

```python
# Python - Modern path operations
from pathlib import Path

path = Path("data") / "file.txt"
path.write_text("Hello World")
content = path.read_text()
path.unlink()
```
