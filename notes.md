# Spring boot

## Key differences

- **Website**: Usually they provide information to users, also provide some level of interaction. Implemented using Apache server
    - __Static__ -> The static websites doesn't have interaction with a database or an application in the server, so all users obtain the same data. They do not interact with users but are faster and cheaper.
    - __Dynamic__ -> Content is generated on the fly, and can generate responses based on the input. They interact with users but need more time to process requests, also they are more expensive than static. 
- **Web application**: High level of interaction with users, they are designed to store, analyze and manipulate data. Implemented using Tomcat

- **SOAP** (Simple Object Access Protocol): Relies on XML, originally developed by Microsoft. It is very extensive, but you must use only the needed pieces. It is intolerant to errors and you have to create the required XML structure every time. 
- **REST** (Representational State Transfer): It is a lightweight alternative to SOAP, it relies on a simple URL. Output data in the following commands: 
    - CSV
    - JSON
    - RSS

## Definitions

- **Boilerplate code**: Unit of repetitive sections of code that have to be included in many places with little or no alteration. 
- **AOP**: Aspect Oriented Programming.

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