# 🎯 Java vs Python — Sets Cheat Sheet

Comparison between sets in Java and Python, including creation, manipulation and common operations.

---

<table>
<tr>
<th>Operation</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Set Creation</strong></td>
<td>

```java
// HashSet (most common)
Set<String> set = new HashSet<>();
Set<Integer> numbers = new HashSet<>(Arrays.asList(1, 2, 3));

// LinkedHashSet (maintains insertion order)
Set<String> linkedSet = new LinkedHashSet<>();

// TreeSet (sorted)
Set<String> treeSet = new TreeSet<>();

// Immutable set (Java 9+)
Set<String> immutable = Set.of("a", "b", "c");
```

</td>
<td>

```python
# Empty set
set = set()
# Note: {} creates a dict, not a set!

# Set with elements
numbers = {1, 2, 3}
fruits = {"apple", "banana", "orange"}

# From list
numbers = set([1, 2, 3])

# Immutable set (frozenset)
immutable = frozenset(["a", "b", "c"])
```

</td>
</tr>
<tr>
<td><strong>Add Elements</strong></td>
<td>

```java
Set<String> set = new HashSet<>();

// Add single element
set.add("element");

// Add multiple elements
set.addAll(Arrays.asList("a", "b", "c"));

// Add from another set
Set<String> other = new HashSet<>();
set.addAll(other);
```

</td>
<td>

```python
set = set()

# Add single element
set.add("element")

# Add multiple elements
set.update(["a", "b", "c"])

# Add from another set
other = {"x", "y", "z"}
set.update(other)
```

</td>
</tr>
<tr>
<td><strong>Remove Elements</strong></td>
<td>

```java
Set<String> set = new HashSet<>(Arrays.asList("a", "b", "c"));

// Remove by value
boolean removed = set.remove("b");

// Remove all elements
set.clear();

// Remove all elements from another set
Set<String> toRemove = new HashSet<>(Arrays.asList("a", "b"));
set.removeAll(toRemove);
```

</td>
<td>

```python
set = {"a", "b", "c"}

# Remove by value
set.remove("b")  # Raises KeyError if not found
set.discard("b")  # No error if not found

# Remove and return arbitrary element
element = set.pop()

# Remove all elements
set.clear()

# Remove elements from another set
to_remove = {"a", "b"}
set -= to_remove
```

</td>
</tr>
<tr>
<td><strong>Check Membership</strong></td>
<td>

```java
Set<String> set = new HashSet<>(Arrays.asList("a", "b", "c"));

// Check if contains
boolean contains = set.contains("b");

// Check if empty
boolean empty = set.isEmpty();

// Get size
int size = set.size();
```

</td>
<td>

```python
set = {"a", "b", "c"}

# Check if contains
contains = "b" in set

# Check if empty
empty = len(set) == 0

# Get size
size = len(set)
```

</td>
</tr>
<tr>
<td><strong>Set Operations</strong></td>
<td>

```java
Set<String> set1 = new HashSet<>(Arrays.asList("a", "b", "c"));
Set<String> set2 = new HashSet<>(Arrays.asList("b", "c", "d"));

// Union
Set<String> union = new HashSet<>(set1);
union.addAll(set2);

// Intersection
Set<String> intersection = new HashSet<>(set1);
intersection.retainAll(set2);

// Difference
Set<String> difference = new HashSet<>(set1);
difference.removeAll(set2);

// Symmetric difference
Set<String> symmetric = new HashSet<>(set1);
symmetric.addAll(set2);
symmetric.removeAll(intersection);
```

</td>
<td>

```python
set1 = {"a", "b", "c"}
set2 = {"b", "c", "d"}

# Union
union = set1 | set2
# or
union = set1.union(set2)

# Intersection
intersection = set1 & set2
# or
intersection = set1.intersection(set2)

# Difference
difference = set1 - set2
# or
difference = set1.difference(set2)

# Symmetric difference
symmetric = set1 ^ set2
# or
symmetric = set1.symmetric_difference(set2)
```

</td>
</tr>
<tr>
<td><strong>Iteration</strong></td>
<td>

```java
Set<String> set = new HashSet<>(Arrays.asList("a", "b", "c"));

// For-each
for (String item : set) {
    System.out.println(item);
}

// Stream API
set.stream().forEach(System.out::println);

// Iterator
Iterator<String> iterator = set.iterator();
while (iterator.hasNext()) {
    System.out.println(iterator.next());
}
```

</td>
<td>

```python
set = {"a", "b", "c"}

# Simple for
for item in set:
    print(item)

# Set comprehension
squares = {x**2 for x in range(5)}

# Convert to list for indexed access
items = list(set)
```

</td>
</tr>
<tr>
<td><strong>Set Comparison</strong></td>
<td>

```java
Set<String> set1 = new HashSet<>(Arrays.asList("a", "b"));
Set<String> set2 = new HashSet<>(Arrays.asList("a", "b", "c"));

// Check if subset
boolean isSubset = set1.containsAll(set2);

// Check if superset
boolean isSuperset = set2.containsAll(set1);

// Check if disjoint (no common elements)
boolean isDisjoint = Collections.disjoint(set1, set2);
```

</td>
<td>

```python
set1 = {"a", "b"}
set2 = {"a", "b", "c"}

# Check if subset
is_subset = set1 <= set2
# or
is_subset = set1.issubset(set2)

# Check if proper subset
is_proper_subset = set1 < set2

# Check if superset
is_superset = set2 >= set1
# or
is_superset = set2.issuperset(set1)

# Check if disjoint
is_disjoint = set1.isdisjoint(set2)
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `HashSet` for general-purpose sets (O(1) average operations)
- Use `LinkedHashSet` to maintain insertion order
- Use `TreeSet` for sorted sets (O(log n) operations)
- `Set.of()` creates immutable sets (Java 9+)
- Sets don't allow duplicate elements

### 🐍 Python
- Sets are mutable and unordered by default
- Use `frozenset` for immutable sets
- Set operations use mathematical symbols (`|`, `&`, `-`, `^`)
- Sets automatically remove duplicates
- Use `set()` constructor, not `{}` (which creates dict)

---

💡 **Extra Examples**

```java
// Java - Advanced set operations
Set<String> names = new HashSet<>(Arrays.asList("Alice", "Bob", "Charlie"));

// Filtering with Stream API
Set<String> longNames = names.stream()
    .filter(name -> name.length() > 4)
    .collect(Collectors.toSet());

// Converting to array
String[] array = names.toArray(new String[0]);

// Creating set from array
Set<Integer> numbers = Arrays.stream(new int[]{1, 2, 3, 2, 1})
    .boxed()
    .collect(Collectors.toSet());

// Custom comparator for TreeSet
Set<String> sortedSet = new TreeSet<>(String.CASE_INSENSITIVE_ORDER);
sortedSet.addAll(Arrays.asList("apple", "Banana", "cherry"));
```

```python
# Python - Advanced set operations
names = {"Alice", "Bob", "Charlie"}

# Filtering with set comprehension
long_names = {name for name in names if len(name) > 4}

# Converting to list
names_list = list(names)

# Creating set from string (removes duplicates)
unique_chars = set("hello")  # {'h', 'e', 'l', 'o'}

# Set operations with multiple sets
set1 = {1, 2, 3}
set2 = {3, 4, 5}
set3 = {5, 6, 7}

# Union of all sets
all_union = set1 | set2 | set3

# Intersection of all sets
all_intersection = set1 & set2 & set3

# Chain operations
result = set1.union(set2).intersection(set3)

# Remove duplicates from list
unique_list = list(set([1, 2, 2, 3, 3, 3]))
```
