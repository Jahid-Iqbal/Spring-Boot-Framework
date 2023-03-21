# @Component

When we annotated a class with @Component than a instance of that class is being created and bring that instance/ object/ bean inside the IoC container.

**Example:**  
In below example the class BubbleSortAlgo is annotated with @Component. So, an instance is created as `bubbleSortAlgo`. So, we can access that object by name.

```java
import org.springframework.stereotype.Component;

@Component      //Creating the instance as bubbleSortAlgo
public class BubbleSortAlgo implements SortAlgo{

}
@Component
public class BinarySearch {

    @Autowired
    private SortAlgo bubbleSortAlgo;    //Using the instance od BubbleSortAlgo class.
}
```
