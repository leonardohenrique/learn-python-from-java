# 📅 Java vs Python — DateTime Module Cheat Sheet

Date and time handling comparison between Java and Python

---

<table>
<tr>
<th>Operation</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Current Date/Time</strong></td>
<td>

```java
import java.time.LocalDateTime;
import java.time.LocalDate;
import java.time.LocalTime;

LocalDateTime now = LocalDateTime.now();
LocalDate today = LocalDate.now();
LocalTime currentTime = LocalTime.now();
```

</td>
<td>

```python
from datetime import datetime, date, time

now = datetime.now()
today = date.today()
current_time = datetime.now().time()
```

</td>
</tr>
<tr>
<td><strong>Create Specific Date</strong></td>
<td>

```java
import java.time.LocalDate;
import java.time.LocalDateTime;

LocalDate date = LocalDate.of(2024, 1, 15);
LocalDateTime dateTime = LocalDateTime.of(2024, 1, 15, 14, 30);
```

</td>
<td>

```python
from datetime import datetime, date

date_obj = date(2024, 1, 15)
datetime_obj = datetime(2024, 1, 15, 14, 30)
```

</td>
</tr>
<tr>
<td><strong>Parse Date String</strong></td>
<td>

```java
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;

String dateStr = "2024-01-15";
LocalDate date = LocalDate.parse(dateStr);
// Custom format
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");
LocalDate customDate = LocalDate.parse("15/01/2024", formatter);
```

</td>
<td>

```python
from datetime import datetime

date_str = "2024-01-15"
date_obj = datetime.fromisoformat(date_str)
# Custom format
date_obj = datetime.strptime("15/01/2024", "%d/%m/%Y")
```

</td>
</tr>
<tr>
<td><strong>Format Date to String</strong></td>
<td>

```java
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;

LocalDate date = LocalDate.now();
String formatted = date.format(DateTimeFormatter.ofPattern("dd/MM/yyyy"));
String iso = date.toString(); // ISO format
```

</td>
<td>

```python
from datetime import datetime

date_obj = datetime.now()
formatted = date_obj.strftime("%d/%m/%Y")
iso = date_obj.isoformat()
```

</td>
</tr>
<tr>
<td><strong>Date Arithmetic</strong></td>
<td>

```java
import java.time.LocalDate;
import java.time.temporal.ChronoUnit;

LocalDate date = LocalDate.now();
LocalDate tomorrow = date.plusDays(1);
LocalDate nextWeek = date.plusWeeks(1);
LocalDate nextMonth = date.plusMonths(1);

// Difference between dates
long daysBetween = ChronoUnit.DAYS.between(date, tomorrow);
```

</td>
<td>

```python
from datetime import datetime, timedelta

date_obj = datetime.now()
tomorrow = date_obj + timedelta(days=1)
next_week = date_obj + timedelta(weeks=1)
next_month = date_obj + timedelta(days=30)

# Difference between dates
diff = tomorrow - date_obj
days_between = diff.days
```

</td>
</tr>
<tr>
<td><strong>Time Zones</strong></td>
<td>

```java
import java.time.ZonedDateTime;
import java.time.ZoneId;

ZonedDateTime utc = ZonedDateTime.now(ZoneId.of("UTC"));
ZonedDateTime ny = ZonedDateTime.now(ZoneId.of("America/New_York"));
```

</td>
<td>

```python
from datetime import datetime
import pytz

utc = datetime.now(pytz.UTC)
ny = datetime.now(pytz.timezone('America/New_York'))
```

</td>
</tr>
<tr>
<td><strong>Timestamp (Unix Time)</strong></td>
<td>

```java
import java.time.Instant;

Instant now = Instant.now();
long timestamp = now.getEpochSecond();
Instant fromTimestamp = Instant.ofEpochSecond(timestamp);
```

</td>
<td>

```python
import time
from datetime import datetime

timestamp = time.time()
now = datetime.fromtimestamp(timestamp)
timestamp_from_datetime = now.timestamp()
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `java.time` package (Java 8+) for modern date/time
- `LocalDateTime` for date and time without timezone
- `ZonedDateTime` for timezone-aware operations
- `ChronoUnit` for date/time calculations

### 🐍 Python
- `datetime` module for most date/time operations
- `timedelta` for date arithmetic
- Use `pytz` library for timezone support
- `time` module for Unix timestamps

---

💡 **Extra Examples**

```java
// Java - Working with periods and durations
import java.time.*;
import java.time.temporal.ChronoUnit;

LocalDate birthDate = LocalDate.of(1990, 5, 15);
LocalDate today = LocalDate.now();
Period age = Period.between(birthDate, today);
System.out.println("Age: " + age.getYears() + " years");

Duration duration = Duration.ofHours(2).plusMinutes(30);
```

```python
# Python - Working with time deltas
from datetime import datetime, timedelta

birth_date = datetime(1990, 5, 15)
today = datetime.now()
age = today - birth_date
print(f"Age: {age.days // 365} years")

duration = timedelta(hours=2, minutes=30)
```
