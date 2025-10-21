# ⚙️ Java vs Python — Operators Cheat Sheet

A quick side-by-side comparison of the most common **operators** in Java and Python.

---

| Category | Java 🟦 | Python 🐍 | Example |
|-----------|---------|-----------|----------|
| **Arithmetic** | `+`, `-`, `*`, `/`, `%` | `+`, `-`, `*`, `/`, `%`, `**` | `a + b`, `a ** 2` (Python exponentiation) |
| **Assignment** | `=`, `+=`, `-=`, `*=`, `/=`, `%=` | `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `**=` | `x += 5` |
| **Comparison (Relational)** | `==`, `!=`, `>`, `<`, `>=`, `<=` | `==`, `!=`, `>`, `<`, `>=`, `<=` | `a >= b` |
| **Logical** | `&&`, `||`, `!` | `and`, `or`, `not` | `a and b`, `not a` |
| **Bitwise** | `&`, `|`, `^`, `~`, `<<`, `>>` | `&`, `|`, `^`, `~`, `<<`, `>>` | `x << 1` |
| **Ternary** | `condition ? trueValue : falseValue` | `trueValue if condition else falseValue` | `max = a if a > b else b` |
| **Increment / Decrement** | `++`, `--` | *Not available (use `x += 1` or `x -= 1`)* | `x += 1` |
| **Membership** | *N/A* | `in`, `not in` | `"a" in "abc"` |
| **Identity** | *N/A* | `is`, `is not` | `a is b` |
| **Type Check** | `instanceof` | `isinstance(obj, Class)` | `if (obj instanceof String)` / `isinstance(obj, str)` |
| **Null / None Check** | `if (obj != null)` | `if obj is not None` | — |
| **String Concatenation** | `"Hello " + name` | `"Hello " + name` or `f"Hello {name}"` | — |
| **Exponentiation** | `Math.pow(a, b)` | `a ** b` | `2 ** 3 → 8` |
| **Modulo (Remainder)** | `a % b` | `a % b` | — |

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