# Spring boot

## Key differences

- **Website**: Usually they provide information to users, also provide some level of interaction. Implemented using Apache server
    - __Static__ -> The static websites doesn't have interaction with a database or an application in the server, so all users obtain the same data. They do not interact with users but are faster and cheaper.
    - __Dynamic__ -> Content is generated on the fly, and can generate responses based on the input. They interact with users but need more time to process requests, also they are more expensive than static. 
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
- JMS (Java messaging service): for asynchronous messages to a __Message broker__

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


WARNING: __Do not use the src/main/webapp directory when application is packaged as JAR__, it only works with WAR packaging.

## Spring boot starters

A curated list of compatible Maven dependencies, tested  and verified by Spring developers. You can add it in Spring Initializr. 

## Spring boot starter parent

- Default Maven configuration: Java version, UTF-encoding
- Dependency management
    - You use version on parent only
- Default configuration of Spring boot plugin

## Build and run from command line

You can build your application using either the provided maven program in the downloaded project or by a command if you have Maven installed:
- ```./mvnw package``` (on root folder)
- ```mvn package``` (on root folder)

Both commands will produce a jar file in the ```target/``` folder, so you can execute it by: 
- ```java -jar JAR_FILE``` (on target folder)
- ```mvn spring-boot:run``` (on  root folder)
- ```./mvnw spring-boot:run``` (on root folder)

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

## Inversion of Control

__Spring container__ have primary functions: 
 - An object factory who manages and create objects (**Inversion of Control**)
 - Inject object dependencies (**Dependency Injection**)
 
 __Inversion of Control__: Client delegates to another object the responsibility of providing its dependencies

 __Dependency injection__: Spring uses autowiring -> class that match. Multiple types of Dependency injection, covered two of them:

1. Constructor Injection: Generally recommended, used when you have required dependencies  
    - Define the dependency interface and class (@Component annotation that mark the class as Spring beam, important detail is that Spring only search in the same folder where is the main application, including sub-folders, but not in other packages)
    - Create a demo REST controller
    - Create a constructor in your REST controller class for injection
    - Add @GetMapping for the endpoint
2. Setter Injection: Inject dependencies by calling the setter methods of your class. Works with Optional dependencies

 There are three methods to Configure the Spring Container: 
 1. XML configuration file (legacy)
 2. Java Annotations (modern)
 3. Java Source Code (modern)

 ### Annotations 

#### Spring Core 

- Which class is the application main program
    - @SpringBootApplication (initialize some default required modules)
- Which class is a beam
    - @Component
- Which class is a controller
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

- __Map class to database table__
    - Create a class with public or protected no-argument constructor  (can have more constructors) and the annotation 
        - @Entity
    - Give a name to the table. 
        - @Table(name="class_name_snake_case")
    - Map fields to database columns
        - @Id, used to specify the __primary key__. Generate the primary key using: 
            - ```GenerationType.AUTO```
            - ```GenerationType.IDENTITY```
            - ```GenerationType.SEQUENCE```
            - ```GenerationType.TABLE```
            - Use custom, create implementation of org.hibernate.id.IdentifierGenerator
        - @Column(name="class_name_snake_case")  -> If not used, the Table and Column name will be the same as Java field and could cause tons of problems in case of refactoring.

- __DAO__  
    - Create an interface
    - Define DAO implementation
        - @Repository: Translates JDBC exceptions
        - @Autowired: Inject the entity manager
        - @Override: Override the constructor defined in the interface
        - @Transactional: Automatically begin and end the transaction for JPA code


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

Use an existing third party class in Spring framework
    - Create Configuration class
    - Define Bean method to configure the beam
    - Inject the bean into the controller

## Hibernate

Is a framework that handles all of the low-level SQL, it minimizes the JDBC code. 
Provides Object-to-Relational Mapping (**ORM**).  Here is a simple snippet: 

```java
import java.util.List;
import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;

public class Example {
    public static void main(String[] args) {
        // Create a Hibernate configuration
        Configuration config = new Configuration()
                .setProperty("hibernate.connection.driver_class", "org.postgresql.Driver")
                .setProperty("hibernate.connection.url", "jdbc:postgresql://localhost:5432/your_database_name")
                .setProperty("hibernate.connection.username", "your_username")
                .setProperty("hibernate.connection.password", "your_password")
                .setProperty("hibernate.dialect", "org.hibernate.dialect.PostgreSQLDialect")
                .setProperty("hibernate.show_sql", "true")
                .setProperty("hibernate.hbm2ddl.auto", "update")
                .addAnnotatedClass(User.class);

        // Create a Hibernate session factory
        SessionFactory sessionFactory = config.buildSessionFactory();

        // Create a Hibernate session
        Session session = sessionFactory.openSession();

        // Run a SELECT query using Hibernate Query Language (HQL)
        List<User> users = session.createQuery("FROM User", User.class).getResultList();

        // Output data of each user
        for (User user : users) {
            System.out.println("ID: " + user.getId() + " - Name: " + user.getName() + " - Email: " + user.getEmail());
        }

        // Close the Hibernate session
        session.close();

        // Close the Hibernate session factory
        sessionFactory.close();
    }
}
```

### ORM

Developer defines a mapping between Java __class and database table__

### JPA Specification

Jakarta Persistance API, previously known as Java Persistance API. It is a **standard API for ORM**.  It defines a set of interfaces and requires an implementation to be usable, some frameworks implement JPA such as Hibernate, EclipseLink and OpenJPA

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

The __Automatic data source configuration__  in Spring boot is based on configs/entries from __Maven pom file__, this means that **JPA Entity Manager and Data source** are automatically created by Spring Boot based on the file: application.properties.

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