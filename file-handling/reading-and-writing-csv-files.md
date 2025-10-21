# 📊 Java vs Python — Reading and Writing CSV Files Cheat Sheet

CSV file operations comparison between Java and Python for data processing and manipulation.

---

<table>
<tr>
<th>Operation</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Reading CSV File</strong></td>
<td>

```java
// Using OpenCSV library
import com.opencsv.CSVReader;
import java.io.FileReader;
import java.io.IOException;

try (CSVReader reader = new CSVReader(new FileReader("data.csv"))) {
    String[] nextLine;
    while ((nextLine = reader.readNext()) != null) {
        for (String cell : nextLine) {
            System.out.print(cell + " ");
        }
        System.out.println();
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

</td>
<td>

```python
# Using csv module
import csv

with open('data.csv', 'r') as file:
    reader = csv.reader(file)
    for row in reader:
        print(' '.join(row))
```

</td>
</tr>
<tr>
<td><strong>Writing CSV File</strong></td>
<td>

```java
// Using OpenCSV library
import com.opencsv.CSVWriter;
import java.io.FileWriter;
import java.io.IOException;

try (CSVWriter writer = new CSVWriter(new FileWriter("output.csv"))) {
    String[] header = {"Name", "Age", "City"};
    writer.writeNext(header);
    
    String[] data1 = {"John", "25", "New York"};
    String[] data2 = {"Jane", "30", "London"};
    writer.writeNext(data1);
    writer.writeNext(data2);
} catch (IOException e) {
    e.printStackTrace();
}
```

</td>
<td>

```python
# Using csv module
import csv

with open('output.csv', 'w', newline='') as file:
    writer = csv.writer(file)
    writer.writerow(['Name', 'Age', 'City'])
    writer.writerow(['John', '25', 'New York'])
    writer.writerow(['Jane', '30', 'London'])
```

</td>
</tr>
<tr>
<td><strong>Reading with Headers</strong></td>
<td>

```java
// Using OpenCSV with headers
import com.opencsv.CSVReaderHeaderAware;
import java.io.FileReader;
import java.io.IOException;
import java.util.Map;

try (CSVReaderHeaderAware reader = new CSVReaderHeaderAware(new FileReader("data.csv"))) {
    Map<String, String> values;
    while ((values = reader.readMap()) != null) {
        System.out.println("Name: " + values.get("Name"));
        System.out.println("Age: " + values.get("Age"));
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

</td>
<td>

```python
# Using csv.DictReader
import csv

with open('data.csv', 'r') as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(f"Name: {row['Name']}")
        print(f"Age: {row['Age']}")
```

</td>
</tr>
<tr>
<td><strong>Writing with Headers</strong></td>
<td>

```java
// Using OpenCSV with headers
import com.opencsv.CSVWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Arrays;

try (CSVWriter writer = new CSVWriter(new FileWriter("output.csv"))) {
    // Write header
    writer.writeNext(new String[]{"Name", "Age", "City"});
    
    // Write data
    writer.writeNext(new String[]{"John", "25", "New York"});
    writer.writeNext(new String[]{"Jane", "30", "London"});
} catch (IOException e) {
    e.printStackTrace();
}
```

</td>
<td>

```python
# Using csv.DictWriter
import csv

with open('output.csv', 'w', newline='') as file:
    fieldnames = ['Name', 'Age', 'City']
    writer = csv.DictWriter(file, fieldnames=fieldnames)
    
    writer.writeheader()
    writer.writerow({'Name': 'John', 'Age': '25', 'City': 'New York'})
    writer.writerow({'Name': 'Jane', 'Age': '30', 'City': 'London'})
```

</td>
</tr>
<tr>
<td><strong>Custom Delimiter</strong></td>
<td>

```java
// Using custom delimiter
import com.opencsv.CSVReader;
import java.io.FileReader;
import java.io.IOException;

try (CSVReader reader = new CSVReader(new FileReader("data.tsv"), '\t')) {
    String[] nextLine;
    while ((nextLine = reader.readNext()) != null) {
        // Process tab-separated values
        for (String cell : nextLine) {
            System.out.print(cell + " | ");
        }
        System.out.println();
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

</td>
<td>

```python
# Using custom delimiter
import csv

with open('data.tsv', 'r') as file:
    reader = csv.reader(file, delimiter='\t')
    for row in reader:
        print(' | '.join(row))
```

</td>
</tr>
<tr>
<td><strong>Pandas Alternative (Python)</strong></td>
<td>

```java
// Java doesn't have direct equivalent to pandas
// Use libraries like Apache Commons CSV or OpenCSV
// For complex data manipulation, consider using
// frameworks like Apache Spark or custom data structures
```

</td>
<td>

```python
# Using pandas for advanced CSV operations
import pandas as pd

# Read CSV
df = pd.read_csv('data.csv')

# Display first 5 rows
print(df.head())

# Filter data
filtered = df[df['Age'] > 25]

# Write to CSV
filtered.to_csv('filtered_data.csv', index=False)
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use OpenCSV library for robust CSV handling
- Always handle `IOException` in file operations
- Use try-with-resources for automatic resource management
- Consider Apache Commons CSV for more advanced features
- For large files, use streaming approach to avoid memory issues

### 🐍 Python
- Use `csv` module for basic operations (built-in)
- Use `pandas` for complex data analysis and manipulation
- Always specify `newline=''` when writing CSV files
- Use `DictReader`/`DictWriter` for header-based operations
- Consider `csv.Sniffer` for automatic delimiter detection

---

💡 **Extra Examples**

```java
// Java - Processing large CSV files
try (CSVReader reader = new CSVReader(new FileReader("large_file.csv"))) {
    String[] nextLine;
    int lineNumber = 0;
    while ((nextLine = reader.readNext()) != null) {
        lineNumber++;
        if (lineNumber % 1000 == 0) {
            System.out.println("Processed " + lineNumber + " lines");
        }
        // Process each line
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

```python
# Python - Processing large CSV files with chunking
import pandas as pd

# Read in chunks for large files
chunk_size = 1000
for chunk in pd.read_csv('large_file.csv', chunksize=chunk_size):
    # Process each chunk
    print(f"Processing chunk with {len(chunk)} rows")
    # Perform operations on chunk
```
