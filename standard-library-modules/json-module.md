# 📄 Java vs Python — JSON Module Cheat Sheet

JSON parsing and serialization comparison between Java and Python

---

<table>
<tr>
<th>Operation</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Parse JSON String</strong></td>
<td>

```java
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.JsonNode;

ObjectMapper mapper = new ObjectMapper();
String json = "{\"name\":\"John\",\"age\":30}";
JsonNode node = mapper.readTree(json);
String name = node.get("name").asText();
int age = node.get("age").asInt();
```

</td>
<td>

```python
import json

json_str = '{"name":"John","age":30}'
data = json.loads(json_str)
name = data["name"]
age = data["age"]
```

</td>
</tr>
<tr>
<td><strong>Parse JSON to Object</strong></td>
<td>

```java
import com.fasterxml.jackson.databind.ObjectMapper;

public class Person {
    private String name;
    private int age;
    // getters and setters
}

ObjectMapper mapper = new ObjectMapper();
String json = "{\"name\":\"John\",\"age\":30}";
Person person = mapper.readValue(json, Person.class);
```

</td>
<td>

```python
import json
from dataclasses import dataclass

@dataclass
class Person:
    name: str
    age: int

json_str = '{"name":"John","age":30}'
data = json.loads(json_str)
person = Person(**data)
```

</td>
</tr>
<tr>
<td><strong>Convert Object to JSON</strong></td>
<td>

```java
import com.fasterxml.jackson.databind.ObjectMapper;

Person person = new Person("John", 30);
ObjectMapper mapper = new ObjectMapper();
String json = mapper.writeValueAsString(person);
// Pretty print
String prettyJson = mapper.writerWithDefaultPrettyPrinter()
    .writeValueAsString(person);
```

</td>
<td>

```python
import json

person = {"name": "John", "age": 30}
json_str = json.dumps(person)
# Pretty print
pretty_json = json.dumps(person, indent=2)
```

</td>
</tr>
<tr>
<td><strong>Read JSON from File</strong></td>
<td>

```java
import com.fasterxml.jackson.databind.ObjectMapper;
import java.nio.file.Files;
import java.nio.file.Paths;

ObjectMapper mapper = new ObjectMapper();
String content = Files.readString(Paths.get("data.json"));
JsonNode data = mapper.readTree(content);
```

</td>
<td>

```python
import json

with open('data.json', 'r') as file:
    data = json.load(file)
```

</td>
</tr>
<tr>
<td><strong>Write JSON to File</strong></td>
<td>

```java
import com.fasterxml.jackson.databind.ObjectMapper;
import java.nio.file.Files;
import java.nio.file.Paths;

ObjectMapper mapper = new ObjectMapper();
Person person = new Person("John", 30);
String json = mapper.writeValueAsString(person);
Files.write(Paths.get("output.json"), json.getBytes());
```

</td>
<td>

```python
import json

person = {"name": "John", "age": 30}
with open('output.json', 'w') as file:
    json.dump(person, file)
```

</td>
</tr>
<tr>
<td><strong>Handle Nested Objects</strong></td>
<td>

```java
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.JsonNode;

String json = "{\"user\":{\"name\":\"John\",\"address\":{\"city\":\"NYC\"}}}";
JsonNode node = mapper.readTree(json);
String city = node.get("user").get("address").get("city").asText();
```

</td>
<td>

```python
import json

json_str = '{"user":{"name":"John","address":{"city":"NYC"}}}'
data = json.loads(json_str)
city = data["user"]["address"]["city"]
```

</td>
</tr>
<tr>
<td><strong>Handle Arrays</strong></td>
<td>

```java
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.JsonNode;
import java.util.List;

String json = "[{\"name\":\"John\"},{\"name\":\"Jane\"}]";
JsonNode array = mapper.readTree(json);
for (JsonNode item : array) {
    String name = item.get("name").asText();
    System.out.println(name);
}
```

</td>
<td>

```python
import json

json_str = '[{"name":"John"},{"name":"Jane"}]'
data = json.loads(json_str)
for item in data:
    name = item["name"]
    print(name)
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use Jackson library for JSON processing
- `ObjectMapper` is the main class for JSON operations
- `JsonNode` for tree model access
- Use annotations like `@JsonProperty` for field mapping

### 🐍 Python
- Built-in `json` module for basic operations
- `json.loads()` for string parsing
- `json.load()` for file reading
- Use `dataclasses` or `pydantic` for object mapping

---

💡 **Extra Examples**

```java
// Java - Custom serialization
import com.fasterxml.jackson.annotation.JsonProperty;

public class User {
    @JsonProperty("user_name")
    private String name;
    
    @JsonProperty("user_age")
    private int age;
    
    // constructors, getters, setters
}

ObjectMapper mapper = new ObjectMapper();
mapper.configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false);
```

```python
# Python - Custom serialization
import json
from dataclasses import dataclass, asdict

@dataclass
class User:
    name: str
    age: int

user = User("John", 30)
json_str = json.dumps(asdict(user))
```
