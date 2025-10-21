# 🔄 Java vs Python — While Loops Cheat Sheet

Comparison of while loop syntax and usage patterns between Java and Python

---

<table>
<tr>
<th>Concept</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Basic While Loop</strong></td>
<td>

```java
int count = 0;
while (count < 5) {
    System.out.println("Count: " + count);
    count++;
}
```

</td>
<td>

```python
count = 0
while count < 5:
    print(f"Count: {count}")
    count += 1
```

</td>
</tr>
<tr>
<td><strong>Infinite Loop</strong></td>
<td>

```java
while (true) {
    System.out.println("Infinite loop");
    // Need break statement to exit
    if (someCondition) {
        break;
    }
}
```

</td>
<td>

```python
while True:
    print("Infinite loop")
    # Need break statement to exit
    if some_condition:
        break
```

</td>
</tr>
<tr>
<td><strong>Do-While Equivalent</strong></td>
<td>

```java
int value;
do {
    System.out.print("Enter a number: ");
    value = scanner.nextInt();
} while (value < 0);
```

</td>
<td>

```python
# Python doesn't have do-while
# Use this pattern instead:
while True:
    value = int(input("Enter a number: "))
    if value >= 0:
        break
```

</td>
</tr>
<tr>
<td><strong>Loop with Multiple Conditions</strong></td>
<td>

```java
int i = 0, j = 10;
while (i < 5 && j > 0) {
    System.out.println("i: " + i + ", j: " + j);
    i++;
    j--;
}
```

</td>
<td>

```python
i, j = 0, 10
while i < 5 and j > 0:
    print(f"i: {i}, j: {j}")
    i += 1
    j -= 1
```

</td>
</tr>
<tr>
<td><strong>Nested While Loops</strong></td>
<td>

```java
int i = 0;
while (i < 3) {
    int j = 0;
    while (j < 3) {
        System.out.print(i + "," + j + " ");
        j++;
    }
    System.out.println();
    i++;
}
```

</td>
<td>

```python
i = 0
while i < 3:
    j = 0
    while j < 3:
        print(f"{i},{j}", end=" ")
        j += 1
    print()
    i += 1
```

</td>
</tr>
<tr>
<td><strong>Loop Control (break/continue)</strong></td>
<td>

```java
int i = 0;
while (i < 10) {
    i++;
    if (i == 3) {
        continue; // Skip iteration
    }
    if (i == 7) {
        break; // Exit loop
    }
    System.out.println(i);
}
```

</td>
<td>

```python
i = 0
while i < 10:
    i += 1
    if i == 3:
        continue  # Skip iteration
    if i == 7:
        break  # Exit loop
    print(i)
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Always ensure loop condition will eventually become false to avoid infinite loops
- Use `do-while` when you need to execute the loop body at least once
- Consider using `for` loops when you know the exact number of iterations
- Be careful with floating-point conditions in while loops due to precision issues

### 🐍 Python
- Python doesn't have `do-while` loops - use `while True` with `break` instead
- Use `else` clause with while loops for code that runs when loop completes normally
- Prefer `for` loops with `range()` when possible for better readability
- Use `enumerate()` with while loops when you need both index and value

---

💡 **Extra Examples**

```java
// Java - While with array processing
int[] numbers = {1, 2, 3, 4, 5};
int index = 0;
while (index < numbers.length) {
    if (numbers[index] % 2 == 0) {
        System.out.println("Even: " + numbers[index]);
    }
    index++;
}
```

```python
# Python - While with list processing
numbers = [1, 2, 3, 4, 5]
index = 0
while index < len(numbers):
    if numbers[index] % 2 == 0:
        print(f"Even: {numbers[index]}")
    index += 1

# Python - While with else clause
count = 0
while count < 3:
    print(f"Attempt {count + 1}")
    count += 1
else:
    print("Loop completed successfully")
```
