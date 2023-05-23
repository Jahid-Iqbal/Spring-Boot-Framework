# Tight Coupling
> When a code snippet is directly dependent on other code/ class, if any changes happened in a class that directly impacts on other class/codes is called tightly coupled.

In below example `BinarySearch.searchNumbers()` is directly dependent on `BubbleSort.sort()` function. So, the relation between them is tight coupling.
```java
public class BinarySearch {
	public int searchNumber(int[] numbers) {
		
		BubbleSort bs= new BubbleSort();
		bs.sort(numbers);
		
		return 3;
	}
```

```java
public class BubbleSort {
	
	public int[] sort(int[] numbers) {
		return numbers;
	} 
```