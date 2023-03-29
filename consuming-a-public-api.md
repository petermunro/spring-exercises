# Spring Exercise: Consuming a Public API using Spring RESTClient

In this exercise, you will learn how to use Spring RESTClient to consume data from a public API. We will be using the OpenWeatherMap API, which provides weather information for different cities. You will need to sign up for a free API key to access the service.

1. Sign up for an API key: Go to the OpenWeatherMap website (https://openweathermap.org/) and sign up for a free account. Once you've signed up and logged in, go to the API keys section and generate a new API key.

2. Create a new Spring Boot project: Using Spring Initializr (https://start.spring.io/), create a new Spring Boot project with the following dependencies:

    - Web
    - Lombok

3. Import the project: Import the generated project into your favorite IDE.

4. Create a `WeatherService` class: In your project, create a new class called `WeatherService`. This class will be responsible for consuming the OpenWeatherMap API using Spring's RESTClient.

5. Add necessary annotations: Annotate the `WeatherService` class with `@Service` to make it a Spring service.

6. Create a `RestTemplate` bean: In the main application class, create a new `RestTemplate` bean by adding the following method:

    ```java
    @Bean
    public `RestTemplate` restTemplate(RestTemplateBuilder builder) {
        return builder.build();
    }
    ```

7. Inject the `RestTemplate`: In the `WeatherService` class, inject the `RestTemplate` bean using the `@Autowired` annotation.

8. Add the API key: In the `application.properties` file, add the following line with your OpenWeatherMap API key:

    ```
    openweathermap.api-key=YOUR_API_KEY
    ```

    In the `WeatherService` class, use the `@Value` annotation to inject the API key:

    ```java
    @Value("${openweathermap.api-key}")
    private String apiKey;
    ```

9. Create a method to consume the API: In the `WeatherService` class, create a method called `getWeatherForCity` that takes a `String cityName` as an argument. The method should return the weather information for the given city. Use the following API endpoint to fetch the data:

    ```
    http://api.openweathermap.org/data/2.5/weather?q={cityName}&appid={apiKey}&units=metric
    ```

    Replace `{cityName}` and `{apiKey}` with the appropriate variables.

10. Parse the API response:

    - Create a new class called `WeatherResponse` to represent the response from the OpenWeatherMap API.

    - Use Lombok annotations (see [below](#aside-project-lombok) for an introduction to Project Lombok) to generate getters and setters, as well as `@JsonIgnoreProperties(ignoreUnknown = true)` to ignore unknown fields. Map the response fields to the class properties.

11. Call the API and deserialize the response:

    - In the `getWeatherForCity` method, use the `RestTemplate` to call the API and deserialize the JSON response into a `WeatherResponse` object.
    - Return the `WeatherResponse` object.

12. Create a simple controller:

    - Create a new class called `WeatherController` and annotate it with `@RestController`.
    - In this class, inject the `WeatherService` using the `@Autowired` annotation.
    - Create a new endpoint that takes a `cityName` as a path variable and returns the weather information for the city by calling the `getWeatherForCity` method from the `WeatherService`.

Test your application: Start your Spring Boot application and use a tool like Postman or your browser to call the endpoint you created.
For example, if your application is running on http://localhost:8080, you can call the endpoint with a URL like:

  ```
  http://localhost:8080/weather/London
  ```

Replace "London" with the city name you want to fetch the weather information for.

## Stretch Goals

1. Handle errors: If the API returns an error, handle it gracefully by catching exceptions and returning a suitable error message. You can use a `try-catch` block in the `WeatherService` class and return a custom error response.

2. Customize the response: Instead of returning the entire `WeatherResponse` object, create a new class called `WeatherSummary` that contains only the information you want to display. In the `WeatherService` class, map the `WeatherResponse` object to a `WeatherSummary` object before returning it to the controller.
3. Explore other API endpoints: The OpenWeatherMap API provides various other endpoints to fetch weather information, such as forecast data or historical data. Explore the API documentation and try to implement a new endpoint in your application that consumes a different OpenWeatherMap API endpoint.

By completing this exercise, you have learned how to use Spring `RESTClient` to consume data from a public API. You have also learned how to handle errors, parse API responses, and create simple RESTful endpoints in a Spring Boot application.


---

## Aside: Project Lombok

[Project Lombok](https://projectlombok.org/) is a Java library that helps reduce boilerplate code in your applications. It provides a set of annotations and tools that simplify common tasks like generating getters, setters, constructors, `toString`, `equals`, and `hashCode` methods. By using Lombok, you can keep your codebase clean, concise, and more readable.

Here are some key Lombok annotations and their purpose:

- `@Getter` and `@Setter`: Generates getter and setter methods for class fields.

- `@ToString`: Generates a toString method that includes the class fields.

- `@EqualsAndHashCode`: Generates equals and hashCode methods based on the  class fields.

- `@NoArgsConstructor`, `@AllArgsConstructor`, and `@RequiredArgsConstructor`:  Generates constructors with no arguments, all arguments, or only required (final or non-null) arguments, respectively.

- `@Data`: A shortcut that combines `@Getter`, `@Setter`, `@ToString`,
`@EqualsAndHashCode`, and `@RequiredArgsConstructor` for a class.

- `@Builder`: Generates a builder pattern implementation for a class, allowing 
for more readable and flexible object creation.

- `@Slf4j`, `@Log4j2`, etc.: Adds a logging framework-specific logger to the 
  class, enabling simple logging without explicitly declaring a logger instance.

To use Lombok in your project, you need to add it as a dependency and enable annotation processing in your IDE. Most modern IDEs, such as IntelliJ IDEA and Eclipse, support Lombok via plugins.

Keep in mind that, although Lombok makes your code cleaner and more concise, it may also introduce some drawbacks. Some developers argue that Lombok adds an extra layer of complexity and can make it more difficult for new developers to understand the codebase. Additionally, it adds another dependency to your project, which might have compatibility issues with other libraries or tools. Weigh the benefits and drawbacks before adopting Lombok in your projects.
