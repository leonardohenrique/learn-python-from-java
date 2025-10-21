# 📦 Java vs Python — Built-in Modules Cheat Sheet

Comparison of built-in modules and standard library functionality between Java and Python

---

<table>
<tr>
<th>Category</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>File Operations</strong></td>
<td>

```java
import java.io.File;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

// File operations
File file = new File("example.txt");
boolean exists = file.exists();
long size = file.length();

// Reading file
try (FileReader reader = new FileReader("input.txt")) {
    int character;
    while ((character = reader.read()) != -1) {
        System.out.print((char) character);
    }
}

// Writing file
try (FileWriter writer = new FileWriter("output.txt")) {
    writer.write("Hello, World!");
}
```

</td>
<td>

```python
import os
import shutil

# File operations
file_path = "example.txt"
exists = os.path.exists(file_path)
size = os.path.getsize(file_path)

# Reading file
with open("input.txt", "r") as file:
    content = file.read()
    print(content)

# Writing file
with open("output.txt", "w") as file:
    file.write("Hello, World!")

# File operations
shutil.copy("source.txt", "destination.txt")
os.remove("file_to_delete.txt")
```

</td>
</tr>
<tr>
<td><strong>Date and Time</strong></td>
<td>

```java
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.LocalTime;
import java.time.format.DateTimeFormatter;

// Current date and time
LocalDate today = LocalDate.now();
LocalTime now = LocalTime.now();
LocalDateTime dateTime = LocalDateTime.now();

// Formatting
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
String formatted = dateTime.format(formatter);

// Parsing
LocalDate parsed = LocalDate.parse("2023-12-25");
```

</td>
<td>

```python
from datetime import datetime, date, time
import time as time_module

# Current date and time
today = date.today()
now = datetime.now()
current_time = time()

# Formatting
formatted = now.strftime("%Y-%m-%d %H:%M:%S")

# Parsing
parsed = datetime.strptime("2023-12-25", "%Y-%m-%d")

# Unix timestamp
timestamp = time_module.time()
```

</td>
</tr>
<tr>
<td><strong>JSON Processing</strong></td>
<td>

```java
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.JsonNode;

// JSON serialization
ObjectMapper mapper = new ObjectMapper();
Map<String, Object> data = new HashMap<>();
data.put("name", "John");
data.put("age", 30);

String json = mapper.writeValueAsString(data);

// JSON deserialization
String jsonString = "{\"name\":\"John\",\"age\":30}";
JsonNode node = mapper.readTree(jsonString);
String name = node.get("name").asText();
int age = node.get("age").asInt();
```

</td>
<td>

```python
import json

# JSON serialization
data = {"name": "John", "age": 30}
json_string = json.dumps(data)

# JSON deserialization
json_string = '{"name": "John", "age": 30}'
data = json.loads(json_string)
name = data["name"]
age = data["age"]

# File operations
with open("data.json", "w") as file:
    json.dump(data, file)

with open("data.json", "r") as file:
    data = json.load(file)
```

</td>
</tr>
<tr>
<td><strong>Regular Expressions</strong></td>
<td>

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

// Pattern matching
Pattern pattern = Pattern.compile("\\d{3}-\\d{3}-\\d{4}");
Matcher matcher = pattern.matcher("123-456-7890");
boolean matches = matcher.matches();

// Finding matches
Pattern emailPattern = Pattern.compile("\\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\\.[A-Z|a-z]{2,}\\b");
Matcher emailMatcher = emailPattern.matcher("Contact: john@example.com");
while (emailMatcher.find()) {
    System.out.println("Found email: " + emailMatcher.group());
}

// Replacement
String text = "Hello 123 World 456";
String replaced = text.replaceAll("\\d+", "NUMBER");
```

</td>
<td>

```python
import re

# Pattern matching
pattern = r"\d{3}-\d{3}-\d{4}"
matches = re.match(pattern, "123-456-7890")

# Finding matches
email_pattern = r"\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b"
text = "Contact: john@example.com"
emails = re.findall(email_pattern, text)

# Replacement
text = "Hello 123 World 456"
replaced = re.sub(r"\d+", "NUMBER", text)

# Compiling patterns for reuse
compiled_pattern = re.compile(r"\d+")
matches = compiled_pattern.findall(text)
```

</td>
</tr>
<tr>
<td><strong>Collections</strong></td>
<td>

```java
import java.util.*;
import java.util.stream.Collectors;

// Lists
List<String> list = new ArrayList<>();
list.add("apple");
list.add("banana");
list.add("cherry");

// Sets
Set<String> set = new HashSet<>();
set.add("apple");
set.add("banana");

// Maps
Map<String, Integer> map = new HashMap<>();
map.put("apple", 5);
map.put("banana", 3);

// Stream operations
List<String> filtered = list.stream()
    .filter(s -> s.startsWith("a"))
    .collect(Collectors.toList());
```

</td>
<td>

```python
from collections import defaultdict, Counter, deque
from typing import List, Dict, Set

# Lists
my_list = ["apple", "banana", "cherry"]
my_list.append("date")

# Sets
my_set = {"apple", "banana", "cherry"}
my_set.add("date")

# Dictionaries
my_dict = {"apple": 5, "banana": 3, "cherry": 8}

# Advanced collections
counter = Counter(["apple", "banana", "apple", "cherry"])
default_dict = defaultdict(list)
deque_obj = deque([1, 2, 3])

# List comprehensions
filtered = [item for item in my_list if item.startswith("a")]
```

</td>
</tr>
<tr>
<td><strong>Mathematical Operations</strong></td>
<td>

```java
import java.lang.Math;
import java.math.BigDecimal;
import java.math.RoundingMode;

// Basic math
double result = Math.sqrt(16);
double power = Math.pow(2, 3);
double abs = Math.abs(-5.5);

// Trigonometric functions
double sin = Math.sin(Math.PI / 2);
double cos = Math.cos(0);

// Random numbers
Random random = new Random();
int randomInt = random.nextInt(100);
double randomDouble = random.nextDouble();

// BigDecimal for precision
BigDecimal price = new BigDecimal("19.99");
BigDecimal tax = price.multiply(new BigDecimal("0.08"));
BigDecimal total = price.add(tax).setScale(2, RoundingMode.HALF_UP);
```

</td>
<td>

```python
import math
import random
from decimal import Decimal

# Basic math
result = math.sqrt(16)
power = math.pow(2, 3)
abs_value = abs(-5.5)

# Trigonometric functions
sin_value = math.sin(math.pi / 2)
cos_value = math.cos(0)

# Random numbers
random_int = random.randint(1, 100)
random_float = random.random()

# Decimal for precision
price = Decimal("19.99")
tax = price * Decimal("0.08")
total = price + tax
```

</td>
</tr>
<tr>
<td><strong>System Information</strong></td>
<td>

```java
import java.lang.management.ManagementFactory;
import java.lang.management.MemoryMXBean;
import java.lang.management.RuntimeMXBean;

// System properties
String osName = System.getProperty("os.name");
String javaVersion = System.getProperty("java.version");
String userHome = System.getProperty("user.home");

// Memory information
MemoryMXBean memoryBean = ManagementFactory.getMemoryMXBean();
long heapUsed = memoryBean.getHeapMemoryUsage().getUsed();
long heapMax = memoryBean.getHeapMemoryUsage().getMax();

// Runtime information
RuntimeMXBean runtimeBean = ManagementFactory.getRuntimeMXBean();
long uptime = runtimeBean.getUptime();
```

</td>
<td>

```python
import sys
import os
import platform
import psutil

# System information
os_name = platform.system()
python_version = sys.version
user_home = os.path.expanduser("~")

# Memory information
memory = psutil.virtual_memory()
heap_used = memory.used
heap_total = memory.total

# Process information
process = psutil.Process()
cpu_percent = process.cpu_percent()
memory_info = process.memory_info()
```

</td>
</tr>
<tr>
<td><strong>Network Operations</strong></td>
<td>

```java
import java.net.URL;
import java.net.HttpURLConnection;
import java.io.BufferedReader;
import java.io.InputStreamReader;

// HTTP requests
URL url = new URL("https://api.example.com/data");
HttpURLConnection connection = (HttpURLConnection) url.openConnection();
connection.setRequestMethod("GET");

int responseCode = connection.getResponseCode();
BufferedReader reader = new BufferedReader(
    new InputStreamReader(connection.getInputStream())
);
String line;
StringBuilder response = new StringBuilder();
while ((line = reader.readLine()) != null) {
    response.append(line);
}
reader.close();
```

</td>
<td>

```python
import urllib.request
import urllib.parse
import requests

# Using urllib
url = "https://api.example.com/data"
with urllib.request.urlopen(url) as response:
    data = response.read().decode('utf-8')

# Using requests (third-party)
response = requests.get("https://api.example.com/data")
data = response.json()
status_code = response.status_code

# POST request
data = {"key": "value"}
response = requests.post("https://api.example.com/data", json=data)
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `java.util.*` for collections and utilities
- `java.time.*` for modern date/time operations
- `java.lang.Math` for mathematical functions
- Third-party libraries like Jackson for JSON processing

### 🐍 Python
- Built-in modules are always available
- Use `import` to access module functionality
- Many operations are more concise than Java
- Rich standard library covers most common needs

---

💡 **Extra Examples**

```java
// Java - Working with multiple built-in modules
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.*;
import java.util.stream.Collectors;

public class BuiltInExample {
    public static void main(String[] args) {
        // Date formatting
        LocalDateTime now = LocalDateTime.now();
        String formatted = now.format(DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss"));
        
        // Collection operations
        List<String> words = Arrays.asList("apple", "banana", "cherry", "date");
        List<String> filtered = words.stream()
            .filter(w -> w.length() > 5)
            .collect(Collectors.toList());
        
        // Random numbers
        Random random = new Random();
        int randomNumber = random.nextInt(100);
        
        System.out.println("Formatted date: " + formatted);
        System.out.println("Filtered words: " + filtered);
        System.out.println("Random number: " + randomNumber);
    }
}
```

```python
# Python - Working with multiple built-in modules
from datetime import datetime
import random
import json
import os

def built_in_example():
    # Date formatting
    now = datetime.now()
    formatted = now.strftime("%Y-%m-%d %H:%M:%S")
    
    # Collection operations
    words = ["apple", "banana", "cherry", "date"]
    filtered = [word for word in words if len(word) > 5]
    
    # Random numbers
    random_number = random.randint(1, 100)
    
    # JSON operations
    data = {"timestamp": formatted, "words": filtered}
    json_string = json.dumps(data, indent=2)
    
    # File operations
    with open("output.json", "w") as file:
        file.write(json_string)
    
    print(f"Formatted date: {formatted}")
    print(f"Filtered words: {filtered}")
    print(f"Random number: {random_number}")
    print(f"File size: {os.path.getsize('output.json')} bytes")

if __name__ == "__main__":
    built_in_example()
```
