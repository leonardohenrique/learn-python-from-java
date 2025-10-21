# 📋 Java vs Python — Lists Cheat Sheet

Comparison between lists in Java and Python, including creation, manipulation and common operations.

---

<table>
<tr>
<th>Operation</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>List Creation</strong></td>
<td>

```java
// ArrayList (most common)
List<String> list = new ArrayList<>();
List<Integer> numbers = new ArrayList<>(Arrays.asList(1, 2, 3));

// LinkedList
List<String> linkedList = new LinkedList<>();

// Immutable list (Java 9+)
List<String> immutable = List.of("a", "b", "c");
```

</td>
<td>

```python
# Empty list
list = []
list = list()

# List with elements
numbers = [1, 2, 3]
fruits = ["apple", "banana", "orange"]

# Immutable list (tuple)
immutable = ("a", "b", "c")
```

</td>
</tr>
<tr>
<td><strong>Add Elements</strong></td>
<td>

```java
List<String> list = new ArrayList<>();

// Add at the end
list.add("element");

// Add at specific position
list.add(1, "middle");

// Add multiple elements
list.addAll(Arrays.asList("a", "b", "c"));
```

</td>
<td>

```python
list = []

# Add at the end
list.append("element")

# Add at specific position
list.insert(1, "middle")

# Add multiple elements
list.extend(["a", "b", "c"])
```

</td>
</tr>
<tr>
<td><strong>Access Elements</strong></td>
<td>

```java
List<String> list = Arrays.asList("a", "b", "c");

// By index
String first = list.get(0);

// Check if contains
boolean contains = list.contains("b");

// Element index
int index = list.indexOf("b");
```

</td>
<td>

```python
list = ["a", "b", "c"]

# By index
first = list[0]

# Check if contains
contains = "b" in list

# Element index
index = list.index("b")
```

</td>
</tr>
<tr>
<td><strong>Remove Elements</strong></td>
<td>

```java
List<String> list = new ArrayList<>(Arrays.asList("a", "b", "c"));

// By index
list.remove(0);

// By value
list.remove("b");

// Remove all
list.clear();
```

</td>
<td>

```python
list = ["a", "b", "c"]

# By index
del list[0]
# or
list.pop(0)

# By value
list.remove("b")

# Remove all
list.clear()
```

</td>
</tr>
<tr>
<td><strong>Iteration</strong></td>
<td>

```java
List<String> list = Arrays.asList("a", "b", "c");

// For-each
for (String item : list) {
    System.out.println(item);
}

// Stream API
list.stream().forEach(System.out::println);

// With index
for (int i = 0; i < list.size(); i++) {
    System.out.println(i + ": " + list.get(i));
}
```

</td>
<td>

```python
list = ["a", "b", "c"]

# Simple for
for item in list:
    print(item)

# With enumerate (index)
for i, item in enumerate(list):
    print(f"{i}: {item}")

# List comprehension
[print(item) for item in list]
```

</td>
</tr>
<tr>
<td><strong>Filtering and Transformation</strong></td>
<td>

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

// Filter (Stream API)
List<Integer> even = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());

// Transform
List<String> strings = numbers.stream()
    .map(String::valueOf)
    .collect(Collectors.toList());
```

</td>
<td>

```python
numbers = [1, 2, 3, 4, 5]

# Filter
even = [n for n in numbers if n % 2 == 0]
# or
even = list(filter(lambda n: n % 2 == 0, numbers))

# Transform
strings = [str(n) for n in numbers]
# or
strings = list(map(str, numbers))
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `ArrayList` for frequent random access
- Use `LinkedList` for frequent insertions/removals in the middle
- `List.of()` creates immutable lists (Java 9+)
- Stream API is powerful for functional operations

### 🐍 Python
- Lists are dynamic and heterogeneous by default
- List comprehensions are more pythonic than loops
- Use `enumerate()` to get index and value
- `del` removes by index, `remove()` by value

---

💡 **Extra Examples**

```java
// Java - Advanced operations
List<String> names = Arrays.asList("Ana", "Bruno", "Carlos");

// Sorting
names.sort(String::compareTo);

// Binary search (list must be sorted)
int position = Collections.binarySearch(names, "Bruno");

// Reverse
Collections.reverse(names);

// Sublist
List<String> sub = names.subList(0, 2);
```

```python
# Python - Advanced operations
names = ["Ana", "Bruno", "Carlos"]

# Sorting
names.sort()  # in-place
# or
sorted_names = sorted(names)  # new list

# Reverse
names.reverse()  # in-place
# or
reversed_names = names[::-1]  # new list

# Sublist
sub = names[0:2]

# List union
combined = list1 + list2
```