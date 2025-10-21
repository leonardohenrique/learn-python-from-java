# ⚙️ Java vs Python — Sys Module Cheat Sheet

System-specific parameters and functions comparison between Java and Python

---

<table>
<tr>
<th>Operation</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Command Line Arguments</strong></td>
<td>

```java
public class Main {
    public static void main(String[] args) {
        for (String arg : args) {
            System.out.println(arg);
        }
        // Access specific argument
        if (args.length > 0) {
            String firstArg = args[0];
        }
    }
}
```

</td>
<td>

```python
import sys

for arg in sys.argv:
    print(arg)
# Access specific argument
if len(sys.argv) > 1:
    first_arg = sys.argv[1]
```

</td>
</tr>
<tr>
<td><strong>Exit Program</strong></td>
<td>

```java
// Exit with status code
System.exit(0);  // Success
System.exit(1);  // Error
```

</td>
<td>

```python
import sys

# Exit with status code
sys.exit(0)  # Success
sys.exit(1)  # Error
```

</td>
</tr>
<tr>
<td><strong>Standard Input/Output</strong></td>
<td>

```java
import java.util.Scanner;

Scanner scanner = new Scanner(System.in);
String input = scanner.nextLine();
System.out.println("Output: " + input);
System.err.println("Error message");
```

</td>
<td>

```python
import sys

input_text = sys.stdin.readline()
print("Output:", input_text)
print("Error message", file=sys.stderr)
```

</td>
</tr>
<tr>
<td><strong>Python Version Info</strong></td>
<td>

```java
// Java version
String version = System.getProperty("java.version");
String vendor = System.getProperty("java.vendor");
System.out.println("Java version: " + version);
```

</td>
<td>

```python
import sys

print(f"Python version: {sys.version}")
print(f"Version info: {sys.version_info}")
print(f"Executable: {sys.executable}")
```

</td>
</tr>
<tr>
<td><strong>Platform Information</strong></td>
<td>

```java
String osName = System.getProperty("os.name");
String osVersion = System.getProperty("os.version");
String osArch = System.getProperty("os.arch");
System.out.println("OS: " + osName);
```

</td>
<td>

```python
import sys

print(f"Platform: {sys.platform}")
print(f"Byte order: {sys.byteorder}")
print(f"Max size: {sys.maxsize}")
```

</td>
</tr>
<tr>
<td><strong>Module Path</strong></td>
<td>

```java
// Classpath
String classpath = System.getProperty("java.class.path");
System.out.println("Classpath: " + classpath);
```

</td>
<td>

```python
import sys

print("Python path:")
for path in sys.path:
    print(f"  {path}")
```

</td>
</tr>
<tr>
<td><strong>Memory Usage</strong></td>
<td>

```java
Runtime runtime = Runtime.getRuntime();
long totalMemory = runtime.totalMemory();
long freeMemory = runtime.freeMemory();
long usedMemory = totalMemory - freeMemory;
System.out.println("Used memory: " + usedMemory);
```

</td>
<td>

```python
import sys

# Get size of an object
size = sys.getsizeof("Hello World")
print(f"Size: {size} bytes")

# Get reference count
ref_count = sys.getrefcount("Hello World")
print(f"Reference count: {ref_count}")
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `System.getProperty()` for system properties
- `main(String[] args)` receives command line arguments
- `System.out`, `System.err` for standard streams
- `Runtime.getRuntime()` for memory and system info

### 🐍 Python
- `sys.argv[0]` is the script name
- `sys.path` contains module search paths
- `sys.getsizeof()` for object memory usage
- `sys.getrefcount()` for reference counting

---

💡 **Extra Examples**

```java
// Java - System properties
import java.util.Properties;

Properties props = System.getProperties();
props.list(System.out);

// Memory management
Runtime.getRuntime().gc(); // Suggest garbage collection
```

```python
# Python - System information
import sys

# Check if running in interactive mode
if hasattr(sys, 'ps1'):
    print("Interactive mode")

# Get recursion limit
print(f"Recursion limit: {sys.getrecursionlimit()}")
sys.setrecursionlimit(2000)
```
