# 🔢 Java vs Python — Math Module Cheat Sheet

Mathematical operations and functions comparison between Java and Python

---

<table>
<tr>
<th>Operation</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Basic Math Functions</strong></td>
<td>

```java
import java.lang.Math;

double result = Math.sqrt(16);        // 4.0
double power = Math.pow(2, 3);        // 8.0
double abs = Math.abs(-5);            // 5.0
double max = Math.max(10, 20);        // 20.0
double min = Math.min(10, 20);        // 10.0
```

</td>
<td>

```python
import math

result = math.sqrt(16)        # 4.0
power = math.pow(2, 3)        # 8.0
abs_val = abs(-5)             # 5
max_val = max(10, 20)         # 20
min_val = min(10, 20)         # 10
```

</td>
</tr>
<tr>
<td><strong>Trigonometric Functions</strong></td>
<td>

```java
import java.lang.Math;

double sin = Math.sin(Math.PI / 2);   // 1.0
double cos = Math.cos(0);             // 1.0
double tan = Math.tan(Math.PI / 4);   // 1.0
double asin = Math.asin(1);           // π/2
double acos = Math.acos(1);           // 0.0
double atan = Math.atan(1);           // π/4
```

</td>
<td>

```python
import math

sin_val = math.sin(math.pi / 2)   # 1.0
cos_val = math.cos(0)             # 1.0
tan_val = math.tan(math.pi / 4)   # 1.0
asin_val = math.asin(1)           # π/2
acos_val = math.acos(1)           # 0.0
atan_val = math.atan(1)           # π/4
```

</td>
</tr>
<tr>
<td><strong>Logarithmic Functions</strong></td>
<td>

```java
import java.lang.Math;

double log = Math.log(10);          // Natural log
double log10 = Math.log10(100);     // Base 10 log
double log2 = Math.log(8) / Math.log(2); // Base 2 log
double exp = Math.exp(1);           // e^1
```

</td>
<td>

```python
import math

log_val = math.log(10)         # Natural log
log10_val = math.log10(100)    # Base 10 log
log2_val = math.log2(8)        # Base 2 log
exp_val = math.exp(1)          # e^1
```

</td>
</tr>
<tr>
<td><strong>Rounding Functions</strong></td>
<td>

```java
import java.lang.Math;

double round = Math.round(3.7);      // 4
double ceil = Math.ceil(3.2);        // 4.0
double floor = Math.floor(3.8);      // 3.0
double rint = Math.rint(3.5);        // 4.0
```

</td>
<td>

```python
import math

round_val = round(3.7)         # 4
ceil_val = math.ceil(3.2)      # 4.0
floor_val = math.floor(3.8)    # 3.0
trunc_val = math.trunc(3.8)    # 3.0
```

</td>
</tr>
<tr>
<td><strong>Random Numbers</strong></td>
<td>

```java
import java.util.Random;

Random random = new Random();
int randomInt = random.nextInt(100);     // 0-99
double randomDouble = random.nextDouble(); // 0.0-1.0
boolean randomBool = random.nextBoolean();
```

</td>
<td>

```python
import random

random_int = random.randint(0, 99)    # 0-99
random_float = random.random()        # 0.0-1.0
random_bool = random.choice([True, False])
```

</td>
</tr>
<tr>
<td><strong>Constants</strong></td>
<td>

```java
import java.lang.Math;

double pi = Math.PI;              // 3.14159...
double e = Math.E;                // 2.71828...
```

</td>
<td>

```python
import math

pi = math.pi              # 3.14159...
e = math.e                # 2.71828...
```

</td>
</tr>
<tr>
<td><strong>Advanced Functions</strong></td>
<td>

```java
import java.lang.Math;

double factorial = 1;
for (int i = 1; i <= 5; i++) {
    factorial *= i;  // 120
}
double gcd = gcd(48, 18);  // Custom method needed
double lcm = lcm(12, 18);  // Custom method needed
```

</td>
<td>

```python
import math

factorial = math.factorial(5)     # 120
gcd_val = math.gcd(48, 18)        # 6
lcm_val = math.lcm(12, 18)        # 36
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `java.lang.Math` for mathematical operations
- All methods are static
- Returns `double` for most operations
- Need custom methods for factorial, gcd, lcm

### 🐍 Python
- Use `math` module for mathematical functions
- Built-in functions like `abs()`, `max()`, `min()`
- `math.factorial()`, `math.gcd()`, `math.lcm()` available
- `random` module for random number generation

---

💡 **Extra Examples**

```java
// Java - Custom math utilities
public class MathUtils {
    public static int gcd(int a, int b) {
        return b == 0 ? a : gcd(b, a % b);
    }
    
    public static int lcm(int a, int b) {
        return Math.abs(a * b) / gcd(a, b);
    }
    
    public static long factorial(int n) {
        if (n <= 1) return 1;
        return n * factorial(n - 1);
    }
}
```

```python
# Python - Math utilities
import math

# Working with degrees and radians
degrees = 90
radians = math.radians(degrees)
back_to_degrees = math.degrees(radians)

# Statistical functions
numbers = [1, 2, 3, 4, 5]
mean = sum(numbers) / len(numbers)
```
