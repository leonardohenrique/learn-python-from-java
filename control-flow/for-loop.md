# 🔄 Java vs Python — For Loops Cheat Sheet

Comparison of for loop syntax and usage patterns between Java and Python

---

<table>
<tr>
<th>Loop Type</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Basic For Loop</strong></td>
<td>

```java
// Traditional for loop
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}

// Enhanced for loop (for-each)
int[] numbers = {1, 2, 3, 4, 5};
for (int num : numbers) {
    System.out.println(num);
}
```

</td>
<td>

```python
# Range-based for loop
for i in range(5):
    print(i)

# Iterating over iterables
numbers = [1, 2, 3, 4, 5]
for num in numbers:
    print(num)
```

</td>
</tr>
<tr>
<td><strong>Range with Start/End</strong></td>
<td>

```java
// Start from 1, end at 10
for (int i = 1; i <= 10; i++) {
    System.out.println(i);
}

// Step by 2
for (int i = 0; i < 10; i += 2) {
    System.out.println(i);
}
```

</td>
<td>

```python
# Start from 1, end at 10
for i in range(1, 11):
    print(i)

# Step by 2
for i in range(0, 10, 2):
    print(i)
```

</td>
</tr>
<tr>
<td><strong>Reverse Loop</strong></td>
<td>

```java
// Countdown from 10 to 1
for (int i = 10; i >= 1; i--) {
    System.out.println(i);
}

// Reverse array iteration
int[] arr = {1, 2, 3, 4, 5};
for (int i = arr.length - 1; i >= 0; i--) {
    System.out.println(arr[i]);
}
```

</td>
<td>

```python
# Countdown from 10 to 1
for i in range(10, 0, -1):
    print(i)

# Reverse list iteration
arr = [1, 2, 3, 4, 5]
for item in reversed(arr):
    print(item)

# Or with indices
for i in range(len(arr) - 1, -1, -1):
    print(arr[i])
```

</td>
</tr>
<tr>
<td><strong>Loop with Index</strong></td>
<td>

```java
// Using traditional for loop
String[] fruits = {"apple", "banana", "orange"};
for (int i = 0; i < fruits.length; i++) {
    System.out.println(i + ": " + fruits[i]);
}

// Using enhanced for loop with counter
int index = 0;
for (String fruit : fruits) {
    System.out.println(index + ": " + fruit);
    index++;
}
```

</td>
<td>

```python
# Using enumerate
fruits = ["apple", "banana", "orange"]
for i, fruit in enumerate(fruits):
    print(f"{i}: {fruit}")

# With custom start index
for i, fruit in enumerate(fruits, 1):
    print(f"{i}: {fruit}")
```

</td>
</tr>
<tr>
<td><strong>Nested Loops</strong></td>
<td>

```java
// Nested for loops
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        System.out.println("(" + i + ", " + j + ")");
    }
}

// Enhanced nested loops
String[][] matrix = {{"a", "b"}, {"c", "d"}};
for (String[] row : matrix) {
    for (String cell : row) {
        System.out.print(cell + " ");
    }
    System.out.println();
}
```

</td>
<td>

```python
# Nested for loops
for i in range(3):
    for j in range(3):
        print(f"({i}, {j})")

# Nested iteration over collections
matrix = [["a", "b"], ["c", "d"]]
for row in matrix:
    for cell in row:
        print(cell, end=" ")
    print()
```

</td>
</tr>
<tr>
<td><strong>Loop Control</strong></td>
<td>

```java
// Break and continue
for (int i = 0; i < 10; i++) {
    if (i == 3) {
        continue; // Skip iteration
    }
    if (i == 7) {
        break; // Exit loop
    }
    System.out.println(i);
}

// Labeled break
outer: for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (i == 1 && j == 1) {
            break outer; // Break outer loop
        }
        System.out.println("(" + i + ", " + j + ")");
    }
}
```

</td>
<td>

```python
# Break and continue
for i in range(10):
    if i == 3:
        continue  # Skip iteration
    if i == 7:
        break  # Exit loop
    print(i)

# Using else clause
for i in range(5):
    if i == 10:  # This will never be true
        break
else:
    print("Loop completed without break")
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use enhanced for-each loops when you don't need the index
- Traditional for loops give you more control over iteration
- Use labeled breaks for nested loop control
- Consider using `IntStream.range()` for functional-style loops

### 🐍 Python
- `range()` is lazy and memory-efficient for large ranges
- `enumerate()` is the Pythonic way to get index and value
- Use `else` clause with loops for clean completion handling
- List comprehensions can often replace simple for loops

---

💡 **Extra Examples**

```java
// Java - Functional style with streams
IntStream.range(0, 5)
    .filter(i -> i % 2 == 0)
    .forEach(System.out::println);

// Java - Multiple variables in for loop
for (int i = 0, j = 10; i < j; i++, j--) {
    System.out.println("i: " + i + ", j: " + j);
}
```

```python
# Python - List comprehension
squares = [x**2 for x in range(5)]
print(squares)  # [0, 1, 4, 9, 16]

# Python - Multiple variables with zip
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
for name, age in zip(names, ages):
    print(f"{name} is {age} years old")

# Python - Dictionary iteration
person = {"name": "John", "age": 30, "city": "New York"}
for key, value in person.items():
    print(f"{key}: {value}")
```
