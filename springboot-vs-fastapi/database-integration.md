# 🗄️ Java vs Python — Database Integration Cheat Sheet

Comparison of database integration and ORM usage between Spring Boot and FastAPI

---

<table>
<tr>
<th>Database Aspect</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Entity/Model Definition</strong></td>
<td>

```java
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false, unique = true)
    private String email;
    
    @Column(nullable = false)
    private String name;
    
    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL)
    private List<Post> posts = new ArrayList<>();
    
    // Constructors, getters, setters
}
```

</td>
<td>

```python
from sqlalchemy import Column, Integer, String, ForeignKey
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import relationship

Base = declarative_base()

class User(Base):
    __tablename__ = "users"
    
    id = Column(Integer, primary_key=True, index=True)
    email = Column(String, unique=True, index=True, nullable=False)
    name = Column(String, nullable=False)
    
    posts = relationship("Post", back_populates="user")

# Pydantic models for API
class UserBase(BaseModel):
    email: str
    name: str

class UserCreate(UserBase):
    pass

class UserResponse(UserBase):
    id: int
    class Config:
        from_attributes = True
```

</td>
</tr>
<tr>
<td><strong>Repository/DAO Layer</strong></td>
<td>

```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    
    List<User> findByNameContainingIgnoreCase(String name);
    
    Optional<User> findByEmail(String email);
    
    @Query("SELECT u FROM User u WHERE u.name LIKE %:name%")
    List<User> findUsersByName(@Param("name") String name);
    
    @Modifying
    @Query("UPDATE User u SET u.name = :name WHERE u.id = :id")
    int updateUserName(@Param("id") Long id, @Param("name") String name);
}
```

</td>
<td>

```python
from sqlalchemy.orm import Session
from typing import List, Optional

class UserRepository:
    def __init__(self, db: Session):
        self.db = db
    
    def find_all(self) -> List[User]:
        return self.db.query(User).all()
    
    def find_by_id(self, user_id: int) -> Optional[User]:
        return self.db.query(User).filter(User.id == user_id).first()
    
    def find_by_email(self, email: str) -> Optional[User]:
        return self.db.query(User).filter(User.email == email).first()
    
    def find_by_name_containing(self, name: str) -> List[User]:
        return self.db.query(User).filter(
            User.name.contains(name)
        ).all()
    
    def create(self, user: UserCreate) -> User:
        db_user = User(**user.dict())
        self.db.add(db_user)
        self.db.commit()
        self.db.refresh(db_user)
        return db_user
```

</td>
</tr>
<tr>
<td><strong>Service Layer</strong></td>
<td>

```java
@Service
@Transactional
public class UserService {
    
    @Autowired
    private UserRepository userRepository;
    
    public List<User> findAll() {
        return userRepository.findAll();
    }
    
    public User findById(Long id) {
        return userRepository.findById(id)
            .orElseThrow(() -> new UserNotFoundException("User not found"));
    }
    
    public User save(User user) {
        if (userRepository.existsByEmail(user.getEmail())) {
            throw new EmailAlreadyExistsException("Email already exists");
        }
        return userRepository.save(user);
    }
    
    public void deleteById(Long id) {
        if (!userRepository.existsById(id)) {
            throw new UserNotFoundException("User not found");
        }
        userRepository.deleteById(id);
    }
}
```

</td>
<td>

```python
from fastapi import HTTPException, status
from typing import List, Optional

class UserService:
    def __init__(self, user_repo: UserRepository):
        self.user_repo = user_repo
    
    def find_all(self) -> List[User]:
        return self.user_repo.find_all()
    
    def find_by_id(self, user_id: int) -> User:
        user = self.user_repo.find_by_id(user_id)
        if not user:
            raise HTTPException(
                status_code=status.HTTP_404_NOT_FOUND,
                detail="User not found"
            )
        return user
    
    def create(self, user_data: UserCreate) -> User:
        if self.user_repo.find_by_email(user_data.email):
            raise HTTPException(
                status_code=status.HTTP_400_BAD_REQUEST,
                detail="Email already exists"
            )
        return self.user_repo.create(user_data)
    
    def delete(self, user_id: int) -> None:
        user = self.find_by_id(user_id)
        self.user_repo.delete(user_id)
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `@Transactional` for automatic transaction management
- Leverage Spring Data JPA for CRUD operations
- Use `@Query` for custom SQL queries
- Implement custom exceptions for better error handling

### 🐍 Python
- Use SQLAlchemy for ORM and Alembic for migrations
- Separate Pydantic models for API from SQLAlchemy models
- Use dependency injection for database sessions
- Implement proper error handling with HTTPException

---

💡 **Extra Examples**

```java
// Java - Database Configuration
@Configuration
@EnableJpaRepositories
public class DatabaseConfig {
    
    @Bean
    @ConfigurationProperties("spring.datasource")
    public DataSource dataSource() {
        return DataSourceBuilder.create().build();
    }
    
    @Bean
    public LocalContainerEntityManagerFactoryBean entityManagerFactory() {
        LocalContainerEntityManagerFactoryBean em = new LocalContainerEntityManagerFactoryBean();
        em.setDataSource(dataSource());
        em.setPackagesToScan("com.example.entity");
        em.setJpaVendorAdapter(new HibernateJpaVendorAdapter());
        return em;
    }
}
```

```python
# Python - Database Configuration
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker
from config import settings

engine = create_engine(settings.database_url)
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

# Dependency injection in FastAPI
@app.get("/users/{user_id}")
async def get_user(user_id: int, db: Session = Depends(get_db)):
    user_repo = UserRepository(db)
    user_service = UserService(user_repo)
    return user_service.find_by_id(user_id)
```
