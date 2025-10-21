# 📝 Java vs Python — String Manipulation Cheat Sheet

Comparison of string operations, methods, and best practices between Java and Python

---

<table>
<tr>
<th>Operation</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>String Declaration</strong></td>
<td>

```java
String str = "Hello World";
String str2 = new String("Hello World");
```

</td>
<td>

```python
str = "Hello World"
str2 = 'Hello World'
```

</td>
</tr>
<tr>
<td><strong>String Concatenation</strong></td>
<td>

```java
String result = str1 + str2;
String result2 = str1.concat(str2);
String result3 = String.join(" ", str1, str2);
```

</td>
<td>

```python
result = str1 + str2
result2 = " ".join([str1, str2])
result3 = f"{str1} {str2}"
```

</td>
</tr>
<tr>
<td><strong>String Length</strong></td>
<td>

```java
int length = str.length();
```

</td>
<td>

```python
length = len(str)
```

</td>
</tr>
<tr>
<td><strong>Substring/Slicing</strong></td>
<td>

```java
String sub = str.substring(0, 5);
String sub2 = str.substring(6);
```

</td>
<td>

```python
sub = str[0:5]
sub2 = str[6:]
```

</td>
</tr>
<tr>
<td><strong>Case Conversion</strong></td>
<td>

```java
String upper = str.toUpperCase();
String lower = str.toLowerCase();
```

</td>
<td>

```python
upper = str.upper()
lower = str.lower()
```

</td>
</tr>
<tr>
<td><strong>String Comparison</strong></td>
<td>

```java
boolean equal = str1.equals(str2);
boolean equalIgnoreCase = str1.equalsIgnoreCase(str2);
int compare = str1.compareTo(str2);
```

</td>
<td>

```python
equal = str1 == str2
equal_ignore_case = str1.lower() == str2.lower()
compare = str1 < str2  # Returns boolean
```

</td>
</tr>
<tr>
<td><strong>String Search</strong></td>
<td>

```java
boolean contains = str.contains("World");
int index = str.indexOf("World");
boolean startsWith = str.startsWith("Hello");
boolean endsWith = str.endsWith("World");
```

</td>
<td>

```python
contains = "World" in str
index = str.find("World")
starts_with = str.startswith("Hello")
ends_with = str.endswith("World")
```

</td>
</tr>
<tr>
<td><strong>String Replacement</strong></td>
<td>

```java
String replaced = str.replace("World", "Python");
String replacedAll = str.replaceAll("l", "L");
```

</td>
<td>

```python
replaced = str.replace("World", "Python")
replaced_all = str.replace("l", "L")
```

</td>
</tr>
<tr>
<td><strong>String Splitting</strong></td>
<td>

```java
String[] parts = str.split(" ");
String[] parts2 = str.split(" ", 2);
```

</td>
<td>

```python
parts = str.split(" ")
parts2 = str.split(" ", 1)
```

</td>
</tr>
<tr>
<td><strong>String Trimming</strong></td>
<td>

```java
String trimmed = str.trim();
String stripped = str.strip();
```

</td>
<td>

```python
trimmed = str.strip()
left_stripped = str.lstrip()
right_stripped = str.rstrip()
```

</td>
</tr>
<tr>
<td><strong>String Formatting</strong></td>
<td>

```java
String formatted = String.format("Hello %s, you are %d years old", name, age);
String formatted2 = String.format("Value: %.2f", value);
```

</td>
<td>

```python
formatted = "Hello {}, you are {} years old".format(name, age)
formatted2 = f"Hello {name}, you are {age} years old"
formatted3 = "Value: {:.2f}".format(value)
```

</td>
</tr>
<tr>
<td><strong>String Building</strong></td>
<td>

```java
StringBuilder sb = new StringBuilder();
sb.append("Hello");
sb.append(" ");
sb.append("World");
String result = sb.toString();
```

</td>
<td>

```python
# Strings are immutable, but efficient concatenation
result = "".join(["Hello", " ", "World"])
# Or use f-strings for simple cases
result = f"Hello World"
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `StringBuilder` for multiple string concatenations to avoid performance issues
- Always use `.equals()` for string comparison, not `==`
- `String` is immutable in Java - operations return new strings
- Use `String.join()` for joining multiple strings with a delimiter

### 🐍 Python
- Strings are immutable and optimized for performance
- Use f-strings (f"...") for modern string formatting
- `in` operator is very efficient for substring checking
- String slicing is very powerful and intuitive

---

💡 **Extra Examples**

```java
// Java - String manipulation
String text = "  Hello World  ";
String processed = text.trim()
                      .toLowerCase()
                      .replace("world", "Python")
                      .toUpperCase();
System.out.println(processed); // "HELLO PYTHON"

// String building
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 5; i++) {
    sb.append("Item ").append(i).append(" ");
}
String result = sb.toString().trim();
```

```python
# Python - String manipulation
text = "  Hello World  "
processed = text.strip().lower().replace("world", "Python").upper()
print(processed)  # "HELLO PYTHON"

# String building
result = " ".join(f"Item {i}" for i in range(5))
# Or using f-string
result = " ".join([f"Item {i}" for i in range(5)])
```
