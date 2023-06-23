# @RestController

`@RestController` combines the annotation `@Controller` and `@ResponseBody` to simplify the development of RestFul web services. Classes annotated with `@RestController` are marked as Controller in Spring MVC and responsible to manage Http request and response. Also those classes are available for `ComponentScan` mechanism.

`@RestController` is implicitly annotated with @Controller and `@ResponseBody`.

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Controller
@ResponseBody
public @interface RestController {

}
```

**Example:**
```java
@RestController
public class MyRestController {

    @GetMapping("/hello")
    public String helloWorld() {
        return "Hello, World!";
    }
}
```
In this example, the helloWorld method is annotated with @GetMapping to handle HTTP GET requests to the "/hello" URL. Since the class is annotated with `@RestController`, the @ResponseBody annotation is implicit, and the return value "Hello, World!" is directly serialized into the HTTP response body as plain text.

The `@RestController` annotation is particularly useful when developing RESTful web services where the response is primarily in the form of serialized data, such as JSON or XML. It eliminates the need to explicitly use `@ResponseBody` on every handler method within the controller class.
