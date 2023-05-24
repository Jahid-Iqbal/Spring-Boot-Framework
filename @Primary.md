# @Primary

When a class has dependencies on multiple classes then compiler will be confused which one should be considered. So, to resolve the scenario @Primary can be used. 

**Example:**
```java
public interface SortAlgo {
	public int[] sort(int[] numbers);

}

@Component
@Primary
public class BubbleSort implements SortAlgo{

	@Override
	public int[] sort(int[] numbers) {
		return numbers;
	}
}

@Component
public class QuickSort implements SortAlgo{

	@Override
	public int[] sort(int[] numbers) {
		return numbers;
	}
}

@Component
public class BinarySearch {
	
	@Autowired
	private SortAlgo sa;
	
	
	public BinarySearch(SortAlgo sa) {
		super();
		this.sa = sa;
	}


	public int searchNumber(int[] numbers) {
		
		System.out.println(sa);     //com.crud.springboot.BubbleSort@4f186450
		
		return 3;
	}

}

@SpringBootApplication
public class PracticeProjectApplication {

	public static void main(String[] args) {
	
		ApplicationContext ac=SpringApplication.run(PracticeProjectApplication.class, args);
		
		BinarySearch bs= ac.getBean(BinarySearch.class);
		bs.searchNumber(new int[] {2,3,4});
	}

}
```
`BinarySearch` has dependencies on `BubbleSort` and `QuickSort` class via SortAlgo interface. So, compiler would be confused which bean should consider for BinarySearch. As, `@Primary` annotation is used on BubbleSort class so, compiler will consider that class as dependencies.