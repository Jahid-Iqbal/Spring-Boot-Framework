# @Qualifier
>When a class has dependencies on multiple candidates then you can select the candidate by using the name of that candidate using annotation @Qualifier.

**Example:**
```java
public interface SortAlgo {
	public int[] sort(int[] numbers);

}

@Component
@Qualifier("bubble")
public class BubbleSort implements SortAlgo{

	@Override
	public int[] sort(int[] numbers) {
		return numbers;
	}
}

@Component
@Qualifier("quick")
public class QuickSort implements SortAlgo{

	@Override
	public int[] sort(int[] numbers) {
		return numbers;
	}
}

@Component
public class BinarySearch {
	
	@Autowired
    @Qualifier("bubble")
	private SortAlgo sa;

	public int searchNumber(int[] numbers) {
		
		System.out.println(sa);     //com.crud.springboot.BubbleSort@5b022357
		
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