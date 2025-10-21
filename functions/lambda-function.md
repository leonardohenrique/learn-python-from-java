# ⚡ Java vs Python — Lambda Functions Cheat Sheet

Comparison of lambda expressions and functional programming constructs between Java and Python

---

<table>
<tr>
<th>Concept</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Basic Lambda Expression</strong></td>
<td>

```java
// Java 8+ lambda syntax
Function<Integer, Integer> square = x -> x * x;
BiFunction<Integer, Integer, Integer> add = (a, b) -> a + b;

// Usage
int result = square.apply(5); // 25
int sum = add.apply(3, 4);    // 7
```

</td>
<td>

```python
# Python lambda syntax
square = lambda x: x * x
add = lambda a, b: a + b

# Usage
result = square(5)  # 25
sum_val = add(3, 4)  # 7
```

</td>
</tr>
<tr>
<td><strong>Lambda with Collections</strong></td>
<td>

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

// Map operation
List<Integer> squares = numbers.stream()
    .map(x -> x * x)
    .collect(Collectors.toList());

// Filter operation
List<Integer> evens = numbers.stream()
    .filter(x -> x % 2 == 0)
    .collect(Collectors.toList());
```

</td>
<td>

```python
numbers = [1, 2, 3, 4, 5]

# Map operation
squares = list(map(lambda x: x * x, numbers))

# Filter operation
evens = list(filter(lambda x: x % 2 == 0, numbers))

# List comprehensions (more Pythonic)
squares = [x * x for x in numbers]
evens = [x for x in numbers if x % 2 == 0]
```

</td>
</tr>
<tr>
<td><strong>Lambda with Sorting</strong></td>
<td>

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

// Sort by length
names.sort((a, b) -> a.length() - b.length());

// Sort by length (descending)
names.sort((a, b) -> b.length() - a.length());

// Using Comparator
names.sort(Comparator.comparing(String::length));
```

</td>
<td>

```python
names = ["Alice", "Bob", "Charlie"]

# Sort by length
names.sort(key=lambda x: len(x))

# Sort by length (descending)
names.sort(key=lambda x: len(x), reverse=True)

# Using sorted() function
sorted_names = sorted(names, key=lambda x: len(x))
```

</td>
</tr>
<tr>
<td><strong>Lambda with Reduce</strong></td>
<td>

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

// Sum all numbers
int sum = numbers.stream()
    .reduce(0, (a, b) -> a + b);

// Find maximum
int max = numbers.stream()
    .reduce(Integer.MIN_VALUE, (a, b) -> a > b ? a : b);
```

</td>
<td>

```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]

# Sum all numbers
sum_val = reduce(lambda a, b: a + b, numbers)

# Find maximum
max_val = reduce(lambda a, b: a if a > b else b, numbers)
```

</td>
</tr>
<tr>
<td><strong>Lambda with Multiple Parameters</strong></td>
<td>

```java
// BiFunction for two parameters
BiFunction<Integer, Integer, Integer> multiply = (a, b) -> a * b;

// Custom functional interface for three parameters
@FunctionalInterface
interface TriFunction<T, U, V, R> {
    R apply(T t, U u, V v);
}

TriFunction<Integer, Integer, Integer, Integer> addThree = 
    (a, b, c) -> a + b + c;
```

</td>
<td>

```python
# Multiple parameters in lambda
multiply = lambda a, b: a * b

# Three parameters
add_three = lambda a, b, c: a + b + c

# More complex lambda
process_data = lambda x, y, z: (x + y) * z if x > 0 else y * z
```

</td>
</tr>
<tr>
<td><strong>Lambda with Conditional Logic</strong></td>
<td>

```java
// Conditional lambda
Function<Integer, String> classify = x -> 
    x > 0 ? "positive" : x < 0 ? "negative" : "zero";

// Lambda with if-else
Predicate<Integer> isEven = x -> x % 2 == 0;
Predicate<Integer> isOdd = x -> x % 2 != 0;
```

</td>
<td>

```python
# Conditional lambda
classify = lambda x: "positive" if x > 0 else "negative" if x < 0 else "zero"

# Lambda with if-else
is_even = lambda x: x % 2 == 0
is_odd = lambda x: x % 2 != 0

# More complex conditional
process = lambda x: x * 2 if x > 10 else x + 1 if x > 5 else x
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Lambda expressions require functional interfaces
- Use method references (`::`) when possible for cleaner code
- Stream API provides powerful functional operations
- Lambda expressions are compiled to anonymous classes

### 🐍 Python
- Lambda functions are limited to single expressions
- Use list comprehensions for better readability
- Lambda functions are first-class objects
- Can be assigned to variables or passed as arguments

---

💡 **Extra Examples**

```java
// Java - Method references and complex lambdas
List<String> words = Arrays.asList("hello", "world", "java", "python");

// Method reference
words.forEach(System.out::println);

// Complex lambda with multiple operations
Map<String, Integer> wordLengths = words.stream()
    .filter(word -> word.length() > 3)
    .collect(Collectors.toMap(
        word -> word,
        String::length
    ));

// Lambda with exception handling
Function<String, Integer> safeParseInt = s -> {
    try {
        return Integer.parseInt(s);
    } catch (NumberFormatException e) {
        return 0;
    }
};
```

```python
# Python - Advanced lambda usage
words = ["hello", "world", "java", "python"]

# Lambda with map and filter
long_words = list(map(lambda w: w.upper(), 
                     filter(lambda w: len(w) > 3, words)))

# Lambda in higher-order functions
def apply_operation(numbers, operation):
    return [operation(x) for x in numbers]

result = apply_operation([1, 2, 3, 4], lambda x: x ** 2)

# Lambda with default arguments (using partial)
from functools import partial

multiply_by = lambda factor, x: factor * x
double = partial(multiply_by, 2)
triple = partial(multiply_by, 3)
```
