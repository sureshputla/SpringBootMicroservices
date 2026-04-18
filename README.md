# SpringBootMicroservices

> A hands-on, beginner-friendly project to learn and practice **Microservices with Spring Boot**.

---

## 📋 2-Week Learning Plan

This plan takes you from **zero** to building and running a small microservices system.  
No prior Spring Boot or Microservices knowledge is required — only basic Java familiarity is assumed.

---

### Prerequisites (before Day 1)

| Topic | What you need |
|-------|--------------|
| Java | Basic OOP — classes, interfaces, collections, generics |
| Build tool | Install [Maven](https://maven.apache.org/download.cgi) or [Gradle](https://gradle.org/install/) |
| IDE | [IntelliJ IDEA Community](https://www.jetbrains.com/idea/download/) (recommended) or VS Code with Java extensions |
| Docker | Install [Docker Desktop](https://www.docker.com/products/docker-desktop/) |
| Git | `git` CLI or GitHub Desktop |

---

## 🗓️ Week 1 — Spring Boot Fundamentals

### Day 1 — Introduction to Spring & Spring Boot

**Goals**
- Understand what the Spring Framework is and the problems it solves (Dependency Injection, IoC).
- Understand what Spring Boot adds on top of Spring (auto-configuration, embedded server, starters).
- Generate and run your first Spring Boot application.

**Topics**
- Spring Core: beans, `ApplicationContext`, `@Component`, `@Autowired`
- Spring Boot: `@SpringBootApplication`, `spring-boot-starters`, embedded Tomcat
- Project Lombok (`@Data`, `@Builder`, `@Slf4j`) to reduce boilerplate

**Hands-on**
1. Go to [https://start.spring.io](https://start.spring.io), select Maven, Java 17, add **Spring Web** dependency, download and open the project.
2. Create a `HelloController` with a single `GET /hello` endpoint that returns `"Hello, Spring Boot!"`.
3. Run the app and verify it at `http://localhost:8080/hello`.

**Resources**
- [Spring Quickstart Guide](https://spring.io/quickstart)
- [Baeldung — What is Spring Boot?](https://www.baeldung.com/spring-boot)

---

### Day 2 — Building REST APIs

**Goals**
- Build a full CRUD REST API.
- Understand request mapping, path variables, request bodies, and response status codes.

**Topics**
- `@RestController`, `@RequestMapping`, `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`
- `@PathVariable`, `@RequestParam`, `@RequestBody`
- `ResponseEntity<T>` for controlling HTTP status codes
- Global exception handling with `@ControllerAdvice` and `@ExceptionHandler`

**Hands-on**
1. Create a `Product` model (`id`, `name`, `price`).
2. Build a `ProductController` with endpoints: `GET /products`, `GET /products/{id}`, `POST /products`, `PUT /products/{id}`, `DELETE /products/{id}`.
3. Use an in-memory `List` as temporary storage (no database yet).
4. Add a custom `ProductNotFoundException` and a `@ControllerAdvice` that returns a `404` response.

**Resources**
- [Baeldung — Building a REST API with Spring Boot](https://www.baeldung.com/building-a-restful-web-service-with-spring-and-java-based-configuration)
- [Spring MVC Annotations Guide](https://www.baeldung.com/spring-mvc-annotations)

---

### Day 3 — Persistence with Spring Data JPA

**Goals**
- Connect a Spring Boot app to a relational database.
- Use Spring Data JPA to avoid writing boilerplate SQL.

**Topics**
- JPA / Hibernate basics: entities, relationships (`@OneToMany`, `@ManyToOne`), `@Id`, `@GeneratedValue`
- `JpaRepository` and derived query methods (`findByName`, `findByPriceGreaterThan`)
- H2 in-memory database for development; PostgreSQL for production
- `application.properties` / `application.yml` database configuration
- Database migrations with **Flyway** or **Liquibase** (brief introduction)

**Hands-on**
1. Add `spring-boot-starter-data-jpa` and `h2` dependencies.
2. Annotate `Product` with `@Entity` and update `ProductController` to use a `ProductRepository`.
3. Open the H2 console at `http://localhost:8080/h2-console` and inspect the auto-created table.
4. Add a `Category` entity and set up a `@ManyToOne` relationship from `Product` to `Category`.

**Resources**
- [Baeldung — Spring Data JPA](https://www.baeldung.com/the-persistence-layer-with-spring-data-jpa)
- [Spring Data JPA Docs](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/)

---

### Day 4 — Configuration, Profiles, and Validation

**Goals**
- Understand how Spring Boot manages external configuration.
- Apply validation to API inputs.

**Topics**
- `application.properties` vs `application.yml`
- `@Value`, `@ConfigurationProperties`
- Spring Profiles (`@Profile`, `--spring.profiles.active=dev`)
- Bean Validation: `@NotNull`, `@Size`, `@Min`, `@Max`, `@Email`, `@Valid` on `@RequestBody`

**Hands-on**
1. Move hardcoded values (e.g., app name, page size) to `application.yml`.
2. Create `application-dev.yml` and `application-prod.yml` with different datasource configs.
3. Add `@NotNull`, `@Size(min=2)` to the `Product` model and `@Valid` to the POST/PUT endpoints.
4. Run the app with `-Dspring.profiles.active=dev` and verify the correct config is loaded.

**Resources**
- [Baeldung — Spring Boot Configuration](https://www.baeldung.com/spring-boot-application-configuration)
- [Bean Validation with Spring Boot](https://www.baeldung.com/spring-boot-bean-validation)

---

### Day 5 — Security with Spring Security

**Goals**
- Secure REST endpoints with HTTP Basic and JWT token-based authentication.

**Topics**
- `spring-boot-starter-security` and default form login
- `SecurityFilterChain` configuration (Spring Security 6 style)
- Password encoding with `BCryptPasswordEncoder`
- JWT (JSON Web Token): structure, signing, and validation
- Roles and method-level security (`@PreAuthorize`)

**Hands-on**
1. Add `spring-boot-starter-security`. Notice all endpoints are now protected.
2. Configure an in-memory `UserDetailsService` with two users: `USER` and `ADMIN` roles.
3. Protect `DELETE /products/{id}` to require `ADMIN` role.
4. *(Stretch goal)* Add the `jjwt` library, create a `JwtService`, and replace Basic Auth with JWT bearer token authentication.

**Resources**
- [Baeldung — Spring Security Getting Started](https://www.baeldung.com/spring-security-login)
- [Spring Security with JWT](https://www.baeldung.com/spring-security-oauth-jwt)

---

### Day 6 — Testing Spring Boot Applications

**Goals**
- Write unit and integration tests for Spring Boot applications.

**Topics**
- JUnit 5 and Mockito basics
- `@SpringBootTest` for full integration tests
- `@WebMvcTest` for testing controllers in isolation (MockMvc)
- `@DataJpaTest` for testing the repository layer with an embedded database
- `@MockBean` to replace real beans with mocks in the Spring context

**Hands-on**
1. Write a unit test for a `ProductService` method using Mockito.
2. Write a `@WebMvcTest` for `ProductController`: test happy path and 404 error case.
3. Write a `@DataJpaTest` to verify a custom repository query.
4. Run all tests with `mvn test` and check coverage.

**Resources**
- [Baeldung — Testing in Spring Boot](https://www.baeldung.com/spring-boot-testing)
- [Mockito Documentation](https://site.mockito.org/)

---

### Day 7 — Week 1 Review & Mini-Project

**Goals**
- Consolidate everything learned in Week 1.

**Mini-Project: Product Catalogue Service**

Build a standalone Spring Boot service with:
- `Product` and `Category` JPA entities
- Full CRUD REST API (`/api/v1/products`, `/api/v1/categories`)
- Input validation on all write endpoints
- `dev` profile using H2; `prod` profile stub using PostgreSQL config
- JWT-secured endpoints (read = public, write = `ADMIN`)
- At least 10 tests covering the controller and repository layers

---

## 🗓️ Week 2 — Microservices with Spring Cloud

### Day 8 — Introduction to Microservices

**Goals**
- Understand what Microservices are and when (not) to use them.
- Learn the key patterns that make Microservices work.

**Topics**
- Monolith vs Microservices: tradeoffs (team autonomy, independent deployment, network complexity)
- The 12-Factor App principles
- Key patterns: Service Discovery, API Gateway, Circuit Breaker, Distributed Tracing, Event-Driven Communication
- Domain-Driven Design (DDD) basics: bounded contexts and how they map to services

**Hands-on**
1. Sketch a simple e-commerce system on paper (or [draw.io](https://draw.io)): identify `Order Service`, `Product Service`, `User Service`, and `Notification Service`.
2. Define the API contract (HTTP verbs + path + request/response bodies) for each service.

**Resources**
- [Martin Fowler — Microservices](https://martinfowler.com/articles/microservices.html)
- [12factor.net](https://12factor.net/)
- [Microservices Patterns (book)](https://microservices.io/patterns/index.html)

---

### Day 9 — Service Discovery with Netflix Eureka

**Goals**
- Run multiple services that automatically discover each other without hardcoded URLs.

**Topics**
- Why service discovery? (dynamic IPs, multiple instances, load balancing)
- Eureka Server and Eureka Client
- `@EnableEurekaServer`, `spring-cloud-starter-netflix-eureka-client`
- Client-side load balancing with Spring Cloud LoadBalancer

**Hands-on**
1. Create a new Spring Boot project `discovery-server`; add `spring-cloud-starter-netflix-eureka-server` and annotate the main class with `@EnableEurekaServer`.
2. Register the **Product Service** (from Day 7) as a Eureka client.
3. Create a minimal **Order Service** that also registers with Eureka.
4. Open the Eureka dashboard at `http://localhost:8761` and verify both services appear.

**Resources**
- [Baeldung — Spring Cloud Netflix Eureka](https://www.baeldung.com/spring-cloud-netflix-eureka)
- [Spring Cloud Netflix Docs](https://docs.spring.io/spring-cloud-netflix/docs/current/reference/html/)

---

### Day 10 — API Gateway with Spring Cloud Gateway

**Goals**
- Route all external traffic through a single entry point.
- Apply cross-cutting concerns (authentication, rate limiting, logging) in one place.

**Topics**
- Spring Cloud Gateway: routes, predicates, filters
- Route configuration in `application.yml`
- Global filter for logging
- Integration with Eureka for dynamic routing (`lb://service-name`)
- *(Optional)* Rate limiting with Redis `RequestRateLimiter` filter

**Hands-on**
1. Create a `api-gateway` project with `spring-cloud-starter-gateway` and the Eureka client dependency.
2. Configure routes for Product Service and Order Service in `application.yml`.
3. Add a `GlobalFilter` that logs the request method and path.
4. Test that `http://localhost:8080/api/v1/products` (via the gateway) correctly reaches Product Service.

**Resources**
- [Baeldung — Spring Cloud Gateway](https://www.baeldung.com/spring-cloud-gateway)
- [Spring Cloud Gateway Docs](https://docs.spring.io/spring-cloud-gateway/docs/current/reference/html/)

---

### Day 11 — Inter-Service Communication

**Goals**
- Call one microservice from another synchronously.

**Topics**
- Synchronous vs asynchronous communication
- `RestTemplate` (legacy) and `WebClient` (reactive, preferred)
- OpenFeign declarative HTTP client (`@FeignClient`)
- Passing request headers (e.g., JWT token) between services using `RequestInterceptor`

**Hands-on**
1. Add `spring-cloud-starter-openfeign` to Order Service.
2. Create a `ProductClient` interface annotated with `@FeignClient(name = "product-service")`.
3. In the Order Service, when creating an order, call `ProductClient` to verify the product exists and fetch its price.
4. Test with Eureka running: create an order via the API Gateway and observe the Feign call in logs.

**Resources**
- [Baeldung — Spring Cloud OpenFeign](https://www.baeldung.com/spring-cloud-openfeign)
- [Baeldung — WebClient Guide](https://www.baeldung.com/spring-5-webclient)

---

### Day 12 — Resilience with Circuit Breaker (Resilience4j)

**Goals**
- Prevent cascading failures when one service is slow or unavailable.

**Topics**
- Failure patterns in distributed systems: timeouts, cascading failures
- Circuit Breaker states: Closed → Open → Half-Open
- Resilience4j: `@CircuitBreaker`, `@Retry`, `@TimeLimiter`, `@Bulkhead`
- Fallback methods
- Actuator endpoint `/actuator/health` for circuit breaker state

**Hands-on**
1. Add `resilience4j-spring-boot3` and `spring-boot-starter-aop` to Order Service.
2. Annotate the Feign call to Product Service with `@CircuitBreaker(name = "productService", fallbackMethod = "productFallback")`.
3. Write a fallback that returns a default `ProductResponse` with a warning message.
4. Stop Product Service and verify Order Service returns the fallback response instead of an error.

**Resources**
- [Baeldung — Resilience4j](https://www.baeldung.com/resilience4j)
- [Resilience4j Docs](https://resilience4j.readme.io/docs/getting-started)

---

### Day 13 — Centralized Configuration & Distributed Tracing

**Goals**
- Manage configuration for all services from one place.
- Trace a request as it flows through multiple services.

**Topics (Config Server)**
- `spring-cloud-config-server` and Git-backed configuration
- `spring-cloud-starter-config` on the client side
- Refreshing config without restarting: `@RefreshScope` and `/actuator/refresh`

**Topics (Distributed Tracing)**
- Why distributed tracing? (correlating logs across services)
- Micrometer Tracing + Zipkin (or Jaeger)
- `traceId` and `spanId` propagation via HTTP headers
- Viewing traces in the Zipkin UI

**Hands-on**
1. Create a `config-server` project, back it with a local Git repo, and push `product-service.yml` there.
2. Update Product Service to fetch its config from the Config Server.
3. Add `micrometer-tracing-bridge-brave` and `zipkin-reporter-brave` to all services.
4. Run Zipkin with Docker: `docker run -d -p 9411:9411 openzipkin/zipkin`.
5. Make a request through the Gateway → Order Service → Product Service and find the full trace in the Zipkin UI.

**Resources**
- [Baeldung — Spring Cloud Config](https://www.baeldung.com/spring-cloud-configuration)
- [Spring Boot Distributed Tracing (Micrometer)](https://www.baeldung.com/spring-boot-3-spring-6-new-features#tracing)

---

### Day 14 — Containerisation with Docker & Final Project

**Goals**
- Package each service into a Docker image and run the entire system with Docker Compose.

**Topics**
- Writing a `Dockerfile` for a Spring Boot app (multi-stage build)
- `docker-compose.yml`: services, networks, volumes, environment variables, `depends_on`
- Health checks and service startup order
- Pulling it all together: Discovery Server → Config Server → API Gateway → Services

**Hands-on**
1. Write a multi-stage `Dockerfile` for each service (builder stage with Maven, runtime stage with `eclipse-temurin:17-jre`).
2. Write a `docker-compose.yml` that starts: Zipkin, PostgreSQL, Config Server, Discovery Server, API Gateway, Product Service, Order Service.
3. Run `docker compose up --build` and verify all services start and register with Eureka.
4. Send an end-to-end request through the gateway and trace it in Zipkin.

**Resources**
- [Dockerfile best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [Docker Compose Docs](https://docs.docker.com/compose/)

---

## 🏗️ Final Architecture Overview

```
                         ┌──────────────────┐
                         │   Config Server   │  :8888
                         └────────┬─────────┘
                                  │ (fetches config)
          ┌───────────────────────┼───────────────────────┐
          │                       │                       │
┌─────────▼──────┐    ┌───────────▼───────┐    ┌─────────▼──────┐
│ Discovery Server│    │   API Gateway     │    │  Zipkin (traces)│
│   (Eureka)     │    │  Spring Cloud GW  │    │   :9411         │
│   :8761        │    │   :8080           │    └────────────────┘
└─────────▲──────┘    └──────────┬────────┘
          │ (registers)          │ (routes)
          │               ┌──────┴──────┐
          │               │             │
┌─────────┴──────────┐  ┌─▼────────────▼──┐
│  Product Service   │  │  Order Service   │
│   :8081            │◄─│  :8082           │
│   (PostgreSQL :5432)│  │  (Feign client)  │
└────────────────────┘  └─────────────────┘
```

---

## 📚 Recommended Reading Order

| # | Resource | Type |
|---|----------|------|
| 1 | [Spring Boot Reference Docs](https://docs.spring.io/spring-boot/docs/current/reference/html/) | Documentation |
| 2 | [Spring Microservices in Action (book)](https://www.manning.com/books/spring-microservices-in-action-second-edition) | Book |
| 3 | [Microservices Patterns (book)](https://www.manning.com/books/microservices-patterns) | Book |
| 4 | [Baeldung Spring Cloud series](https://www.baeldung.com/spring-cloud) | Blog |
| 5 | [Martin Fowler's Microservices article](https://martinfowler.com/articles/microservices.html) | Article |

---

## ✅ Daily Checklist Template

For each day, track your progress:

- [ ] Read the theory
- [ ] Complete the hands-on exercises
- [ ] Push code to your own fork/branch
- [ ] Note one thing that confused you — search for the answer and write it down

---

## 🗂️ Suggested Repository Structure

```
SpringBootMicroservices/
├── discovery-server/        # Eureka Server (Day 9)
├── config-server/           # Spring Cloud Config (Day 13)
├── api-gateway/             # Spring Cloud Gateway (Day 10)
├── product-service/         # Product Catalogue (Days 1-7, 9-13)
├── order-service/           # Order management (Days 9-13)
├── docker-compose.yml       # Full system (Day 14)
└── README.md
```

Each sub-project is a standalone Spring Boot application generated from [start.spring.io](https://start.spring.io).

---

*Happy learning! 🚀 Commit your code every day and don't skip the hands-on exercises — building things is the fastest way to learn.*
