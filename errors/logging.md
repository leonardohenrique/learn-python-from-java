# 📝 Java vs Python — Logging Cheat Sheet

Comprehensive comparison of logging mechanisms between Java and Python, covering different logging frameworks and best practices.

---

<table>
<tr>
<th>Logging Concept</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Basic Logging Setup</strong></td>
<td>

```java
import java.util.logging.Logger;
import java.util.logging.Level;

public class MyClass {
    private static final Logger logger = 
        Logger.getLogger(MyClass.class.getName());
    
    public void doSomething() {
        logger.info("Starting operation");
        logger.warning("This is a warning");
        logger.severe("Error occurred");
    }
}
```

</td>
<td>

```python
import logging

# Basic setup
logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

def do_something():
    logger.info("Starting operation")
    logger.warning("This is a warning")
    logger.error("Error occurred")
```

</td>
</tr>
<tr>
<td><strong>Log Levels</strong></td>
<td>

```java
// Java Log Levels (in order)
logger.severe("SEVERE - System errors");
logger.warning("WARNING - Potential problems");
logger.info("INFO - General information");
logger.config("CONFIG - Configuration info");
logger.fine("FINE - Detailed tracing");
logger.finer("FINER - More detailed tracing");
logger.finest("FINEST - Most detailed tracing");
```

</td>
<td>

```python
# Python Log Levels (in order)
logger.critical("CRITICAL - System errors")
logger.error("ERROR - Serious problems")
logger.warning("WARNING - Potential issues")
logger.info("INFO - General information")
logger.debug("DEBUG - Detailed information")
```

</td>
</tr>
<tr>
<td><strong>Configuration</strong></td>
<td>

```java
// Programmatic configuration
Logger logger = Logger.getLogger("com.example");
logger.setLevel(Level.INFO);

// Console handler
ConsoleHandler consoleHandler = new ConsoleHandler();
consoleHandler.setLevel(Level.INFO);
logger.addHandler(consoleHandler);

// File handler
FileHandler fileHandler = new FileHandler("app.log");
fileHandler.setLevel(Level.WARNING);
logger.addHandler(fileHandler);
```

</td>
<td>

```python
# Programmatic configuration
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    handlers=[
        logging.FileHandler('app.log'),
        logging.StreamHandler()
    ]
)

# Or using dictConfig
import logging.config

LOGGING_CONFIG = {
    'version': 1,
    'handlers': {
        'file': {
            'class': 'logging.FileHandler',
            'filename': 'app.log',
            'level': 'INFO'
        }
    },
    'loggers': {
        '': {
            'handlers': ['file'],
            'level': 'INFO'
        }
    }
}

logging.config.dictConfig(LOGGING_CONFIG)
```

</td>
</tr>
<tr>
<td><strong>Structured Logging</strong></td>
<td>

```java
// Using SLF4J + Logback
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.slf4j.MDC;

public class StructuredLogging {
    private static final Logger logger = 
        LoggerFactory.getLogger(StructuredLogging.class);
    
    public void logWithContext() {
        MDC.put("userId", "12345");
        MDC.put("requestId", "req-abc");
        
        logger.info("User action completed", 
            kv("action", "login"), 
            kv("duration", 150));
        
        MDC.clear();
    }
}
```

</td>
<td>

```python
# Using structlog
import structlog

logger = structlog.get_logger()

def log_with_context():
    logger = logger.bind(
        user_id="12345",
        request_id="req-abc"
    )
    
    logger.info("User action completed",
        action="login",
        duration=150)
```

</td>
</tr>
<tr>
<td><strong>Exception Logging</strong></td>
<td>

```java
try {
    riskyOperation();
} catch (Exception e) {
    logger.log(Level.SEVERE, "Operation failed", e);
    // Or with SLF4J
    logger.error("Operation failed", e);
}

// With custom message
logger.error("Failed to process user {}: {}", 
    userId, e.getMessage(), e);
```

</td>
<td>

```python
try:
    risky_operation()
except Exception as e:
    logger.exception("Operation failed")
    # Or with custom message
    logger.error(f"Failed to process user {user_id}: {e}", 
                 exc_info=True)
```

</td>
</tr>
<tr>
<td><strong>Performance Logging</strong></td>
<td>

```java
// Using AOP with Spring
@Around("@annotation(LogExecutionTime)")
public Object logExecutionTime(ProceedingJoinPoint joinPoint) 
        throws Throwable {
    long startTime = System.currentTimeMillis();
    
    try {
        Object result = joinPoint.proceed();
        long executionTime = System.currentTimeMillis() - startTime;
        logger.info("Method {} executed in {} ms", 
            joinPoint.getSignature().getName(), executionTime);
        return result;
    } catch (Exception e) {
        long executionTime = System.currentTimeMillis() - startTime;
        logger.error("Method {} failed after {} ms", 
            joinPoint.getSignature().getName(), executionTime, e);
        throw e;
    }
}
```

</td>
<td>

```python
# Using decorators
import time
import functools

def log_execution_time(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        start_time = time.time()
        try:
            result = func(*args, **kwargs)
            execution_time = time.time() - start_time
            logger.info(f"Method {func.__name__} executed in {execution_time:.2f} ms")
            return result
        except Exception as e:
            execution_time = time.time() - start_time
            logger.error(f"Method {func.__name__} failed after {execution_time:.2f} ms", 
                        exc_info=True)
            raise
    return wrapper

@log_execution_time
def my_method():
    # method implementation
    pass
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use SLF4J as logging facade for better flexibility
- Configure log levels via application.properties in Spring Boot
- Use MDC (Mapped Diagnostic Context) for request tracing
- Consider using Logback or Log4j2 for better performance

### 🐍 Python
- Use `logging.config.dictConfig()` for complex configurations
- Leverage `structlog` for structured logging in production
- Use `logger.exception()` to automatically include stack traces
- Configure logging early in your application startup

---

💡 **Extra Examples**

```java
// Java - Spring Boot Logging Configuration
# application.properties
logging.level.com.example=DEBUG
logging.level.org.springframework=WARN
logging.file.name=app.log
logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} - %msg%n
logging.pattern.file=%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n

// Custom logback-spring.xml
<configuration>
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>
    
    <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>app.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>app.%d{yyyy-MM-dd}.log</fileNamePattern>
            <maxHistory>30</maxHistory>
        </rollingPolicy>
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>
    
    <root level="INFO">
        <appender-ref ref="STDOUT" />
        <appender-ref ref="FILE" />
    </root>
</configuration>
```

```python
# Python - Advanced Logging Configuration
import logging
import logging.handlers
from pathlib import Path

def setup_logging():
    # Create logs directory
    log_dir = Path("logs")
    log_dir.mkdir(exist_ok=True)
    
    # Configure root logger
    logging.basicConfig(
        level=logging.INFO,
        format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
        handlers=[
            # Console handler
            logging.StreamHandler(),
            # Rotating file handler
            logging.handlers.RotatingFileHandler(
                log_dir / "app.log",
                maxBytes=10*1024*1024,  # 10MB
                backupCount=5
            ),
            # Timed rotating file handler
            logging.handlers.TimedRotatingFileHandler(
                log_dir / "app_daily.log",
                when='midnight',
                interval=1,
                backupCount=30
            )
        ]
    )
    
    # Set specific logger levels
    logging.getLogger('requests').setLevel(logging.WARNING)
    logging.getLogger('urllib3').setLevel(logging.WARNING)

# Usage with context managers
import contextlib

@contextlib.contextmanager
def log_context(logger, level, message, **kwargs):
    logger.log(level, f"Starting: {message}", extra=kwargs)
    try:
        yield
        logger.log(level, f"Completed: {message}", extra=kwargs)
    except Exception as e:
        logger.log(level, f"Failed: {message} - {e}", extra=kwargs)
        raise

# Usage
with log_context(logger, logging.INFO, "Processing data", user_id=123):
    # Your code here
    pass
```
