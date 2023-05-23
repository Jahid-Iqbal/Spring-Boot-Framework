# Loose Coupling
> When a class/ code snippet is using another classes references but not directly dependent on that code or in changing a code doesn't bother another is called loose coupling.

**Example:**

```java
//Interface
public interface SortAlgo {
	public int[] sort(int[] numbers);

}

//Implementing the interface
public class BubbleSort implements SortAlgo{

	@Override
	public int[] sort(int[] numbers) {
		return numbers;
	}

//Implementing the interface
public class QuickSort implements SortAlgo{

	@Override
	public int[] sort(int[] numbers) {
		return numbers;
	}

}

//Calling the sort algo using the interface. That's how interface helps to make a code loosely coupled.
public class BinarySearch {
	
	private SortAlgo sa;
	
	
	public BinarySearch(SortAlgo sa) {
		super();
		this.sa = sa;
	}


	public int searchNumber(int[] numbers) {
		
		System.out.println(sa);
		
		return 3;
	}

}

//Using the desired sort algo to perform the BinarySearch. Making the code dynamic
@SpringBootApplication
public class PracticeProjectApplication {

	public static void main(String[] args) {
		BinarySearch bs= new BinarySearch(new QuickSort());
//		com.crud.springboot.QuickSort@3c130745
		
		BinarySearch bss= new BinarySearch(new QuickSort());
//		com.crud.springboot.BubbleSort@3c130745
		
		int res= bs.searchNumber(new int[]{1,2,3});
		System.out.print(res);

	}

}
```

