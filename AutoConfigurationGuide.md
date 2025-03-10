# Creating Custom Auto-Configuration in Spring Boot

## What is Auto-Configuration?

Auto-configuration allows Spring Boot to automatically configure beans based on:
- Dependencies on the classpath
- Existing beans in the application context
- Property settings

## When to Use Custom Auto-Configuration?

Use custom auto-configurations when:
- You have reusable functionality that should be conditionally enabled
- You're building a library or starter for others to use
- You want to provide sensible defaults with customization options

## Steps to Create Custom Auto-Configuration

### Step 1: Define Your Service

Create the service interface and implementation:

```java
public interface GreetingService {
    String greet(String name);
}

public class DefaultGreetingService implements GreetingService {
    private final String greeting;

    public DefaultGreetingService(String greeting) {
        this.greeting = greeting;
    }

    @Override
    public String greet(String name) {
        return greeting + ", " + name + "!";
    }
}
```

### Step 2: Create Configuration Properties

Define properties for customization:

```java
@ConfigurationProperties(prefix = "greeting")
public class GreetingProperties {
    private String message = "Hello";

    public String getMessage() {
        return message;
    }

    public void setMessage(String message) {
        this.message = message;
    }
}
```

### Step 3: Create Auto-Configuration Class

Create the auto-configuration class with conditions:

```java
@Configuration
@EnableConfigurationProperties(GreetingProperties.class)
@ConditionalOnClass(GreetingService.class)
public class GreetingAutoConfiguration {

    @Bean
    @ConditionalOnMissingBean
    public GreetingService greetingService(GreetingProperties properties) {
        return new DefaultGreetingService(properties.getMessage());
    }
}
```

### Step 4: Register Auto-Configuration

For Spring Boot 2.7 and earlier:

```
META-INF/spring.factories

org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
com.example.greeting.GreetingAutoConfiguration
```

For Spring Boot 3.0 and later:

```
META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports

com.example.greeting.GreetingAutoConfiguration
```

### Step 5: Add Auto-Configuration Metadata (Optional)

```
META-INF/spring-autoconfigure-metadata.properties

com.example.greeting.GreetingAutoConfiguration.ConditionalOnClass=com.example.greeting.GreetingService
```

## Testing Auto-Configurations

### Unit Testing

```java
@Test
void testDefaultGreetingService() {
    DefaultGreetingService service = new DefaultGreetingService("Hello");
    assertEquals("Hello, World!", service.greet("World"));
}
```

### Integration Testing

```java
@SpringBootTest(classes = GreetingAutoConfiguration.class)
class GreetingAutoConfigurationTest {

    @Autowired
    private GreetingService greetingService;

    @Test
    void defaultGreetingService() {
        assertEquals("Hello, World!", greetingService.greet("World"));
    }
}
```

## Best Practices

- Follow naming conventions
- Provide sensible defaults
- Allow customization
- Use appropriate conditions
- Keep auto-configurations focused
- Add metadata for performance and IDE support
- Test thoroughly

## Conclusion

Creating custom auto-configurations allows you to encapsulate complex configuration logic, provide reusable components, and build modular applications. Follow these guidelines to create robust auto-configurations that integrate seamlessly with Spring Boot. 