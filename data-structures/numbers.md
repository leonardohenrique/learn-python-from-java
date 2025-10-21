# 🔢 Java vs Python — Numbers Cheat Sheet  
### Integers & Floating-point Numbers

A side-by-side comparison of how **numeric types** work in Java and Python.

---

<table>
<tr>
<th>Category</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Integer Type</strong></td>
<td>

```java
byte b = 127;
short s = 32000;
int i = 42;
long l = 123456789L;
```

</td>
<td>

```python
# int has unlimited precision
a = 42
big_number = 2**1000  # No overflow
```

</td>
</tr>
<tr>
<td><strong>Floating-point Type</strong></td>
<td>

```java
float f = 3.14f;
double d = 3.14159;
```

</td>
<td>

```python
# float is double precision by default
x = 3.14
y = 2.5e-10
```

</td>
</tr>
<tr>
<td><strong>Precision</strong></td>
<td>

```java
// Fixed-size types
int maxInt = Integer.MAX_VALUE;  // 32-bit
double maxDouble = Double.MAX_VALUE;  // 64-bit
```

</td>
<td>

```python
# Arbitrary precision
import sys
print(sys.maxsize)  # Platform dependent
# int grows automatically
```

</td>
</tr>
<tr>
<td><strong>Integer Range</strong></td>
<td>

```java
// int: -2³¹ to 2³¹-1
int min = Integer.MIN_VALUE;
int max = Integer.MAX_VALUE;

// long: -2⁶³ to 2⁶³-1
long longMin = Long.MIN_VALUE;
```

</td>
<td>

```python
# No explicit limit (limited by memory)
import sys
print(sys.maxsize)  # Platform dependent
# Can create arbitrarily large integers
```

</td>
</tr>
<tr>
<td><strong>Floating-point Range</strong></td>
<td>

```java
// float: ~±3.4e38
float floatMax = Float.MAX_VALUE;

// double: ~±1.7e308
double doubleMax = Double.MAX_VALUE;
```

</td>
<td>

```python
# IEEE 754 double precision
import sys
print(sys.float_info.max)  # ~1.8e308
```

</td>
</tr>
<tr>
<td><strong>Numeric Literals</strong></td>
<td>

```java
int decimal = 42;
int binary = 0b1010;    // 10
int octal = 010;        // 8
int hex = 0xFF;         // 255
```

</td>
<td>

```python
decimal = 42
binary = 0b1010    # 10
octal = 0o10       # 8
hex = 0xFF         # 255
```

</td>
</tr>
<tr>
<td><strong>Underscores in numbers</strong></td>
<td>

```java
int num = 1_000_000;
long bigNum = 123_456_789L;
```

</td>
<td>

```python
num = 1_000_000
big_num = 123_456_789
```

</td>
</tr>
<tr>
<td><strong>Type Casting</strong></td>
<td>

```java
int a = 5;
double b = (double) a;  // Explicit casting
float c = (float) 3.14;
```

</td>
<td>

```python
a = 5
b = float(a)  # Explicit conversion
c = int(3.14)  # Truncates to 3
```

</td>
</tr>
<tr>
<td><strong>Division <code>/</code></strong></td>
<td>

```java
int a = 5, b = 2;
System.out.println(a / b);     // 2 (integer division)
System.out.println(a / 2.0);   // 2.5 (float division)
```

</td>
<td>

```python
a, b = 5, 2
print(a / b)  # 2.5 (always float division)
```

</td>
</tr>
<tr>
<td><strong>Integer Division</strong></td>
<td>

```java
int a = 5, b = 2;
int result = a / b;           // 2
int result2 = (int)(a / 2.0); // 2
```

</td>
<td>

```python
a, b = 5, 2
result = a // b  # 2 (integer division)
```

</td>
</tr>
<tr>
<td><strong>Modulo</strong></td>
<td>

```java
int a = 5, b = 2;
int remainder = a % b;  // 1
```

</td>
<td>

```python
a, b = 5, 2
remainder = a % b  # 1
```

</td>
</tr>
<tr>
<td><strong>Exponentiation</strong></td>
<td>

```java
double result = Math.pow(2, 3);  // 8.0
double result2 = Math.pow(5, 2); // 25.0
```

</td>
<td>

```python
result = 2 ** 3  # 8
result2 = 5 ** 2  # 25
```

</td>
</tr>
<tr>
<td><strong>Rounding</strong></td>
<td>

```java
double num = 3.7;
long rounded = Math.round(num);     // 4
double floor = Math.floor(num);     // 3.0
double ceil = Math.ceil(num);       // 4.0
```

</td>
<td>

```python
import math
num = 3.7
rounded = round(num)        # 4
floor = math.floor(num)     # 3.0
ceil = math.ceil(num)       # 4.0
```

</td>
</tr>
<tr>
<td><strong>NaN and Infinity</strong></td>
<td>

```java
double nan = Double.NaN;
double posInf = Double.POSITIVE_INFINITY;
double negInf = Double.NEGATIVE_INFINITY;
```

</td>
<td>

```python
nan = float('nan')
pos_inf = float('inf')
neg_inf = -float('inf')
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Strongly typed: you must define the number type (`int`, `double`, etc.).
- Integer overflow **wraps around** (e.g., exceeding max `int`).
- Use `BigInteger` or `BigDecimal` for arbitrary precision.

### 🐍 Python
- `int` grows automatically (no overflow).
- `/` always returns float, use `//` for integer division.
- Use the `decimal` or `fractions` modules for precise arithmetic.

---

💡 **Extra Examples**

```java
// Java
int a = 5;
double b = 2.0;
System.out.println(a / b); // 2.5
System.out.println(a / 2); // 2 (integer division)
System.out.println(Math.pow(a, 3)); // 125.0
```

```python
# Python
a, b = 5, 2.0
print(a / b)  # 2.5
print(a // 2)  # 2
print(a ** 3)  # 125
```

---

**Author:** Leonardo Henrique  
**File:** `numbers-java-vs-python.md`
