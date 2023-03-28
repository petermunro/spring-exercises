# Creating a RESTful Greeting Service

In this exercise, we will explore Spring's dependency injection mechanism and various usages of the `@Autowired` annotation. We will create a simple application with different components and learn how to wire them together using Spring.

1. Start by creating a simple Spring project with the web dependency.

2. Create an interface called `GreetingService` with a single method `String greet(String name)`.

3. Implement the `GreetingService` interface in two separate classes: `EnglishGreetingService` and `SpanishGreetingService`. Each class should return a greeting message in their respective language.

4. Annotate both `EnglishGreetingService` and `SpanishGreetingService` with the `@Service` annotation. This tells Spring to manage these classes as beans.

5. Create a class called `GreetingController` and annotate it with `@RestController`.

6. This class will have two dependencies:

   - `EnglishGreetingService`
   - `SpanishGreetingService`

   Declare both dependencies in `GreetingController` by adding private
   fields for `EnglishGreetingService` and `SpanishGreetingService`.

7. Inject the dependencies using the `@Autowired` annotation. You can use one of the following methods:

   - Constructor injection: Create a constructor that takes both services as parameters, annotate the constructor with `@Autowired`, and assign the parameters to the private fields.
   - Setter injection: Create setter methods for both services, annotate the setter methods with `@Autowired`, and assign the parameters to the private fields.
   - Field injection: Add the `@Autowired` annotation before each private field.

   Choose one method and implement it in your `GreetingController`.

8. Create two GET mappings in `GreetingController`:

   - `/greet/english`: This endpoint should take a name query parameter and return the greeting message from `EnglishGreetingService`.
   - `/greet/spanish`: This endpoint should take a name query parameter and return the greeting message from SpanishGreetingService.

9. Test your application by running it and using a browser or a tool like Postman to send GET requests to `/greet/english?name=John` and `/greet/spanish?name=Juan`.

10. Try changing the injection method in step 7 to one of the other methods and observe if there are any changes in the behaviour of your application.

11. Answer the following questions:

      1. What is the purpose of the `@Autowired` annotation in Spring?

      2. What are the differences between the three injection methods (field, constructor, and setter)?

      3. How can you use the `@Qualifier` annotation to resolve ambiguity when there are multiple implementations of the same interface?

      4. How can you create a custom bean using the @Bean annotation in a configuration class?

      5. What are the different bean scopes in Spring, and how can you change the scope of a bean using the @Scope annotation?
