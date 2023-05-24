# @Autowired

>Creating the dependencies

**Example:** Autowiring in general concept.
```java
public class BinarySearch {
	
	private SortAlgo sa;
	
	
	public BinarySearch(SortAlgo sa) {
		super();
		this.sa = sa;
	}
}


public interface SortAlgo {
	public int[] sort(int[] numbers);

}

public class BubbleSort implements SortAlgo{

	@Override
	public int[] sort(int[] numbers) {
		return numbers;
	}

public class PracticeProjectApplication {

	public static void main(String[] args) {
        BinarySearch bs= new BinarySearch(new QuickSort());
        //Class BInarySearch is dependent on QuickSort. So, these two classes are autowired.
    }
}

```

**Example:** Autowiring using annotation @Autowired in Springboot framework.

```java
@Component  //Creating a bean and bring that in IoC container
public class BinarySearch {
	
    @Autowired  //Creating the dependencies and relationship
	private SortAlgo sa;
	
	//Constructor is not required
	// public BinarySearch(SortAlgo sa) {
	// 	super();
	// 	this.sa = sa;
	// }

    	public int searchNumber(int[] numbers) {
		System.out.println(sa); //printing the object		
		return 3;
	}
}


public interface SortAlgo {
	public int[] sort(int[] numbers);

}

@Component  //Creating a bean and bring that in IoC container
public class BubbleSort implements SortAlgo{

	@Override
	public int[] sort(int[] numbers) {
		return numbers;
	}

public class PracticeProjectApplication {

	public static void main(String[] args) {
      	ApplicationContext ac=SpringApplication.run(PracticeProjectApplication.class, args);		
		BinarySearch bs= ac.getBean(BinarySearch.class);
		bs.searchNumber(new int[] {2,3,4});     //com.crud.springboot.BubbleSort@1d12b024
    }
}
```
Here, @Component is creating beans of BInarySearch and BubbleSort class. @Autowired creating the dependencies between them.

**Autowiring by Name:**  
When a bean has a dependencies on multiple beans than @Primary is being used. Another approach id autowiring bu name.

**Example:**  
```java
public interface SortAlgo {
	public int[] sort(int[] numbers);

}
//@Primary annotation is not used
@Component
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
	private SortAlgo bubbleSort;    //autowiring by name. @Component created a bean named bubbleSort of class BubbleSort.
	
	public BinarySearch(SortAlgo bubbleSort) {
		super();
		this.bubbleSort = bubbleSort;
	}


	public int searchNumber(int[] numbers) {
		System.out.println(bubbleSort);	
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