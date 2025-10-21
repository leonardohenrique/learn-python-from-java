# 📦 Java vs Python — External Packages Cheat Sheet

Comparison of external package management and dependency handling between Java and Python

---

<table>
<tr>
<th>Concept</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Package Manager</strong></td>
<td>

```java
// Maven - pom.xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>my-project</artifactId>
    <version>1.0.0</version>
    
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <version>2.7.0</version>
        </dependency>
    </dependencies>
</project>

// Gradle - build.gradle
plugins {
    id 'java'
    id 'org.springframework.boot' version '2.7.0'
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web:2.7.0'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
}
```

</td>
<td>

```python
# pip - requirements.txt
requests==2.28.0
numpy==1.21.0
pandas==1.3.0
flask==2.2.0

# pip install
pip install requests numpy pandas flask

# pip freeze
pip freeze > requirements.txt

# Poetry - pyproject.toml
[tool.poetry]
name = "my-project"
version = "1.0.0"

[tool.poetry.dependencies]
python = "^3.8"
requests = "^2.28.0"
numpy = "^1.21.0"
```

</td>
</tr>
<tr>
<td><strong>Dependency Resolution</strong></td>
<td>

```java
// Maven dependency resolution
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.13.0</version>
</dependency>

// Exclude transitive dependencies
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <version>5.3.0</version>
    <exclusions>
        <exclusion>
            <groupId>commons-logging</groupId>
            <artifactId>commons-logging</artifactId>
        </exclusion>
    </exclusions>
</dependency>

// Dependency scope
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.2</version>
    <scope>test</scope>
</dependency>
```

</td>
<td>

```python
# pip dependency resolution
pip install requests[security]  # Extra dependencies
pip install --no-deps package  # Skip dependencies

# Poetry dependency resolution
[tool.poetry.dependencies]
requests = {version = "^2.28.0", extras = ["security"]}
numpy = "^1.21.0"

# Optional dependencies
[tool.poetry.group.dev.dependencies]
pytest = "^7.0.0"
black = "^22.0.0"

# Install with extras
pip install "requests[security]"
poetry install --with dev
```

</td>
</tr>
<tr>
<td><strong>Virtual Environments</strong></td>
<td>

```java
// Java doesn't have built-in virtual environments
// Use different approaches:

// 1. Maven profiles
<profiles>
    <profile>
        <id>dev</id>
        <dependencies>
            <dependency>
                <groupId>com.h2database</groupId>
                <artifactId>h2</artifactId>
                <scope>runtime</scope>
            </dependency>
        </dependencies>
    </profile>
    <profile>
        <id>prod</id>
        <dependencies>
            <dependency>
                <groupId>mysql</groupId>
                <artifactId>mysql-connector-java</artifactId>
                <scope>runtime</scope>
            </dependency>
        </dependencies>
    </profile>
</profiles>

// 2. Docker for isolation
FROM openjdk:17-jdk-slim
COPY target/my-app.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

</td>
<td>

```python
# Python virtual environments
# Create virtual environment
python -m venv myenv

# Activate (Windows)
myenv\Scripts\activate

# Activate (Unix/Mac)
source myenv/bin/activate

# Deactivate
deactivate

# Poetry virtual environments
poetry install  # Creates and uses virtual env
poetry shell    # Activates virtual env
poetry run python script.py  # Run in virtual env

# Conda environments
conda create -n myenv python=3.9
conda activate myenv
conda install numpy pandas
```

</td>
</tr>
<tr>
<td><strong>Package Installation</strong></td>
<td>

```java
// Maven installation
mvn clean install

// Gradle installation
gradle build

// Manual JAR installation
mvn install:install-file \
    -Dfile=my-library.jar \
    -DgroupId=com.example \
    -DartifactId=my-library \
    -Dversion=1.0.0 \
    -Dpackaging=jar

// Local repository
<repository>
    <id>local-repo</id>
    <url>file://${project.basedir}/lib</url>
</repository>
```

</td>
<td>

```python
# pip installation methods
pip install package-name                    # From PyPI
pip install package-name==1.0.0            # Specific version
pip install package-name>=1.0.0,<2.0.0     # Version range
pip install -e .                           # Editable install
pip install -r requirements.txt            # From file

# Install from different sources
pip install git+https://github.com/user/repo.git
pip install package-name --index-url https://pypi.org/simple/
pip install package-name --find-links /path/to/wheels/

# Poetry installation
poetry add package-name
poetry add package-name@^1.0.0
poetry add --dev pytest
```

</td>
</tr>
<tr>
<td><strong>Package Publishing</strong></td>
<td>

```java
// Maven publishing to Maven Central
<distributionManagement>
    <repository>
        <id>ossrh</id>
        <url>https://s01.oss.sonatype.org/service/local/staging/deploy/maven2/</url>
    </repository>
</distributionManagement>

<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-gpg-plugin</artifactId>
            <version>1.6</version>
            <executions>
                <execution>
                    <id>sign-artifacts</id>
                    <phase>verify</phase>
                    <goals>
                        <goal>sign</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>

// Deploy to Maven Central
mvn clean deploy
```

</td>
<td>

```python
# Python package publishing to PyPI
# setup.py
from setuptools import setup, find_packages

setup(
    name="my-package",
    version="1.0.0",
    packages=find_packages(),
    install_requires=["requests"],
    author="Your Name",
    author_email="your.email@example.com",
    description="A sample package",
    long_description=open("README.md").read(),
    long_description_content_type="text/markdown",
    url="https://github.com/yourusername/my-package",
    classifiers=[
        "Programming Language :: Python :: 3",
        "License :: OSI Approved :: MIT License",
    ],
)

# Build and upload
python -m build
twine upload dist/*

# Poetry publishing
poetry build
poetry publish
```

</td>
</tr>
<tr>
<td><strong>Dependency Conflicts</strong></td>
<td>

```java
// Maven dependency conflict resolution
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <version>5.3.0</version>
</dependency>

// Force specific version
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.13.0</version>
</dependency>

// Check dependency tree
mvn dependency:tree

// Resolve conflicts
mvn dependency:resolve

// Exclude conflicting dependency
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-web</artifactId>
    <version>5.3.0</version>
    <exclusions>
        <exclusion>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

</td>
<td>

```python
# pip dependency conflict resolution
# Check installed packages
pip list

# Check package dependencies
pip show package-name

# Resolve conflicts
pip install --upgrade package-name
pip install --force-reinstall package-name

# Poetry conflict resolution
poetry show --tree
poetry update
poetry lock --no-update

# pip-tools for dependency management
pip-compile requirements.in
pip-sync requirements.txt

# Check for conflicts
pip check
```

</td>
</tr>
<tr>
<td><strong>Package Caching</strong></td>
<td>

```java
// Maven local repository caching
// ~/.m2/repository/ (default location)

// Configure custom repository location
<settings>
    <localRepository>/path/to/custom/repo</localRepository>
</settings>

// Gradle caching
// ~/.gradle/caches/ (default location)

// Configure cache location
gradle.properties:
org.gradle.caching=true
org.gradle.parallel=true
```

</td>
<td>

```python
# pip caching
# ~/.cache/pip/ (default location)

# Configure cache location
pip install --cache-dir /path/to/cache package-name

# Poetry caching
# ~/.cache/pypoetry/ (default location)

# Configure cache
poetry config cache-dir /path/to/cache

# Clear cache
pip cache purge
poetry cache clear pypi --all
```

</td>
</tr>
<tr>
<td><strong>Security and Vulnerabilities</strong></td>
<td>

```java
// Maven security scanning
<plugin>
    <groupId>org.owasp</groupId>
    <artifactId>dependency-check-maven</artifactId>
    <version>7.0.0</version>
    <executions>
        <execution>
            <goals>
                <goal>check</goal>
            </goals>
        </execution>
    </executions>
</plugin>

// Run security check
mvn org.owasp:dependency-check-maven:check

// Snyk integration
snyk test
snyk monitor
```

</td>
<td>

```python
# pip security scanning
pip install safety
safety check

# Poetry security
poetry audit

# pip-audit
pip install pip-audit
pip-audit

# Snyk for Python
snyk test
snyk monitor

# GitHub Dependabot
# .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: "pip"
    directory: "/"
    schedule:
      interval: "weekly"
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use Maven or Gradle for dependency management
- Maven Central is the primary repository
- Use profiles for environment-specific dependencies
- Docker provides environment isolation

### 🐍 Python
- Use pip for simple projects, Poetry for complex ones
- Virtual environments are essential for isolation
- PyPI is the primary package repository
- Use requirements.txt or pyproject.toml for dependencies

---

💡 **Extra Examples**

```java
// Java - Complete Maven project setup
// pom.xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>my-spring-app</artifactId>
    <version>1.0.0</version>
    <packaging>jar</packaging>
    
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.7.0</version>
    </parent>
    
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
        <dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
            <scope>runtime</scope>
        </dependency>
    </dependencies>
    
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```

```python
# Python - Complete Poetry project setup
# pyproject.toml
[tool.poetry]
name = "my-fastapi-app"
version = "1.0.0"
description = "A FastAPI application"
authors = ["Your Name <your.email@example.com>"]

[tool.poetry.dependencies]
python = "^3.8"
fastapi = "^0.68.0"
uvicorn = "^0.15.0"
sqlalchemy = "^1.4.0"
alembic = "^1.7.0"

[tool.poetry.group.dev.dependencies]
pytest = "^6.2.0"
black = "^21.0.0"
flake8 = "^3.9.0"

[build-system]
requires = ["poetry-core>=1.0.0"]
build-backend = "poetry.core.masonry.api"

# requirements.txt alternative
fastapi==0.68.0
uvicorn==0.15.0
sqlalchemy==1.4.0
alembic==1.7.0
pytest==6.2.0
black==21.0.0
flake8==3.9.0
```
