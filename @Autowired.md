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
When, @Autowired is used then no need to implement the constructor for that instance variable.