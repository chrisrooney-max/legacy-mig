<!-- Input files processed:
- src/spring-framework/build.gradle
- src/spring-framework/settings.gradle
- src/spring-framework/gradle.properties
- src/spring-framework/buildSrc/build.gradle
- src/spring-framework/buildSrc/gradle.properties
- src/spring-framework/framework-platform/framework-platform.gradle
- src/spring-framework/framework-api/framework-api.gradle
- src/spring-framework/framework-bom/framework-bom.gradle
- src/spring-framework/integration-tests/integration-tests.gradle
- src/spring-framework/spring-aop/spring-aop.gradle
- src/spring-framework/spring-aspects/spring-aspects.gradle
- src/spring-framework/spring-beans/spring-beans.gradle
- src/spring-framework/spring-context/spring-context.gradle
- src/spring-framework/spring-context-indexer/spring-context-indexer.gradle
- src/spring-framework/spring-context-support/spring-context-support.gradle
- src/spring-framework/spring-core/spring-core.gradle
- src/spring-framework/spring-core-test/spring-core-test.gradle
- src/spring-framework/spring-expression/spring-expression.gradle
- src/spring-framework/spring-instrument/spring-instrument.gradle
- src/spring-framework/spring-jdbc/spring-jdbc.gradle
- src/spring-framework/spring-jms/spring-jms.gradle
- src/spring-framework/spring-messaging/spring-messaging.gradle
- src/spring-framework/spring-orm/spring-orm.gradle
- src/spring-framework/spring-oxm/spring-oxm.gradle
- src/spring-framework/spring-r2dbc/spring-r2dbc.gradle
- src/spring-framework/spring-test/spring-test.gradle
- src/spring-framework/spring-tx/spring-tx.gradle
- src/spring-framework/spring-web/spring-web.gradle
- src/spring-framework/spring-webflux/spring-webflux.gradle
- src/spring-framework/spring-webmvc/spring-webmvc.gradle
- src/spring-framework/spring-websocket/spring-websocket.gradle
- src/spring-framework/gradle/spring-module.gradle
- src/spring-framework/gradle/ide.gradle
- src/spring-framework/spring-beans/src/main/resources/META-INF/spring.handlers
- src/spring-framework/spring-beans/src/main/resources/META-INF/spring.schemas
- src/spring-framework/spring-context/src/main/resources/META-INF/spring.handlers
- src/spring-framework/spring-context/src/main/resources/META-INF/spring.schemas
- src/spring-framework/spring-aop/src/main/resources/META-INF/spring.handlers
- src/spring-framework/spring-tx/src/main/resources/META-INF/spring.handlers
- src/spring-framework/spring-webmvc/src/main/resources/META-INF/spring.handlers
- src/spring-framework/spring-webmvc/src/main/resources/org/springframework/web/servlet/DispatcherServlet.properties
- src/spring-framework/spring-aspects/src/main/resources/META-INF/aop.xml
- src/spring-framework/spring-web/src/main/resources/META-INF/web-fragment.xml
- src/spring-framework/spring-jdbc/src/main/resources/org/springframework/jdbc/support/sql-error-codes.xml
- src/spring-framework/spring-core/src/main/java/org/springframework/aot/AotDetector.java
- src/spring-framework/spring-core/src/main/java/org/springframework/core/SpringVersion.java
- src/spring-framework/spring-core/src/main/java/org/springframework/core/retry/RetryTemplate.java
- src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/BeanFactory.java
- src/spring-framework/spring-context/src/main/java/org/springframework/context/ApplicationContext.java
- src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/DispatcherServlet.java (partial)
- src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/DispatcherHandler.java (partial)
- src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/JdbcTemplate.java (partial)
- src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/PlatformTransactionManager.java
- src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/annotation/Transactional.java (partial)
- src/spring-framework/spring-web/src/main/java/org/springframework/web/client/RestTemplate.java (partial)
- src/spring-framework/spring-web/src/main/java/org/springframework/web/client/RestClient.java (partial)
- src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/function/client/WebClient.java (partial)
- All package-level directory listings for all 22 Spring modules (5,206 non-test Java source files surveyed in full)
-->

# Spring Framework — Application Analysis

**Produced for:** Legacy Application Programme (LAP)
**Date:** 29 April 2026
**Analyst note:** This is an analysis of the Spring Framework open-source codebase itself (version 7.1.0-SNAPSHOT), not an application built on top of Spring. It is a comprehensive, multi-module Java application framework that end-user applications depend upon. Every section below treats the framework's own code as the subject of analysis.

---

## 1. Application Overview

- **Purpose:** Spring Framework is a comprehensive, open-source application framework and inversion-of-control container for the Java platform, providing foundational infrastructure services — including dependency injection, aspect-oriented programming, web MVC, reactive programming, data access, messaging, and testing support — that Java/Kotlin applications build upon rather than re-implement.

- **Technology stack:**
  - Primary language: Java (with significant Kotlin support)
  - Secondary language: Kotlin 2.3.20
  - Build system: Gradle 8.x (multi-project)
  - Target runtime: Java 17 minimum (with multi-release JAR targets for Java 21 and Java 24 in `spring-core`)
  - Reactive runtime: Project Reactor (Reactor Core, Reactor Netty)

- **Framework version:** `7.1.0-SNAPSHOT` (see `src/spring-framework/gradle.properties`)

- **Module structure:**

  | Module | Role |
  |--------|------|
  | `spring-core` | Foundational utilities — type conversion, resource loading, environment abstraction, annotation processing, AOT code generation, reactive adapter registry, retry template |
  | `spring-beans` | IoC container primitives — `BeanFactory`, `BeanDefinition`, bean lifecycle, XML and Groovy bean configuration, property binding |
  | `spring-context` | Full `ApplicationContext`, event system, caching (`@EnableCaching`), scheduling (`@EnableScheduling`), async execution (`@EnableAsync`), validation, scripting, JMX, EJB integration, resilience/retry |
  | `spring-context-support` | Additional context integrations — Caffeine/JCache caching, JavaMail, Quartz scheduler, FreeMarker configuration |
  | `spring-context-indexer` | Annotation processor that generates `META-INF/spring.components` index at compile time for faster component scanning |
  | `spring-aop` | AOP framework — JDK dynamic proxies, CGLIB proxies, `Advisor`/`Pointcut`/`Advice` abstractions, AOP Alliance integration |
  | `spring-aspects` | AspectJ-based aspects — `@Configurable` support, transaction aspects, load-time weaving configuration |
  | `spring-expression` | Spring Expression Language (SpEL) — parser, evaluation context, operators, property access |
  | `spring-instrument` | Java agent (`InstrumentationSavingAgent`) for load-time class transformation |
  | `spring-web` | Web layer foundations — HTTP abstractions (`HttpMethod`, `HttpHeaders`, `MediaType`, `ResponseEntity`), `RestTemplate`, `RestClient`, `HttpMessageConverter` implementations, CORS, multipart, Servlet filters, web service HTTP interface client proxies |
  | `spring-webmvc` | Servlet-based MVC — `DispatcherServlet`, `HandlerMapping`, `HandlerAdapter`, annotation-driven controllers (`@Controller`, `@RequestMapping`), functional routing (`RouterFunction`), view resolution, JSP tag library |
  | `spring-webflux` | Reactive web — `DispatcherHandler`, reactive functional routing, `WebClient`, WebFlux configuration, reactive WebSocket |
  | `spring-websocket` | WebSocket server support — handler abstractions, SockJS fallback, STOMP sub-protocol over WebSocket |
  | `spring-messaging` | Messaging abstractions — `Message`, `MessageChannel`, `MessageHandler`, STOMP protocol, RSocket client, SIMP broker for WebSocket messaging |
  | `spring-tx` | Transaction management — `PlatformTransactionManager`, `ReactiveTransactionManager`, `@Transactional`, declarative transaction AOP, JTA support |
  | `spring-jdbc` | JDBC abstraction — `JdbcTemplate`, `NamedParameterJdbcTemplate`, `JdbcClient`, `RowMapper`, stored procedures, SQL error-code translation, embedded database support |
  | `spring-orm` | ORM integration — JPA (`LocalContainerEntityManagerFactoryBean`, `JpaTransactionManager`), Hibernate native (`LocalSessionFactoryBean`, `HibernateTransactionManager`), EclipseLink |
  | `spring-oxm` | XML marshalling/unmarshalling — `Marshaller`/`Unmarshaller` interfaces, JAXB2, XStream, MIME support |
  | `spring-r2dbc` | Reactive relational database — `DatabaseClient`, reactive named-parameter expansion, `R2dbcTransactionManager` |
  | `spring-jms` | JMS integration — `JmsTemplate`, message listener container, `@JmsListener`, JCA endpoint manager |
  | `spring-test` | Testing support — Spring TestContext Framework, `MockMvc`, `WebTestClient`, test application contexts, `@SpringJUnitConfig`, transactional test utilities, `@DynamicPropertySource` |
  | `spring-core-test` | AOT runtime hints testing agent and test fixtures shared by other modules |
  | `framework-platform` | Gradle Java Platform BOM — centralises version management for all third-party dependencies |
  | `framework-bom` | Published Bill of Materials for downstream consumers |
  | `framework-api` | Aggregation project for unified Javadoc generation |
  | `framework-docs` | Documentation sources (Antora/Asciidoc) and code samples |
  | `integration-tests` | Cross-module integration test suite |

- **External dependencies (principal libraries):**
  - `commons-logging:commons-logging` — logging abstraction (API dependency in `spring-core`)
  - `org.jspecify:jspecify` — null-safety annotations
  - `org.aspectj:aspectjweaver` — AspectJ AOP weaving
  - `com.palantir.javapoet:javapoet` (repackaged as `org.springframework.javapoet`) — Java source code generation for AOT
  - `org.objenesis:objenesis` (repackaged as `org.springframework.objenesis`) — object instantiation without constructors
  - `io.projectreactor:reactor-core` / `reactor-netty-http` — reactive streams, Reactor Netty transport
  - `io.micrometer:micrometer-observation` — observability API (metrics/tracing)
  - `io.micrometer:context-propagation` — reactive context propagation for Micrometer
  - `com.fasterxml.jackson:jackson-bom` (2.21.2) — JSON/XML/CBOR/Smile serialisation
  - `tools.jackson:jackson-bom` (3.1.1) — Jackson 3.x parallel support (next-gen API)
  - `io.netty:netty-bom` (4.2.12.Final) — Netty I/O
  - `org.jetbrains.kotlin:kotlin-reflect` / `kotlin-stdlib` — Kotlin language support
  - `org.jetbrains.kotlinx:kotlinx-coroutines-*` / `kotlinx-serialization-*` — Kotlin coroutines and serialisation
  - `io.rsocket:rsocket-bom` (1.1.5) — RSocket protocol
  - `jakarta.servlet:jakarta.servlet-api` (6.1.0) — Servlet 6.1
  - `jakarta.persistence:jakarta.persistence-api` (3.2.0) — JPA 3.2
  - `jakarta.jms:jakarta.jms-api` (3.1.0) — JMS 3.1
  - `jakarta.validation:jakarta.validation-api` (3.1.0) — Bean Validation 3.1
  - `jakarta.transaction:jakarta.transaction-api` (2.0.1) — JTA 2.0
  - `jakarta.websocket:jakarta.websocket-api` (2.2.0) — WebSocket 2.2
  - `jakarta.xml.bind:jakarta.xml.bind-api` (3.0.1) — JAXB 3
  - `org.hibernate.orm:hibernate-core` — Hibernate 7 (optional ORM provider)
  - `org.eclipse.persistence:org.eclipse.persistence.jpa` — EclipseLink (optional ORM provider)
  - `org.freemarker:freemarker` — FreeMarker template engine (optional view layer)
  - `org.apache.groovy:groovy-bom` (5.0.5) — Groovy scripting support
  - `org.graalvm.sdk:graal-sdk` — GraalVM native image hints
  - `io.projectreactor.tools:blockhound` — blocking call detection in reactive code
  - `com.github.ben-manes.caffeine:caffeine` — Caffeine in-memory cache
  - `org.quartz-scheduler:quartz` — Quartz job scheduler (via `spring-context-support`)
  - `org.apache.httpcomponents.client5:httpclient5` — Apache HttpClient 5 (optional HTTP transport)
  - `io.vavr:vavr` — functional data structures (optional transaction support)
  - `org.webjars:webjars-locator-lite` — static asset versioning (optional)
  - JUnit 5 / JUnit Platform (6.0.3), Mockito (5.23.0), AssertJ (3.27.7), MockK (1.14.5) — testing

- **Configuration summary:**
  - Version controlled via `gradle.properties`: `version=7.1.0-SNAPSHOT`
  - Kotlin version: `kotlinVersion=2.3.20`, Byte Buddy version: `byteBuddyVersion=1.17.6`
  - Gradle caching and parallel execution enabled (`org.gradle.caching=true`, `org.gradle.parallel=true`)
  - JVM heap for build: `-Xmx2048m`
  - Multi-release JARs: `spring-core` targets Java 21 and Java 24 class file versions alongside the baseline
  - AOT mode toggled via system property `spring.aot.enabled=true` or automatically in GraalVM native images
  - XML namespace handlers registered via `META-INF/spring.handlers` in each module (beans, context, aop, tx, mvc, websocket, etc.)
  - SQL error-code translation configured via `spring-jdbc`'s bundled `sql-error-codes.xml` covering DB2, Derby, H2, HyperSQL, MySQL, Oracle, PostgreSQL, SQL Server, Sybase, and others

---

## 2. User Roles and Access Control

Spring Framework is an infrastructure framework, not an end-user application. It does not define application-level user roles, authentication mechanisms, or access control policies itself. It provides the tooling for application developers to implement those concerns. The sections below describe what the framework supplies as building blocks.

| Role | Permissions / Access | Source |
|------|---------------------|--------|
| Framework developer / contributor | Full access to all module source code; commits governed by DCO sign-off | `src/spring-framework/.github/dco.yml` |
| Application developer (downstream consumer) | Uses published framework JARs; no special access required beyond the published API | `src/spring-framework/framework-bom/` |
| No end-user roles defined | The framework contains no user authentication or role-based access control of its own | N/A |

- **Authentication mechanism:** Not present in the framework itself. Spring Framework provides integration hooks (`DelegatingFilterProxy`, `WebFilter`) that Spring Security (a separate project) plugs into. The framework's `UserRoleAuthorizationInterceptor` in `spring-webmvc` (`src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/handler/UserRoleAuthorizationInterceptor.java`) provides a simple Servlet-role check as a `HandlerInterceptor`, delegating to `HttpServletRequest.isUserInRole()`.

- **Authorisation approach:** The framework does not implement authorisation itself. It provides the proxy/AOP infrastructure (`AopProxyFactory`, `ProxyFactory`, `MethodInterceptor`) on top of which Spring Security can apply method-level security annotations such as `@PreAuthorize`. The `@Transactional` annotation's proxy machinery is an analogous pattern for transactional boundaries.

---

## 3. Features and Capabilities

#### Inversion of Control / Dependency Injection Container

- **Description:** The framework's foundational feature. Beans (application components) are described as `BeanDefinition` instances; the container instantiates, wires, and manages their lifecycle. Dependency injection is supported via constructor injection, setter injection, and field injection (the latter through `@Autowired`). Configuration can be XML-based, annotation-based (`@Configuration`, `@Bean`, `@Component`), or programmatic (`GenericApplicationContext`, `BeanDefinitionBuilder`).
- **Key classes/interfaces:**
  - `BeanFactory` — root IoC container interface
  - `DefaultListableBeanFactory` — primary concrete implementation
  - `AbstractAutowireCapableBeanFactory` — autowiring and lifecycle orchestration
  - `ApplicationContext` — enriched container interface (extends `BeanFactory`, `MessageSource`, `ApplicationEventPublisher`, `ResourcePatternResolver`)
  - `GenericApplicationContext` / `AnnotationConfigApplicationContext` / `ClassPathXmlApplicationContext` — concrete context implementations
  - `BeanDefinition` / `RootBeanDefinition` — bean metadata model
  - `ConfigurationClassPostProcessor` — processes `@Configuration` classes
  - `ClassPathBeanDefinitionScanner` — component-scan implementation
  - `AnnotatedBeanDefinitionReader` — registers `@Component`-annotated classes
- **Source files:**
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/BeanFactory.java`
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/DefaultListableBeanFactory.java`
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/AbstractAutowireCapableBeanFactory.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/ApplicationContext.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/support/AbstractApplicationContext.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/support/GenericApplicationContext.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/ConfigurationClassPostProcessor.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/ClassPathBeanDefinitionScanner.java`
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/RootBeanDefinition.java`

#### Aspect-Oriented Programming (AOP)

- **Description:** Provides proxy-based AOP supporting both JDK dynamic proxies and CGLIB subclass proxies. Supports the AspectJ annotation model (`@Aspect`, `@Before`, `@After`, `@Around`, `@Pointcut`) via auto-proxy infrastructure (`EnableAspectJAutoProxy`). Also supports full AspectJ load-time weaving through the Java instrumentation agent.
- **Key classes/interfaces:**
  - `AopProxy` / `AopProxyFactory` / `DefaultAopProxyFactory` — proxy creation
  - `JdkDynamicAopProxy` — JDK reflection-based proxy
  - `CglibAopProxy` / `ObjenesisCglibAopProxy` — CGLIB subclass proxy
  - `Advisor` / `Pointcut` / `MethodInterceptor` — AOP Alliance interception model
  - `ReflectiveMethodInvocation` — joins method invocations
  - `ProxyFactory` / `ProxyFactoryBean` — programmatic proxy creation
  - `AbstractAdvisingBeanPostProcessor` — base for annotation-driven advisors
  - `AopNamespaceHandler` — XML `<aop:*>` namespace handler
- **Source files:**
  - `src/spring-framework/spring-aop/src/main/java/org/springframework/aop/framework/` (all files)
  - `src/spring-framework/spring-aop/src/main/java/org/springframework/aop/aspectj/` (AspectJ integration)
  - `src/spring-framework/spring-aop/src/main/resources/META-INF/spring.handlers`
  - `src/spring-framework/spring-aspects/src/main/resources/META-INF/aop.xml`

#### Servlet-Based Web MVC (Spring Web MVC)

- **Description:** A Model-View-Controller framework built on the Jakarta Servlet API. `DispatcherServlet` is the front controller; it delegates to `HandlerMapping` to select a handler, `HandlerAdapter` to invoke it, and `ViewResolver` to render the response. Controllers are typically annotated with `@Controller`/`@RestController` and `@RequestMapping`. Also supports functional-style routing via `RouterFunction` / `RouterFunctions`.
- **Key classes/interfaces:**
  - `DispatcherServlet` — front controller
  - `RequestMappingHandlerMapping` — maps `@RequestMapping` annotations to handlers
  - `RequestMappingHandlerAdapter` — invokes annotated handler methods
  - `ExceptionHandlerExceptionResolver` — `@ExceptionHandler` resolution
  - `ViewResolver` / `InternalResourceViewResolver` — view resolution
  - `ModelAndView` — data model and view name holder
  - `HttpMessageConverter` / `HttpMessageConverters` — message body read/write
  - `HandlerInterceptor` — pre/post/completion hooks on requests
  - `WebMvcConfigurer` / `WebMvcConfigurationSupport` — Java config extension points
  - `RouterFunction` / `RouterFunctions` / `HandlerFunction` — functional routing DSL
  - `ResponseEntityExceptionHandler` — base class for global exception handling
- **Source files:**
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/DispatcherServlet.java`
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/RequestMappingHandlerMapping.java`
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/RequestMappingHandlerAdapter.java`
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/config/annotation/WebMvcConfigurationSupport.java`
  - `src/spring-framework/spring-webmvc/src/main/resources/org/springframework/web/servlet/DispatcherServlet.properties`
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/function/` (all files)
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/view/` (all files)

#### Reactive Web (Spring WebFlux)

- **Description:** Non-blocking, reactive web framework built on Project Reactor and the Reactive Streams specification. `DispatcherHandler` is the reactive equivalent of `DispatcherServlet`. Supports both annotation-based controllers (identical annotation model to Spring Web MVC) and functional routing. HTTP client is `WebClient`.
- **Key classes/interfaces:**
  - `DispatcherHandler` — reactive front controller
  - `WebHandler` / `WebFilter` / `WebFilterChain` — reactive server abstraction
  - `RouterFunction` / `RouterFunctions` / `HandlerFunction` — reactive functional routing
  - `WebClient` — non-blocking, reactive HTTP client
  - `WebFluxConfigurer` / `WebFluxConfigurationSupport` — configuration extension points
  - `ServerWebExchange` — reactive request/response exchange
  - `EnableWebFlux` — Java config switch
- **Source files:**
  - `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/DispatcherHandler.java`
  - `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/function/client/WebClient.java`
  - `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/config/WebFluxConfigurationSupport.java`
  - `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/function/server/` (all files)
  - `src/spring-framework/spring-web/src/main/java/org/springframework/web/server/` (all files)

#### HTTP Client Abstraction

- **Description:** Provides both synchronous and reactive HTTP clients for outbound HTTP calls. `RestTemplate` is the classic synchronous client (superseded). `RestClient` is the modern fluent synchronous client (introduced in 6.1). `WebClient` is the reactive client. HTTP interface proxies (`@GetExchange`, `@PostExchange` etc.) allow declaring HTTP service interfaces that are generated as proxies at runtime.
- **Key classes/interfaces:**
  - `RestTemplate` — synchronous, template-method pattern HTTP client
  - `RestClient` / `DefaultRestClient` — fluent synchronous HTTP client
  - `WebClient` / `DefaultWebClient` — reactive HTTP client
  - `ClientHttpRequestFactory` — pluggable transport (JDK HttpClient, Apache HttpClient 5, Reactor Netty, Jetty)
  - `ClientHttpRequestInterceptor` — interceptors for `RestTemplate` / `RestClient`
  - `ExchangeFilterFunction` — filter for `WebClient`
  - `HttpServiceProxyFactory` — generates HTTP interface proxies
- **Source files:**
  - `src/spring-framework/spring-web/src/main/java/org/springframework/web/client/RestTemplate.java`
  - `src/spring-framework/spring-web/src/main/java/org/springframework/web/client/RestClient.java`
  - `src/spring-framework/spring-web/src/main/java/org/springframework/web/client/DefaultRestClient.java`
  - `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/function/client/WebClient.java`
  - `src/spring-framework/spring-web/src/main/java/org/springframework/web/service/` (all files)

#### Transaction Management

- **Description:** Provides a consistent transaction abstraction over JDBC, JPA/Hibernate, JTA, JMS, and reactive data sources. Declarative transactions via `@Transactional` are the most common pattern; the annotation is applied through AOP proxying at the method level. Programmatic transactions are supported via `TransactionTemplate`. Supports transaction propagation, isolation levels, timeouts, read-only hints, and rollback rules.
- **Key classes/interfaces:**
  - `PlatformTransactionManager` — synchronous transaction SPI (`getTransaction`, `commit`, `rollback`)
  - `ReactiveTransactionManager` — reactive equivalent
  - `AbstractPlatformTransactionManager` — base implementation (handles propagation, suspension, synchronisation)
  - `DataSourceTransactionManager` — JDBC-specific manager
  - `JpaTransactionManager` — JPA-specific manager
  - `HibernateTransactionManager` — Hibernate native session manager
  - `JtaTransactionManager` — XA / JTA manager
  - `TransactionTemplate` — programmatic transaction helper
  - `TransactionSynchronizationManager` — thread-local resource/synchronisation registry
  - `@Transactional` — declarative annotation (class or method level)
  - `AnnotationTransactionAttributeSource` — reads `@Transactional` metadata
  - `EnableTransactionManagement` — Java config switch
- **Source files:**
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/PlatformTransactionManager.java`
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/support/AbstractPlatformTransactionManager.java`
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/annotation/Transactional.java`
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/support/TransactionTemplate.java`
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/datasource/DataSourceTransactionManager.java`
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/support/JdbcTransactionManager.java`
  - `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/JpaTransactionManager.java`
  - `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/hibernate/HibernateTransactionManager.java`

#### JDBC Data Access

- **Description:** Simplifies JDBC use by managing connection acquisition and release, exception translation, `Statement`/`PreparedStatement`/`CallableStatement` lifecycle, `ResultSet` iteration, and SQL warning handling. Provides callback interfaces for user code to supply SQL and extract results. Named-parameter support via `NamedParameterJdbcTemplate`. Fluent API via `JdbcClient` (introduced in 6.1). Object-based RDBMS operations via `SqlQuery`/`SqlUpdate`/`StoredProcedure`. SQL error codes translated to a consistent `DataAccessException` hierarchy.
- **Key classes/interfaces:**
  - `JdbcTemplate` / `JdbcOperations` — core JDBC template
  - `NamedParameterJdbcTemplate` / `NamedParameterJdbcOperations` — named parameters
  - `JdbcClient` / `DefaultJdbcClient` — fluent, chainable JDBC client
  - `RowMapper<T>` — maps a `ResultSet` row to an object
  - `BeanPropertyRowMapper<T>` / `DataClassRowMapper<T>` — reflective row mappers
  - `ResultSetExtractor<T>` — extracts entire `ResultSet`
  - `PreparedStatementCreator` / `PreparedStatementSetter` — prepared statement callbacks
  - `SQLErrorCodesFactory` / `SQLExceptionTranslator` — error code to `DataAccessException` translation
  - `SqlQuery` / `SqlUpdate` / `StoredProcedure` — object-oriented RDBMS operations
  - `SimpleJdbcCall` / `SimpleJdbcInsert` — simplified stored-procedure and insert wrappers
  - `DataSourceUtils` — connection binding/release
  - `EmbeddedDatabaseBuilder` — in-memory databases (H2, Derby, HSQL) for testing
- **Source files:**
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/JdbcTemplate.java`
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/namedparam/NamedParameterJdbcTemplate.java`
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/simple/JdbcClient.java`
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/` (all files)
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/object/` (all files)
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/support/SQLErrorCodesFactory.java`
  - `src/spring-framework/spring-jdbc/src/main/resources/org/springframework/jdbc/support/sql-error-codes.xml`

#### ORM / JPA Integration

- **Description:** Integrates with JPA-compliant providers (Hibernate, EclipseLink) and with Hibernate's native session API. Provides `LocalContainerEntityManagerFactoryBean` to set up a container-managed `EntityManagerFactory` within Spring. Vendor adapters (`HibernateJpaVendorAdapter`, `EclipseLinkJpaVendorAdapter`) abstract away provider differences.
- **Key classes/interfaces:**
  - `LocalContainerEntityManagerFactoryBean` — creates JPA `EntityManagerFactory`
  - `SharedEntityManagerCreator` — thread-safe `EntityManager` proxy
  - `JpaTransactionManager` — participates in `@Transactional`
  - `JpaVendorAdapter` / `HibernateJpaVendorAdapter` / `EclipseLinkJpaVendorAdapter` — vendor abstraction
  - `LocalSessionFactoryBean` / `LocalSessionFactoryBuilder` — Hibernate native `SessionFactory` setup
  - `HibernateTransactionManager` — Hibernate native transaction management
  - `SpringBeanContainer` — makes Spring DI available inside Hibernate
- **Source files:**
  - `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/LocalContainerEntityManagerFactoryBean.java`
  - `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/JpaTransactionManager.java`
  - `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/vendor/HibernateJpaVendorAdapter.java`
  - `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/hibernate/LocalSessionFactoryBean.java`

#### Reactive Relational Data Access (R2DBC)

- **Description:** Non-blocking, reactive database access using the R2DBC SPI. `DatabaseClient` is the reactive analogue of `JdbcTemplate`, returning `Mono`/`Flux` publishers. Named-parameter expansion is fully supported.
- **Key classes/interfaces:**
  - `DatabaseClient` / `DefaultDatabaseClient` — reactive SQL execution
  - `NamedParameterExpander` — named-parameter `:name` expansion
  - `R2dbcTransactionManager` — reactive transaction manager
  - `RowsFetchSpec` / `FetchSpec` — result publisher abstractions
- **Source files:**
  - `src/spring-framework/spring-r2dbc/src/main/java/org/springframework/r2dbc/core/DatabaseClient.java`
  - `src/spring-framework/spring-r2dbc/src/main/java/org/springframework/r2dbc/core/DefaultDatabaseClient.java`
  - `src/spring-framework/spring-r2dbc/src/main/java/org/springframework/r2dbc/connection/` (connection and transaction classes)

#### Messaging Abstractions and JMS Integration

- **Description:** `spring-messaging` provides generic messaging primitives (`Message`, `MessageChannel`, `MessageHandler`) used by both `spring-jms`, `spring-websocket`, and `spring-messaging`'s STOMP and RSocket support. `spring-jms` provides `JmsTemplate`, message listener containers, and `@JmsListener` annotation support, integrating JMS 3.1 brokers (Apache ActiveMQ Artemis is the test broker).
- **Key classes/interfaces:**
  - `Message<T>` / `MessageChannel` / `MessageHandler` — messaging abstractions
  - `JmsTemplate` — synchronous JMS send/receive
  - `DefaultMessageListenerContainer` — asynchronous JMS listener container
  - `@JmsListener` / `JmsListenerAnnotationBeanPostProcessor` — annotation-driven listeners
  - `StompBrokerRelayMessageHandler` — full-featured STOMP broker relay
  - `SimpleBrokerMessageHandler` — in-process STOMP broker
  - `RSocketRequester` / `RSocketStrategies` — RSocket client abstraction
- **Source files:**
  - `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/Message.java`
  - `src/spring-framework/spring-jms/src/main/java/org/springframework/jms/core/JmsTemplate.java`
  - `src/spring-framework/spring-jms/src/main/java/org/springframework/jms/listener/DefaultMessageListenerContainer.java`
  - `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/simp/stomp/StompBrokerRelayMessageHandler.java`
  - `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/rsocket/RSocketRequester.java`

#### WebSocket Support

- **Description:** Full WebSocket server support including raw WebSocket handler dispatch (`WebSocketHandler`), SockJS fallback transport for environments that do not support native WebSocket, and STOMP messaging over WebSocket with a sub-protocol. `@EnableWebSocketMessageBroker` activates the message broker configuration.
- **Key classes/interfaces:**
  - `WebSocketHandler` / `TextMessage` / `BinaryMessage` — core WebSocket API
  - `WebSocketSession` — active connection
  - `SockJsService` — SockJS transport abstraction
  - `StompSubProtocolHandler` — STOMP framing over WebSocket
  - `EnableWebSocketMessageBroker` / `WebSocketMessageBrokerConfigurer` — broker setup
  - `SimpMessagingTemplate` — send messages to WebSocket destinations
- **Source files:**
  - `src/spring-framework/spring-websocket/src/main/java/org/springframework/web/socket/` (all files)
  - `src/spring-framework/spring-websocket/src/main/java/org/springframework/web/socket/sockjs/` (all files)
  - `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/simp/` (all files)

#### Spring Expression Language (SpEL)

- **Description:** A powerful, runtime expression language supporting property access, method invocation, collection projection/selection, arithmetic, logical and relational operators, bean references, type expressions, constructor calls, and variables. Used extensively internally by the framework (e.g., `@Value`, `@Cacheable`, `@ConditionalOnExpression`, event listeners).
- **Key classes/interfaces:**
  - `Expression` / `ExpressionParser` / `SpelExpressionParser` — public API
  - `EvaluationContext` / `StandardEvaluationContext` — execution context
  - `BeanResolver` — resolves bean references within expressions
  - `SpelNode` / `Ast` — internal AST
- **Source files:**
  - `src/spring-framework/spring-expression/src/main/java/org/springframework/expression/` (all files)
  - `src/spring-framework/spring-expression/src/main/java/org/springframework/expression/spel/` (all files)

#### Caching Abstraction

- **Description:** Cache-agnostic abstraction enabling declarative caching with `@Cacheable`, `@CachePut`, `@CacheEvict`, and `@Caching`. Integrates with Caffeine, JCache (JSR-107), and any custom `CacheManager`/`Cache` implementation. Reactive caching is supported.
- **Key classes/interfaces:**
  - `Cache` / `CacheManager` — core abstraction interfaces
  - `@Cacheable` / `@CachePut` / `@CacheEvict` — declarative annotations
  - `EnableCaching` — Java config switch
  - `CaffeineCacheManager` / `JCacheCacheManager` — provider adapters
  - `CacheInterceptor` — AOP-based cache interception
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/cache/` (all files)
  - `src/spring-framework/spring-context-support/src/main/java/org/springframework/cache/caffeine/`
  - `src/spring-framework/spring-context-support/src/main/java/org/springframework/cache/jcache/`

#### Task Scheduling and Asynchronous Execution

- **Description:** `@Scheduled` enables cron-based, fixed-rate, and fixed-delay task scheduling. `@Async` enables asynchronous method execution backed by a configurable `TaskExecutor`. Reactive scheduling (via Kotlin coroutines and Reactor) is also supported.
- **Key classes/interfaces:**
  - `@Scheduled` / `ScheduledAnnotationBeanPostProcessor` — scheduling engine
  - `@Async` / `AsyncAnnotationBeanPostProcessor` — async execution
  - `TaskScheduler` / `TaskExecutor` — abstractions for scheduling and execution
  - `SimpleAsyncTaskExecutor` / `VirtualThreadTaskExecutor` — concrete executors
  - `EnableScheduling` / `EnableAsync` — Java config switches
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/annotation/` (all files)
  - `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/` (all files)
  - `src/spring-framework/spring-context-support/src/main/java/org/springframework/scheduling/quartz/`

#### Bean Validation and Data Binding

- **Description:** Integrates the Jakarta Bean Validation (JSR-380/3.1) API. `LocalValidatorFactoryBean` creates and exposes a `javax.validation.Validator`. `MethodValidationPostProcessor` applies validation to annotated method parameters and return values via AOP. `DataBinder` performs type conversion and validation during HTTP request parameter binding.
- **Key classes/interfaces:**
  - `LocalValidatorFactoryBean` / `SpringValidatorAdapter` — Validator integration
  - `MethodValidationPostProcessor` / `MethodValidationInterceptor` — method-level validation
  - `DataBinder` — binds request parameters to model objects
  - `Errors` / `BindingResult` — binding/validation result containers
  - `Validator` — Spring's own lighter validation interface
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/validation/beanvalidation/` (all files)
  - `src/spring-framework/spring-context/src/main/java/org/springframework/validation/` (all files)
  - `src/spring-framework/spring-web/src/main/java/org/springframework/web/bind/` (web data binding)

#### Type Conversion and Formatting

- **Description:** A unified type conversion framework (`ConversionService`) replaces `java.beans.PropertyEditor`. Converters (`Converter<S,T>`), `ConverterFactory<S,R>`, and `GenericConverter` are the extension points. The formatting sub-system (`Formatter`) adds locale-aware print/parse for numbers, dates, and currency, with `@NumberFormat` and `@DateTimeFormat` annotations.
- **Key classes/interfaces:**
  - `ConversionService` / `DefaultConversionService` / `FormattingConversionService`
  - `Converter<S,T>` / `ConditionalConverter` / `GenericConverter`
  - `Formatter<T>` / `FormatterRegistry`
  - `@NumberFormat` / `@DateTimeFormat`
- **Source files:**
  - `src/spring-framework/spring-core/src/main/java/org/springframework/core/convert/` (all files)
  - `src/spring-framework/spring-context/src/main/java/org/springframework/format/` (all files)

#### Ahead-of-Time (AOT) Compilation and GraalVM Native Image Support

- **Description:** Introduced in Spring 6.0, the AOT engine performs build-time analysis of bean definitions and generates Java source code (`GeneratedFiles`) and GraalVM `RuntimeHints` (reflection, resource, proxy, serialisation hints). `AotDetector.useGeneratedArtifacts()` switches the runtime to use pre-generated artefacts instead of reflection-heavy initialisation. The context AOT processor (`ContextAotProcessor`, `ApplicationContextAotGenerator`) runs during the build phase.
- **Key classes/interfaces:**
  - `AotDetector` — runtime switch between AOT and standard mode
  - `RuntimeHints` / `ReflectionHints` / `ResourceHints` / `ProxyHints` — hint categories
  - `RuntimeHintsRegistrar` — extension point for registering hints
  - `GenerationContext` / `GeneratedFiles` / `GeneratedClasses` — code generation infrastructure
  - `ContextAotProcessor` / `ApplicationContextAotGenerator` — context-level AOT processing
  - `@Reflective` / `@RegisterReflection` / `@RegisterReflectionForBinding` — hint annotations
- **Source files:**
  - `src/spring-framework/spring-core/src/main/java/org/springframework/aot/` (all files)
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/aot/` (all files)

#### Resilience and Retry

- **Description:** Introduced in Spring 7.0. `RetryTemplate` provides a programmatic retry loop backed by a configurable `RetryPolicy` and `BackOff`. `@Retryable` (in `spring-context`'s resilience package) provides declarative method-level retry via AOP. `@ConcurrencyLimit` provides concurrency throttling. `@EnableResilientMethods` activates annotation-driven resilience.
- **Key classes/interfaces:**
  - `RetryTemplate` / `RetryOperations` — programmatic retry
  - `RetryPolicy` / `DefaultRetryPolicy` — retry decision logic
  - `@Retryable` (core) / `RetryAnnotationBeanPostProcessor` — declarative retry
  - `@ConcurrencyLimit` / `ConcurrencyLimitBeanPostProcessor` — concurrency throttling
  - `EnableResilientMethods` — Java config switch
- **Source files:**
  - `src/spring-framework/spring-core/src/main/java/org/springframework/core/retry/RetryTemplate.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/resilience/` (all files)

#### Environment Abstraction and Externalised Configuration

- **Description:** `Environment` provides access to profiles and `PropertySource` hierarchies. `PropertySource` implementations cover system properties, environment variables, command-line arguments (JOpt Simple), JNDI, and servlet context parameters. `@PropertySource` loads `.properties`/`.yaml` files into the environment. `${...}` placeholders resolved via `PropertySourcesPlaceholderConfigurer`.
- **Key classes/interfaces:**
  - `Environment` / `ConfigurableEnvironment` / `StandardEnvironment`
  - `PropertySource<T>` / `PropertiesPropertySource` / `SystemEnvironmentPropertySource`
  - `MutablePropertySources` / `PropertySourcesPropertyResolver`
  - `Profiles` — profile matching logic
  - `PropertySourcesPlaceholderConfigurer` — `${...}` resolution in bean definitions
  - `@PropertySource` — loads property files
- **Source files:**
  - `src/spring-framework/spring-core/src/main/java/org/springframework/core/env/` (all files)
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/support/PropertySourcesPlaceholderConfigurer.java`

#### Application Event System

- **Description:** Synchronous and asynchronous event publication between loosely coupled components. Events extend `ApplicationEvent`. Listeners implement `ApplicationListener<E>` or use `@EventListener`. `@TransactionalEventListener` binds event processing to transaction phases. The multicaster can be made async by injecting an `Executor`.
- **Key classes/interfaces:**
  - `ApplicationEventPublisher` / `SimpleApplicationEventMulticaster` — publication and dispatch
  - `ApplicationListener<E>` — typed listener interface
  - `@EventListener` / `ApplicationListenerMethodAdapter` — annotation-driven listeners
  - `@TransactionalEventListener` — transaction-bound listeners
  - `ContextRefreshedEvent`, `ContextClosedEvent`, etc. — lifecycle events
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/event/` (all files)
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/event/` (transactional event listener)

#### Resource Loading

- **Description:** Abstracts access to file-system, classpath, URL, and VFS resources behind a uniform `Resource` interface. `ResourceLoader` / `DefaultResourceLoader` resolve resource descriptors. `PathMatchingResourcePatternResolver` supports Ant-style path patterns for scanning.
- **Key classes/interfaces:**
  - `Resource` / `WritableResource` — core abstraction
  - `ClassPathResource` / `FileSystemResource` / `UrlResource` / `ByteArrayResource`
  - `ResourceLoader` / `DefaultResourceLoader` / `ResourcePatternResolver`
  - `PathMatchingResourcePatternResolver` — classpath scanning
  - `VfsResource` / `VfsUtils` — JBoss VFS support
- **Source files:**
  - `src/spring-framework/spring-core/src/main/java/org/springframework/core/io/` (all files)

#### XML Object/XML Marshalling (OXM)

- **Description:** Provides provider-agnostic `Marshaller`/`Unmarshaller` interfaces over JAXB2 and XStream. Used by Spring Web MVC's `MarshallingView` and `MarshallingHttpMessageConverter`.
- **Key classes/interfaces:**
  - `Marshaller` / `Unmarshaller` — SPI interfaces
  - `Jaxb2Marshaller` — JAXB 3 implementation
  - `XStreamMarshaller` — XStream implementation
- **Source files:**
  - `src/spring-framework/spring-oxm/src/main/java/org/springframework/oxm/` (all files)

#### Testing Framework

- **Description:** The Spring TestContext Framework manages a shared, cached `ApplicationContext` across test methods, avoiding expensive context creation per test. Integration with JUnit 5 (`@SpringJUnitConfig`, `@SpringJUnitWebConfig`), JUnit 4, and TestNG. `MockMvc` provides in-process MVC testing without a running server. `WebTestClient` provides reactive/end-to-end testing. `@DynamicPropertySource` injects runtime-discovered properties (e.g., container ports). `@Sql` runs SQL scripts before/after tests.
- **Key classes/interfaces:**
  - `TestContextManager` — orchestrates `TestExecutionListener` callbacks
  - `SmartContextLoader` / `AnnotationConfigContextLoader` — context loading strategy
  - `MockMvc` — in-process Spring MVC test runner
  - `WebTestClient` — reactive test client
  - `@SpringJUnitConfig` / `@SpringJUnitWebConfig` — composite JUnit 5 annotations
  - `@DynamicPropertySource` — dynamic property injection for test containers
  - `@Sql` / `@SqlConfig` — SQL script execution in tests
- **Source files:**
  - `src/spring-framework/spring-test/src/main/java/org/springframework/test/context/` (all files)
  - `src/spring-framework/spring-test/src/main/java/org/springframework/test/web/servlet/MockMvc.java`
  - `src/spring-framework/spring-test/src/main/java/org/springframework/test/web/reactive/` (WebTestClient)

---

## 4. Workflows and Behaviours

#### Servlet HTTP Request Processing (Spring Web MVC)

- **Type:** User-facing
- **Trigger:** An HTTP request received by the Servlet container is forwarded to `DispatcherServlet`.
- **Steps:**
  1. `DispatcherServlet.doService()` — wraps `doDispatch()` and sets up request attributes (`src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/DispatcherServlet.java`).
  2. `DispatcherServlet.doDispatch()` — checks for multipart; iterates `HandlerMapping` list to find a matching `HandlerExecutionChain`.
  3. `HandlerInterceptor.preHandle()` — called for each interceptor in the chain.
  4. `HandlerAdapter.handle()` — invokes the controller method (e.g., via `RequestMappingHandlerAdapter`, which resolves method arguments, calls the method, and processes the return value).
  5. `HandlerInterceptor.postHandle()` — called after handler execution (before rendering).
  6. View resolution: `ViewResolver.resolveViewName()` → `View.render()` writes the response body.
  7. `HandlerInterceptor.afterCompletion()` — called after rendering (even on exception).
  8. On exception: `HandlerExceptionResolver` chain is consulted.
- **State transitions:** Request moves through `HandlerExecutionChain` states (pre-handle → handle → post-handle → after-completion). Async processing (`DeferredResult`, `Callable`) suspends the chain and resumes it on a separate thread.
- **Source files:**
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/DispatcherServlet.java`
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/HandlerExecutionChain.java`
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/RequestMappingHandlerAdapter.java`

#### Reactive HTTP Request Processing (Spring WebFlux)

- **Type:** User-facing
- **Trigger:** An HTTP request received by a reactive server (Reactor Netty, Tomcat in async mode, Jetty) is adapted to a `ServerWebExchange`.
- **Steps:**
  1. `WebHttpHandlerBuilder` assembles a processing chain: `WebFilter`s → `DispatcherHandler`.
  2. `DispatcherHandler.handle()` returns `Mono<Void>` — iterates `HandlerMapping` list reactively.
  3. First matching `HandlerMapping` returns the handler as `Mono<Object>`.
  4. `HandlerAdapter` invokes the handler, returning `Mono<HandlerResult>`.
  5. `HandlerResultHandler` renders the result (writes the response body).
  6. Error handling via `WebExceptionHandler` chain.
- **State transitions:** All transitions are reactive (non-blocking); each step is a `Mono` composition.
- **Source files:**
  - `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/DispatcherHandler.java`
  - `src/spring-framework/spring-web/src/main/java/org/springframework/web/server/adapter/WebHttpHandlerBuilder.java`
  - `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/result/` (result handlers)

#### Bean Creation and Dependency Injection Lifecycle

- **Type:** System/background
- **Trigger:** `ApplicationContext.refresh()` or first access to a singleton bean via `BeanFactory.getBean()`.
- **Steps:**
  1. `AbstractApplicationContext.refresh()` — invokes `obtainFreshBeanFactory()`, `invokeBeanFactoryPostProcessors()` (including `ConfigurationClassPostProcessor` for annotation-based config), `registerBeanPostProcessors()`, `finishBeanFactoryInitialization()`.
  2. `DefaultListableBeanFactory.preInstantiateSingletons()` — instantiates all non-lazy singletons.
  3. `AbstractAutowireCapableBeanFactory.createBean()` — calls `instantiateBean()` (Objenesis or reflection), then `populateBean()` (dependency injection), then `initializeBean()`.
  4. Lifecycle callbacks: `BeanNameAware`, `BeanFactoryAware`, `ApplicationContextAware`, `BeanPostProcessor.postProcessBeforeInitialization()`, `InitializingBean.afterPropertiesSet()`, custom `init-method`, `BeanPostProcessor.postProcessAfterInitialization()`.
  5. Singleton is cached in `DefaultSingletonBeanRegistry`.
  6. On `close()`: `DisposableBean.destroy()`, custom `destroy-method`, `DestructionAwareBeanPostProcessor.postProcessBeforeDestruction()`.
- **State transitions:** Bean passes through `CREATING → CREATED → INITIALIZING → INITIALIZED → DESTROYING → DESTROYED` conceptual states managed by `DefaultSingletonBeanRegistry`'s internal maps.
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/support/AbstractApplicationContext.java`
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/AbstractAutowireCapableBeanFactory.java`
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/DefaultSingletonBeanRegistry.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/support/PostProcessorRegistrationDelegate.java`

#### Declarative Transaction Execution

- **Type:** User-facing (transparent to callers)
- **Trigger:** A call to a method annotated with `@Transactional` on a Spring-managed proxy.
- **Steps:**
  1. AOP proxy intercepts the method call; `TransactionInterceptor.invoke()` is called.
  2. `AnnotationTransactionAttributeSource` reads `@Transactional` metadata (propagation, isolation, rollbackFor, etc.).
  3. `PlatformTransactionManager.getTransaction()` is called; the transaction manager obtains a connection/session and binds it to `TransactionSynchronizationManager` (thread-local).
  4. The actual method body executes.
  5. On success: `PlatformTransactionManager.commit()`.
  6. On `RuntimeException` (or configured rollback exception): `PlatformTransactionManager.rollback()`.
  7. The resource (connection/session) is released; synchronisations are flushed.
- **State transitions:** Active transaction → (method execution) → Committed or Rolled Back.
- **Source files:**
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/interceptor/TransactionInterceptor.java`
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/support/AbstractPlatformTransactionManager.java`
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/support/TransactionSynchronizationManager.java`

#### AOT Build-Time Processing

- **Type:** System/background (build-time)
- **Trigger:** Invoked by the build tooling (`ContextAotProcessor`) during a native-image build or explicit AOT processing step.
- **Steps:**
  1. `ContextAotProcessor` loads the application context in an AOT-aware mode.
  2. `ApplicationContextAotGenerator` collects `BeanRegistrationAotProcessor` and `BeanFactoryInitializationAotProcessor` contributions from all registered beans.
  3. Contributions write `RuntimeHints` and generate Java source files (via `GenerationContext`, `GeneratedFiles`, the repackaged JavaPoet library).
  4. Generated source files are compiled and included in the native image.
  5. At native image runtime, `AotDetector.useGeneratedArtifacts()` returns `true`; the context uses pre-generated artefacts instead of reflection.
- **State transitions:** Build-time context load → hint collection → code generation → artefact compilation → runtime artefact use.
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/aot/ContextAotProcessor.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/aot/ApplicationContextAotGenerator.java`
  - `src/spring-framework/spring-core/src/main/java/org/springframework/aot/hint/RuntimeHints.java`
  - `src/spring-framework/spring-core/src/main/java/org/springframework/aot/generate/GenerationContext.java`
  - `src/spring-framework/spring-core/src/main/java/org/springframework/aot/AotDetector.java`

#### Scheduled Task Execution

- **Type:** System/background
- **Trigger:** `@EnableScheduling` activates `SchedulingConfiguration`; `ScheduledAnnotationBeanPostProcessor` scans all beans at context refresh for `@Scheduled` annotations.
- **Steps:**
  1. `ScheduledAnnotationBeanPostProcessor` discovers `@Scheduled` methods and registers `ScheduledTask` objects with `TaskScheduler`.
  2. At the configured interval (cron, fixedRate, fixedDelay), `TaskScheduler` fires the task.
  3. If `@Async` is also present, execution is delegated to a thread pool.
  4. Reactive scheduling (`@Scheduled` on coroutine-returning methods) dispatches via Reactor.
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/annotation/ScheduledAnnotationBeanPostProcessor.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/annotation/ScheduledAnnotationReactiveSupport.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/support/` (trigger and task wrappers)

#### WebSocket STOMP Message Broker Workflow

- **Type:** User-facing (bidirectional, long-lived)
- **Trigger:** A WebSocket handshake from a browser client; `@EnableWebSocketMessageBroker` configures the pipeline.
- **Steps:**
  1. HTTP upgrade to WebSocket via `WebSocketHttpRequestHandler`.
  2. `StompSubProtocolHandler` decodes STOMP frames from WebSocket messages.
  3. `SimpAnnotationMethodMessageHandler` routes `@MessageMapping` annotated methods; `StompBrokerRelayMessageHandler` (or `SimpleBrokerMessageHandler`) distributes to subscriptions.
  4. Application code sends messages via `SimpMessagingTemplate`.
  5. `StompEncoder` encodes and sends STOMP frames back over the WebSocket session.
- **State transitions:** WebSocket session states: `OPEN → (STOMP CONNECTED) → (message exchange) → (STOMP DISCONNECT) → CLOSED`.
- **Source files:**
  - `src/spring-framework/spring-websocket/src/main/java/org/springframework/web/socket/messaging/`
  - `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/simp/stomp/StompBrokerRelayMessageHandler.java`
  - `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/simp/SimpMessagingTemplate.java`

#### Method Retry Execution

- **Type:** User-facing / system/background (transparent to callers)
- **Trigger:** A call to a method annotated with `@Retryable` on a Spring-managed proxy, or a programmatic call through `RetryTemplate.execute()`.
- **Steps:**
  1. AOP proxy (via `RetryAnnotationBeanPostProcessor`) intercepts the call.
  2. `SimpleRetryInterceptor` or `RetryTemplate` consults the configured `RetryPolicy` to decide whether to attempt.
  3. The method executes; if it throws a retryable exception the `BackOff` strategy is consulted for a delay.
  4. After the configured maximum attempts or if the exception is non-retryable, the exception propagates.
  5. `RetryListener` callbacks are fired at each phase.
- **Source files:**
  - `src/spring-framework/spring-core/src/main/java/org/springframework/core/retry/RetryTemplate.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/resilience/retry/SimpleRetryInterceptor.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/resilience/annotation/RetryAnnotationBeanPostProcessor.java`

---

## 5. Business Rules and Validation

The Spring Framework's "business rules" are the enforced invariants of the framework's own APIs and lifecycle. They are not domain rules of an end-user business application.

| ID | Rule | Description | Criticality | Source |
|----|------|-------------|-------------|--------|
| BR-001 | Singleton beans must be thread-safe | Singleton-scoped beans are shared across all threads; the container makes no concurrency guarantees for bean state | Core | `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/DefaultSingletonBeanRegistry.java` |
| BR-002 | Circular dependency resolution via constructor injection is disallowed | If beans A and B each require the other via constructor injection, the container throws `BeanCurrentlyInCreationException`; setter/field injection supports circular deps via early singleton exposure | Core | `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/BeanCurrentlyInCreationException.java`; `AbstractAutowireCapableBeanFactory.java` |
| BR-003 | `@Transactional` on private methods has no effect | AOP proxying cannot intercept private methods; the annotation is ignored silently on private visibility in proxy mode | Core | `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/annotation/Transactional.java` (Javadoc); reference manual |
| BR-004 | Rollback by default only for `RuntimeException` and `Error` | Checked exceptions do not trigger rollback unless explicitly listed in `rollbackFor` | Core | `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/annotation/Transactional.java` |
| BR-005 | Transaction propagation `REQUIRED` (default) joins an existing transaction | A new `@Transactional` method invoked within an active transaction participates in it; `REQUIRES_NEW` suspends and creates a fresh transaction | Core | `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/TransactionDefinition.java` |
| BR-006 | Bean definitions are immutable after context refresh | Post-processor modifications to `BeanDefinition` objects must occur before `finishBeanFactoryInitialization()`; late changes are not reflected in already-created singletons | Core | `src/spring-framework/spring-context/src/main/java/org/springframework/context/support/AbstractApplicationContext.java` |
| BR-007 | `FactoryBean` prefix `&` dereferences the factory itself | Prefixing a bean name with `&` in `BeanFactory.getBean()` returns the `FactoryBean` instance, not the object it produces | Supporting | `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/BeanFactory.java` |
| BR-008 | CORS preflight requests must be handled before authentication filters | `CorsFilter` / `PreFlightRequestFilter` must be ordered before any security filter chain to correctly respond to `OPTIONS` requests | Supporting | `src/spring-framework/spring-web/src/main/java/org/springframework/web/filter/CorsFilter.java`; `CorsConfiguration.java` |
| BR-009 | SQL error codes drive exception translation hierarchy | `SQLErrorCodesFactory` loads `sql-error-codes.xml`; matching vendor error codes are translated to specific `DataAccessException` subclasses (`DuplicateKeyException`, `DataIntegrityViolationException`, etc.) | Core | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/support/SQLErrorCodeSQLExceptionTranslator.java`; `src/spring-framework/spring-jdbc/src/main/resources/org/springframework/jdbc/support/sql-error-codes.xml` |
| BR-010 | AOT-processed artefacts take precedence over reflective initialisation | When `spring.aot.enabled=true` or running as a GraalVM native image, the context uses pre-generated bean registration code; missing artefacts cause an exception rather than fallback | Core | `src/spring-framework/spring-core/src/main/java/org/springframework/aot/AotDetector.java` |
| BR-011 | `@Cacheable` SpEL condition evaluated before method execution | The `condition` attribute is evaluated before the call; the `unless` attribute is evaluated after (with access to `#result`). If `condition` is false, the method is always executed and the cache is not updated | Supporting | `src/spring-framework/spring-context/src/main/java/org/springframework/cache/interceptor/CacheAspectSupport.java` |
| BR-012 | Retry maximum attempts (default 3 retries) with 1-second fixed backoff | `RetryTemplate` default: `DefaultRetryPolicy` allows at most 3 retry attempts; `FixedBackOff` default is 1 000 ms | Supporting | `src/spring-framework/spring-core/src/main/java/org/springframework/core/retry/RetryTemplate.java` |
| BR-013 | `@Scheduled` cron expressions follow UNIX cron with optional seconds field | The scheduler supports 6-field cron expressions (seconds, minutes, hours, day-of-month, month, day-of-week) | Supporting | `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/support/CronExpression.java` |
| BR-014 | Single-bean ambiguity must be resolved via `@Primary` or `@Qualifier` | When multiple beans of the same type are eligible for injection, the container throws `NoUniqueBeanDefinitionException` unless one is marked `@Primary` or the injection point carries a `@Qualifier` | Core | `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/NoUniqueBeanDefinitionException.java` |
| BR-015 | HTTP message converters are selected by content negotiation | For `@RequestBody`/`@ResponseBody`, `AbstractMessageConverterMethodArgumentResolver` selects the first `HttpMessageConverter` capable of reading/writing the negotiated `MediaType` | Core | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/AbstractMessageConverterMethodProcessor.java` |
| BR-016 | WebSocket connections require HTTP upgrade — SockJS fallback available | Raw WebSocket requires browser/proxy support; `SockJsService` provides long-polling, streaming, and other transport fallbacks for environments without WebSocket | Supporting | `src/spring-framework/spring-websocket/src/main/java/org/springframework/web/socket/sockjs/SockJsService.java` |
| BR-017 | `@EventListener` methods in the same thread as publisher are called synchronously | By default, event dispatch is synchronous in the calling thread; an `AsyncTaskExecutor` must be configured in the multicaster to make dispatch asynchronous | Peripheral | `src/spring-framework/spring-context/src/main/java/org/springframework/context/event/SimpleApplicationEventMulticaster.java` |
| BR-018 | Bean scopes `request` and `session` require an active web request | Accessing a `request`- or `session`-scoped bean outside an active HTTP request throws `ScopeNotActiveException` | Supporting | `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/ScopeNotActiveException.java` |

---

## 6. Domain Model

Spring Framework is an infrastructure framework; its "domain model" consists of the framework's own abstractions rather than business entities. There is no persistent entity model or database schema owned by the framework itself.

#### BeanDefinition

- **Purpose:** Holds metadata describing a bean — class, scope, constructor arguments, property values, init/destroy methods, lazy-init flag, dependencies.
- **Source file:** `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/config/BeanDefinition.java`; `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/AbstractBeanDefinition.java`; `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/RootBeanDefinition.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| `beanClassName` | `String` | Fully qualified class name of the bean | `BeanDefinition.java` |
| `scope` | `String` | Scope (singleton, prototype, request, session, etc.) | `BeanDefinition.java` |
| `lazyInit` | `boolean` | Whether to defer instantiation until first access | `BeanDefinition.java` |
| `constructorArgumentValues` | `ConstructorArgumentValues` | Constructor argument metadata | `AbstractBeanDefinition.java` |
| `propertyValues` | `MutablePropertyValues` | Property injection metadata | `AbstractBeanDefinition.java` |
| `initMethodName` | `String` | Name of custom init method | `AbstractBeanDefinition.java` |
| `destroyMethodName` | `String` | Name of custom destroy method | `AbstractBeanDefinition.java` |
| `dependsOn` | `String[]` | Beans that must be initialised before this one | `AbstractBeanDefinition.java` |
| `primary` | `boolean` | Whether this bean is preferred for autowiring | `AbstractBeanDefinition.java` |
| `factoryBeanName` | `String` | Factory bean producing this bean | `AbstractBeanDefinition.java` |
| `factoryMethodName` | `String` | Factory method on the factory bean | `AbstractBeanDefinition.java` |

#### ApplicationContext

- **Purpose:** Central interface providing the fully configured Spring container including bean access, event publication, message resolution, resource loading, and environment access.
- **Source file:** `src/spring-framework/spring-context/src/main/java/org/springframework/context/ApplicationContext.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| `id` | `String` | Unique identifier for this context | `ApplicationContext.java` |
| `applicationName` | `String` | Logical name of the deployed application | `ApplicationContext.java` |
| `displayName` | `String` | Human-readable context name | `ApplicationContext.java` |
| `startupDate` | `long` | Timestamp (ms) of context load | `ApplicationContext.java` |
| `parent` | `ApplicationContext` | Parent context (for hierarchical containers) | `ApplicationContext.java` |

#### Message (Messaging)

- **Purpose:** Represents a message in the Spring Messaging abstraction — a payload plus headers.
- **Source file:** `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/Message.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| `payload` | `T` | The message body | `Message.java` |
| `headers` | `MessageHeaders` | Key/value metadata | `Message.java`; `MessageHeaders.java` |

#### HttpHeaders

- **Purpose:** Represents HTTP message headers as a case-insensitive multi-value map.
- **Source file:** `src/spring-framework/spring-web/src/main/java/org/springframework/http/HttpHeaders.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| (content-type) | `MediaType` | `Content-Type` header | `HttpHeaders.java` |
| (accept) | `List<MediaType>` | `Accept` header | `HttpHeaders.java` |
| (authorization) | `String` | `Authorization` header | `HttpHeaders.java` |
| (cache-control) | `String` | `Cache-Control` header | `HttpHeaders.java` |
| (etag) | `String` | `ETag` header | `HttpHeaders.java` |

#### TransactionDefinition

- **Purpose:** Describes the properties of a transaction — propagation behaviour, isolation level, timeout, and read-only flag.
- **Source file:** `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/TransactionDefinition.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| `propagationBehavior` | `int` | One of the PROPAGATION_* constants | `TransactionDefinition.java` |
| `isolationLevel` | `int` | One of the ISOLATION_* constants | `TransactionDefinition.java` |
| `timeout` | `int` | Seconds; -1 = default | `TransactionDefinition.java` |
| `readOnly` | `boolean` | Hint for optimisations | `TransactionDefinition.java` |
| `name` | `String` | Transaction name for monitoring | `TransactionDefinition.java` |

#### RuntimeHints

- **Purpose:** Aggregates GraalVM native image hints (reflection, resource patterns, proxy interfaces, serialisation) collected during AOT processing.
- **Source file:** `src/spring-framework/spring-core/src/main/java/org/springframework/aot/hint/RuntimeHints.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| `reflection` | `ReflectionHints` | Reflection access hints | `RuntimeHints.java` |
| `resources` | `ResourceHints` | Resource pattern hints | `RuntimeHints.java` |
| `proxies` | `ProxyHints` | JDK proxy interface hints | `RuntimeHints.java` |
| `serialization` | `SerializationHints` | Java serialisation hints | `RuntimeHints.java` |

#### SQLErrorCodes

- **Purpose:** Database-specific mapping of SQL error codes and states to Spring `DataAccessException` categories; loaded from `sql-error-codes.xml`.
- **Source file:** `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/support/SQLErrorCodes.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| `databaseProductName` | `String` (pattern) | Matched against `DatabaseMetaData.getDatabaseProductName()` | `SQLErrorCodes.java` |
| `badSqlGrammarCodes` | `String[]` | Error codes for bad SQL grammar | `sql-error-codes.xml` |
| `duplicateKeyCodes` | `String[]` | Error codes for unique constraint violations | `sql-error-codes.xml` |
| `dataIntegrityViolationCodes` | `String[]` | Error codes for data integrity violations | `sql-error-codes.xml` |
| `dataAccessResourceFailureCodes` | `String[]` | Error codes for resource failures | `sql-error-codes.xml` |
| `transientDataAccessResourceCodes` | `String[]` | Error codes for transient failures | `sql-error-codes.xml` |
| `cannotAcquireLockCodes` | `String[]` | Error codes for lock contention | `sql-error-codes.xml` |
| `deadlockLoserCodes` | `String[]` | Error codes for deadlock victims | `sql-error-codes.xml` |
| `useSqlStateForTranslation` | `boolean` | Use SQLSTATE instead of vendor error code | `SQLErrorCodes.java` |

#### RetryTemplate

- **Purpose:** Executes a retryable operation, consulting `RetryPolicy` and `BackOff` to determine whether and when to retry on failure.
- **Source file:** `src/spring-framework/spring-core/src/main/java/org/springframework/core/retry/RetryTemplate.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| `retryPolicy` | `RetryPolicy` | Decides whether a failure is retryable | `RetryTemplate.java` |
| `backOff` | `BackOff` | Calculates delay between retries | `RetryTemplate.java` |
| `retryListener` | `RetryListener` | Observes retry lifecycle events | `RetryTemplate.java` |

---

#### Enumerations

| Enum Name | Values | Source |
|-----------|--------|--------|
| `HttpMethod` | `GET, HEAD, POST, PUT, PATCH, DELETE, OPTIONS, TRACE` (plus others) | `src/spring-framework/spring-web/src/main/java/org/springframework/http/HttpMethod.java` |
| `HttpStatus` | Standard 1xx–5xx HTTP status codes | `src/spring-framework/spring-web/src/main/java/org/springframework/http/HttpStatus.java` |
| `Propagation` (Transaction) | `REQUIRED, SUPPORTS, MANDATORY, REQUIRES_NEW, NOT_SUPPORTED, NEVER, NESTED` | `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/annotation/Propagation.java` |
| `Isolation` (Transaction) | `DEFAULT, READ_UNCOMMITTED, READ_COMMITTED, REPEATABLE_READ, SERIALIZABLE` | `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/annotation/Isolation.java` |
| `ScopedProxyMode` | `DEFAULT, NO, INTERFACES, TARGET_CLASS` | `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/ScopedProxyMode.java` |
| `FilterType` | `ANNOTATION, ASSIGNABLE_TYPE, ASPECTJ, REGEX, CUSTOM` | `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/FilterType.java` |
| `StompCommand` | `STOMP, CONNECT, CONNECTED, SEND, SUBSCRIBE, UNSUBSCRIBE, ACK, NACK, BEGIN, COMMIT, ABORT, DISCONNECT, MESSAGE, RECEIPT, ERROR` | `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/simp/stomp/StompCommand.java` |
| `ExecutableMode` | `INVOKE, INTROSPECT` | `src/spring-framework/spring-core/src/main/java/org/springframework/aot/hint/ExecutableMode.java` |
| `MemberCategory` (AOT) | `PUBLIC_FIELDS, DECLARED_FIELDS, PUBLIC_CONSTRUCTORS, INVOKE_DECLARED_CONSTRUCTORS, DECLARED_CONSTRUCTORS, …` | `src/spring-framework/spring-core/src/main/java/org/springframework/aot/hint/MemberCategory.java` |
| `SimpMessageType` | `CONNECT, CONNECT_ACK, MESSAGE, SUBSCRIBE, UNSUBSCRIBE, HEARTBEAT, DISCONNECT, DISCONNECT_ACK, OTHER` | `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/simp/SimpMessageType.java` |
| `AdviceMode` | `PROXY, ASPECTJ` | `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/AdviceMode.java` |
| `Database` (JPA Vendor) | `DEFAULT, DB2, DERBY, H2, HANA, HSQL, INFORMIX, MYSQL, ORACLE, POSTGRESQL, SQL_SERVER, SYBASE` | `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/vendor/Database.java` |
| `ProxyType` | `JDK, CGLIB` | `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/ProxyType.java` |

---

#### Relationships

| Entity A | Entity B | Relationship Type | Source |
|----------|----------|-------------------|--------|
| `ApplicationContext` | `BeanFactory` | Extends (is-a) | `ApplicationContext.java` |
| `ApplicationContext` | `ApplicationEventPublisher` | Extends (is-a) | `ApplicationContext.java` |
| `ApplicationContext` | `MessageSource` | Extends (is-a) | `ApplicationContext.java` |
| `ApplicationContext` | `ResourcePatternResolver` | Extends (is-a) | `ApplicationContext.java` |
| `DefaultListableBeanFactory` | `BeanDefinition` | Registers/owns many | `DefaultListableBeanFactory.java` |
| `BeanDefinition` | `Bean` instance | Describes/produces one | `AbstractAutowireCapableBeanFactory.java` |
| `DispatcherServlet` | `HandlerMapping` | Delegates to (1-to-many) | `DispatcherServlet.java` |
| `DispatcherServlet` | `HandlerAdapter` | Delegates to (1-to-many) | `DispatcherServlet.java` |
| `DispatcherServlet` | `ViewResolver` | Delegates to (1-to-many) | `DispatcherServlet.java` |
| `HandlerExecutionChain` | `HandlerInterceptor` | Contains (ordered list) | `HandlerExecutionChain.java` |
| `PlatformTransactionManager` | `TransactionStatus` | Creates/manages | `PlatformTransactionManager.java` |
| `TransactionInterceptor` | `PlatformTransactionManager` | Uses | `TransactionInterceptor.java` |
| `JdbcTemplate` | `DataSource` | Uses (holds reference to) | `JdbcTemplate.java` |
| `LocalContainerEntityManagerFactoryBean` | `EntityManagerFactory` | Produces | `LocalContainerEntityManagerFactoryBean.java` |
| `Message` | `MessageHeaders` | Contains | `Message.java` |
| `RuntimeHints` | `ReflectionHints`, `ResourceHints`, `ProxyHints`, `SerializationHints` | Aggregates | `RuntimeHints.java` |
| `SQLErrorCodes` | `DataAccessException` subclass | Maps to | `SQLErrorCodeSQLExceptionTranslator.java` |
| `RetryTemplate` | `RetryPolicy`, `BackOff`, `RetryListener` | Composed of | `RetryTemplate.java` |

---

## 7. Integration Points

| Integration | Type | Endpoint / Target | Direction | Source |
|-------------|------|-------------------|-----------|--------|
| JDBC databases (DB2, Derby, H2, HSQL, MySQL, Oracle, PostgreSQL, SQL Server, Sybase, SAP HANA) | Database | Via `DataSource` (JDBC URL) | bidirectional | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/JdbcTemplate.java`; `sql-error-codes.xml` |
| JPA providers (Hibernate 7, EclipseLink) | Database (via ORM) | `EntityManagerFactory` / persistence unit | bidirectional | `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/LocalContainerEntityManagerFactoryBean.java` |
| R2DBC databases (reactive) | Database | `ConnectionFactory` (R2DBC URL) | bidirectional | `src/spring-framework/spring-r2dbc/src/main/java/org/springframework/r2dbc/core/DatabaseClient.java` |
| JMS brokers (Apache ActiveMQ Artemis; any JMS 3.1 provider) | Messaging | JNDI or direct `ConnectionFactory` | bidirectional | `src/spring-framework/spring-jms/src/main/java/org/springframework/jms/core/JmsTemplate.java`; `DefaultMessageListenerContainer.java` |
| STOMP-over-WebSocket (full external broker relay) | Messaging | TCP to broker (e.g. RabbitMQ, ActiveMQ) | bidirectional | `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/simp/stomp/StompBrokerRelayMessageHandler.java` |
| RSocket (TCP / WebSocket transport) | Messaging | RSocket server endpoint | bidirectional | `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/rsocket/RSocketRequester.java` |
| HTTP outbound calls via `RestTemplate` | HTTP client | Any HTTP/HTTPS endpoint | outbound | `src/spring-framework/spring-web/src/main/java/org/springframework/web/client/RestTemplate.java` |
| HTTP outbound calls via `RestClient` | HTTP client | Any HTTP/HTTPS endpoint | outbound | `src/spring-framework/spring-web/src/main/java/org/springframework/web/client/RestClient.java` |
| HTTP outbound calls via `WebClient` (reactive) | HTTP client | Any HTTP/HTTPS endpoint | outbound | `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/function/client/WebClient.java` |
| HTTP interface proxies (`@GetExchange`, `@PostExchange`, etc.) | HTTP client | Configured base URL | outbound | `src/spring-framework/spring-web/src/main/java/org/springframework/web/service/invoker/HttpServiceProxyFactory.java` |
| Servlet container (Tomcat, Jetty 12, WildFly, etc.) | External system | Servlet 6.1 SPI | inbound | `src/spring-framework/spring-web/src/main/resources/META-INF/web-fragment.xml`; `DispatcherServlet.java` |
| Reactor Netty HTTP server (WebFlux) | External system | Netty pipeline | inbound | `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/` |
| JNDI (application server) | External system | JNDI context | inbound | `src/spring-framework/spring-context/src/main/java/org/springframework/jndi/JndiTemplate.java` |
| JTA / XA transaction coordinator (application server) | External system | `TransactionManager` / `UserTransaction` JNDI | bidirectional | `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/jta/JtaTransactionManager.java` |
| JavaMail / Jakarta Mail | External system | SMTP host | outbound | `src/spring-framework/spring-context-support/src/main/java/org/springframework/mail/javamail/JavaMailSenderImpl.java` |
| Quartz Scheduler | External system | In-process scheduler; optional JDBC job store | bidirectional | `src/spring-framework/spring-context-support/src/main/java/org/springframework/scheduling/quartz/` |
| JMX MBean server | External system | Local or remote MBean server (RMI) | outbound | `src/spring-framework/spring-context/src/main/java/org/springframework/jmx/export/MBeanExporter.java` |
| GraalVM native image build tools | External system | Build-time AOT processor | outbound | `src/spring-framework/spring-context/src/main/java/org/springframework/context/aot/ContextAotProcessor.java` |
| Micrometer observation / tracing | External system | `ObservationRegistry` (tracing backends: Zipkin, OTLP, etc.) | outbound | `src/spring-framework/spring-web/src/main/java/org/springframework/web/filter/ServerHttpObservationFilter.java`; `RestClient.java` |
| Class-path resource files (`.properties`, `.yaml`, `.xml`) | File I/O | Classpath / file system | inbound | `src/spring-framework/spring-core/src/main/java/org/springframework/core/io/ClassPathResource.java`; `YamlPropertiesFactoryBean.java` |

---

## 8. Reports

Spring Framework does not contain any report generation features of its own (no embedded report engine, no scheduled reports, no PDF/Excel output as an operational concern of the framework itself). The `spring-webmvc` module does include optional integration with libraries that *applications* can use for report-like views:

| Report | Type | Purpose | Data Sources | Parameters | Output Format | Source |
|--------|------|---------|-------------|------------|---------------|--------|
| PDF view (OpenPDF) | View rendering | Renders a Spring MVC `View` as PDF via OpenPDF | `ModelAndView` model map | View-defined | PDF | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/view/document/AbstractPdfView.java` |
| Excel/OOXML view (Apache POI) | View rendering | Renders a Spring MVC `View` as XLSX via Apache POI | `ModelAndView` model map | View-defined | XLSX | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/view/document/AbstractXlsxView.java` |
| Atom/RSS feed view (ROME) | View rendering | Renders a Spring MVC `View` as Atom or RSS XML | `ModelAndView` model map | View-defined | XML (Atom/RSS) | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/view/feed/AbstractAtomFeedView.java`; `AbstractRssFeedView.java` |

These are view types that application code must subclass and wire; the framework provides the integration skeleton only.

---

## 9. Cross-Reference: Application to Data Layer

#### 9.1 Data Access Patterns

Spring Framework supports four distinct data access patterns, each with its own module:

- **JDBC (synchronous, imperative):** Template-method pattern via `JdbcTemplate` and `NamedParameterJdbcTemplate`, or the fluent `JdbcClient` (6.1+). Application code supplies SQL and result extraction callbacks; the framework manages connections and translates exceptions. (`spring-jdbc`)
- **JPA / ORM (synchronous, object-relational):** Provider-managed `EntityManagerFactory` (`LocalContainerEntityManagerFactoryBean`); thread-bound `EntityManager` proxies; `JpaTransactionManager` participates in `@Transactional`. Hibernate native API also supported. (`spring-orm`)
- **R2DBC (reactive, non-blocking):** `DatabaseClient` for reactive SQL with `Mono`/`Flux` return types; `R2dbcTransactionManager` for reactive transactions. (`spring-r2dbc`)
- **Object-based RDBMS operations:** `SqlQuery`, `SqlUpdate`, `StoredProcedure` — encapsulate SQL as reusable Java objects. (`spring-jdbc/object`)

There is no entity or schema owned by the Spring Framework itself; the data access layer is an abstraction through which **downstream application** schemas are accessed.

---

#### 9.2 Entity-to-Table Mapping

Spring Framework owns no database schema. The table below lists the framework classes that model data structures in the context of data access configuration, not application-domain entities.

| Entity / Class | Database Table(s) | Source |
|---------------|-------------------|--------|
| `SQLErrorCodes` | N/A — loaded from `sql-error-codes.xml`, not a DB table | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/support/SQLErrorCodes.java` |
| Quartz `JobDetail` / `Trigger` (via `spring-context-support`) | Quartz JDBC job store tables (e.g. `QRTZ_JOB_DETAILS`, `QRTZ_TRIGGERS`) — managed by Quartz itself | `src/spring-framework/spring-context-support/src/main/java/org/springframework/scheduling/quartz/LocalDataSourceJobStore.java` |
| Embedded database schemas (`EmbeddedDatabaseBuilder`) | In-memory H2/Derby/HSQL schemas created from supplied SQL scripts — for test use | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/datasource/embedded/EmbeddedDatabaseBuilder.java` |

No further entity-to-table mapping exists within the framework codebase. Application schemas are outside the framework's scope.

---

#### 9.3 Repository / DAO Methods

The framework provides the template/DAO infrastructure; it does not implement application-specific repositories. The table below covers the framework's own data-access classes.

| Repository / DAO | Key Methods | Purpose | Source |
|-----------------|-------------|---------|--------|
| `JdbcTemplate` | `query()`, `queryForObject()`, `queryForList()`, `update()`, `batchUpdate()`, `execute()`, `call()` | Core JDBC operations with callback-based result extraction and exception translation | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/JdbcTemplate.java` |
| `NamedParameterJdbcTemplate` | `query()`, `queryForObject()`, `queryForList()`, `update()`, `batchUpdate()` with `SqlParameterSource` | Named-parameter variant of `JdbcTemplate` | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/namedparam/NamedParameterJdbcTemplate.java` |
| `JdbcClient` | `sql(String).param(…).query(Class)`, `.update()`, `.queryValue()` | Fluent, chainable JDBC client (Spring 6.1+) | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/simple/JdbcClient.java` |
| `SimpleJdbcCall` | `execute()`, `executeObject()`, `executeFunction()` | Stored procedure / function invocation | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/simple/SimpleJdbcCall.java` |
| `SimpleJdbcInsert` | `execute()`, `executeAndReturnKey()`, `executeBatch()` | Simplified table insert with generated key retrieval | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/simple/SimpleJdbcInsert.java` |
| `SqlQuery<T>` | `execute()`, `findObject()` | Encapsulates a SQL SELECT as a reusable Java object | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/object/SqlQuery.java` |
| `SqlUpdate` | `update()`, `updateByNamedParam()` | Encapsulates a SQL INSERT/UPDATE/DELETE | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/object/SqlUpdate.java` |
| `StoredProcedure` | `execute()` | Abstract base for stored procedures | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/object/StoredProcedure.java` |
| `DatabaseClient` (R2DBC) | `sql(String).bind(…).fetch()`, `.rowsUpdated()` | Reactive (non-blocking) SQL execution returning `Mono`/`Flux` | `src/spring-framework/spring-r2dbc/src/main/java/org/springframework/r2dbc/core/DatabaseClient.java` |
| `SharedEntityManagerCreator` (JPA) | Creates thread-safe `EntityManager` proxy | Routes JPA calls through container-managed `EntityManager` bound to current transaction | `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/SharedEntityManagerCreator.java` |
| `JmsTemplate` | `send()`, `convertAndSend()`, `receive()`, `receiveAndConvert()`, `execute()` | Synchronous JMS send/receive with connection management | `src/spring-framework/spring-jms/src/main/java/org/springframework/jms/core/JmsTemplate.java` |
| `SQLErrorCodesFactory` | `getErrorCodes(DataSource)` | Looks up `SQLErrorCodes` for a given `DataSource` by interrogating `DatabaseMetaData` | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/support/SQLErrorCodesFactory.java` |
