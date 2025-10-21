# ⚙️ Java vs Python — Operators Cheat Sheet

A quick side-by-side comparison of the most common **operators** in Java and Python.

---

<table>
<tr>
<th>Category</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Arithmetic</strong></td>
<td>

```java
int a = 5, b = 2;
System.out.println(a + b);  // 7
System.out.println(a - b);  // 3
System.out.println(a * b);  // 10
System.out.println(a / b);  // 2 (integer division)
System.out.println(a % b);  // 1
// No built-in exponentiation
double result = Math.pow(a, 2);  // 25.0
```

</td>
<td>

```python
a, b = 5, 2
print(a + b)  # 7
print(a - b)  # 3
print(a * b)  # 10
print(a / b)  # 2.5 (float division)
print(a % b)  # 1
print(a ** 2)  # 25 (exponentiation)
```

</td>
</tr>
<tr>
<td><strong>Assignment</strong></td>
<td>

```java
int x = 10;
x += 5;   // x = 15
x -= 3;   // x = 12
x *= 2;   // x = 24
x /= 4;   // x = 6
x %= 5;   // x = 1
```

</td>
<td>

```python
x = 10
x += 5    # x = 15
x -= 3    # x = 12
x *= 2    # x = 24
x /= 4    # x = 6.0
x %= 5    # x = 1.0
x **= 2   # x = 1.0 (exponentiation)
```

</td>
</tr>
<tr>
<td><strong>Comparison (Relational)</strong></td>
<td>

```java
int a = 5, b = 3;
boolean eq = (a == b);    // false
boolean ne = (a != b);    // true
boolean gt = (a > b);     // true
boolean lt = (a < b);     // false
boolean ge = (a >= b);    // true
boolean le = (a <= b);    // false
```

</td>
<td>

```python
a, b = 5, 3
eq = (a == b)    # False
ne = (a != b)    # True
gt = (a > b)     # True
lt = (a < b)     # False
ge = (a >= b)    # True
le = (a <= b)    # False
```

</td>
</tr>
<tr>
<td><strong>Logical</strong></td>
<td>

```java
boolean a = true, b = false;
boolean andResult = a && b;    // false
boolean orResult = a || b;     // true
boolean notResult = !a;        // false
```

</td>
<td>

```python
a, b = True, False
and_result = a and b    # False
or_result = a or b      # True
not_result = not a      # False
```

</td>
</tr>
<tr>
<td><strong>Bitwise</strong></td>
<td>

```java
int a = 5, b = 3;  // 101, 011
int and = a & b;   // 001 (1)
int or = a | b;    // 111 (7)
int xor = a ^ b;   // 110 (6)
int not = ~a;      // -6
int left = a << 1; // 1010 (10)
int right = a >> 1; // 10 (2)
```

</td>
<td>

```python
a, b = 5, 3  # 101, 011
and_op = a & b   # 1
or_op = a | b    # 7
xor = a ^ b      # 6
not_op = ~a      # -6
left = a << 1    # 10
right = a >> 1   # 2
```

</td>
</tr>
<tr>
<td><strong>Ternary</strong></td>
<td>

```java
int a = 5, b = 3;
int max = (a > b) ? a : b;  // 5
String result = (a > 0) ? "positive" : "negative";
```

</td>
<td>

```python
a, b = 5, 3
max_val = a if a > b else b  # 5
result = "positive" if a > 0 else "negative"
```

</td>
</tr>
<tr>
<td><strong>Increment / Decrement</strong></td>
<td>

```java
int x = 5;
x++;        // x = 6 (post-increment)
++x;        // x = 7 (pre-increment)
x--;        // x = 6 (post-decrement)
--x;        // x = 5 (pre-decrement)
```

</td>
<td>

```python
x = 5
x += 1      # x = 6 (no ++ operator)
x -= 1      # x = 5 (no -- operator)
# Alternative: x = x + 1
```

</td>
</tr>
<tr>
<td><strong>Membership</strong></td>
<td>

```java
// No built-in membership operator
String str = "hello";
boolean contains = str.contains("e");  // true
// For collections, use contains() method
List<String> list = Arrays.asList("a", "b", "c");
boolean inList = list.contains("a");   // true
```

</td>
<td>

```python
# Built-in membership operators
text = "hello"
contains = "e" in text        # True
not_contains = "x" not in text  # True

# Works with lists, tuples, sets, dicts
my_list = ["a", "b", "c"]
in_list = "a" in my_list      # True
```

</td>
</tr>
<tr>
<td><strong>Identity</strong></td>
<td>

```java
// No direct identity operator
String a = "hello";
String b = "hello";
boolean sameRef = (a == b);  // true (string interning)
// For objects, use == for reference comparison
Object obj1 = new Object();
Object obj2 = new Object();
boolean sameObject = (obj1 == obj2);  // false
```

</td>
<td>

```python
# Identity operators compare object identity
a = "hello"
b = "hello"
same_ref = a is b        # True (string interning)
not_same = a is not b    # False

# For different objects
obj1 = object()
obj2 = object()
same_object = obj1 is obj2  # False
```

</td>
</tr>
<tr>
<td><strong>Type Check</strong></td>
<td>

```java
Object obj = "hello";
if (obj instanceof String) {
    String str = (String) obj;
    System.out.println("It's a string: " + str);
}
```

</td>
<td>

```python
obj = "hello"
if isinstance(obj, str):
    print(f"It's a string: {obj}")

# Also works with multiple types
if isinstance(obj, (str, int)):
    print("It's a string or int")
```

</td>
</tr>
<tr>
<td><strong>Null / None Check</strong></td>
<td>

```java
String name = null;
if (name != null) {
    System.out.println("Name: " + name);
} else {
    System.out.println("Name is null");
}
```

</td>
<td>

```python
name = None
if name is not None:
    print(f"Name: {name}")
else:
    print("Name is None")
```

</td>
</tr>
<tr>
<td><strong>String Concatenation</strong></td>
<td>

```java
String name = "World";
String greeting = "Hello " + name;  // "Hello World"
// String.format() for complex formatting
String formatted = String.format("Hello %s, you are %d years old", name, 25);
```

</td>
<td>

```python
name = "World"
greeting = "Hello " + name  # "Hello World"
# f-strings (preferred)
formatted = f"Hello {name}, you are {25} years old"
# .format() method
formatted2 = "Hello {}, you are {} years old".format(name, 25)
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Uses **C-style** operators (`&&`, `||`, `++`, `--`).
- Strictly typed — operations must match variable types.
- No built-in exponentiation (`Math.pow()` required).

### 🐍 Python
- Uses **plain words** for logic (`and`, `or`, `not`).
- `**` for exponentiation.
- `is` compares **object identity**, not equality.
- Operators are **overloadable** in custom classes (`__add__`, `__eq__`, etc.).

---

💡 **Extra Examples**

```java
// Java
int a = 5, b = 2;
System.out.println(a + b);  // 7
System.out.println(a / b);  // 2 (integer division)
System.out.println(a % b);  // 1
```

```python
# Python
a, b = 5, 2
print(a + b)  # 7
print(a / b)  # 2.5 (float division)
print(a % b)  # 1
```