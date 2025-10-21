# 📚 Java vs Python — Dictionary/Map Cheat Sheet

Comparison of dictionary/map data structures between Java and Python, covering creation, manipulation, and common operations.

---

<table>
<tr>
<th>Operation</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Create Dictionary/Map</strong></td>
<td>

```java
// HashMap (most common)
Map<String, Integer> map = new HashMap<>();
Map<String, Integer> map2 = Map.of("key1", 1, "key2", 2);

// LinkedHashMap (preserves insertion order)
Map<String, Integer> linkedMap = new LinkedHashMap<>();

// TreeMap (sorted by keys)
Map<String, Integer> treeMap = new TreeMap<>();
```

</td>
<td>

```python
# Dictionary creation
dict1 = {}
dict2 = {"key1": 1, "key2": 2}
dict3 = dict(key1=1, key2=2)

# Using dict() constructor
dict4 = dict([("key1", 1), ("key2", 2)])
```

</td>
</tr>
<tr>
<td><strong>Add/Update Elements</strong></td>
<td>

```java
// Add or update
map.put("key", 42);
map.putIfAbsent("key", 100); // only if key doesn't exist

// Update existing value
map.merge("key", 10, Integer::sum); // adds 10 to existing value
```

</td>
<td>

```python
# Add or update
dict1["key"] = 42
dict1.update({"key2": 100, "key3": 200})

# Update with default
dict1.setdefault("new_key", 0)
```

</td>
</tr>
<tr>
<td><strong>Access Elements</strong></td>
<td>

```java
// Get value
Integer value = map.get("key");
Integer valueOrDefault = map.getOrDefault("key", 0);

// Check if key exists
boolean exists = map.containsKey("key");

// Get all keys/values
Set<String> keys = map.keySet();
Collection<Integer> values = map.values();
```

</td>
<td>

```python
# Get value
value = dict1["key"]  # raises KeyError if not found
value = dict1.get("key", 0)  # returns default if not found

# Check if key exists
exists = "key" in dict1

# Get all keys/values
keys = dict1.keys()
values = dict1.values()
items = dict1.items()
```

</td>
</tr>
<tr>
<td><strong>Remove Elements</strong></td>
<td>

```java
// Remove by key
Integer removed = map.remove("key");
boolean wasRemoved = map.remove("key", 42); // only if value matches

// Remove all elements
map.clear();

// Remove while iterating
map.entrySet().removeIf(entry -> entry.getValue() < 10);
```

</td>
<td>

```python
# Remove by key
removed = dict1.pop("key", None)  # returns default if not found
del dict1["key"]  # raises KeyError if not found

# Remove all elements
dict1.clear()

# Remove while iterating (create new dict)
dict1 = {k: v for k, v in dict1.items() if v >= 10}
```

</td>
</tr>
<tr>
<td><strong>Iteration</strong></td>
<td>

```java
// Iterate over entries
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    String key = entry.getKey();
    Integer value = entry.getValue();
}

// Iterate over keys
for (String key : map.keySet()) {
    Integer value = map.get(key);
}

// Using forEach (Java 8+)
map.forEach((key, value) -> 
    System.out.println(key + " = " + value));
```

</td>
<td>

```python
# Iterate over items
for key, value in dict1.items():
    print(f"{key} = {value}")

# Iterate over keys
for key in dict1:
    value = dict1[key]

# Iterate over values
for value in dict1.values():
    print(value)
```

</td>
</tr>
<tr>
<td><strong>Dictionary Comprehension</strong></td>
<td>

```java
// Java doesn't have dictionary comprehension
// Use streams for similar functionality
Map<String, Integer> doubled = map.entrySet()
    .stream()
    .collect(Collectors.toMap(
        Map.Entry::getKey,
        entry -> entry.getValue() * 2
    ));

// Filter and transform
Map<String, Integer> filtered = map.entrySet()
    .stream()
    .filter(entry -> entry.getValue() > 10)
    .collect(Collectors.toMap(
        Map.Entry::getKey,
        Map.Entry::getValue
    ));
```

</td>
<td>

```python
# Dictionary comprehension
doubled = {k: v * 2 for k, v in dict1.items()}

# Filter and transform
filtered = {k: v for k, v in dict1.items() if v > 10}

# Create from lists
keys = ['a', 'b', 'c']
values = [1, 2, 3]
new_dict = {k: v for k, v in zip(keys, values)}
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `HashMap` for general-purpose maps (O(1) average access)
- Use `LinkedHashMap` when you need insertion order
- Use `TreeMap` when you need sorted keys (O(log n) access)
- Always specify generic types: `Map<String, Integer>`
- Use `getOrDefault()` to avoid null checks

### 🐍 Python
- Dictionaries maintain insertion order (Python 3.7+)
- Use `get()` method to avoid KeyError exceptions
- Dictionary comprehensions are very efficient and readable
- Keys must be hashable (immutable types)
- Use `collections.defaultdict` for default values

---

💡 **Extra Examples**

```java
// Java - Complex operations
Map<String, List<Integer>> multiMap = new HashMap<>();
multiMap.computeIfAbsent("group1", k -> new ArrayList<>()).add(42);

// Merge two maps
Map<String, Integer> map1 = Map.of("a", 1, "b", 2);
Map<String, Integer> map2 = Map.of("b", 3, "c", 4);
Map<String, Integer> merged = new HashMap<>(map1);
map2.forEach((key, value) -> 
    merged.merge(key, value, Integer::sum));
```

```python
# Python - Complex operations
from collections import defaultdict

# Multi-map equivalent
multi_dict = defaultdict(list)
multi_dict["group1"].append(42)

# Merge two dictionaries (Python 3.9+)
dict1 = {"a": 1, "b": 2}
dict2 = {"b": 3, "c": 4}
merged = dict1 | dict2  # or {**dict1, **dict2}

# Nested dictionary access
nested = {"level1": {"level2": {"value": 42}}}
value = nested.get("level1", {}).get("level2", {}).get("value")
```
