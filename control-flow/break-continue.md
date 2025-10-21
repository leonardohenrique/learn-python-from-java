# 🔄 Java vs Python — Break & Continue Cheat Sheet

Control flow statements for loop interruption and iteration control

---

<table>
<tr>
<th>Control Flow</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Break Statement</strong></td>
<td>

```java
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break; // Exit loop immediately
    }
    System.out.println(i);
}
// Output: 0 1 2 3 4
```

</td>
<td>

```python
for i in range(10):
    if i == 5:
        break  # Exit loop immediately
    print(i)
# Output: 0 1 2 3 4
```

</td>
</tr>
<tr>
<td><strong>Continue Statement</strong></td>
<td>

```java
for (int i = 0; i < 5; i++) {
    if (i == 2) {
        continue; // Skip current iteration
    }
    System.out.println(i);
}
// Output: 0 1 3 4
```

</td>
<td>

```python
for i in range(5):
    if i == 2:
        continue  # Skip current iteration
    print(i)
# Output: 0 1 3 4
```

</td>
</tr>
<tr>
<td><strong>Nested Loops - Break</strong></td>
<td>

```java
outer: for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (i == 1 && j == 1) {
            break outer; // Break outer loop
        }
        System.out.println(i + "," + j);
    }
}
// Output: 0,0 0,1 0,2 1,0
```

</td>
<td>

```python
for i in range(3):
    for j in range(3):
        if i == 1 and j == 1:
            break  # Only breaks inner loop
        print(f"{i},{j}")
    else:
        continue  # Only executes if inner loop completes
    break  # Break outer loop
# Output: 0,0 0,1 0,2 1,0
```

</td>
</tr>
<tr>
<td><strong>While Loop with Break</strong></td>
<td>

```java
int count = 0;
while (true) {
    count++;
    if (count > 3) {
        break;
    }
    System.out.println("Count: " + count);
}
// Output: Count: 1 Count: 2 Count: 3
```

</td>
<td>

```python
count = 0
while True:
    count += 1
    if count > 3:
        break
    print(f"Count: {count}")
# Output: Count: 1 Count: 2 Count: 3
```

</td>
</tr>
<tr>
<td><strong>Continue in While Loop</strong></td>
<td>

```java
int i = 0;
while (i < 5) {
    i++;
    if (i == 3) {
        continue;
    }
    System.out.println(i);
}
// Output: 1 2 4 5
```

</td>
<td>

```python
i = 0
while i < 5:
    i += 1
    if i == 3:
        continue
    print(i)
# Output: 1 2 4 5
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use labeled breaks (`break label;`) to exit nested loops
- `break` and `continue` work in all loop types (for, while, do-while)
- Labels must be declared before the loop they reference

### 🐍 Python
- No labeled breaks - use flags or exception handling for complex cases
- `for-else` construct: `else` executes only if loop completes normally
- `break` and `continue` work in for and while loops

---

💡 **Extra Examples**

```java
// Java - Multiple breaks with labels
search: for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (i * j == 4) {
            System.out.println("Found at: " + i + "," + j);
            break search;
        }
    }
}
```

```python
# Python - Using for-else for search
found = False
for i in range(3):
    for j in range(3):
        if i * j == 4:
            print(f"Found at: {i},{j}")
            found = True
            break
    if found:
        break
else:
    print("Not found")
```
