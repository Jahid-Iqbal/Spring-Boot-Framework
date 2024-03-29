# JUnit Testing

Write a test code to check the result of `sum()` method.

**Source Code:**
```java
package com.JUnitTest;

public class SumArray {
	
	public int sum(int[] numbers) {
		int sum=0;
		for(int x:numbers) {
			sum+=x;
		}
		return sum;
	}
}
```

**Test Code:**  
`test()` provides green bar as the expected and actual values are same.  
`test2()` provides error as the expected and actual values are not same.
```java
package com.JUnitTest;

import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;

class SumArrayTest {

	SumArray sa=new SumArray();
	@Test
	void test() {
		int result= sa.sum(new int[] {1,2,3});	//Green Bar
		assertEquals(6,result);					//assertEqulas(expected, actual)
	}
	
	@Test
	void test2() {
		assertEquals(11,sa.sum(new int[] {1,2,3,4}));	//org.opentest4j.AssertionFailedError: expected: <11> but was: <10>
	}
}
```

### Important Annotations:
**`@BeforeEach:`**  
Run the method before running each @Test method.   

**`@AfterEach:`**:  
Run the method after running each @Test method.   

**`@BeforeAll:`**  
Run the method before running any method.   

**`@AfterAll:`**  
Run the method after running any method.   

```java
package com.JUnitTest;

import static org.junit.jupiter.api.Assertions.*;

import org.junit.After;
import org.junit.AfterClass;
import org.junit.Before;
import org.junit.BeforeClass;
import org.junit.jupiter.api.AfterAll;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeAll;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

class SumArrayTest {

	SumArray sa=new SumArray();
	
	@BeforeEach
	void before() {
		System.out.println("Before");
	}
	
	@AfterEach
	void after() {
		System.out.println("After");
	}
	
	@BeforeAll
	static void beforeClass() {
		System.out.println("Before All");
	}
	
	@AfterAll
	static void afterClass() {
		System.out.println("After All");
	}
	
	@Test
	void test1() {
		System.out.println("Test01");
		assertEquals(6,sa.sum(new int[] {1,2,3}));
	}
	
	@Test
	void test2() {
		System.out.println("Test02");
		assertEquals(10,sa.sum(new int[] {1,2,3,4}));
	}
}
```
**Output:**  
```java
Before Class    //@BeforeAll
Before          //@BeforeEach
Test01          //Test
After           //@AfterEach
Before          //@BeforeEach
Test02          //Test
After           //@AfterEach
After Class     //@AfterAll
```

### Spring-boot testing using JUnit

```java
//Source folder
package com.crud.springboot.basic;

import javax.annotation.PostConstruct;
import javax.annotation.PreDestroy;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.beans.factory.config.ConfigurableBeanFactory;
import org.springframework.context.annotation.Scope;
import org.springframework.stereotype.Component;

@Component
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public class BinarySearch {
	
	private Logger logger= LoggerFactory.getLogger(this.getClass());
	
	@Autowired
	@Qualifier("bubble")
	private SortAlgo sortAlgo;

	public int searchNumber(int[] numbers) {
		System.out.println(sortAlgo);	
		return 3;
	}
}

//Test folder
package com.crud.springboot.basic;	//package name should be same as the source folder

import static org.junit.Assert.*;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringRunner;

import com.crud.springboot.PracticeProjectApplication;

@RunWith(SpringRunner.class)
@ContextConfiguration(classes=PracticeProjectApplication.class)
public class BinarySearchTest {
	
	@Autowired
	BinarySearch bs;

	@Test
	public void test() {

		int res= bs.searchNumber(new int[] {1,2,3} );
		assertEquals(3,res);
	}

}

```
