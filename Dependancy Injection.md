# Dependency Injection
>Dependency injection is a design pattern that removes  the dependency of the programs. 

**Why Dependency Injection is required?**
- It makes the code loosely coupled.
- Easy to perform testing. We can create a mock object of each class and do testing as required.

`Students std= new Students();`

If you instantiate any object using `new` keyword then that will be tightly coupled. To solve this problem dependency injection is used.

**Example:**  
Think about an Apple laptop. Apple may buy hard drives from Hitachi, processor from Intel. If we create dependency as like,

```java
Class AppleLaptop{
    Hitachi hdd= new Hitachi();
}
```
Here, in any case of changing the hdd company then directly `AppleLaptop` class need to be modified which is called tight coupling. So, the problem can be solved using below technique.

```java
@Component
Class AppleLaptop{
    
    @Autowired
    HardDrive hd;
}

Interface HardDrive{

}

Class Hitachi implements HardDrive{

}
```
Here, If the hard drive company needs to be changed then just change the Hitachi class. No need to change in any other class or code. This scenario is called loose coupling.