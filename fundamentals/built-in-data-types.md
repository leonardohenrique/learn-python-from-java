# 🔢 Java vs Python — Built-in Data Types Cheat Sheet

Comparison of built-in data types between Java and Python, showing how primitive and reference types work in both languages.

---

<table>
<tr>
<th>Data Type</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Integer</strong></td>
<td>

```java
int number = 42;
long bigNumber = 123456789L;
byte smallNumber = 127;
short mediumNumber = 32000;
```

</td>
<td>

```python
number = 42
big_number = 123456789
# Python automatically handles int size
```

</td>
</tr>
<tr>
<td><strong>Floating Point</strong></td>
<td>

```java
float decimal = 3.14f;
double precise = 3.14159265359;
```

</td>
<td>

```python
decimal = 3.14
precise = 3.14159265359
# Python uses double precision by default
```

</td>
</tr>
<tr>
<td><strong>Boolean</strong></td>
<td>

```java
boolean isTrue = true;
boolean isFalse = false;
```

</td>
<td>

```python
is_true = True
is_false = False
# Capital T and F in Python
```

</td>
</tr>
<tr>
<td><strong>Character</strong></td>
<td>

```java
char letter = 'A';
char unicode = '\u0041';
```

</td>
<td>

```python
letter = 'A'
# Python doesn't have char type
# Strings are sequences of characters
```

</td>
</tr>
<tr>
<td><strong>String</strong></td>
<td>

```java
String text = "Hello World";
String multiline = """
    This is a
    multiline string
    """;
```

</td>
<td>

```python
text = "Hello World"
multiline = """
    This is a
    multiline string
    """
```

</td>
</tr>
<tr>
<td><strong>Array/List</strong></td>
<td>

```java
int[] numbers = {1, 2, 3, 4, 5};
String[] names = {"Alice", "Bob", "Charlie"};
List<String> list = new ArrayList<>();
```

</td>
<td>

```python
numbers = [1, 2, 3, 4, 5]
names = ["Alice", "Bob", "Charlie"]
# Lists are dynamic and heterogeneous
```

</td>
</tr>
<tr>
<td><strong>Map/Dictionary</strong></td>
<td>

```java
Map<String, Integer> map = new HashMap<>();
map.put("age", 25);
map.put("score", 95);
```

</td>
<td>

```python
map = {"age": 25, "score": 95}
# Dictionary literals are more concise
```

</td>
</tr>
<tr>
<td><strong>Set</strong></td>
<td>

```java
Set<String> set = new HashSet<>();
set.add("apple");
set.add("banana");
```

</td>
<td>

```python
set = {"apple", "banana"}
# Set literals with curly braces
```

</td>
</tr>
<tr>
<td><strong>Tuple</strong></td>
<td>

```java
// No direct tuple equivalent
// Use custom classes or records
record Point(int x, int y) {}
Point point = new Point(10, 20);
```

</td>
<td>

```python
point = (10, 20)
coordinates = (1, 2, 3)
# Tuples are immutable sequences
```

</td>
</tr>
<tr>
<td><strong>None/Null</strong></td>
<td>

```java
String value = null;
Integer number = null;
```

</td>
<td>

```python
value = None
number = None
# Python uses None instead of null
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- All primitive types have fixed sizes (int = 32 bits, long = 64 bits)
- Must declare variable types explicitly
- Arrays have fixed size, use Collections for dynamic arrays
- char is 16-bit Unicode character
- String is immutable reference type

### 🐍 Python
- Dynamic typing - no need to declare types
- All integers are arbitrary precision (no overflow)
- Lists can hold different types of objects
- Strings are immutable sequences
- None is the single null-like value

---

💡 **Extra Examples**

```java
// Java - Type checking and casting
int number = 42;
double decimal = (double) number;  // Explicit casting
String text = String.valueOf(number);  // Convert to string

// Check types at runtime
if (obj instanceof String) {
    String str = (String) obj;
}
```

```python
# Python - Dynamic typing and type hints
number = 42
decimal = float(number)  # Type conversion
text = str(number)  # Convert to string

# Type hints (optional)
def greet(name: str) -> str:
    return f"Hello, {name}!"

# Check types at runtime
if isinstance(obj, str):
    print("It's a string!")
```
