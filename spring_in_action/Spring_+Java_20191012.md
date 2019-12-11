# Spring

> The only constant is change.
> --- Heraclitus

Some time ago, the most common types of applications developed were
browser-based web applications, backed by relational databases. We’re now also
interested in developing applications composed of microservices destined for the
cloud that persist data in a variety of databases.

## What is Spring?

Any non-trivial application is composed of many components, each responsible for
its own piece of the overall application functionality, coordinating with the
other application elements to get the job done. When the application is run,
those components somehow need to be created and introduced to each other.

* **Container**: also known as _Spring application context_, creates and manages
  application components
* **Beans**: components, wired together inside the Spring application context to
  make a complete application
* **Dependency injection**: act of wiring beans together, the container creates
  and maintains all components and injects those into the beans that need them,
  which is done typically through constructor arguments or property accessor
  methods
* **Autowiring**: Spring automatically injects the components with the other
  beans that they depend on
* **Component scanning**: Spring can automatically discover components from an
  application’s classpath and create them as beans in the container
* **Sping Boot**: an extension of the Spring Framework that offers several
  productivity enhancements
* **Autoconfiguration**: the most well-known enhancement coming with Spring Boot

Spring Boot can make reasonable guesses of what components need to be configured
and wired together, based on entries in the classpath, environment variables,
and other factors.

## Get Started

Spring Boot applications tend to bring everything they need with them and Tomcat
is a part of the application!

With Spring you can focus on the code that meets the requirements of an
application rather than on satisfying the demands of a framework. Although
you’ll no doubt need to write some framework-specific code from time to time,
it’ll usually be only a small fraction of your codebase. Spring (with Spring
Boot) can be considered the _frameworkless framework_.

### Spring Boot DevTools

DevTools is a Spring package, providing Spring developers with some handy
development-time tools:

* Automatic application restart when code changes
* Automatic browser refresh when browser-destined resources (such as templates,
  JavaScript, stylesheets, and so on) change, a browser plugin of LiveReload
  needs to be installed to enable auto refreshing
* Automatic disable of template caches
* Built in H2 Console if the H2 database is in use

When DevTools is in play, the application is loaded into two separate class
loaders in the Java virtual machine (JVM). One class loader is loaded with your
Java code, property files, and pretty much anything that’s in the `src/main/`
path of the project. These are items that are likely to change frequently. The
other class loader is loaded with dependency libraries, which aren’t likely to
change as often.

By default, template options such as Thymeleaf and FreeMarker are configured to
cache the results of template parsing so that templates don’t need to be reparsed
with every request they serve.

### The Core Spring Framework

The core Spring Framework is the foundation of everything else in the Spring
universe. It provides the core container and dependency injection framework,
and:

* SpringMVC, a powerful, annotation-based web framework which can be used to
  serve classic web requests and also to create REST APIs
* JDBC, more specifically a template-based JDBC support of `JdbcTemplate`

## Developing Web Applications

* **Domain**: classes defining the entities
* **Controller**: handling HTTP requests, handing a request off to a view to
  render HTML or writing data directly to the body of a response (RESTful).
* **View**: a HTML file with Thymeleaf attributes

`Model` is an object that ferries data between a controller and whatever view is
charged with rendering that data. There should be no space after `redirect:`
when it is used, e.g.: `redirect:/orders/current`.

If there is no `action` attribute declared in the `<form>` tag, the browser will
gather up all the data in the form and send it to the server in an HTTP POST
request to the same path.

### User Input Validation

Spring supports Java’s Bean Validation API, and wit Spring Boot the Validation
API and the Hibernate implementation of the Validation API are automatically
added to the project as transient dependencies of Spring Boot’s web starter.
Usually, in order to apply validation in Spring MVC, you need to:

* Declare validation rules on the domain class
* Specify that validation in the controller methods
* Modify the form views to display validation errors

Thymeleaf offers convenient access to the `Errors` object via the `fields` property
and with its `th:errors` attribute.

## Template Engine - Thymeleaf

Thymeleaf is designed to be decoupled from any particular web framework, so it
is unaware of Spring’s model abstraction and are unable to work with the data
that the controller places in `Model`. Therefore, before Spring hands the
request over to a view, it copies the model data into ***request attributes***
that Thymeleaf options has ready access to.

* `th:src`: a Thymeleaf attribute
* `th:text`: replacing the tag body with the value from a request attribute
* `th:value`: value bound to a form element to be posted
* `th:field`: ???
* `th:if="${#fields.hasErrors('ccNumber')`: ???
* `th:object`: refering to a domain object
* `th:each`: iterating ove a collection
* ` @{...}`: an expression to reference the resource with a context-relative
  path, serving from the `/static` path as the root
* `${...}`: refering to the value of a request attribute (in the bracket)
* `*{...}`: opposit to the attribute above, writing the value to the request
  attribute

## Annotation

* `@Configuration`: indicating to Spring that this is a configuration class that
  will provide beans to the container
* `@Bean`: indicating that the objects they return should be added as beans in
  the container
* `@SpringBootApplication`: a composite application that combines three other
  annotations
    + `@SpringBootConfiguration`: a specialized form `@Configuration`,
      designates this class as a configuration class
    + `@EnableAutoConfiguration`: tells Spring Boot to automatically configure
      any components that it thinks you’ll need
    + `@ComponentScan`: automatically discover `@Component`, `@Controller`,
      `@Service`, and others to register them in the container
* `@Controller`: identifying the class as a component for scanning, other
  annotations (including `@Component`, `@Service`, and `@Repository`) serve a
  similar purpose
* `@RequestMapping`: a class-level annotation, specifying the path the
  controller serves
* `@GetMapping`: indicating that the path serves a HTTP GET request, a new
  annotation since Spring 4.3, used to be
  `@RequestMapping(method=RequestMethod.GET)`, there are also other mapping
  annotations: `@PostMapping`, `@PutMapping`, `@DeleteMapping` and
  `@PatchMapping`
* `@Data`: a Lombok annotation, generating the missing / essential JavaBean
  methods and constructor at runtime in order to keep the code slim and trim
* `@Slf4j`: Simple Logging Facade for Java, a Lombok annotation, making logging
  much easier

## To be Revisited

* [TODO] Write tests
* [TODO] How exactly the autoconfiguration happens
* [TODO] Deeper look into Spring Boot
* [TODO] How should the submit from the form match the domain object?