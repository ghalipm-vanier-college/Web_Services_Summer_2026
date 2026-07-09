# **Spring Security + Basic Authentication**

---

# Step 1. Add Spring Security Dependency

In `pom.xml`, add:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

Reload the Maven project.

---

# Step 2. Run the Application

Start your application again.

You'll immediately notice something changed.

If you open

```
http://localhost:8080/students
```

instead of seeing your page, you'll get

```
401 Unauthorized
```

or a login page.

That means Spring Security is already protecting your application.

---

# Step 3. Find the Generated Password

In the console you'll see something similar to

```
Using generated security password:

4f9b8f8f-4bc1-4e0e-b30d-f6c2f5...
```

Username is always

```
user
```

Password is the generated one.

---

# Step 4. Login

Open

```
http://localhost:8080/students
```

Login using

```
Username:
user

Password:
<generated password>
```

Now your application works again.

---

# Step 5. Create Your Own Username and Password

Instead of using the generated password, add to

```
application.properties
```

```properties
spring.security.user.name=admin
spring.security.user.password=admin123
```

Restart the application.

Now login with

```
Username:
admin

Password:
admin123
```

---

# Step 6. Allow CSS Without Login (Optional)

Without configuration, Spring Security may block your CSS.

Create a configuration class.

```java
package org.example.springdb.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.web.SecurityFilterChain;

@Configuration
public class SecurityConfig {

    @Bean
    SecurityFilterChain filterChain(HttpSecurity http)
            throws Exception {

        http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/css/**").permitAll()
                .anyRequest().authenticated()
            )
            .formLogin();

        return http.build();
    }
}
```

Now CSS files under

```
src/main/resources/static/css
```

will load normally.

---

# Step 7. Secure REST APIs

Suppose you have

```java
@GetMapping("/api/students")
public List<Student> getStudents() {
    return repository.findAll();
}
```

Calling

```
GET /api/students
```

without authentication returns

```
401 Unauthorized
```

After logging in, it returns

```json
[
  {
    "id":1,
    "name":"Alice"
  }
]
```

---

# Step 8. Test with Postman

Create

```
GET

http://localhost:8080/api/students
```

Choose

```
Authorization
↓

Basic Auth
```

Enter

```
Username

admin

Password

admin123
```

Click

```
Send
```

The API should now return the JSON response.

---

# Step 9. Where Does JWT Fit?

Explain the evolution like this:

```
No Security
        ↓
Spring Security
        ↓
Basic Authentication
        ↓
JWT Authentication
        ↓
OAuth2 (Google, GitHub, Microsoft Login)
```

Note that **Spring Security** is the framework, while **Basic Authentication**, **JWT**, and **OAuth2** are different authentication mechanisms built on top of it.

---
