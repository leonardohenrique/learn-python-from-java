# 🛣️ Java vs Python — Routing & Endpoints Cheat Sheet

Comparison of HTTP routing and endpoint creation between Spring Boot and FastAPI

---

<table>
<tr>
<th>Routing Aspect</th>
<th>Java 🟦</th>
<th>Python 🐍</th>
</tr>
<tr>
<td><strong>Basic GET Endpoint</strong></td>
<td>

```java
@RestController
@RequestMapping("/api")
public class UserController {
    
    @GetMapping("/users")
    public List<User> getUsers() {
        return userService.findAll();
    }
    
    @GetMapping("/users/{id}")
    public User getUser(@PathVariable Long id) {
        return userService.findById(id);
    }
}
```

</td>
<td>

```python
from fastapi import FastAPI, Path
from typing import List

app = FastAPI()

@app.get("/api/users")
async def get_users():
    return user_service.find_all()

@app.get("/api/users/{user_id}")
async def get_user(user_id: int = Path(..., gt=0)):
    return user_service.find_by_id(user_id)
```

</td>
</tr>
<tr>
<td><strong>POST with Request Body</strong></td>
<td>

```java
@PostMapping("/users")
public ResponseEntity<User> createUser(@RequestBody @Valid User user) {
    User savedUser = userService.save(user);
    return ResponseEntity.status(HttpStatus.CREATED)
                        .body(savedUser);
}

@PostMapping("/users/{id}/posts")
public Post createPost(@PathVariable Long id, 
                      @RequestBody @Valid Post post) {
    return postService.createPost(id, post);
}
```

</td>
<td>

```python
from pydantic import BaseModel
from fastapi import HTTPException, status

class UserCreate(BaseModel):
    name: str
    email: str

@app.post("/api/users", status_code=201)
async def create_user(user: UserCreate):
    return user_service.create(user)

@app.post("/api/users/{user_id}/posts")
async def create_post(user_id: int, post: PostCreate):
    return post_service.create_post(user_id, post)
```

</td>
</tr>
<tr>
<td><strong>Query Parameters</strong></td>
<td>

```java
@GetMapping("/users")
public List<User> getUsers(
    @RequestParam(defaultValue = "0") int page,
    @RequestParam(defaultValue = "10") int size,
    @RequestParam(required = false) String name) {
    
    return userService.findUsers(page, size, name);
}

@GetMapping("/search")
public List<User> searchUsers(@RequestParam Map<String, String> params) {
    return userService.search(params);
}
```

</td>
<td>

```python
from typing import Optional

@app.get("/api/users")
async def get_users(
    page: int = 0,
    size: int = 10,
    name: Optional[str] = None
):
    return user_service.find_users(page, size, name)

@app.get("/api/search")
async def search_users(**params: str):
    return user_service.search(params)
```

</td>
</tr>
</table>

---

## 🧩 Quick Tips

### ☕ Java
- Use `@RestController` for REST APIs
- Leverage `@Valid` for automatic validation
- Use `ResponseEntity` for custom HTTP status codes
- Group endpoints with `@RequestMapping` at class level

### 🐍 Python
- Use Pydantic models for request/response validation
- Leverage type hints for automatic documentation
- Use `status_code` parameter for HTTP status codes
- Use `Path()` and `Query()` for parameter validation

---

💡 **Extra Examples**

```java
// Java - Advanced Routing
@RestController
@RequestMapping("/api/v1")
@Validated
public class AdvancedController {
    
    @GetMapping(value = "/users", produces = MediaType.APPLICATION_JSON_VALUE)
    public ResponseEntity<Page<User>> getUsers(
        @RequestParam(defaultValue = "0") int page,
        @RequestParam(defaultValue = "10") int size,
        @RequestParam(defaultValue = "id") String sort) {
        
        Pageable pageable = PageRequest.of(page, size, Sort.by(sort));
        Page<User> users = userService.findAll(pageable);
        return ResponseEntity.ok(users);
    }
}
```

```python
# Python - Advanced Routing
from fastapi import Query, Depends
from typing import List

@app.get("/api/v1/users", response_model=List[UserResponse])
async def get_users(
    page: int = Query(0, ge=0),
    size: int = Query(10, ge=1, le=100),
    sort: str = Query("id", regex="^(id|name|email)$")
):
    return user_service.find_all(page, size, sort)
```
