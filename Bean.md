# Bean
>Bean is nothing but an instance or object.

```java
BubbleSort bubble= new BubbleSort();
```
Here, `bubble` is a instance/ object of `BubbleSort` class. So `bubble` is also called as Bean.

`@SpringBootApplication` annotation scans for the beans inside that package and sub-packages. So, we don't need to add `@ComponentScan` annotation externally.