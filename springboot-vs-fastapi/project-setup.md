# 🚀 Java vs Python — Project Setup Cheat Sheet

Comparison of project initialization and configuration between Spring Boot and FastAPI

---

<table>
<tr>
<th>Setup Aspect</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Project Initialization</strong></td>
<td>

```java
// Using Spring Initializr
// https://start.spring.io/
// Select: Web, JPA, H2, DevTools

// Or Maven command line
mvn archetype:generate \
  -DgroupId=com.example \
  -DartifactId=myapp \
  -DarchetypeArtifactId=maven-archetype-quickstart
```

</td>
<td>

```python
# Create virtual environment
python -m venv venv
source venv/bin/activate  # Linux/Mac
# venv\Scripts\activate   # Windows

# Install FastAPI
pip install fastapi uvicorn

# Create main.py
from fastapi import FastAPI
app = FastAPI()
```

</td>
</tr>
<tr>
<td><strong>Dependency Management</strong></td>
<td>

```java
// pom.xml (Maven)
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
</dependencies>
```

</td>
<td>

```python
# requirements.txt
fastapi==0.104.1
uvicorn[standard]==0.24.0
sqlalchemy==2.0.23
alembic==1.12.1

# Install dependencies
pip install -r requirements.txt
```

</td>
</tr>
<tr>
<td><strong>Application Configuration</strong></td>
<td>

```java
// application.properties
server.port=8080
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driver-class-name=org.h2.Driver
spring.jpa.hibernate.ddl-auto=create-drop

// Or application.yml
server:
  port: 8080
spring:
  datasource:
    url: jdbc:h2:mem:testdb
    driver-class-name: org.h2.Driver
  jpa:
    hibernate:
      ddl-auto: create-drop
```

</td>
<td>

```python
# config.py
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    app_name: str = "FastAPI App"
    debug: bool = False
    database_url: str = "sqlite:///./test.db"
    
    class Config:
        env_file = ".env"

settings = Settings()

# .env file
APP_NAME=My FastAPI App
DEBUG=true
DATABASE_URL=sqlite:///./test.db
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use Spring Initializr for quick project setup
- Leverage Spring Boot's auto-configuration
- Use profiles for different environments (dev, prod, test)

### 🐍 Python
- Always use virtual environments for dependency isolation
- Use Pydantic for configuration validation
- Consider using Poetry for advanced dependency management

---

💡 **Extra Examples**

```java
// Java - Main Application Class
@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

```python
# Python - Main Application
from fastapi import FastAPI
from config import settings

app = FastAPI(title=settings.app_name)

@app.get("/")
async def root():
    return {"message": "Hello World"}

# Run with: uvicorn main:app --reload
```
