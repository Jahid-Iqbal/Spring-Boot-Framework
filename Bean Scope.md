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

## Complex Scope Scenario- Mix prototype and singleton

The sub class has a scope prototype and the dependent class has a scope singleton.

```java
@Component
@Scope(value=ConfigurableBeanFactory.SCOPE_PROTOTYPE, proxyMode=ScopedProxyMode.TARGET_CLASS)
public class JdbcConnection {
	
	public JdbcConnection() {
		System.out.println("Jdbc Connection");
	}

}


@Component
//@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public class PersonDao {
	
	@Autowired
	public JdbcConnection jdbc;

	public JdbcConnection getJdbc() {
		return jdbc;
	}

	public void setJdbc(JdbcConnection jdbc) {
		this.jdbc = jdbc;
	}

}

@SpringBootApplication
public class PracticeProjectScopeApplication {

	private static Logger logger= LoggerFactory.getLogger(PracticeProjectScopeApplication.class);
	
	public static void main(String[] args) {

		ApplicationContext ac=SpringApplication.run(PracticeProjectScopeApplication.class, args);
		
		PersonDao person= ac.getBean(PersonDao.class);
		PersonDao person2= ac.getBean(PersonDao.class);
		
		logger.info("{}",person);			//PersonDao@1f1cae23
		logger.info("{}",person.getJdbc());	//JdbcConnection@1eaf1e62
		logger.info("{}",person.getJdbc());	//JdbcConnection@5631962 
		
		logger.info("{}",person2);			//PersonDao@1f1cae23
		logger.info("{}",person2.getJdbc()); //JdbcConnection@c81fd12
		
	}

}
```

## Difference between Spring Singleton and Gang of Four (GOF) Singleton

As of GOF singleton scope, an instance will be created per JVM. Meaning what ever the situation is a program is running on a single JVM and it creates a single instance per JVM.

As of Spring singleton, an instance is created per ApplicationContext. If a program contains multiple ApplicationContext then single instance will be created for each ApplicationContext.