# 📦 Java vs Python — Tuples Cheat Sheet

Comparison between tuples in Java and Python, including creation, manipulation and common operations.

---

<table>
<tr>
<th>Operation</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Tuple Creation</strong></td>
<td>

```java
// Using Pair (Apache Commons Lang)
Pair<String, Integer> pair = Pair.of("key", 42);

// Using Triple (Apache Commons Lang)
Triple<String, Integer, Boolean> triple = Triple.of("name", 25, true);

// Custom record (Java 14+)
record Person(String name, int age) {}
Person person = new Person("John", 30);

// Using Map.Entry
Map.Entry<String, Integer> entry = Map.entry("key", 42);
```

</td>
<td>

```python
# Empty tuple
empty = ()
empty = tuple()

# Tuple with elements
coordinates = (10, 20)
person = ("John", 25, True)

# Single element tuple (note the comma)
single = (42,)

# Tuple unpacking
name, age, active = person
```

</td>
</tr>
<tr>
<td><strong>Access Elements</strong></td>
<td>

```java
Pair<String, Integer> pair = Pair.of("key", 42);

// Get left and right
String left = pair.getLeft();
Integer right = pair.getRight();

// Custom record access
Person person = new Person("John", 30);
String name = person.name();
int age = person.age();
```

</td>
<td>

```python
person = ("John", 25, True)

# By index
name = person[0]
age = person[1]
active = person[2]

# Negative indexing
last = person[-1]

# Slicing
first_two = person[:2]
```

</td>
</tr>
<tr>
<td><strong>Immutability</strong></td>
<td>

```java
// Records are immutable by default
record Point(int x, int y) {}

Point p = new Point(10, 20);
// p.x = 30; // Compilation error!

// Create new instance
Point newPoint = new Point(30, 40);

// Apache Commons Pair is also immutable
Pair<String, Integer> pair = Pair.of("key", 42);
// pair.setLeft("new"); // No such method!
```

</td>
<td>

```python
coordinates = (10, 20)

# Tuples are immutable
# coordinates[0] = 30  # TypeError!

# Create new tuple
new_coordinates = (30, 40)

# Concatenation creates new tuple
combined = coordinates + new_coordinates
```

</td>
</tr>
<tr>
<td><strong>Iteration</strong></td>
<td>

```java
Pair<String, Integer> pair = Pair.of("key", 42);

// Iterate over values
for (Object value : Arrays.asList(pair.getLeft(), pair.getRight())) {
    System.out.println(value);
}

// Record iteration (Java 14+)
Person person = new Person("John", 30);
// Records don't implement Iterable directly
// Need to use reflection or manual iteration
```

</td>
<td>

```python
person = ("John", 25, True)

# Simple iteration
for item in person:
    print(item)

# With enumerate
for i, item in enumerate(person):
    print(f"{i}: {item}")

# Tuple unpacking in loops
for name, age in [("Alice", 25), ("Bob", 30)]:
    print(f"{name} is {age}")
```

</td>
</tr>
<tr>
<td><strong>Tuple Unpacking</strong></td>
<td>

```java
// Manual unpacking
Pair<String, Integer> pair = Pair.of("key", 42);
String key = pair.getLeft();
Integer value = pair.getRight();

// Record destructuring (Java 14+)
Person person = new Person("John", 30);
String name = person.name();
int age = person.age();

// Pattern matching (Java 17+ preview)
if (person instanceof Person p) {
    // p is automatically available
    System.out.println(p.name());
}
```

</td>
<td>

```python
person = ("John", 25, True)

# Unpacking
name, age, active = person

# Partial unpacking
name, *rest = person  # name="John", rest=[25, True]

# Ignoring values
name, _, active = person  # ignore age

# Multiple assignment
x, y = 10, 20
```

</td>
</tr>
<tr>
<td><strong>Common Operations</strong></td>
<td>

```java
Pair<String, Integer> pair1 = Pair.of("a", 1);
Pair<String, Integer> pair2 = Pair.of("b", 2);

// Equality
boolean equal = pair1.equals(pair2);

// Hash code
int hash = pair1.hashCode();

// String representation
String str = pair1.toString();

// Sorting (if implementing Comparable)
List<Pair<String, Integer>> pairs = Arrays.asList(pair1, pair2);
pairs.sort(Comparator.comparing(Pair::getLeft));
```

</td>
<td>

```python
tuple1 = ("a", 1)
tuple2 = ("b", 2)

# Equality
equal = tuple1 == tuple2

# Hash (if all elements are hashable)
hash_val = hash(tuple1)

# String representation
str_repr = str(tuple1)

# Sorting
tuples = [tuple1, tuple2]
sorted_tuples = sorted(tuples)

# Count occurrences
count = tuple1.count("a")

# Find index
index = tuple1.index(1)
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `Pair`/`Triple` from Apache Commons Lang for simple tuples
- Use `record` (Java 14+) for structured data with multiple fields
- Records provide automatic `equals()`, `hashCode()`, and `toString()`
- Consider `Map.Entry` for key-value pairs

### 🐍 Python
- Tuples are immutable and hashable (if all elements are hashable)
- Use parentheses `()` or just commas for tuple creation
- Single element tuples need a trailing comma: `(42,)`
- Tuple unpacking is very powerful for multiple assignments

---

💡 **Extra Examples**

```java
// Java - Advanced tuple usage
record Point3D(int x, int y, int z) {
    public double distance() {
        return Math.sqrt(x*x + y*y + z*z);
    }
}

Point3D point = new Point3D(1, 2, 3);
System.out.println(point.distance());

// Using Pair for function returns
public static Pair<String, Integer> parseNameAge(String input) {
    String[] parts = input.split(":");
    return Pair.of(parts[0], Integer.parseInt(parts[1]));
}

Pair<String, Integer> result = parseNameAge("John:25");
```

```python
# Python - Advanced tuple usage
def get_coordinates():
    return 10, 20, 30  # Returns tuple

x, y, z = get_coordinates()

# Named tuples (more readable)
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y', 'z'])
p = Point(1, 2, 3)
print(p.x, p.y, p.z)

# Tuple as dictionary key (because it's hashable)
locations = {
    (0, 0): "origin",
    (1, 1): "corner"
}

# Multiple return values
def get_stats(numbers):
    return min(numbers), max(numbers), sum(numbers)

min_val, max_val, total = get_stats([1, 2, 3, 4, 5])
```
