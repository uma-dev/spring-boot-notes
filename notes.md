# Spring boot

## Key differences

- **Website**: Usually they provide information to users, also provide some level of interaction. Implemented using Apache server
  - **Static** -> The static websites doesn't have interaction with a database or an application in the server, so all users obtain the same data. They do not interact with users but are faster and cheaper.
  - **Dynamic** -> Content is generated on the fly, and can generate responses based on the input. They interact with users but need more time to process requests, also they are more expensive than static.
- **Web application**: High level of interaction with users, they are designed to store, analyze and manipulate data. Implemented using Tomcat

- **SOAP** (Simple Object Access Protocol): Relies on XML, originally developed by Microsoft. It is very extensive, but you must use only the needed pieces. It is intolerant to errors and you have to create the required XML structure every time. It uses:
  - XML (exclusively)
- **REST** (Representational State Transfer): It is a lightweight and fastest alternative to SOAP, it relies on a simple URL. Output data in the following commands:
  - CSV
  - JSON
  - RSS
  - XML

## Definitions

- **Boilerplate code**: Unit of repetitive sections of code that have to be included in many places with little or no alteration.
- **AOP**: Aspect Oriented Programming.
- **Spring Bean**: Is a regular Java class that is managed by Spring
- **Singleton**: In programming, a singleton is a design pattern that restricts the instantiation of a class to a single instance and provides a global point of access to that instance. In other words, a singleton class ensures that there is only one instance of the class created during the lifetime of the program and provides a way to access that instance from anywhere in the code.
- **Entity Class**: Java class that is mapped to a database table
- **snake case**: all letters in lower case, separated with underscores
- **screaming snake case**: all letters in upper case, separated with underscores
- **Why SQL uses snake case**: mysql is case insensitive, so one way to do not loose words meaning is using snake case.
- **Data Access Object**: Also known as DAO, it is a common design pattern, is responsible for interfacing with the database

## Deployment

In Spring boot you can deploy apps with a Tomcat embedded inside the jar file or in a traditional way using a WAR file. Spring does not replace Spring, instead it actually use Spring code behind the scenes, so it does not runs slower of faster.

## Spring Initializr

The main idea is to create a quickly a Spring project after selecting dependencies. Can import the project to whatever IDE/text editor you are using. It is available at this [link](https://start.spring.io/)

## Big picture

### Core container

Its the main component of Spring, it manages bean dependencies and has a bean factory for creating beans.

- Beans
- Core
- SpEL (spring expression language)
- Context

### Infrastructure

- AOP: Allows to create application wide services like logging, security, transactions, etc. It adds functionality to objects declaratively.
- Aspects
- Instrumentation: Make use of class loader implementations.
- Messaging

### Data Access Layer

- JDBC: Helper classes that reduce up to 50% the code to interact with db.
- ORM (Object to Relational Mapping): Integration with Java Hibernate.
- Transactions: Make use of AOP, adds transaction support
- OXM:
- JMS (Java messaging service): for asynchronous messages to a **Message broker**

### Web Layer

- Servlet
- WebSocket
- Web

### Test Layer

Support for test driven development (TDD)

- Unit
- Integration
- Mock

## Spring projects

Additional and optional Spring modules built on top of Spring Framework. You only need to use what you need. Some examples:

- Spring Cloud, Spring Data (db)
- Spring Batch, Spring Security
- Spring Web Services (SOAP and REST) and Spring LDAP
- etc

## Maven project structure

Its a useful Project management tool for building a Java project. The most popular use if for building management and dependencies. Some problems that Maven solve are:

- Automatically download the required JAR files required for the project (on the config file).
- Add them to the build path
- Standard folder structure

- src/main/java: Java source code
- src/main/resources: Config files and properties of the app
- src/main/webapp: JSP files and web config files and other web assets
- src/test: Unit testing source code and properties
- target: Compiled code

### POM.xml

This file on the root contains three sections:

- Project metadata (project name, versions, output file type)
- Dependencies
- Plug ins

### Project Coordinates

Uniquely identify a project also known as GAV.

- Group ID (name of company, conventionally in reverse domain name)
- Artifact ID (name of the project)
- Version **Optional but highly recommended** (specific release version, if its under active development, use -SNAPSHOT. Some packages doesn't need a version since they )

### Dependencies coordinates

You can search it in:

- Project page, like: spring.io, hibernate.org, etc
- **Maven central repo**: [Maven repo](http://search.maven.org)

The structure is also GAV as the project coordinates, but the version is optional.

### Plugins coordinates

The structure is also GAV as the project coordinates, but the version is optional.

## Spring project structure

It uses the standard Maven structure:

- src/main/java: Java source code
- src/main/resources: Config files and properties of the app
- src/test/java: Unit testing source code
- maven wrapper files: allows to run maven project
  - mvnw.sh (Linux/Mac)
  - mvnw.cmd (Windows)

WARNING: **Do not use the src/main/webapp directory when application is packaged as JAR**, it only works with WAR packaging.

## Spring boot starters

A curated list of compatible Maven dependencies, tested and verified by Spring developers. You can add it in Spring Initializr.

## Spring boot starter parent

- Default Maven configuration: Java version, UTF-encoding
- Dependency management
  - You use version on parent only
- Default configuration of Spring boot plugin

## Build and run from command line

You can build your application using either the provided maven program in the downloaded project or by a command if you have Maven installed:

- `./mvnw package` (on root folder)
- `mvn package` (on root folder)

Both commands will produce a jar file in the `target/` folder, so you can execute it by:

- `java -jar JAR_FILE` (on target folder)
- `mvn spring-boot:run` (on root folder)
- `./mvnw spring-boot:run` (on root folder)

## Spring Boot Properties

You can find the 1000+ properties list in this [link](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#appendix.application-properties), the properties are grouped on the following categories (with some examples):

- Core
  - Log levels
  - Log file name
- Web
  - Port (default 8080)
  - Context path of the application (default is "/")
  - Timeout (default 30 min)
- Security
  - User name
  - Password
- Data
  - JDBC url of the db
  - Username of the db
  - Password of the db
- Actuator
  - Endpoints to include
  - Endpoints to exclude
  - Base path for actuator endpoints
- Integration
- DevTools
- Testing
- **Profiles**: You can set profiles to control
  - which beans are loaded into Spring’s application context @Profile("Profile"), @ActiveProfiles()
  - connection strings to databases
  - URLs to external systems

## Inversion of Control

**Spring container** have primary functions:

- An object factory who manages and create objects (**Inversion of Control**)
- Inject object dependencies (**Dependency Injection**)

**Inversion of Control**: Client delegates to another object the responsibility of providing its dependencies

**Dependency injection**: Spring uses autowiring -> class that match. Multiple types of Dependency injection, covered two of them:

1. Constructor Injection: Generally recommended, used when you have required dependencies
   - Define the dependency interface and class (@Component annotation that mark the class as Spring beam, important detail is that Spring only search in the same folder where is the main application, including sub-folders, but not in other packages)
   - Create a demo REST controller
   - Create a constructor in your REST controller class for injection
   - Add @GetMapping for the endpoint
2. Setter Injection: Inject dependencies by calling the setter methods of your class. Works with Optional dependencies

There are three methods to Configure the Spring Container:

1.  XML configuration file (legacy)
2.  Java Annotations (modern)
3.  Java Source Code (modern)

### Annotations

#### Spring Core

- Which class is the application main program
  - @SpringBootApplication (initialize some default required modules)
- Which class is a beam
  - @Component
- Which class is a REST controller
  - @RestController
- Dependency injection
  - @Autowired (setter, field or constructor injection)
- Which class to use:
  - @Primary
  - @Qualifier ("lowerCaseClassName")
- Lazy initialization
  - @Lazy (you can use a global setting in application.properties with
  ```properties
  spring.main.lazy-initialization=true
  ```
  )
- Scope
  - @Scope(ConfigurableBeanFactory.SCOPE_OPTION)
  - The optionS for scope are: singleton, prototype, request, session and global-session
- Beam lifecycle methods
  - Init: @PostConstruct
  - Destroy: @PreDestroy
- Use an existing third party class in Spring framework
  - Create @Configuration class
  - Define @Bean method (to configure the beam)
  - Inject the bean into the controller with @Autowired

#### Hibernate (CRUD)

- **Map class to database table**

  - Create a class with public or protected no-argument constructor (can have more constructors) and the annotation
    - @Entity
  - Give a name to the table.
    - @Table(name="class_name_snake_case")
  - Map fields to database columns
    - @Id, used to specify the **primary key**. Generate the primary key using:
      - `GenerationType.AUTO`
      - `GenerationType.IDENTITY`
      - `GenerationType.SEQUENCE`
      - `GenerationType.TABLE`
      - Use custom, create implementation of org.hibernate.id.IdentifierGenerator
    - @Column(name="class_name_snake_case") -> If not used, the Table and Column name will be the same as Java field and could cause tons of problems in case of refactoring.

- **DAO**
  - Create an interface
  - Define DAO implementation
    - @Repository: Translates JDBC exceptions
    - @Autowired: Inject the entity manager
    - @Override: Override the constructor defined in the interface
    - @Transactional: Automatically begin and end the transaction for JPA code. NOT NEEDED for queries

#### REST CRUD API

- **REST Controller**

  - @RestController: Add REST support
  - @RequestMapping("/api")
  - @GetMapping("/entities")
  - @PostMapping("/entities")

- **Path Variable**

  - @RestController: Add REST support
  - @RequestMapping("/api")
  - @GetMapping("/students/{studentId}")
  - method (@PathVariable int studentId)

- **Request Body**

  - @RestController: Add REST support
  - @RequestMapping("/api")
  - @PostMapping("/students/{studentId}")
  - method (@RequestBody Object theObject)

- **Exception handler**

  - Create custom error response class
  - Create custom exception class
  - Update REST service to **throw** exception if student not found
  - Add an exception handler in the REST class
    - @ExceptionHandler

- **Service**

  - Define an interface
  - Define an implementation
    - Inject the DAO or Repository
    - Apply @Service to the implementation (These class files are used to write business logic in a different layer, separated from @RestController class)
    - Apply @Transactional on service methods and remove if there are any in the DAO methods

- **Global Exception Handling**

  - Use the interceptor/filter
    - @ControllerAdvice
  - Refactor REST service (remove exception handling)
  - Add exception handling code to Controller Advice
    - @ControllerAdvice

- **Declarative Security**
  - Edit pom.xml (add spring-boot-starter-security)
  - Define security constrains
  - Add Java config class
    - @Configuration
  - Add users, passwords and roles
    - Add support for db tables that contain users and roles for a UserDetailsManager function with annotation @Bean
      - Bean

---

- **Validation**
  - @NotNull
  - @Min
  - @Max
  - @Size
  - @Pattern
  - @Future / @Past

### Bean Scopes

Scope: refers to the lifecycle of a beam, this is how long does the beam live and how many instances are created.

In Spring, the beam scope is Singleton, but there a lots of options for multiple purposes like: singleton, prototype, request, session and global-session.

#### Beam lifecycle

1. Container started:
   - Beam Instantiated
   - Dependency Injection
   - Internal Spring Processing
   - Your custom init method
2. Beam ready for use:
   - Your custom destroy method

#### Beam lifecycle methods

Allows to add custom code during bean initialization, like call to custom business logic methods, setting up handles to resources (db, sockets, file, etc)

#### Add an external class to Spring framework

Use an existing third party class in Spring framework - Create Configuration class - Define Bean method to configure the beam - Inject the bean into the controller

---

## Hibernate

Is a framework that handles all of the low-level SQL, it minimizes the JDBC code.
Provides Object-to-Relational Mapping (**ORM**).

### ORM

Developer defines a mapping between Java **class and database table**

### JPA Specification

Jakarta Persistance API, previously known as Java Persistance API. It is a **standard API for ORM**. It defines a set of interfaces and requires an implementation to be usable, some frameworks implement JPA such as Hibernate, EclipseLink and OpenJPA

### JDBC

Java database connectivity. Hibernate / JPA uses JDBC for all database communications, so Hibernate runs in top in JDBC. Here is a snippet:

```java
import java.sql.*;

public class Example {
    public static void main(String[] args) {
        // Database connection parameters
        String url = "jdbc:postgresql://localhost:5432/your_database_name";
        String username = "your_username";
        String password = "your_password";

        // Create a database connection
        try {
            Connection conn = DriverManager.getConnection(url, username, password);

            // Run a SELECT query
            String sql = "SELECT * FROM users";
            Statement statement = conn.createStatement();
            ResultSet result = statement.executeQuery(sql);

            // Output data of each row
            while (result.next()) {
                int id = result.getInt("id");
                String name = result.getString("name");
                String email = result.getString("email");
                System.out.println("ID: " + id + " - Name: " + name + " - Email: " + email);
            }

            // Close the database connection
            conn.close();
        } catch (SQLException e) {
            System.out.println("Connection failed: " + e.getMessage());
        }
    }
}
```

### Hibernate

In Spring boot, Hibernate is the default implementation of the JPA Specification. The main component used for creating queries is:

- EntityManager (from JPA).

The **Automatic data source configuration** in Spring boot is based on configs/entries from **Maven pom file**, this means that **JPA Entity Manager and Data source** are automatically created by Spring Boot based on the file: application.properties.

So the framework can create the following beans and then inject them into the app:

- DataSource
- EntityManager

For setting up the project using Spring Initializr you must add the dependencies:

1. MySQL/JDBC Driver:

```console
mysql-connector-j
```

2. Spring Data JPA:

```console
spring-boot-starter-data-jpa
```

The DB connection is read from the application.properties file showed below:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/student_tracker
spring.datasource.username=user
spring.datasource.password=password
```

#### Entity class (JPA)

It is a Java class that is mapped to a database table. It uses the annotation @Entity. It must have:

- A public or protected no-argument constructor (the class can have additional constructors).

#### DAO

The DAO or Data Access Object needs a JPA Entity Manager (the main component for saving/retrieving data) and JPA Entity Manager needs a Data source. The steps to implement DAO are:

1. Define a DAO interface
2. Define DAO implementation
   - Inject the entity manager
3. Update main app

### Creating tables with code

**NOT RECOMMENDED** since you can delete (drop) the production database, so it is better for testing and developing environments. The general recommendation is to create tables with **SQL scripts**, but in case you need to setup the auto-creation in accordance to annotations, only need to set the next configuration in application.properties

```properties
    spring.jpa.hibernate.ddl-auto=PROPERTY-VALUE
```

whit one of the following options:

- none
- create-only
- drop (delete)
- create-drop (drop on shutdown)
- validate (validate db tables schema)
- update (add any new fields)

---

## REST API

Also known as REST web service REST service RESTful API RESTful web service. They provide information at a endpoint.

### JSON

One popular way they communicate REST API is using JSON format (JavaScript Object Notation), because it is: - lightweight - language independent - simple (is just plain text data).

The format of JSON are name-value pairs, **delimited by columns**, the type of values are:

- Strings, always inside **double-quotes**
- Numbers, **no quotes**
- Boolean, **true or false**
- Nested, **one item inside other**
- Array, **square brackets [], values delimited by comma**
- null

### REST protocol and Methods

REST is commonly used over HTTP protocol. The equivalent of each CRUD operation in a REST request are:

| HTTP Method | CRUD Operation                 |
| :---------- | :----------------------------- |
| POST        | Create a new entity            |
| GET         | Read a list or a single entity |
| PUT         | Update an existing entity      |
| DELETE      | Delete an existing entity      |

### HTTP Messages

The **Request Message** has 3 main parts

- Request line: the HTTP command for the request
- Header variables: request metadata
- Message body: contents of message

The **Response Message** hast also 3 main parts

- Response line: the server protocol and status code
- Header variables: response metadata
- Message body: contents of message

### Status code

| Code Range | Description   |
| :--------- | :------------ |
| 100-199    | Informational |
| 200-299    | Successful    |
| 300-399    | Redirection   |
| 400-499    | Client error  |
| 500-599    | Server error  |

### MIME

The message format is described by MIME content type. The basic syntax is type/sub-type, for example:

- text/html
- text/plain
- application/json
- application/xml

### Path Variables

You can retrieve a single object at an endpoint using a Path variable inside curly braces `{variable}` or we can use `:variable`

`/api/students/0`

`/api/students/1`

`/api/students/{studentId}`

### Data Binding

The process to converting from JSON to a Java POJO and vice versa. It also know as:

- Serialization / Deserialization
- Marshalling / Unmarshalling

Spring uses Jackson project behind the scenes to do data-binding. Its dependency is included in **Spring Web**. Also, you must have the setter methods of the class implemented, in order to allow Jackson to use them.

When JSON data is being passed to REST controller is converted to POJO and when a Java object is being returned from REST controller is converted to JSON automatically.

Behind the scenes, what Jackson do is make calls to getters and setters depending if you want to do serialization or deserialization.

### REST API Design

#### Best Practices

Identify:

1. Who will use the API
2. How will they use the API
3. Design the API based on the requirements

Process

1. Review the requirements
   - Enlist requirements
   - Does it needs full CRUD support?
2. Identify the main resource/ entity
   - The convention is to use plural form of resource in the example -> entity: employees. So the endpoint should look like `/api/employees`
3. Use HTTP methods to assign actions on resource (CRUD)
   - POST at /api/employees
   - GET (all employees) at /api/employees
   - GET (one employee) at /api/employees/{employeeId}
   - PUT at /api/employees/{employeeId}
   - DELETE at /api/employees/{employeeId}

#### Bad Practices

- Don't add actions at endpoints:
  - /api/addEmployees, /api/deleteEmployees, etc.

### Development process

Dependencies in Spring Initializr:

1. MySQL driver
2. Spring Boot DevTools
3. Spring Data JPA
4. Spring Web

Packages and classes

- /rest
- /entity
- /dao
- MainApplication.java

Development process

1. Update db configs in application.properties
2. Create employee entity inside package
3. Create DAO interface
4. Create DAO implementation
5. Create REST controller
6. Inject the DAO implementation in REST controller and expose the method

### Service layer

Uses **Service Facade** design pattern. It is also a good practice even if you will integrate only one data source.

The service layer acts as a Intermediate layer for custom business logic. It integrates data from multiple backend sources such as:

- DAO
- Repositories

Another best practices in the service layers:

- Apply transactional boundaries at the service layer

### JPA Repository

To avoid boiler plate code exposing entities, you can use the JpaRepository interface and obtain full CRUD support by **inheritance**. The development process is:

- Extend the interface, doesn't need implementation since the Repository interfaces are being implemented (backed up) by Spring Container at Runtime.

### Spring Data REST

The easiest way to implement the API is by using the POM file. There is no code required and Spring Data scan for JpaRepository and expose the entities in **simple pluralized form** (Employee -> employees, but it **will not handle automatically:** person -> people ). you only need to add the dependency:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-rest</artifactId>
</dependency>
```

The general 3 requirements are:

1. Your entity
2. JpaRepository
3. Maven POM dependency for `spring-boot-starter-data-rest`

The REST endpoints are HATEOAS compliant:

**HATEOAS** (Hypermedia as the Engine of Application State) is a principle of RESTful architecture that suggests a client should interact with a web service by navigating through hypermedia links dynamically provided by the server.

Some of the advanced features are:

- Pagination, sorting and searching
- Extending and adding custom queries with JPQL
- Query Domain Specific Language (Query DSL)

#### Id managing

One important detail is that Spring Data REST doesn't use ID in the JSON, only in the URL!

#### Sorting

To sort you must add the following to the URL:

- By last name, ascending (default): `http://localhost:8080/employees?sort=lastName`
- By last name, descending `http://localhost:8080/employees?sort=lastName,desc`
- By last name and the by first name, ascending `http://localhost:8080/employees?sort=lastName,firstName,asc`

#### Page size

You can add the configurations in the file application.properties

#### Spring security Login Process JDBC

1. Retrieve password each login from db
   - Custom created tables
   - Tables with Spring security schema
2. Read encoding algorithm
3. For case of bcrypt, encrypt plain text from login form
4. Compare encrypted password with db password
5. Login if theres a match

You can connect additional security configurations to extend Spring security, also you can add your custom login form instead of the default provided by Spring security.

## Thymeleaf

Thymeleaf expression can access Java code, objects and Spring beans.
Its executed on the server side, so the results are included in the HTML returned to the browser, also supports the following features:

- Looping and conditionals
- CSS and Javascript integration
- Templates layouts and fragments

The development process is:

1. Add Thymeleaf to the maven POM file or add it in Spring Initializr
2. Develop Spring MVC Controller
   - Thymeleaf template files go in: src/main/resources/templates
   - For Web apps, the Thymeleaf templates have a .html extension
3. Create Thymeleaf template
   - Create CSS file
     - locally in `/src/main/resources/static/css/file.css`
     - or reference remotely in the template
     - or use bootstrap locally or remotely `/src/main/resources/static/css/bootstrap.min.css`
   - Reference CSS in Thymeleaf template with a href to the **Context path/Context root** (Best practice in the industry is to use reference to the context path dynamically instead of hard coding the the context path) `th: href=@{/css/file.css}`
   - Apply the style with: `class = myclass.css`

Spring Boot search in the following directories for static resources (in order):

1. /META-INF/resources
2. /resources
3. /static (most used in real-time projects)
4. /public (most used in real-time projects)

## Validation

Bean Validation Features:

- Required
- Validate length
- Validate numbers
- Validate with regular expressions
- Custom validation

## Spring Security

Spring Security needs a connection to a database to ensure every time you request a login:

- The username (PK)
- Password
- Your roles or groups, depending on the selected implementation. Its optional to use the predefined Users Schema provided by Spring Security.

Depending on the request matchers and configuration you can restrict URL acces based on roles, show login form error message, use a logout page, display content in HTML (MVC) based on roles.

## Hibernate Advanced mappings

### Relations

Using hibernate provides the following relations for ORM:

- One to one
  - `@OneToOne` annotation
  - `@OneToOne(cascade=CascadeType.ALL)` is a better fit if you want cascade operations. **By default no operations are cascade**
  - `@OneToOne(mappedBy="idMapped")` (One to one bidirectional, see examples)
- One to many
- Many to one
- Many to many

### Joins

Also you can join tables with the annotation:

- `JoinColumn(name = "column to join")`

### Cascade

You can cascade operations with:

- CascadeType.DETACH
- CascadeType.MERGE
- CascadeType.PERSIST
- CascadeType.REFRESH
- CascadeType.REMOVE

It also supports cascade for deleting/saving, fine grained cascade configurations and unidirectional/bidirectional relations.

### Examples

#### One to one

![OneToOne](https://github.com/uma-dev/spring-boot-notes/assets/22565959/3acf20a3-eab4-4aba-8efc-66d2f824c7f0)

1. Simple one to one relationship with cascade

```java
    @OneToOne(cascade=CascadeType.ALL)
    @JoinColumn(name="schedule_detail_id")
    private ScheduleDetail scheduleDetail;

```

2. Bidirectional relationship with cascade

```java
    public class Schedule {
      ...
      @OneToOne(cascade=CascadeType.ALL)
      @JoinColumn(name="schedule_detail_id")
      private ScheduleDetail scheduleDetail;
      ...
    }

    public class ScheduleDetail {
      ...
      @OneToOne(mappedBy="scheduleDetail", cascade=CascadeType.ALL)
      private Schedule schedule;
      ...
    }
```

#### One to many

![OneToMany](https://github.com/uma-dev/spring-boot-notes/assets/22565959/7a6f40c6-d272-406a-ac99-b770417b4d4e)

1. Bidirectional relationship with cascade

```java
    public class Course {
      ...
      // Do not cascade delete operations (bussines rule)
      @ManyToOne(cascade={CascadeType.PERSIST, CascadeType.MERGE,
                          CascadeType.DETACH, CascadeType.REFRESH})
      @JoinColumn(name="instructor_id")
      private Instructor instructor;
      ...
    }

    public class Instructor {
      ...
      @OneToMany(mappedBy="instructor",
                 cascade={CascadeType.PERSIST, CascadeType.MERGE,
                          CascadeType.DETACH, CascadeType.REFRESH})
      private List<Course> courses;
      ...
    }
```

### Fetch types

The best practice in industry is only load data when its needed.
When retrieving data we can use two types of fetch:

- Eager (**retrieve all data**)
- Lazy loading (**retrieve data on demand**):
  \*\* its the preferred approach, to avoid performance issues, but need to keep in mind that there are exeeptions to the rule.
  Lazy needs an open db connection. If not, will throw an exception

The defaults for each annotation are:

- `@OneToOne`: Eager
- `@OneToMany`: Lazy
- `@ManyToOne`: Eager
- `@ManyToMany`: Lazy

Can be overrided:
`@OneToMany(fetch=FetchType.EAGER, mappedBy="instructor)`

## Entity Lifecycle

| Operations | Description                             |
| ---------- | --------------------------------------- |
| DETACH     | Not associated with a Hibernate session |
| MERGE      | Return from detached to reattach        |
| PERSIST    | From new instances to managed state     |
| REMOVE     | From managed to be removed              |
| REFRESH    | Reload object with data                 |

![entityLifecycle](https://github.com/uma-dev/spring-boot-notes/assets/22565959/2f921086-7d94-4404-978a-b2ee5e99845d)
