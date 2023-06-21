# @RequestBody

`@RequestBody` annotation simply transfer the `HttpRequest` body which is in JSON format into a Java object.

Spring has a list of `HttpMessageConverters` registered in the background. For `@RequestBody` the responsibility of the `HTTPMessageConverter` is to convert the request body to a specific class.

**Constructor:**
```java
	public Employee(long id,String name, String designation, int salary) {
		super();
		this.id=id;
		this.name = name;
		this.designation = designation;
		this.salary = salary;
	}
```
**Controller:**
```java
	@PostMapping
	public Employee CreateEmployee(@RequestBody Employee employee) {
		return er.save(employee);
	}
```
Passed HttpRequest body in JSON format and that is converted to Java object by @RequestBody
```json
    {
        "name": "Iqbal",
        "designation": "Software Engineer",
        "salary": 35000
    }
```