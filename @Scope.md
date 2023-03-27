# @Scope

*Singleton:* Creating a single object for all instances. Let say, 3 instances are created for an object, actually the same bean/ object is used by all the instances.

```java
@Component
@Scope(ConfigurableBeanFactory.SCOPE_SINGLETON)
public class BinarySearch {
}

	public static void main(String[] args) {

		ApplicationContext ac= SpringApplication.run(SpringPracticeApplication.class, args);

		BinarySearch bn=ac.getBean(BinarySearch.class);
		BinarySearch bn1=ac.getBean(BinarySearch.class);
		BinarySearch bn2=ac.getBean(BinarySearch.class);

		System.out.println(bn);     //com.practice.demo.BinarySearch@5fe8b721
		System.out.println(bn1);    //com.practice.demo.BinarySearch@5fe8b721
		System.out.println(bn2);    //com.practice.demo.BinarySearch@5fe8b721
        
	}
```
*Prototype:* Creating individual bean/ object for each instance call.

```java
@Component
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public class BinarySearch {
}

	public static void main(String[] args) {

		ApplicationContext ac= SpringApplication.run(SpringPracticeApplication.class, args);

		BinarySearch bn=ac.getBean(BinarySearch.class);
		BinarySearch bn1=ac.getBean(BinarySearch.class);
		BinarySearch bn2=ac.getBean(BinarySearch.class);

		System.out.println(bn);     //com.practice.demo.BinarySearch@7a11c4c7
		System.out.println(bn1);    //com.practice.demo.BinarySearch@4cc547a
		System.out.println(bn2);    //com.practice.demo.BinarySearch@7555b920
        
	}
```