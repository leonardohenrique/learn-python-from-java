# 🎲 Java vs Python — Random Module Cheat Sheet

Random number generation and probability operations comparison between Java and Python

---

<table>
<tr>
<th>Operation</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Basic Random Numbers</strong></td>
<td>

```java
import java.util.Random;

Random random = new Random();
int randomInt = random.nextInt();           // Any int
int boundedInt = random.nextInt(100);       // 0-99
double randomDouble = random.nextDouble();  // 0.0-1.0
float randomFloat = random.nextFloat();     // 0.0-1.0
```

</td>
<td>

```python
import random

random_int = random.randint(0, 100)     # 0-100 inclusive
random_float = random.random()          # 0.0-1.0
random_uniform = random.uniform(1, 10)  # 1.0-10.0
```

</td>
</tr>
<tr>
<td><strong>Random from Collection</strong></td>
<td>

```java
import java.util.Random;
import java.util.List;
import java.util.Arrays;

Random random = new Random();
List<String> items = Arrays.asList("A", "B", "C");
String randomItem = items.get(random.nextInt(items.size()));
```

</td>
<td>

```python
import random

items = ["A", "B", "C"]
random_item = random.choice(items)
random_items = random.choices(items, k=3)  # With replacement
```

</td>
</tr>
<tr>
<td><strong>Shuffle Collection</strong></td>
<td>

```java
import java.util.Collections;
import java.util.Arrays;
import java.util.List;

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
Collections.shuffle(numbers);
```

</td>
<td>

```python
import random

numbers = [1, 2, 3, 4, 5]
random.shuffle(numbers)  # In-place shuffle
# Or create new shuffled list
shuffled = random.sample(numbers, len(numbers))
```

</td>
</tr>
<tr>
<td><strong>Sample without Replacement</strong></td>
<td>

```java
import java.util.Random;
import java.util.List;
import java.util.ArrayList;
import java.util.Collections;

Random random = new Random();
List<Integer> population = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> sample = new ArrayList<>(population);
Collections.shuffle(sample);
sample = sample.subList(0, 3);  // Take first 3
```

</td>
<td>

```python
import random

population = [1, 2, 3, 4, 5]
sample = random.sample(population, 3)  # 3 unique items
```

</td>
</tr>
<tr>
<td><strong>Gaussian/Normal Distribution</strong></td>
<td>

```java
import java.util.Random;

Random random = new Random();
double gaussian = random.nextGaussian();  // Mean=0, StdDev=1
// Custom mean and std dev
double customGaussian = random.nextGaussian() * 2.0 + 5.0;
```

</td>
<td>

```python
import random

gaussian = random.gauss(0, 1)        # Mean=0, StdDev=1
custom_gaussian = random.gauss(5, 2)  # Mean=5, StdDev=2
```

</td>
</tr>
<tr>
<td><strong>Seeded Random</strong></td>
<td>

```java
import java.util.Random;

Random random = new Random(12345);  // Fixed seed
int value1 = random.nextInt(100);
int value2 = random.nextInt(100);
// Same seed produces same sequence
```

</td>
<td>

```python
import random

random.seed(12345)  # Fixed seed
value1 = random.randint(0, 100)
value2 = random.randint(0, 100)
# Same seed produces same sequence
```

</td>
</tr>
<tr>
<td><strong>Weighted Random Choice</strong></td>
<td>

```java
import java.util.Random;
import java.util.List;
import java.util.Arrays;

Random random = new Random();
List<String> items = Arrays.asList("A", "B", "C");
List<Double> weights = Arrays.asList(0.5, 0.3, 0.2);
// Custom implementation needed for weighted selection
```

</td>
<td>

```python
import random

items = ["A", "B", "C"]
weights = [0.5, 0.3, 0.2]
weighted_choice = random.choices(items, weights=weights, k=1)[0]
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `java.util.Random` for basic random operations
- `Collections.shuffle()` for shuffling lists
- Need custom implementation for weighted selection
- `SecureRandom` for cryptographic purposes

### 🐍 Python
- `random` module provides comprehensive random functions
- `random.choices()` for weighted selection
- `random.sample()` for sampling without replacement
- `secrets` module for cryptographic random numbers

---

💡 **Extra Examples**

```java
// Java - Custom weighted random selection
import java.util.Random;
import java.util.List;
import java.util.ArrayList;

public class WeightedRandom {
    private Random random = new Random();
    
    public String weightedChoice(List<String> items, List<Double> weights) {
        double totalWeight = weights.stream().mapToDouble(Double::doubleValue).sum();
        double randomValue = random.nextDouble() * totalWeight;
        
        double currentWeight = 0;
        for (int i = 0; i < items.size(); i++) {
            currentWeight += weights.get(i);
            if (randomValue <= currentWeight) {
                return items.get(i);
            }
        }
        return items.get(items.size() - 1);
    }
}
```

```python
# Python - Advanced random operations
import random

# Generate random string
import string
random_string = ''.join(random.choices(string.ascii_letters, k=10))

# Random boolean with probability
random_bool = random.random() < 0.7  # 70% chance of True

# Random date
from datetime import datetime, timedelta
start_date = datetime(2024, 1, 1)
random_date = start_date + timedelta(days=random.randint(0, 365))
```
