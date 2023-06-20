# Spring JDBC

**JDBC means Java Database Connectivity**
We can manipulate data like finding data or deleting data using JDBC. We can pass the sql query as argument and map with the fields to manipulate the data.

```java
	public List<Person> finAll() {
		return jdbc.query("select * from Person", new BeanPropertyRowMapper(Person.class));
	}
```
Here a sql query is passed as argument and the `BeanPropertyRowMapper(Person.class)` class is used to map tha fields.

CRUD operation using JDBC:


**Repository:**
```java
package com.DatabaseDemo.repository;

import java.sql.Timestamp;
import java.sql.Date;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.BeanPropertyRowMapper;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.core.RowMapper;
import org.springframework.stereotype.Repository;

import com.DatabaseDemo.entity.Person;

@Repository
public class JdbcDataRepository {

	@Autowired
	JdbcTemplate jdbc;
	

    //Creating custom Row Mapper
	class PersonRowMapper implements RowMapper<Person>{

		@Override
		public Person mapRow(ResultSet rs, int rowNum) throws SQLException {
			Person person= new Person();
			person.setId(rs.getInt("id"));
			person.setName(rs.getString("name"));
			person.setLocation(rs.getString("location"));
			person.setBirthDate(rs.getTimestamp("birthDate"));
			return person;
		}
	}

	//Returning all rows of table Person
	public List<Person> finAll() {
		return jdbc.query("select * from Person", new BeanPropertyRowMapper(Person.class));
	}

	//Finding individual row using id
	//query(sql_query,passed_parameter_as_object,mapper)
	public Person findById(int id) {
		return (Person) jdbc.queryForObject("select * from Person where id=?", new Object[] { id },
				new BeanPropertyRowMapper(Person.class));
	}

	//Finding List of rows using name
	public List<Person> findByName(String name) {
		return  jdbc.query("Select * from Person where name=?", new Object[] { name },
				new BeanPropertyRowMapper(Person.class));
	}

	//Finding list of rows using name and location
	public List<Person> findByNameAndLocation(String name,String location){
		return jdbc.query("Select * from Person where name=? and location=?", 
				new Object[] {name,location},
				new BeanPropertyRowMapper(Person.class));
	}
	
	//Deleting an element using id
	public int deleteById(int id) {
		return jdbc.update("delete from Person where id=?", new Object[] {id});
	}
	
	//Deleting rows using name
	public int deleteByName(String name) {
		return jdbc.update("delete from Person where name=?", new Object[] {name});
		
	}

	public int deleteByNameAndLocation(String name, String location) {
		return jdbc.update("delete from Person where name=? and location=?",
				new Object[] {name,location});
	}

	//Insert data to the DB table
	public int insertPerson(Person person) {
		return jdbc.update("insert into Person(id,name,location,birth_date) values(?,?,?,?)",
				new Object[] {person.getId(),person.getName(),person.getLocation(), new Timestamp(person.getBirthDate().getTime())});
	}
	
    //Update data
	public int updatePerson(Person person) {
		return jdbc.update("update Person set name=?,location=? where id=?",
				new Object[] {person.getName(),person.getLocation(),person.getId()});
	}

}
```
**Entity:**
```java
package com.DatabaseDemo.entity;

import java.util.Date;

public class Person {
	private int id;
	private String name;
	private String location;
	private Date birthDate;
	
	public Person() {
		
	}
	public Person(int id, String name, String location, Date date) {
		super();
		this.id = id;
		this.name = name;
		this.location=location;
		this.birthDate = date;
	}

	public int getId() {
		return id;
	}

	public String getLocation() {
		return location;
	}
	public void setLocation(String location) {
		this.location = location;
	}
	public void setId(int id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public Date getBirthDate() {
		return birthDate;
	}

	public void setBirthDate(Date birthDate) {
		this.birthDate = birthDate;
	}
	@Override
	public String toString() {
		return "\nPerson [id=" + id + ", name=" + name + ", location=" + location + ", birthDate=" + birthDate + "]";
	}
}
```
**`Data.sql`**  
Here h2 database is used. So, every time when the server terminates then all the data from the DB would be erased. That's why the necessary sql query can be stored in Data.sql file. That file would run each time the program runs by default.
```sql
create table Person(
	id integer not null,
	name varchar(200) not null,
	location varchar(200),
	birth_date timestamp,
	primary key(id)
);

insert into Person(id,name,location,birth_date) values(1001,'Jahid','Dhaka',current_date());
insert into Person(id,name,location,birth_date) values(1002,'Iqbal','Noakhali',current_date());
insert into Person(id,name,location,birth_date) values(1003,'Jahid','Chittagong',current_date());
insert into Person(id,name,location,birth_date) values(1004,'Jahid','Dhaka',current_date());
insert into Person(id,name,location,birth_date) values(1005,'Babu','Barishal',current_date());
insert into Person(id,name,location,birth_date) values(1006,'Abdullah','Tangail',current_date());
```
**Main:**
```java
package com.DatabaseDemo;

import java.util.Date;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

import com.DatabaseDemo.entity.Person;
import com.DatabaseDemo.repository.JdbcDataRepository;

@SpringBootApplication
public class DatabaseDemoApplication implements CommandLineRunner {
	
	Logger logger=LoggerFactory.getLogger(this.getClass());

	@Autowired
	JdbcDataRepository jdbcRep;
	
	public static void main(String[] args) {
		SpringApplication.run(DatabaseDemoApplication.class, args);
	}

	@Override
	public void run(String... args) throws Exception {
		logger.info("All user-> {}",jdbcRep.finAll());
		logger.info("Find By Id->{}",jdbcRep.findById(1001));
		logger.info("Find By Name->{}",jdbcRep.findByName("Jahid"));
		logger.info("Find by name and location->{}",jdbcRep.findByNameAndLocation("Jahid", "Dhaka"));
		logger.info("Deleted->{}",jdbcRep.deleteById(1002));
		logger.info("Deleted again->{}",jdbcRep.deleteByName("Babu"));
		logger.info("Deleted using name and location->{}",jdbcRep.deleteByNameAndLocation("Jahid", "Dhaka"));
		logger.info("Insert Person->{}",jdbcRep.insertPerson(new Person(1007,"Aminul","Barishal", new Date())));
		logger.info("All user-> {}",jdbcRep.finAll());
		logger.info("Update->{}",jdbcRep.updatePerson(new Person(1007,"Islam","Meherpur",new Date())));
		logger.info("All user-> {}",jdbcRep.finAll());
	}

}
```