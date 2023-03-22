What is Spring Boot? How is it different from other Spring frameworks?
Answer:-  Basically its an extension of the Spring framework, which eliminates the boilerplate configurations required for setting up a Spring application.
          In Spring Boot there are default configurations that allow faster bootstrapping. Spring Framework requires a number of dependencies to create a web app. Spring Boot, on the other hand, can get an application working with just one dependency.
          
          Q2.)What is Spring Data JPA? How is it used in Spring Boot applications?
          Answer:- It provides a framework that works with JPA and provides a complete abstraction over the Data Access Layer. 
           compelling feature is the ability to create repository implementations automatically, at runtime, from a repository interface
           
           Q3.)Explain the concept of Dependency Injection in Spring Boot.
           ANswer:- Dependency Injection is a fundamental aspect of the Spring framework, through which the Spring container “injects” objects into other objects or “dependencies”.
           
           Q4.)What is the purpose of Spring Security in Spring Boot applications?
           Answer:- to offer us a highly customizable way of implementing authentication, authorization, and protection against common attacks.
           
           Q5.) What is a Bean in Spring? How are Beans created in Spring Boot applications?
           Answer:-objects that form the backbone of your application and that are managed by the Spring IoC container are called beans.
           Different Methods to Create a Spring Bean
               Creating Bean Inside an XML Configuration File (beans. xml)
               Using @Component Annotation.
               Using @Bean Annotation.
               
            Q6.)What is Flutter? What are its advantages over other mobile development frameworks?
            Answer:-Flutter is Google's UI toolkit for building beautiful natively compiled applications for mobile, web, and desktop from a single codebase.
            Advantages;-
The hot reload feature make the app development much quicker. With Flutter there is no need to reload the app to see every single change you make in the code.

           Q7.)Explain the difference between Stateless and Stateful Widgets in Flutter.
           Answer_ Stateless widgets are those widgets whose state can’t be changed or altered once they are built.
These widgets are immutable once they are built.
Any change in data, widgets, icons, or variables do not change the state of the app or UI.
They simply override the build() method and return a widget.

Stateful widgets are those widgets whose state can be changed in real-time.
Stateful widget overrides the createState() and returns a state.
They are dynamic in nature.

           Q8.)What is Dart? How is it used in Flutter applications?
           Dart is designed for a technical envelope that is particularly suited to client development, prioritizing both development (sub-second stateful hot reload) and high-quality production experiences across a wide variety of compilation targets.
           We will start your application from the main() function in the PROJECT_ROOT/lib/main. dart , where you pass your main widget to runApp() that will attach it to the screen.
           
           Q9.)Explain the concept of Hot Reload in Flutter. How does it benefit the development process?
           Answer_ Hot reload works by injecting updated source code files into the running Dart Virtual Machine (VM). After the VM updates classes with the new versions of fields and functions, the Flutter framework automatically rebuilds the widget tree, allowing you to quickly view the effects of your changes.
           
           Q10.)What is REST API? What are the key principles of REST architecture?
            REST is an acronym for REpresentational State Transfer and an architectural style for distributed hypermedia systems.
            REST principles are defined by four interface controls, including identifying resources, managing resources through representations, self-descriptive communications, and hypermedia as the engine of the application state.
            
            Q11.)Explain the difference between GET and POST requests in REST API.
            GET_
            1) In case of Get request, only limited amount of data can be sent because data is sent in header.
            2)Get request is not secured because data is exposed in URL bar.
            3) Get request can be bookmarked.
            
            POST_
            1)In case of post request, large amount of data can be sent because data is sent in body.
            2)Post request is secured because data is not exposed in URL bar.
            3)Post request cannot be bookmarked.
            
            Q12)What is CRUD? How is it used in REST API development?
            Answer- CRUD is the acronym for CREATE, READ, UPDATE and DELETE. These terms describe the four essential operations for creating and managing persistent data elements, mainly in relational and NoSQL databases
            REST API calls invoke CRUD operations, understanding their relationship with one another is important for API developers and data engineers.
            
            Q13)What is Swagger? How is it used to document REST APIs?
            Answer- Swagger is an open source set of rules, specifications and tools for developing and describing RESTful APIs.
            
            Q14)What are the benefits of using REST API in modern web development?
            Lightweight. One of the main benefits of REST APIs is that they rely on the HTTP standard, which means it's format-agonistic and you can use XML, JSON, HTML, etc. 
Independent. Another benefit of REST APIs is the fact that the client and server are independent. ...
Scalable and flexible.

            Q15)Write unit tests for the REST API endpoints using JUnit and Mockito.
            1.Create Spring boot application
            Spring Web
            Spring Data JPA
            Lombok
            
            2.MAVEN DEPENDENCIES
            <dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		<dependency>
			<groupId>org.projectlombok</groupId>
			<artifactId>lombok</artifactId>
			<optional>true</optional>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
    
    
    
    
    3.Create JPA Entity
    import lombok.*;

import javax.persistence.*;

@Setter
@Getter
@AllArgsConstructor
@NoArgsConstructor
@Builder

@Entity
@Table(name = "employees")
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private long id;

    @Column(name = "first_name", nullable = false)
    private String firstName;

    @Column(name = "last_name", nullable = false)
    private String lastName;

    @Column(nullable = false)
    private String email;
}

NOTE__ using Lombok annotations to reduce the boilerplate code.
      @Entity annotation is used to mark the class as a persistent Java class.
      @Table annotation is used to provide the details of the table that this entity will be mapped to.
@Id annotation is used to define the primary key.
@GeneratedValue annotation is used to define the primary key generation strategy. In the above case, we have declared the primary key to be an Auto Increment field.
@Column annotation is used to define the properties of the column that will be mapped to the annotated field. You can define several properties like name, length, nullable, updateable, etc.



4. Create Repository Layer
    import net.javaguides.springboot.model.Employee;
import org.springframework.data.jpa.repository.JpaRepository;

public interface EmployeeRepository extends JpaRepository<Employee, Long> {

}

5.Create Service Layer
import net.javaguides.springboot.model.Employee;

import java.util.List;
import java.util.Optional;

public interface EmployeeService {
    Employee saveEmployee(Employee employee);
    List<Employee> getAllEmployees();
    Optional<Employee> getEmployeeById(long id);
    Employee updateEmployee(Employee updatedEmployee);
    void deleteEmployee(long id);
}
  
  
  6.Controller Layer - CRUD REST APIs
  
   created CRUD REST APIs for creating, retrieving, updating, and deleting an Employee
  
  import net.javaguides.springboot.model.Employee;
import net.javaguides.springboot.service.EmployeeService;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/api/employees")
public class EmployeeController {

    private EmployeeService employeeService;

    public EmployeeController(EmployeeService employeeService) {
        this.employeeService = employeeService;
    }

    @PostMapping
    @ResponseStatus(HttpStatus.CREATED)
    public Employee createEmployee(@RequestBody Employee employee){
        return employeeService.saveEmployee(employee);
    }

    @GetMapping
    public List<Employee> getAllEmployees(){
        return employeeService.getAllEmployees();
    }

    @GetMapping("{id}")
    public ResponseEntity<Employee> getEmployeeById(@PathVariable("id") long employeeId){
        return employeeService.getEmployeeById(employeeId)
                .map(ResponseEntity::ok)
                .orElseGet(() -> ResponseEntity.notFound().build());
    }

    @PutMapping("{id}")
    public ResponseEntity<Employee> updateEmployee(@PathVariable("id") long employeeId,
                                                   @RequestBody Employee employee){
        return employeeService.getEmployeeById(employeeId)
                .map(savedEmployee -> {

                    savedEmployee.setFirstName(employee.getFirstName());
                    savedEmployee.setLastName(employee.getLastName());
                    savedEmployee.setEmail(employee.getEmail());

                    Employee updatedEmployee = employeeService.updateEmployee(savedEmployee);
                    return new ResponseEntity<>(updatedEmployee, HttpStatus.OK);

                })
                .orElseGet(() -> ResponseEntity.notFound().build());
    }

    @DeleteMapping("{id}")
    public ResponseEntity<String> deleteEmployee(@PathVariable("id") long employeeId){

        employeeService.deleteEmployee(employeeId);

        return new ResponseEntity<String>("Employee deleted successfully!.", HttpStatus.OK);

    }
}
  
  7.Writing Unit Tests for CRUD REST API's
  and the conclusion
