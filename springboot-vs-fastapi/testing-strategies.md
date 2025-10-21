# 🧪 Java vs Python — Testing Strategies Cheat Sheet

Comparison of testing approaches and frameworks between Spring Boot and FastAPI

---

<table>
<tr>
<th>Testing Aspect</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Unit Testing</strong></td>
<td>

```java
// UserServiceTest.java
@ExtendWith(MockitoExtension.class)
class UserServiceTest {
    
    @Mock
    private UserRepository userRepository;
    
    @InjectMocks
    private UserService userService;
    
    @Test
    void shouldReturnUserWhenValidId() {
        // Given
        Long userId = 1L;
        User expectedUser = new User("John", "john@example.com");
        when(userRepository.findById(userId)).thenReturn(Optional.of(expectedUser));
        
        // When
        User actualUser = userService.findById(userId);
        
        // Then
        assertThat(actualUser).isNotNull();
        assertThat(actualUser.getName()).isEqualTo("John");
        verify(userRepository).findById(userId);
    }
    
    @Test
    void shouldThrowExceptionWhenUserNotFound() {
        // Given
        Long userId = 999L;
        when(userRepository.findById(userId)).thenReturn(Optional.empty());
        
        // When & Then
        assertThatThrownBy(() -> userService.findById(userId))
            .isInstanceOf(UserNotFoundException.class)
            .hasMessage("User not found");
    }
}
```

</td>
<td>

```python
# test_user_service.py
import pytest
from unittest.mock import Mock, patch
from user_service import UserService
from user_repository import UserRepository

class TestUserService:
    
    @pytest.fixture
    def mock_repository(self):
        return Mock(spec=UserRepository)
    
    @pytest.fixture
    def user_service(self, mock_repository):
        return UserService(mock_repository)
    
    def test_should_return_user_when_valid_id(self, user_service, mock_repository):
        # Given
        user_id = 1
        expected_user = User(id=1, name="John", email="john@example.com")
        mock_repository.find_by_id.return_value = expected_user
        
        # When
        actual_user = user_service.find_by_id(user_id)
        
        # Then
        assert actual_user is not None
        assert actual_user.name == "John"
        mock_repository.find_by_id.assert_called_once_with(user_id)
    
    def test_should_raise_exception_when_user_not_found(self, user_service, mock_repository):
        # Given
        user_id = 999
        mock_repository.find_by_id.return_value = None
        
        # When & Then
        with pytest.raises(HTTPException) as exc_info:
            user_service.find_by_id(user_id)
        
        assert exc_info.value.status_code == 404
```

</td>
</tr>
<tr>
<td><strong>Integration Testing</strong></td>
<td>

```java
// UserControllerIntegrationTest.java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
@AutoConfigureTestDatabase(replace = AutoConfigureTestDatabase.Replace.ANY)
@TestPropertySource(locations = "classpath:application-test.properties")
class UserControllerIntegrationTest {
    
    @Autowired
    private TestRestTemplate restTemplate;
    
    @Autowired
    private UserRepository userRepository;
    
    @Test
    void shouldCreateUserSuccessfully() {
        // Given
        UserCreateRequest request = new UserCreateRequest("John", "john@example.com");
        
        // When
        ResponseEntity<UserResponse> response = restTemplate.postForEntity(
            "/api/users", request, UserResponse.class);
        
        // Then
        assertThat(response.getStatusCode()).isEqualTo(HttpStatus.CREATED);
        assertThat(response.getBody().getName()).isEqualTo("John");
        
        // Verify in database
        List<User> users = userRepository.findAll();
        assertThat(users).hasSize(1);
        assertThat(users.get(0).getName()).isEqualTo("John");
    }
    
    @Test
    void shouldReturnAllUsers() {
        // Given
        userRepository.save(new User("John", "john@example.com"));
        userRepository.save(new User("Jane", "jane@example.com"));
        
        // When
        ResponseEntity<UserResponse[]> response = restTemplate.getForEntity(
            "/api/users", UserResponse[].class);
        
        // Then
        assertThat(response.getStatusCode()).isEqualTo(HttpStatus.OK);
        assertThat(response.getBody()).hasSize(2);
    }
}
```

</td>
<td>

```python
# test_user_endpoints.py
import pytest
from fastapi.testclient import TestClient
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker
from main import app, get_db
from database import Base

# Test database setup
SQLALCHEMY_DATABASE_URL = "sqlite:///./test.db"
engine = create_engine(SQLALCHEMY_DATABASE_URL, connect_args={"check_same_thread": False})
TestingSessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)

def override_get_db():
    try:
        db = TestingSessionLocal()
        yield db
    finally:
        db.close()

app.dependency_overrides[get_db] = override_get_db
client = TestClient(app)

@pytest.fixture(scope="function")
def setup_database():
    Base.metadata.create_all(bind=engine)
    yield
    Base.metadata.drop_all(bind=engine)

def test_create_user_successfully(setup_database):
    # Given
    user_data = {"name": "John", "email": "john@example.com"}
    
    # When
    response = client.post("/api/users", json=user_data)
    
    # Then
    assert response.status_code == 201
    assert response.json()["name"] == "John"
    
    # Verify in database
    response = client.get("/api/users")
    assert len(response.json()) == 1

def test_get_all_users(setup_database):
    # Given
    client.post("/api/users", json={"name": "John", "email": "john@example.com"})
    client.post("/api/users", json={"name": "Jane", "email": "jane@example.com"})
    
    # When
    response = client.get("/api/users")
    
    # Then
    assert response.status_code == 200
    assert len(response.json()) == 2
```

</td>
</tr>
<tr>
<td><strong>Test Configuration</strong></td>
<td>

```java
// application-test.properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driver-class-name=org.h2.Driver
spring.jpa.hibernate.ddl-auto=create-drop
spring.jpa.show-sql=true
logging.level.org.springframework.web=DEBUG

// Test Configuration Class
@TestConfiguration
public class TestConfig {
    
    @Bean
    @Primary
    public PasswordEncoder testPasswordEncoder() {
        return new BCryptPasswordEncoder();
    }
    
    @Bean
    @Primary
    public Clock testClock() {
        return Clock.fixed(Instant.parse("2023-01-01T00:00:00Z"), ZoneOffset.UTC);
    }
}

// Base Test Class
@SpringBootTest
@ActiveProfiles("test")
@Transactional
@Rollback
public abstract class BaseIntegrationTest {
    
    @Autowired
    protected TestRestTemplate restTemplate;
    
    @Autowired
    protected UserRepository userRepository;
    
    @BeforeEach
    void setUp() {
        userRepository.deleteAll();
    }
}
```

</td>
<td>

```python
# conftest.py
import pytest
from fastapi.testclient import TestClient
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker
from main import app, get_db
from database import Base

# Test database configuration
SQLALCHEMY_DATABASE_URL = "sqlite:///./test.db"
engine = create_engine(SQLALCHEMY_DATABASE_URL, connect_args={"check_same_thread": False})
TestingSessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)

@pytest.fixture(scope="session")
def test_db():
    Base.metadata.create_all(bind=engine)
    yield
    Base.metadata.drop_all(bind=engine)

@pytest.fixture
def db_session(test_db):
    connection = engine.connect()
    transaction = connection.begin()
    session = TestingSessionLocal(bind=connection)
    yield session
    session.close()
    transaction.rollback()
    connection.close()

@pytest.fixture
def client(db_session):
    def override_get_db():
        yield db_session
    
    app.dependency_overrides[get_db] = override_get_db
    with TestClient(app) as test_client:
        yield test_client
    app.dependency_overrides.clear()

# pytest.ini
[tool:pytest]
testpaths = tests
python_files = test_*.py
python_classes = Test*
python_functions = test_*
addopts = -v --tb=short
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `@SpringBootTest` for integration tests
- Leverage `TestRestTemplate` for HTTP testing
- Use `@MockBean` for mocking Spring beans
- Use `@Transactional` and `@Rollback` for test isolation

### 🐍 Python
- Use `pytest` as the primary testing framework
- Use `TestClient` from FastAPI for HTTP testing
- Use `pytest.fixture` for test setup and teardown
- Use `unittest.mock` for mocking dependencies

---

💡 **Extra Examples**

```java
// Java - Performance Testing
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
class PerformanceTest {
    
    @Test
    @Timeout(value = 5, unit = TimeUnit.SECONDS)
    void shouldRespondWithinTimeLimit() {
        // Performance test implementation
        ResponseEntity<String> response = restTemplate.getForEntity("/api/users", String.class);
        assertThat(response.getStatusCode()).isEqualTo(HttpStatus.OK);
    }
}
```

```python
# Python - Performance Testing
import time
import pytest

def test_response_time_performance(client):
    start_time = time.time()
    response = client.get("/api/users")
    end_time = time.time()
    
    assert response.status_code == 200
    assert (end_time - start_time) < 1.0  # Should respond within 1 second
```
