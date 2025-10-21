# 📦 Java vs Python — Collections Module Cheat Sheet

Advanced collection types and data structures comparison between Java and Python

---

<table>
<tr>
<th>Operation</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Counter (Frequency Count)</strong></td>
<td>

```java
import java.util.Map;
import java.util.HashMap;
import java.util.stream.Collectors;

Map<String, Integer> counter = new HashMap<>();
String[] items = {"a", "b", "a", "c", "b", "a"};
for (String item : items) {
    counter.merge(item, 1, Integer::sum);
}
// Result: {a=3, b=2, c=1}
```

</td>
<td>

```python
from collections import Counter

items = ["a", "b", "a", "c", "b", "a"]
counter = Counter(items)
# Result: Counter({'a': 3, 'b': 2, 'c': 1})
```

</td>
</tr>
<tr>
<td><strong>Default Dictionary</strong></td>
<td>

```java
import java.util.Map;
import java.util.HashMap;
import java.util.function.Function;

Map<String, Integer> map = new HashMap<>();
// Manual default value handling
int value = map.computeIfAbsent("key", k -> 0);
```

</td>
<td>

```python
from collections import defaultdict

# Default to 0
dd = defaultdict(int)
dd["key"] += 1  # No KeyError, starts at 0

# Default to empty list
dd_list = defaultdict(list)
dd_list["key"].append("value")
```

</td>
</tr>
<tr>
<td><strong>Ordered Dictionary</strong></td>
<td>

```java
import java.util.LinkedHashMap;
import java.util.Map;

Map<String, Integer> orderedMap = new LinkedHashMap<>();
orderedMap.put("first", 1);
orderedMap.put("second", 2);
// Maintains insertion order
```

</td>
<td>

```python
from collections import OrderedDict

# Python 3.7+ dicts are ordered by default
# But OrderedDict provides additional features
od = OrderedDict()
od["first"] = 1
od["second"] = 2
# Can move items to end
od.move_to_end("first")
```

</td>
</tr>
<tr>
<td><strong>Named Tuple</strong></td>
<td>

```java
// Java - Create a simple class
public class Point {
    public final int x;
    public final int y;
    
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
    
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Point point = (Point) obj;
        return x == point.x && y == point.y;
    }
    
    @Override
    public int hashCode() {
        return Objects.hash(x, y);
    }
}
```

</td>
<td>

```python
from collections import namedtuple

Point = namedtuple('Point', ['x', 'y'])
p = Point(1, 2)
print(p.x, p.y)  # 1 2
print(p[0], p[1])  # 1 2 (indexable)
```

</td>
</tr>
<tr>
<td><strong>Deque (Double-ended Queue)</strong></td>
<td>

```java
import java.util.ArrayDeque;
import java.util.Deque;

Deque<String> deque = new ArrayDeque<>();
deque.addFirst("first");
deque.addLast("last");
String first = deque.removeFirst();
String last = deque.removeLast();
```

</td>
<td>

```python
from collections import deque

dq = deque()
dq.appendleft("first")
dq.append("last")
first = dq.popleft()
last = dq.pop()
```

</td>
</tr>
<tr>
<td><strong>Chain Map</strong></td>
<td>

```java
import java.util.Map;
import java.util.HashMap;

// Manual implementation needed
Map<String, Object> defaults = new HashMap<>();
Map<String, Object> user = new HashMap<>();
Map<String, Object> env = new HashMap<>();

// Check in order: env -> user -> defaults
Object value = env.getOrDefault("key", 
    user.getOrDefault("key", defaults.get("key")));
```

</td>
<td>

```python
from collections import ChainMap

defaults = {"color": "red", "size": "medium"}
user = {"size": "large"}
env = {"color": "blue"}

# Search order: env -> user -> defaults
chain = ChainMap(env, user, defaults)
color = chain["color"]  # "blue"
size = chain["size"]    # "large"
```

</td>
</tr>
<tr>
<td><strong>UserDict/UserList</strong></td>
<td>

```java
// Java - Extend HashMap or ArrayList
public class CustomMap<K, V> extends HashMap<K, V> {
    @Override
    public V put(K key, V value) {
        System.out.println("Adding: " + key + " = " + value);
        return super.put(key, value);
    }
}
```

</td>
<td>

```python
from collections import UserDict, UserList

class CustomDict(UserDict):
    def __setitem__(self, key, value):
        print(f"Adding: {key} = {value}")
        super().__setitem__(key, value)

class CustomList(UserList):
    def append(self, item):
        print(f"Appending: {item}")
        super().append(item)
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `LinkedHashMap` for ordered maps
- `ArrayDeque` for double-ended queue operations
- `HashMap.merge()` for counter-like operations
- Extend existing collection classes for custom behavior

### 🐍 Python
- `Counter` is perfect for frequency counting
- `defaultdict` eliminates KeyError for missing keys
- `deque` is efficient for queue operations
- `namedtuple` creates lightweight classes
- `ChainMap` for layered configuration

---

💡 **Extra Examples**

```java
// Java - Advanced collections usage
import java.util.*;
import java.util.stream.Collectors;

// Grouping by
List<String> words = Arrays.asList("apple", "banana", "cherry");
Map<Integer, List<String>> grouped = words.stream()
    .collect(Collectors.groupingBy(String::length));

// Partitioning
Map<Boolean, List<String>> partitioned = words.stream()
    .collect(Collectors.partitioningBy(s -> s.length() > 5));
```

```python
# Python - Advanced collections usage
from collections import Counter, defaultdict

# Most common elements
counter = Counter("hello world")
most_common = counter.most_common(3)
# Result: [('l', 3), ('o', 2), ('h', 1)]

# Grouping with defaultdict
dd = defaultdict(list)
words = ["apple", "banana", "cherry"]
for word in words:
    dd[len(word)].append(word)
# Result: {5: ['apple'], 6: ['banana', 'cherry']}

# ChainMap for configuration
import os
config = ChainMap(os.environ, {"DEBUG": "false"})
debug_mode = config.get("DEBUG", "false")
```
