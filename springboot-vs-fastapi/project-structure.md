# 📁 Java vs Python — Project Structure Cheat Sheet

Comparison of project structure and organization between Spring Boot and FastAPI frameworks

---

<table>
<tr>
<th>Structure Component</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Project Root</strong></td>
<td>

```java
my-spring-app/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/
│   │   │       └── MySpringApp.java
│   │   └── resources/
│   │       ├── application.properties
│   │       └── static/
│   └── test/
│       └── java/
├── pom.xml
└── README.md
```

</td>
<td>

```python
my-fastapi-app/
├── app/
│   ├── __init__.py
│   ├── main.py
│   ├── models/
│   ├── routers/
│   └── services/
├── requirements.txt
├── .env
└── README.md
```

</td>
</tr>
<tr>
<td><strong>Configuration Files</strong></td>
<td>

```java
// application.properties
server.port=8080
spring.datasource.url=jdbc:h2:mem:testdb
spring.jpa.hibernate.ddl-auto=create-drop

// pom.xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

</td>
<td>

```python
# .env
DATABASE_URL=sqlite:///./test.db
SECRET_KEY=your-secret-key

# requirements.txt
fastapi==0.104.1
uvicorn==0.24.0
sqlalchemy==2.0.23
```

</td>
</tr>
<tr>
<td><strong>Main Application Class</strong></td>
<td>

```java
@SpringBootApplication
public class MySpringApp {
    public static void main(String[] args) {
        SpringApplication.run(MySpringApp.class, args);
    }
}
```

</td>
<td>

```python
from fastapi import FastAPI

app = FastAPI(title="My FastAPI App")

@app.get("/")
def read_root():
    return {"Hello": "World"}

if __name__ == "__main__":
    import uvicorn
    uvicorn.run(app, host="0.0.0.0", port=8000)
```

</td>
</tr>
<tr>
<td><strong>Package Structure</strong></td>
<td>

```java
com.example.myapp/
├── controller/
│   └── UserController.java
├── service/
│   └── UserService.java
├── repository/
│   └── UserRepository.java
├── model/
│   └── User.java
└── config/
    └── DatabaseConfig.java
```

</td>
<td>

```python
app/
├── routers/
│   └── users.py
├── services/
│   └── user_service.py
├── models/
│   └── user.py
├── database/
│   └── connection.py
└── schemas/
    └── user_schema.py
```

</td>
</tr>
<tr>
<td><strong>Dependency Management</strong></td>
<td>

```java
// Maven (pom.xml)
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>

// Gradle (build.gradle)
implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
```

</td>
<td>

```python
# requirements.txt
fastapi==0.104.1
sqlalchemy==2.0.23
alembic==1.12.1

# pyproject.toml (modern approach)
[tool.poetry.dependencies]
fastapi = "^0.104.1"
sqlalchemy = "^2.0.23"
```

</td>
</tr>
<tr>
<td><strong>Environment Configuration</strong></td>
<td>

```java
// application-dev.properties
spring.datasource.url=jdbc:postgresql://localhost:5432/devdb

// application-prod.properties
spring.datasource.url=jdbc:postgresql://prod-server:5432/proddb

// @Profile("dev")
@Configuration
public class DevConfig { }
```

</td>
<td>

```python
# .env.development
DATABASE_URL=postgresql://user:pass@localhost/devdb

# .env.production
DATABASE_URL=postgresql://user:pass@prod-server/proddb

# config.py
import os
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    database_url: str = "sqlite:///./test.db"
    
    class Config:
        env_file = ".env"
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use Maven or Gradle for dependency management
- Follow standard Maven directory layout (src/main/java, src/test/java)
- Leverage Spring Boot's auto-configuration for rapid setup
- Use profiles for environment-specific configurations

### 🐍 Python
- Use virtual environments (venv, conda, or poetry)
- Follow PEP 8 naming conventions
- Use requirements.txt or pyproject.toml for dependencies
- Leverage FastAPI's automatic OpenAPI documentation

---

💡 **Extra Examples**

```java
// Java - Multi-module Maven project
parent-project/
├── pom.xml
├── common-module/
│   └── pom.xml
├── web-module/
│   └── pom.xml
└── service-module/
    └── pom.xml
```

```python
# Python - Package structure with __init__.py
my_package/
├── __init__.py
├── core/
│   ├── __init__.py
│   └── business_logic.py
├── api/
│   ├── __init__.py
│   └── endpoints.py
└── utils/
    ├── __init__.py
    └── helpers.py
```
