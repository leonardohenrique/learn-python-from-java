# 📦 Java vs Python — Imports Cheat Sheet

Comparison of import mechanisms and module management between Java and Python

---

<table>
<tr>
<th>Concept</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Basic Import</strong></td>
<td>

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Map;
```

</td>
<td>

```python
import os
import sys
import json
```

</td>
</tr>
<tr>
<td><strong>Import Specific Classes</strong></td>
<td>

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
```

</td>
<td>

```python
from os import path, getcwd
from sys import argv, exit
from json import loads, dumps
```

</td>
</tr>
<tr>
<td><strong>Import All (Wildcard)</strong></td>
<td>

```java
import java.util.*;
import java.io.*;
```

</td>
<td>

```python
from os import *
from sys import *
```

</td>
</tr>
<tr>
<td><strong>Import with Alias</strong></td>
<td>

```java
import java.util.ArrayList as List;
import java.util.HashMap as Map;
```

</td>
<td>

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

</td>
</tr>
<tr>
<td><strong>Static Imports</strong></td>
<td>

```java
import static java.lang.Math.PI;
import static java.lang.Math.sqrt;
import static java.util.Collections.sort;

// Usage
double radius = sqrt(25);
List<Integer> numbers = Arrays.asList(3, 1, 4);
sort(numbers);
```

</td>
<td>

```python
from math import pi, sqrt
from collections import Counter

# Usage
radius = sqrt(25)
counter = Counter([1, 2, 2, 3])
```

</td>
</tr>
<tr>
<td><strong>Package/Module Structure</strong></td>
<td>

```java
// Package declaration
package com.example.utils;

// Import from same package
import com.example.utils.StringHelper;
import com.example.model.User;

// Import from different package
import java.util.List;
```

</td>
<td>

```python
# No package declaration needed
# File: utils/string_helper.py

# Import from same package
from .string_helper import format_name
from ..model.user import User

# Import from different package
import os
```

</td>
</tr>
<tr>
<td><strong>Conditional Imports</strong></td>
<td>

```java
// Java doesn't have conditional imports
// Use reflection or factory patterns instead
try {
    Class<?> clazz = Class.forName("com.example.OptionalClass");
    Object instance = clazz.newInstance();
} catch (ClassNotFoundException e) {
    // Handle missing class
}
```

</td>
<td>

```python
try:
    import optional_module
    HAS_OPTIONAL = True
except ImportError:
    HAS_OPTIONAL = False

# Or with conditional logic
if sys.version_info >= (3, 8):
    from typing import Literal
else:
    from typing_extensions import Literal
```

</td>
</tr>
<tr>
<td><strong>Custom Package Creation</strong></td>
<td>

```java
// Directory structure:
// com/example/utils/
//   ├── StringHelper.java
//   └── MathHelper.java

// StringHelper.java
package com.example.utils;

public class StringHelper {
    public static String capitalize(String str) {
        return str.substring(0, 1).toUpperCase() + 
               str.substring(1).toLowerCase();
    }
}

// Usage in another file
import com.example.utils.StringHelper;
String result = StringHelper.capitalize("hello");
```

</td>
<td>

```python
# Directory structure:
# utils/
#   ├── __init__.py
#   ├── string_helper.py
#   └── math_helper.py

# utils/string_helper.py
def capitalize(text):
    return text[0].upper() + text[1:].lower()

# utils/__init__.py
from .string_helper import capitalize
from .math_helper import add, multiply

# Usage
from utils import capitalize
result = capitalize("hello")

# Or
import utils.string_helper as sh
result = sh.capitalize("hello")
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use specific imports instead of wildcards for better performance
- Static imports are useful for utility methods and constants
- Package names should follow reverse domain naming convention
- Import statements must be at the top of the file

### 🐍 Python
- Use `from module import specific_function` for cleaner code
- Avoid `from module import *` to prevent namespace pollution
- Use `__init__.py` files to make directories into packages
- Import statements can be anywhere in the file (but top is recommended)

---

💡 **Extra Examples**

```java
// Java - Multiple imports from same package
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

// Java - Static import for constants
import static java.lang.Math.PI;
import static java.lang.Math.E;

// Java - Import with full qualification
java.util.Date date = new java.util.Date();
```

```python
# Python - Multiple imports from same module
from collections import defaultdict, Counter, deque

# Python - Import with relative paths
from .models import User
from ..utils import helper_function

# Python - Import and rename
import datetime as dt
from datetime import datetime as dt_class

# Python - Import specific attributes
from os.path import join, exists, isfile
```
