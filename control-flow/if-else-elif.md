# 🔀 Java vs Python — Conditional Statements Cheat Sheet

Comparison of if-else-elif statements between Java and Python, covering basic conditionals, nested statements, and ternary operators.

---

<table>
<tr>
<th>Concept</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>if</strong></td>
<td>

```java
int age = 18;
if (age >= 18) {
    System.out.println("Adult");
}
```

</td>
<td>

```python
age = 18
if age >= 18:
    print("Adult")
```

</td>
</tr>
<tr>
<td><strong>if-else</strong></td>
<td>

```java
int score = 85;
if (score >= 70) {
    System.out.println("Pass");
} else {
    System.out.println("Fail");
}
```

</td>
<td>

```python
score = 85
if score >= 70:
    print("Pass")
else:
    print("Fail")
```

</td>
</tr>
<tr>
<td><strong>if-else if-else (multiple conditions)</strong></td>
<td>

```java
int grade = 85;
if (grade >= 90) {
    System.out.println("A");
} else if (grade >= 80) {
    System.out.println("B");
} else if (grade >= 70) {
    System.out.println("C");
} else {
    System.out.println("F");
}
```

</td>
<td>

```python
grade = 85
if grade >= 90:
    print("A")
elif grade >= 80:
    print("B")
elif grade >= 70:
    print("C")
else:
    print("F")
```

</td>
</tr>
<tr>
<td><strong>Ternary operator</strong></td>
<td>

```java
int age = 20;
String status = (age >= 18) ? "Adult" : "Minor";
System.out.println(status);
```

</td>
<td>

```python
age = 20
status = "Adult" if age >= 18 else "Minor"
print(status)
```

</td>
</tr>
<tr>
<td><strong>Nested conditions</strong></td>
<td>

```java
int age = 25;
boolean hasLicense = true;
if (age >= 18) {
    if (hasLicense) {
        System.out.println("Can drive");
    } else {
        System.out.println("Need license");
    }
} else {
    System.out.println("Too young");
}
```

</td>
<td>

```python
age = 25
has_license = True
if age >= 18:
    if has_license:
        print("Can drive")
    else:
        print("Need license")
else:
    print("Too young")
```

</td>
</tr>
<tr>
<td><strong>Logical operators in conditions</strong></td>
<td>

```java
int age = 25;
boolean hasLicense = true;
if (age >= 18 && hasLicense) {
    System.out.println("Can drive");
} else if (age >= 18 || hasLicense) {
    System.out.println("Partial requirements met");
}
```

</td>
<td>

```python
age = 25
has_license = True
if age >= 18 and has_license:
    print("Can drive")
elif age >= 18 or has_license:
    print("Partial requirements met")
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Always use curly braces `{}` even for single statements
- Conditions must be boolean expressions (no truthy/falsy values)
- Use `&&` for AND, `||` for OR, `!` for NOT
- Ternary operator: `condition ? trueValue : falseValue`

### 🐍 Python
- Use indentation (4 spaces) instead of curly braces
- `elif` instead of `else if`
- Truthy/falsy values: empty strings, 0, None, empty collections are falsy
- Use `and`, `or`, `not` keywords instead of symbols
- Ternary operator: `trueValue if condition else falseValue`

---

💡 **Extra Examples**

```java
// Java - Complex condition with method calls
String name = "John";
if (name != null && !name.isEmpty() && name.length() > 2) {
    System.out.println("Valid name: " + name);
}

// Java - Switch-like with if-else chain
String day = "Monday";
if (day.equals("Monday") || day.equals("Tuesday")) {
    System.out.println("Start of week");
} else if (day.equals("Wednesday")) {
    System.out.println("Mid week");
} else if (day.equals("Thursday") || day.equals("Friday")) {
    System.out.println("End of week");
} else {
    System.out.println("Weekend");
}
```

```python
# Python - Complex condition with method calls
name = "John"
if name and len(name) > 2:
    print(f"Valid name: {name}")

# Python - Switch-like with if-elif chain
day = "Monday"
if day in ["Monday", "Tuesday"]:
    print("Start of week")
elif day == "Wednesday":
    print("Mid week")
elif day in ["Thursday", "Friday"]:
    print("End of week")
else:
    print("Weekend")

# Python - Chained comparisons
age = 25
if 18 <= age < 65:
    print("Working age")
```
