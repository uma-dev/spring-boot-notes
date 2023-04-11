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
- Version **Optional but highly recommended** (specific release version, if its under active development, use -SNAPSHOT )

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
    - Define the dependency interface and class (@Component annotation that mark the class as Spring beam)
    - Create a demo REST controller
    - Create a constructor in your REST controller class for injection
    - Add @GetMapping for the endpoint
2. Setter Injection: Optional dependencies

 There are three methods to Configure the Spring Container: 
 1. XML configuration file (legacy)
 2. Java Annotations (modern)
 3. Java Source Code (modern)