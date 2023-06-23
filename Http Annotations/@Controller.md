# @Controller

`@Controller` annotation makes a class as Controller in Spring MVC architecture which is responsible for managing Http request and generating appropriate response. It implements the `@Component` annotation implicitly. So, the class annotated with `@Controller` is available for `ComponentScan` mechanism.

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Component
public @interface Controller {
}
```

Within a controller class, you define methods to handle specific URLs or URL patterns using annotations like `@RequestMapping`, `@GetMapping`, `@PostMapping`, etc.

**Example:**

```java
@Controller
public class MyController {

    @GetMapping("/hello")
    public String helloWorld(Model model) {
        model.addAttribute("message", "Hello, World!");
        return "hello"; // This is the view name
    }
}
```
In this example, the `helloWorld` method is annotated with `@GetMapping` to handle HTTP `GET` requests to the "/hello" URL. It takes a Model object as a parameter, adds an attribute called "message" with the value "Hello, World!", and returns the view name "hello". Spring Boot will then render the appropriate view template (e.g., "hello.html") and send it as the response.

Remember that for the `@Controller` annotation to work in Spring Boot, you need to have the necessary dependencies, such as `Spring Web`, included in your project's build configuration.