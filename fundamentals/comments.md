# 🧠 Java vs Python — Comments Cheat Sheet

A quick comparison showing how to write comments in **Java** and **Python**.

---

<table>
<tr>
<th>Comment Type</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Single-line comment</strong></td>
<td>

```java
// This is a single-line comment
int x = 10; // inline comment
```

</td>
<td>

```python
# This is a single-line comment
x = 10  # inline comment
```

</td>
</tr>
<tr>
<td><strong>Multi-line comment</strong></td>
<td>

```java
/*
  This is a
  multi-line comment
*/
int y = 20;
```

</td>
<td>

```python
"""
This is a multi-line comment (non-assigned string literal)
"""
y = 20
```

</td>
</tr>
<tr>
<td><strong>Inline comment</strong></td>
<td>

```java
int total = 0; // initialize counter
for (int i = 0; i < 10; i++) {
    total += i; // sum values
}
```

</td>
<td>

```python
total = 0  # initialize counter
for i in range(10):
    total += i  # sum values
```

</td>
</tr>
<tr>
<td><strong>Docstrings / Documentation comments</strong></td>
<td>

```java
/**
 * Adds two numbers.
 * @param a first number
 * @param b second number
 * @return sum of the numbers
 */
public int add(int a, int b) {
    return a + b;
}
```

</td>
<td>

```python
def add(a, b):
    """
    Adds two numbers.

    Args:
        a: first number
        b: second number

    Returns:
        Sum of the numbers
    """
    return a + b
```

</td>
</tr>
<tr>
<td><strong>Temporary / Debugging comment</strong></td>
<td>

```java
// TODO: implement validation
// FIXME: handle exceptions
```

</td>
<td>

```python
# TODO: implement validation
# FIXME: handle exceptions
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Uses `//` and `/* ... */`.
- Documentation comments (`/** ... */`) are used by **Javadoc**.

### 🐍 Python
- Uses `#` for simple comments.
- Uses `\"\"\" ... \"\"\"` (or `''' ... '''`) as **docstrings**, which are interpreted by `help()` and IDEs.
- Lines starting with `#` **are not executed**.

---

💡 **Extra tip:**  
Docstrings in Python are real objects and can be accessed at runtime:
```python
print(min.__doc__)
help(add)
```