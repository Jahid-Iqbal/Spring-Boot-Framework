# @ComponentScan

`@SpringBootApplication` annotation implements `@ComponentScan` implicitly. That's why we don't require to implement that annotation explicitly but `@SpringBootApplication` annotation can search/ holds the beans of the same package. It can't find the beans of other packages. To works with the beans from other packages we need to use the annotation `@ComponentScan`.

```java
package com.crud.componentscan;

@Component
public class ComponentDao {
	
	@Autowired
	public ComponentJdbcConnection jdbc;

	public ComponentJdbcConnection getJdbc() {
		return jdbc;
	}

	public void setJdbc(ComponentJdbcConnection jdbc) {
		this.jdbc = jdbc;
	}

}

package com.crud.springboot;

@SpringBootApplication
public class PracticeProjectComponentApplication {

	private static Logger logger= LoggerFactory.getLogger(PracticeProjectComponentApplication.class);
	
	public static void main(String[] args) {

		ApplicationContext ac=SpringApplication.run(PracticeProjectComponentApplication.class, args);
		
		ComponentDao person= ac.getBean(ComponentDao.class);
		ComponentDao person2= ac.getBean(ComponentDao.class);
		
		logger.info("{}",person);
		logger.info("{}",person.getJdbc());
		
		logger.info("{}",person2);
		logger.info("{}",person2.getJdbc());
		
	}

}

//Exception in thread "main" org.springframework.beans.
//factory.NoSuchBeanDefinitionException: No qualifying 
//bean of type 'com.crud.componentscan.ComponentDao' 
//available

```
In above code, `@ComponentScan` annotation is not used and the driver class and other classes are from different packages. So, that throws an exception as `(No qualifying bean of type 'com.crud.componentscan.ComponentDao' available)`

**Example:** Now we can solve the problem using `@ComponentScan` annotation.

```java
package com.crud.componentscan;

@Component
public class ComponentDao {
	
	@Autowired
	public ComponentJdbcConnection jdbc;

	public ComponentJdbcConnection getJdbc() {
		return jdbc;
	}

	public void setJdbc(ComponentJdbcConnection jdbc) {
		this.jdbc = jdbc;
	}

}


package com.crud.springboot;

@SpringBootApplication
@ComponentScan("com.crud.componentscan")    //Import the other packages using @ComponentScan
public class PracticeProjectComponentApplication {

	private static Logger logger= LoggerFactory.getLogger(PracticeProjectComponentApplication.class);
	
	public static void main(String[] args) {

		ApplicationContext ac=SpringApplication.run(PracticeProjectComponentApplication.class, args);
		
		ComponentDao person= ac.getBean(ComponentDao.class);
		ComponentDao person2= ac.getBean(ComponentDao.class);
		
		logger.info("{}",person);
		logger.info("{}",person.getJdbc());
		
		logger.info("{}",person2);
		logger.info("{}",person2.getJdbc());	
	}
}
```
Now this code is producing expected result.