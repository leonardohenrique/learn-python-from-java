# 🔍 Java vs Python — Regular Expressions Cheat Sheet

Regular expression operations comparison between Java and Python

---

<table>
<tr>
<th>Operation</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Basic Pattern Matching</strong></td>
<td>

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

Pattern pattern = Pattern.compile("\\d+");
Matcher matcher = pattern.matcher("123 abc 456");
boolean found = matcher.find();
String match = matcher.group();
```

</td>
<td>

```python
import re

pattern = re.compile(r'\d+')
match = pattern.search("123 abc 456")
if match:
    found = True
    match_text = match.group()
```

</td>
</tr>
<tr>
<td><strong>Find All Matches</strong></td>
<td>

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;
import java.util.List;
import java.util.ArrayList;

Pattern pattern = Pattern.compile("\\d+");
Matcher matcher = pattern.matcher("123 abc 456 def 789");
List<String> matches = new ArrayList<>();
while (matcher.find()) {
    matches.add(matcher.group());
}
```

</td>
<td>

```python
import re

pattern = re.compile(r'\d+')
matches = pattern.findall("123 abc 456 def 789")
# Returns: ['123', '456', '789']
```

</td>
</tr>
<tr>
<td><strong>Replace Text</strong></td>
<td>

```java
import java.util.regex.Pattern;

Pattern pattern = Pattern.compile("\\d+");
String text = "Price: 100, Tax: 20";
String replaced = pattern.matcher(text).replaceAll("XXX");
// Result: "Price: XXX, Tax: XXX"
```

</td>
<td>

```python
import re

pattern = re.compile(r'\d+')
text = "Price: 100, Tax: 20"
replaced = pattern.sub("XXX", text)
# Result: "Price: XXX, Tax: XXX"
```

</td>
</tr>
<tr>
<td><strong>Split by Pattern</strong></td>
<td>

```java
import java.util.regex.Pattern;

Pattern pattern = Pattern.compile("\\s+");
String text = "hello    world   test";
String[] parts = pattern.split(text);
// Result: ["hello", "world", "test"]
```

</td>
<td>

```python
import re

pattern = re.compile(r'\s+')
text = "hello    world   test"
parts = pattern.split(text)
# Result: ['hello', 'world', 'test']
```

</td>
</tr>
<tr>
<td><strong>Named Groups</strong></td>
<td>

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

Pattern pattern = Pattern.compile("(?<year>\\d{4})-(?<month>\\d{2})-(?<day>\\d{2})");
Matcher matcher = pattern.matcher("2024-01-15");
if (matcher.matches()) {
    String year = matcher.group("year");
    String month = matcher.group("month");
    String day = matcher.group("day");
}
```

</td>
<td>

```python
import re

pattern = re.compile(r'(?P<year>\d{4})-(?P<month>\d{2})-(?P<day>\d{2})')
match = pattern.match("2024-01-15")
if match:
    year = match.group('year')
    month = match.group('month')
    day = match.group('day')
```

</td>
</tr>
<tr>
<td><strong>Case Insensitive Matching</strong></td>
<td>

```java
import java.util.regex.Pattern;

Pattern pattern = Pattern.compile("hello", Pattern.CASE_INSENSITIVE);
boolean matches = pattern.matcher("HELLO").matches();
```

</td>
<td>

```python
import re

pattern = re.compile(r'hello', re.IGNORECASE)
match = pattern.match("HELLO")
# Or inline
match = re.match(r'(?i)hello', "HELLO")
```

</td>
</tr>
<tr>
<td><strong>Multiline Matching</strong></td>
<td>

```java
import java.util.regex.Pattern;

Pattern pattern = Pattern.compile("^start", Pattern.MULTILINE);
String text = "line1\nstart line2\nline3";
Matcher matcher = pattern.matcher(text);
boolean found = matcher.find();
```

</td>
<td>

```python
import re

pattern = re.compile(r'^start', re.MULTILINE)
text = "line1\nstart line2\nline3"
match = pattern.search(text)
# Or inline
match = re.search(r'(?m)^start', text)
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `java.util.regex.Pattern` and `Matcher` classes
- `Pattern.compile()` for compiled patterns
- `Matcher.find()` for finding matches
- Use `Pattern.CASE_INSENSITIVE` flag for case-insensitive matching

### 🐍 Python
- Use `re` module for regular expressions
- `re.compile()` for compiled patterns (better performance)
- `re.search()` finds first match, `re.findall()` finds all
- Use flags like `re.IGNORECASE`, `re.MULTILINE`

---

💡 **Extra Examples**

```java
// Java - Complex regex with validation
import java.util.regex.Pattern;

public class EmailValidator {
    private static final Pattern EMAIL_PATTERN = 
        Pattern.compile("^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}$");
    
    public static boolean isValidEmail(String email) {
        return EMAIL_PATTERN.matcher(email).matches();
    }
}

// Using the validator
boolean valid = EmailValidator.isValidEmail("user@example.com");
```

```python
# Python - Complex regex with validation
import re

class EmailValidator:
    EMAIL_PATTERN = re.compile(r'^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$')
    
    @classmethod
    def is_valid_email(cls, email):
        return bool(cls.EMAIL_PATTERN.match(email))

# Using the validator
valid = EmailValidator.is_valid_email("user@example.com")

# Advanced: Extract data with groups
text = "Contact: john@example.com or jane@test.org"
pattern = re.compile(r'(\w+)@(\w+\.\w+)')
matches = pattern.findall(text)
# Result: [('john', 'example.com'), ('jane', 'test.org')]
```
