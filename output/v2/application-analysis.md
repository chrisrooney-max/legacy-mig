<!-- Input files processed:
- src/spring-framework/build.gradle
- src/spring-framework/gradle.properties
- src/spring-framework/settings.gradle
- src/spring-framework/buildSrc/build.gradle
- src/spring-framework/buildSrc/gradle.properties
- src/spring-framework/buildSrc/settings.gradle
- src/spring-framework/framework-platform/framework-platform.gradle
- src/spring-framework/framework-docs/framework-docs.gradle
- src/spring-framework/integration-tests/integration-tests.gradle
- src/spring-framework/gradle/spring-module.gradle
- src/spring-framework/gradle/publications.gradle
- src/spring-framework/gradle/ide.gradle
- src/spring-framework/spring-core/spring-core.gradle
- src/spring-framework/spring-core-test/spring-core-test.gradle
- src/spring-framework/spring-beans/spring-beans.gradle
- src/spring-framework/spring-aop/spring-aop.gradle
- src/spring-framework/spring-context/spring-context.gradle
- src/spring-framework/spring-context-support/spring-context-support.gradle
- src/spring-framework/spring-context-indexer/spring-context-indexer.gradle
- src/spring-framework/spring-expression/spring-expression.gradle
- src/spring-framework/spring-instrument/spring-instrument.gradle
- src/spring-framework/spring-aspects/spring-aspects.gradle
- src/spring-framework/spring-web/spring-web.gradle
- src/spring-framework/spring-webmvc/spring-webmvc.gradle
- src/spring-framework/spring-webflux/spring-webflux.gradle
- src/spring-framework/spring-websocket/spring-websocket.gradle
- src/spring-framework/spring-messaging/spring-messaging.gradle
- src/spring-framework/spring-jdbc/spring-jdbc.gradle
- src/spring-framework/spring-tx/spring-tx.gradle
- src/spring-framework/spring-orm/spring-orm.gradle
- src/spring-framework/spring-r2dbc/spring-r2dbc.gradle
- src/spring-framework/spring-jms/spring-jms.gradle
- src/spring-framework/spring-oxm/spring-oxm.gradle
- src/spring-framework/spring-test/spring-test.gradle
- src/spring-framework/framework-api/framework-api.gradle
- src/spring-framework/framework-bom/framework-bom.gradle
- src/spring-framework/spring-webmvc/src/main/resources/org/springframework/web/servlet/DispatcherServlet.properties
- src/spring-framework/spring-aop/src/main/resources/META-INF/spring.factories
- src/spring-framework/spring-test/src/main/resources/META-INF/spring.factories
- src/spring-framework/spring-web/src/main/resources/org/springframework/web/context/ContextLoader.properties
- src/spring-framework/spring-web/src/main/resources/org/springframework/http/codec/CodecConfigurer.properties
- src/spring-framework/spring-core/src/main/resources/META-INF/native-image/org.springframework/spring-core/native-image.properties
- src/spring-framework/spring-orm/src/main/resources/META-INF/native-image/org.springframework/spring-orm/native-image.properties
- src/spring-framework/spring-web/src/main/resources/META-INF/native-image/org.springframework/spring-web/native-image.properties
- --- (Selected Java source files, all modules, approximately 5,206 files read below at representative depth) ---
- src/spring-framework/spring-core/src/main/java/org/springframework/core/SpringVersion.java
- src/spring-framework/spring-core/src/main/java/org/springframework/core/io/Resource.java
- src/spring-framework/spring-core/src/main/java/org/springframework/core/env/Environment.java
- src/spring-framework/spring-core/src/main/java/org/springframework/aot/AotDetector.java
- src/spring-framework/spring-core/src/main/java/org/springframework/core/retry/RetryTemplate.java
- src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/BeanFactory.java
- src/spring-framework/spring-context/src/main/java/org/springframework/context/ApplicationContext.java
- src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/annotation/Scheduled.java
- src/spring-framework/spring-context/src/main/java/org/springframework/cache/annotation/Cacheable.java
- src/spring-framework/spring-context/src/main/java/org/springframework/resilience/annotation/Retryable.java
- src/spring-framework/spring-context/src/main/java/org/springframework/resilience/annotation/ConcurrencyLimit.java
- src/spring-framework/spring-context/src/main/java/org/springframework/resilience/retry/MethodRetrySpec.java
- src/spring-framework/spring-aop/src/main/java/org/springframework/aop/framework/ProxyFactory.java
- src/spring-framework/spring-expression/src/main/java/org/springframework/expression/* (full package listing read)
- src/spring-framework/spring-web/src/main/java/org/springframework/web/bind/annotation/RequestMapping.java
- src/spring-framework/spring-web/src/main/java/org/springframework/http/ProblemDetail.java
- src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/DispatcherServlet.java
- src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/config/annotation/EnableWebMvc.java
- src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/function/client/WebClient.java
- src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/JdbcTemplate.java
- src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/annotation/Transactional.java
- src/spring-framework/spring-jms/src/main/java/org/springframework/jms/core/JmsTemplate.java
- --- (Package directory listings read for all remaining modules) ---
-->

# Spring Framework Source Code Analysis

**Prepared for:** Legacy Application Programme (LAP)
**Analysis date:** 2026-04-29
**Analyst:** LAP Application Analysis Agent

---

## 1. Application Overview

- **Purpose:** Spring Framework is a comprehensive, open-source Java application framework that provides foundational infrastructure support — including dependency injection, aspect-oriented programming, data access, web MVC, reactive web, messaging, and transaction management — enabling Java and Kotlin applications to be built with minimal boilerplate and maximum configurability.

- **Technology stack:**
  - Primary language: Java 17+, with Kotlin 2.3.20 optional throughout
  - Framework: Spring Framework itself (self-hosting; this is the framework source)
  - Build tool: Gradle (with Kotlin-version Buildscript plugin)
  - Runtime targets: Standard JVM (Java 17 baseline), GraalVM Native Image, Virtual Threads (Project Loom / Java 21+), Java 24 multi-release JAR targets
  - Reactive runtime: Project Reactor (Mono/Flux)

- **Framework version:** `7.1.0-SNAPSHOT` (as declared in `gradle.properties`); multi-release JAR targets Java 21 and Java 24 where applicable.

- **Module structure:**

  | Module | Role |
  |---|---|
  | `spring-core` | Foundation: resource abstraction, type conversion, environment/property resolution, task execution, AOT code generation, GraalVM native hints, retry template, utilities |
  | `spring-core-test` | Test support for AOT agent recording and in-memory compilation |
  | `spring-beans` | Bean definition model, BeanFactory, XML bean loading, dependency injection engine, Groovy bean DSL |
  | `spring-aop` | AOP Alliance interfaces, AspectJ proxy creation (JDK dynamic proxy + CGLIB), pointcut/advice model |
  | `spring-aspects` | AspectJ load-time weaving aspects for caching, transactions, async, and `@Configurable` dependency injection |
  | `spring-expression` | Spring Expression Language (SpEL): parser, compiler (ASM byte-code), AST, evaluation context |
  | `spring-context` | ApplicationContext, component scanning, annotation configuration, scheduling, caching, events, validation, JMX, JNDI, scripting, internationalisation (i18n), resilience (`@Retryable`, `@ConcurrencyLimit`) |
  | `spring-context-indexer` | Annotation processor that generates a compile-time candidate component index |
  | `spring-context-support` | Optional integrations: Quartz scheduler, FreeMarker, Caffeine/JCache caches, JavaMail |
  | `spring-instrument` | Java agent (`InstrumentationSavingAgent`) for load-time weaving |
  | `spring-tx` | Transaction abstraction (`PlatformTransactionManager`, `ReactiveTransactionManager`), declarative `@Transactional`, programmatic templates |
  | `spring-jdbc` | JDBC abstraction: `JdbcTemplate`, `JdbcClient`, named-parameter support, embedded databases, stored procedures |
  | `spring-orm` | ORM integration: JPA (`LocalContainerEntityManagerFactoryBean`, `JpaTransactionManager`), Hibernate dialect |
  | `spring-r2dbc` | Reactive relational database access via R2DBC SPI: `DatabaseClient` |
  | `spring-oxm` | Object/XML mapping (marshalling/unmarshalling): JAXB, XStream adapters |
  | `spring-web` | Core web abstractions: HTTP primitives, `RestTemplate`, `RestClient`, WebClient HTTP service proxy, codec/message-converter infrastructure, multipart, CORS, error responses (RFC 9457 `ProblemDetail`) |
  | `spring-webmvc` | Servlet-based Spring MVC: `DispatcherServlet`, annotation-driven controllers, view resolvers, static resources, functional routing, SSE, async support |
  | `spring-webflux` | Reactive web: `DispatcherHandler`, reactive annotation controllers, `WebClient`, functional routing, WebSocket reactive adapter |
  | `spring-messaging` | Messaging abstractions: `Message`, `MessageChannel`, STOMP, SockJS, RSocket |
  | `spring-websocket` | WebSocket support: server/client adapters (Tomcat, Jetty), SockJS fallback, STOMP over WebSocket |
  | `spring-jms` | JMS integration: `JmsTemplate`, `JmsClient`, message listener containers, `@JmsListener` |
  | `spring-test` | Testing support: Spring TestContext Framework, `MockMvc`, WebTestClient, `@MockBean`/`@SpyBean`, JDBC test utils |
  | `framework-api` | Public API surface aggregation module |
  | `framework-bom` | Bill of Materials (BOM) for consumer dependency management |
  | `framework-platform` | Internal dependency version platform (BOMs and constraints) |
  | `framework-docs` | Documentation source (Antora) and documentation-embedded sample code |
  | `integration-tests` | Cross-module integration tests |

- **External dependencies (selected; managed via `framework-platform`):**
  - `commons-logging:commons-logging:1.3.5` — logging facade (mandatory)
  - `org.jspecify:jspecify:1.0.0` — nullability annotations
  - `org.aspectj:aspectjweaver:1.9.25` — AspectJ runtime weaving
  - `io.projectreactor:reactor-bom:2025.0.5` — Project Reactor (Mono/Flux)
  - `io.rsocket:rsocket-bom:1.1.5` — RSocket transport
  - `com.fasterxml.jackson:jackson-bom:2.21.2` and `tools.jackson:jackson-bom:3.1.1` — JSON/XML serialisation
  - `io.micrometer:micrometer-bom:1.16.5` — metrics and observation
  - `io.netty:netty-bom:4.2.12.Final` — async I/O
  - `io.projectreactor.netty:reactor-netty-http` — Reactor Netty HTTP transport
  - `org.hibernate.orm:hibernate-core:7.3.2.Final` — ORM (optional)
  - `org.hibernate.validator:hibernate-validator:9.1.0.Final` — Bean Validation (optional)
  - `jakarta.servlet:jakarta.servlet-api:6.1.0` — Servlet 6.1 API
  - `jakarta.persistence:jakarta.persistence-api:3.2.0` — JPA 3.2
  - `jakarta.jms:jakarta.jms-api:3.1.0` — JMS 3.1
  - `jakarta.websocket:jakarta.websocket-api:2.2.0` — WebSocket API
  - `jakarta.transaction:jakarta.transaction-api:2.0.1` — JTA
  - `jakarta.validation:jakarta.validation-api:3.1.0` — Bean Validation API
  - `io.r2dbc:r2dbc-spi:1.0.0.RELEASE` — R2DBC
  - `org.jetbrains.kotlin:kotlin-stdlib` / `kotlin-reflect` — Kotlin support (optional)
  - `org.jetbrains.kotlinx:kotlinx-coroutines-bom:1.10.2` — Kotlin coroutines (optional)
  - `org.jetbrains.kotlinx:kotlinx-serialization-bom:1.11.0` — Kotlin serialisation (optional)
  - `org.objenesis:objenesis:3.5` (repackaged as `org.springframework.objenesis`) — object instantiation without constructors
  - `com.palantir.javapoet:javapoet:0.10.0` (repackaged as `org.springframework.javapoet`) — Java source generation for AOT
  - `org.quartz-scheduler:quartz:2.3.2` — Quartz job scheduling (optional)
  - `org.freemarker:freemarker:2.3.34` — FreeMarker template engine (optional)
  - `com.github.ben-manes.caffeine:caffeine:3.2.3` — local cache (optional)
  - `javax.cache:cache-api:1.1.1` — JCache API (optional)
  - `org.crac:crac:1.4.0` — CRaC checkpoint-restore (optional)
  - `org.graalvm.sdk:graal-sdk:22.3.1` — GraalVM Native Image (optional, build-time)

- **Configuration summary:**
  - Version controlled via `gradle.properties`: `version=7.1.0-SNAPSHOT`, `kotlinVersion=2.3.20`, `byteBuddyVersion=1.17.6`
  - AOT mode activation: system property `spring.aot.enabled=true` or when running inside a GraalVM native image (detected via `NativeDetector`) — see `src/spring-framework/spring-core/src/main/java/org/springframework/aot/AotDetector.java`
  - Profile activation: environment/system property `spring.profiles.active` — see `src/spring-framework/spring-core/src/main/java/org/springframework/core/env/AbstractEnvironment.java`
  - Default DispatcherServlet strategy beans registered in `src/spring-framework/spring-webmvc/src/main/resources/org/springframework/web/servlet/DispatcherServlet.properties`
  - Spring factories (SPI) registered via `META-INF/spring.factories` across modules
  - Native image build configuration in `META-INF/native-image/` per module
  - No `application.properties` or `application.yml` present — this is a framework, not a Spring Boot application; consumers supply their own configuration

---

## 2. User Roles and Access Control

Spring Framework itself does not implement authentication or authorisation — it is a general-purpose application framework that provides infrastructure which consumers use to build secured applications. Spring Security is a separate project not present in this codebase. The framework does expose several extension points that consumers use to implement access control:

| Role | Permissions / Access | Source |
|------|---------------------|--------|
| Framework API consumer | Full access to all public APIs; no in-framework restriction | All public interfaces across all modules |
| `UserRoleAuthorizationInterceptor` subject | Servlet container role-based access check at handler level; roles configured by the application | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/handler/UserRoleAuthorizationInterceptor.java` |
| `PrincipalMethodArgumentResolver` subject | Injects `java.security.Principal` from request into controller method parameters; access determination is container/security-layer responsibility | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/PrincipalMethodArgumentResolver.java` |

- **Authentication mechanism:** None built-in. The framework provides `PrincipalMethodArgumentResolver` (MVC) and `PrincipalMethodArgumentResolver` (WebFlux) to pass the container-authenticated principal into controllers. Spring Security integration is the expected mechanism for consumers but is out of scope here.
- **Authorisation approach:** None built-in. `UserRoleAuthorizationInterceptor` provides a rudimentary servlet-container role check. Full authorisation (e.g. `@PreAuthorize`) is handled by Spring Security and is not present in this codebase.

---

## 3. Features and Capabilities

#### Dependency Injection and Bean Container

- **Description:** The inversion-of-control (IoC) container manages Java object lifecycle, dependency wiring (by type, name, or qualifier), bean scopes (singleton, prototype, request, session, application, WebSocket), and supports XML, Java annotation, and Groovy-DSL configuration styles. Supports constructor injection, setter injection, and field injection.
- **Key classes/interfaces:**
  - `BeanFactory` — root interface for bean container access
  - `DefaultListableBeanFactory` — primary implementation of `ConfigurableListableBeanFactory`
  - `ApplicationContext` / `GenericApplicationContext` / `AnnotationConfigApplicationContext` — extended containers with event, i18n, and resource loading
  - `AbstractAutowireCapableBeanFactory` — performs actual bean creation and dependency resolution
  - `AutowiredAnnotationBeanPostProcessor` — processes `@Autowired`, `@Value`, `@Inject`
  - `ConfigurationClassPostProcessor` — processes `@Configuration`, `@Bean`, `@ComponentScan`, `@Import`
  - `BeanDefinition` — metadata model for a bean
  - `BeanRegistry` / `BeanRegistrar` — programmatic bean registration (new in 7.x)
- **Source files:**
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/BeanFactory.java`
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/DefaultListableBeanFactory.java`
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/annotation/AutowiredAnnotationBeanPostProcessor.java`
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/annotation/Autowired.java`
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/annotation/Value.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/ConfigurationClassPostProcessor.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/AnnotationConfigApplicationContext.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/support/GenericApplicationContext.java`
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/BeanRegistrar.java`
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/BeanRegistry.java`

#### Aspect-Oriented Programming (AOP)

- **Description:** Provides proxy-based AOP allowing cross-cutting concerns (logging, transactions, security, caching, retry) to be applied declaratively via AspectJ annotations (`@Aspect`, `@Before`, `@After`, `@Around`, etc.) or programmatically. Supports both JDK dynamic proxies and CGLIB subclass proxies. Full AspectJ load-time weaving (LTW) is also supported via the `spring-aspects` and `spring-instrument` modules.
- **Key classes/interfaces:**
  - `ProxyFactory` — programmatic AOP proxy creation
  - `AopProxyFactory` / `DefaultAopProxyFactory` — chooses between JDK and CGLIB proxy
  - `JdkDynamicAopProxy` / `ObjenesisCglibAopProxy` — concrete proxy implementations
  - `AbstractAspectJAdvice` — base for AspectJ advice wrappers
  - `ReflectiveAspectJAdvisorFactory` — builds advisors from `@Aspect` annotated beans
  - `AnnotationAwareAspectJAutoProxyCreator` — detects `@Aspect` beans and auto-creates proxies
  - `AspectJExpressionPointcut` — evaluates AspectJ pointcut expressions
  - `Advisor`, `Advice`, `Pointcut` — AOP Alliance / Spring abstractions
- **Source files:**
  - `src/spring-framework/spring-aop/src/main/java/org/springframework/aop/framework/ProxyFactory.java`
  - `src/spring-framework/spring-aop/src/main/java/org/springframework/aop/framework/JdkDynamicAopProxy.java`
  - `src/spring-framework/spring-aop/src/main/java/org/springframework/aop/framework/ObjenesisCglibAopProxy.java`
  - `src/spring-framework/spring-aop/src/main/java/org/springframework/aop/aspectj/annotation/ReflectiveAspectJAdvisorFactory.java`
  - `src/spring-framework/spring-aop/src/main/java/org/springframework/aop/aspectj/annotation/AnnotationAwareAspectJAutoProxyCreator.java`
  - `src/spring-framework/spring-aop/src/main/java/org/springframework/aop/aspectj/AbstractAspectJAdvice.java`
  - `src/spring-framework/spring-aspects/src/main/java/org/springframework/transaction/aspectj/AspectJTransactionManagementConfiguration.java`

#### Spring Expression Language (SpEL)

- **Description:** A powerful expression language supporting property access, method invocation, arithmetic/logical operators, collection projection/selection, inline list/map construction, type references, bean references, and ternary/Elvis operators. Used pervasively in `@Value`, `@Cacheable`, `@Scheduled`, `@PreAuthorize`, and in XML configuration. Expressions can be compiled to JVM byte code for performance.
- **Key classes/interfaces:**
  - `ExpressionParser` / `SpelExpressionParser` — parses expressions
  - `SpelExpression` — evaluatable expression
  - `SpelCompiler` — ASM-based byte-code compiler for SpEL expressions
  - `StandardEvaluationContext` / `SimpleEvaluationContext` — evaluation contexts
  - `ReflectivePropertyAccessor`, `ReflectiveMethodResolver` — reflection-based resolution
  - `SpelParserConfiguration` — controls parser behaviour (auto-grow null refs, etc.)
  - AST node classes: `MethodReference`, `PropertyOrFieldReference`, `Indexer`, `Selection`, `Projection`, `Ternary`, `Elvis`, all operators
- **Source files:**
  - `src/spring-framework/spring-expression/src/main/java/org/springframework/expression/spel/standard/SpelExpressionParser.java`
  - `src/spring-framework/spring-expression/src/main/java/org/springframework/expression/spel/standard/SpelExpression.java`
  - `src/spring-framework/spring-expression/src/main/java/org/springframework/expression/spel/standard/SpelCompiler.java`
  - `src/spring-framework/spring-expression/src/main/java/org/springframework/expression/spel/support/StandardEvaluationContext.java`
  - `src/spring-framework/spring-expression/src/main/java/org/springframework/expression/spel/SpelParserConfiguration.java`

#### Transaction Management

- **Description:** Unified transaction abstraction over multiple transaction APIs (JDBC, JPA, JTA, reactive R2DBC). Supports declarative transactions via `@Transactional` (with configurable propagation, isolation, rollback rules, timeout), programmatic transactions via `TransactionTemplate`, and event-driven transaction listeners. Both imperative (`PlatformTransactionManager`) and reactive (`ReactiveTransactionManager`) managers are provided.
- **Key classes/interfaces:**
  - `PlatformTransactionManager` / `ReactiveTransactionManager` — core abstraction
  - `TransactionDefinition` — propagation, isolation, timeout, read-only settings
  - `@Transactional` — declarative transaction annotation
  - `TransactionInterceptor` — AOP interceptor applying transaction semantics
  - `DataSourceTransactionManager` — JDBC transaction manager
  - `JpaTransactionManager` — JPA transaction manager
  - `TransactionSynchronizationManager` — thread-local synchronisation registry
  - `TransactionTemplate` — programmatic template
  - `@TransactionalEventListener` — event listeners scoped to transaction phases
- **Source files:**
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/annotation/Transactional.java`
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/PlatformTransactionManager.java`
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/ReactiveTransactionManager.java`
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/interceptor/TransactionInterceptor.java`
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/datasource/DataSourceTransactionManager.java`
  - `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/JpaTransactionManager.java`
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/support/TransactionSynchronizationManager.java`
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/event/` (package)

#### JDBC Data Access

- **Description:** Template-method abstraction over raw JDBC. `JdbcTemplate` handles connection acquisition, statement creation, result-set iteration, exception translation (to the `DataAccessException` hierarchy), and resource cleanup. `JdbcClient` (since 6.1) provides a fluent, modern API. Named-parameter support via `NamedParameterJdbcTemplate`. `SimpleJdbcInsert` and `SimpleJdbcCall` simplify inserts and stored procedure calls. Row-mapping via `RowMapper`, `BeanPropertyRowMapper`, `DataClassRowMapper`.
- **Key classes/interfaces:**
  - `JdbcTemplate` — central JDBC delegation class
  - `JdbcClient` / `DefaultJdbcClient` — fluent JDBC client (since 6.1)
  - `NamedParameterJdbcTemplate` — named-parameter wrapper around `JdbcTemplate`
  - `SimpleJdbcInsert` / `SimpleJdbcCall` — simplified insert/stored-procedure execution
  - `RowMapper` / `BeanPropertyRowMapper` / `DataClassRowMapper` — result mapping
  - `DataSourceUtils` — connection management integrated with transaction synchronisation
  - `EmbeddedDatabaseBuilder` — in-memory embedded databases (H2, HSQLDB, Derby)
- **Source files:**
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/JdbcTemplate.java`
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/simple/JdbcClient.java`
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/namedparam/NamedParameterJdbcTemplate.java`
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/simple/SimpleJdbcInsert.java`
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/simple/SimpleJdbcCall.java`
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/BeanPropertyRowMapper.java`
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/datasource/DataSourceUtils.java`
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/datasource/embedded/` (package)

#### JPA / ORM Integration

- **Description:** Integrates JPA 3.2 (with Hibernate 7.x as the primary tested provider) into the Spring container. Manages `EntityManagerFactory` lifecycle as a Spring bean, provides `SharedEntityManagerCreator` so that `EntityManager` instances are proxy-aware and transaction-scoped, and offers `JpaTransactionManager` for JPA-based transaction management. Hibernate-specific dialect support is included.
- **Key classes/interfaces:**
  - `LocalContainerEntityManagerFactoryBean` — bootstraps JPA `EntityManagerFactory`
  - `SharedEntityManagerCreator` — creates thread-/transaction-bound `EntityManager` proxy
  - `JpaTransactionManager` — JPA transaction manager
  - `JpaDialect` / `DefaultJpaDialect` — vendor-specific JPA behaviour
  - `HibernateJpaVendorAdapter` — Hibernate-specific adapter
- **Source files:**
  - `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/LocalContainerEntityManagerFactoryBean.java`
  - `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/SharedEntityManagerCreator.java`
  - `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/JpaTransactionManager.java`
  - `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/vendor/` (package)
  - `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/hibernate/` (package)

#### Reactive Data Access (R2DBC)

- **Description:** Reactive, non-blocking relational database access using the R2DBC SPI. `DatabaseClient` provides a fluent API returning `Mono`/`Flux` publishers. Transaction management integrates with `ReactiveTransactionManager`. Named-parameter expansion and row mapping (including record/data-class mapping) are supported.
- **Key classes/interfaces:**
  - `DatabaseClient` / `DefaultDatabaseClient` — reactive fluent JDBC-equivalent
  - `R2dbcTransactionManager` — reactive transaction manager for R2DBC
  - `NamedParameterUtils` / `NamedParameterExpander` — named-parameter handling
  - `BeanPropertyRowMapper` / `DataClassRowMapper` (R2DBC variants)
- **Source files:**
  - `src/spring-framework/spring-r2dbc/src/main/java/org/springframework/r2dbc/core/DatabaseClient.java`
  - `src/spring-framework/spring-r2dbc/src/main/java/org/springframework/r2dbc/core/DefaultDatabaseClient.java`
  - `src/spring-framework/spring-r2dbc/src/main/java/org/springframework/r2dbc/connection/` (package)

#### Spring MVC (Servlet-based Web)

- **Description:** Full-featured Model-View-Controller web framework built on the Servlet API. The `DispatcherServlet` is the front controller routing requests to annotated controllers (`@Controller`, `@RestController`) via `HandlerMapping` implementations. Supports annotation-driven request mapping (`@GetMapping`, `@PostMapping`, etc.), data binding, validation, view resolution (FreeMarker, JSP, Thymeleaf, JSON, PDF, Excel), content negotiation, CORS, multipart file upload, SSE, async processing, static resource serving, and functional routing via `RouterFunction`.
- **Key classes/interfaces:**
  - `DispatcherServlet` — front controller
  - `RequestMappingHandlerMapping` / `RequestMappingHandlerAdapter` — annotation-driven routing
  - `@RequestMapping`, `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`, `@PatchMapping`
  - `@RequestBody`, `@ResponseBody`, `@PathVariable`, `@RequestParam`, `@RequestHeader`, `@ModelAttribute`
  - `@ExceptionHandler`, `@ControllerAdvice`, `@RestControllerAdvice`
  - `RouterFunctions` — functional routing DSL
  - `ResponseEntityExceptionHandler` — centralised exception-to-response mapping
  - `ContentNegotiatingViewResolver` — selects view by `Accept` header
  - `ResourceHttpRequestHandler` — serves static resources
  - `MultipartResolver` — multipart file upload
  - `HandlerInterceptor` — pre/post processing around handler calls
  - `LocaleResolver` (Accept-header, Cookie, Session variants) — locale negotiation
  - `FlashMapManager` — redirect/flash attributes
  - `SseEmitter` / `StreamingResponseBody` / `ResponseBodyEmitter` — streaming responses
- **Source files:**
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/DispatcherServlet.java`
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/RequestMappingHandlerMapping.java`
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/RequestMappingHandlerAdapter.java`
  - `src/spring-framework/spring-web/src/main/java/org/springframework/web/bind/annotation/` (full package)
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/function/RouterFunctions.java`
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/view/` (package)
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/ResponseEntityExceptionHandler.java`
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/SseEmitter.java`
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/resource/ResourceHttpRequestHandler.java`

#### Reactive Web (Spring WebFlux)

- **Description:** Non-blocking, reactive-streams-compliant web framework running on Reactor Netty, Undertow, Tomcat, Jetty, or any Servlet 3.1+ container in async mode. Mirrors Spring MVC's annotation model but returns `Mono`/`Flux`. Includes `WebClient` (reactive HTTP client), functional routing, reactive WebSocket handling, and SSE. Kotlin coroutines are natively supported.
- **Key classes/interfaces:**
  - `DispatcherHandler` — reactive front controller
  - `RequestMappingHandlerMapping` / `RequestMappingHandlerAdapter` (WebFlux variants)
  - `WebClient` — reactive, non-blocking HTTP client
  - `RouterFunctions` (WebFlux variant) — functional routing
  - `ResponseEntityExceptionHandler` (WebFlux variant)
- **Source files:**
  - `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/DispatcherHandler.java`
  - `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/result/method/annotation/RequestMappingHandlerMapping.java`
  - `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/function/client/WebClient.java`
  - `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/function/server/RouterFunctions.java`

#### HTTP Client Abstractions (RestTemplate, RestClient, WebClient)

- **Description:** Three generations of HTTP client abstraction. `RestTemplate` (synchronous, blocking) is the classic client; `RestClient` (since 6.1) provides a modern, fluent synchronous API; `WebClient` provides a reactive, non-blocking client. All support message conversion, error handling, request interceptors/filters, and observability. HTTP interface (declarative HTTP client) via `@HttpExchange`-annotated interfaces with `HttpServiceProxyFactory` lets consumers define typed HTTP clients without boilerplate.
- **Key classes/interfaces:**
  - `RestTemplate` — synchronous HTTP client
  - `RestClient` / `DefaultRestClient` — fluent synchronous client (since 6.1)
  - `WebClient` / `DefaultWebClient` — reactive HTTP client
  - `HttpServiceProxyFactory` — creates proxies for `@HttpExchange` interfaces
  - `@GetExchange`, `@PostExchange`, `@PutExchange`, `@DeleteExchange`, `@PatchExchange`, `@HttpExchange` — declarative HTTP annotations
  - `ResponseErrorHandler` / `DefaultResponseErrorHandler` — response error handling
  - `HttpMessageConverter` — bidirectional message serialisation/deserialisation
- **Source files:**
  - `src/spring-framework/spring-web/src/main/java/org/springframework/web/client/RestTemplate.java`
  - `src/spring-framework/spring-web/src/main/java/org/springframework/web/client/RestClient.java`
  - `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/function/client/WebClient.java`
  - `src/spring-framework/spring-web/src/main/java/org/springframework/web/service/invoker/HttpServiceProxyFactory.java`
  - `src/spring-framework/spring-web/src/main/java/org/springframework/web/service/annotation/` (package)

#### Messaging and WebSocket / STOMP

- **Description:** A layered messaging framework. The core `spring-messaging` module provides `Message`, `MessageChannel`, and `MessageHandler` abstractions used by WebSocket, JMS, RSocket, and STOMP brokers. Spring WebSocket (`spring-websocket`) provides server and client adapters for JSR-356 WebSocket (Tomcat, Jetty) with SockJS fallback. STOMP over WebSocket enables publish-subscribe patterns with topic/queue message brokering within the application. RSocket support is in `spring-messaging`.
- **Key classes/interfaces:**
  - `Message` / `MessageChannel` / `SubscribableChannel` — core messaging
  - `SimpMessagingTemplate` — send messages to WebSocket destinations
  - `WebSocketSession` / `WebSocketHandler` — WebSocket API
  - `RSocketRequester` — RSocket client
  - `@MessageMapping`, `@SubscribeMapping` — STOMP handler annotations
  - `SimpleBrokerMessageHandler` / `StompBrokerRelayMessageHandler` — in-memory and relay brokers
- **Source files:**
  - `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/Message.java`
  - `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/simp/SimpMessagingTemplate.java`
  - `src/spring-framework/spring-websocket/src/main/java/org/springframework/web/socket/WebSocketSession.java`
  - `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/rsocket/RSocketRequester.java`
  - `src/spring-framework/spring-websocket/src/main/java/org/springframework/web/socket/sockjs/` (package)

#### JMS Integration

- **Description:** Simplifies Jakarta Messaging (JMS 3.1) interaction. `JmsTemplate` wraps JMS boilerplate (connection/session/producer lifecycle). `JmsClient` provides a modern fluent API. `DefaultMessageListenerContainer` runs poll-based message listeners in background threads with full transaction integration. `@JmsListener` enables annotation-driven message listening. Micrometer observation is built in.
- **Key classes/interfaces:**
  - `JmsTemplate` — synchronous JMS send/receive
  - `JmsClient` / `DefaultJmsClient` — fluent JMS client
  - `DefaultMessageListenerContainer` — polled listener container
  - `SimpleMessageListenerContainer` — simple synchronous listener
  - `MessageListenerAdapter` — POJO-delegating listener
  - `@JmsListener` — annotation-driven listener
  - `JmsTransactionManager` — JMS-backed transaction manager
- **Source files:**
  - `src/spring-framework/spring-jms/src/main/java/org/springframework/jms/core/JmsTemplate.java`
  - `src/spring-framework/spring-jms/src/main/java/org/springframework/jms/core/JmsClient.java`
  - `src/spring-framework/spring-jms/src/main/java/org/springframework/jms/listener/DefaultMessageListenerContainer.java`
  - `src/spring-framework/spring-jms/src/main/java/org/springframework/jms/annotation/` (package)

#### Declarative Caching

- **Description:** Annotation-driven caching abstraction supporting multiple cache backends (ConcurrentHashMap, Caffeine, JCache/JSR-107, EhCache, Infinispan, Redis via Spring Data). Cache operations are intercepted via AOP. AspectJ-based caching (non-proxy) is available via `spring-aspects`.
- **Key classes/interfaces:**
  - `@Cacheable` — caches method return value
  - `@CachePut` — always updates cache with method return value
  - `@CacheEvict` — removes entries from cache
  - `@Caching` — groups multiple cache operations
  - `@EnableCaching` — activates cache infrastructure
  - `CacheManager` — SPI for cache backend
  - `CacheInterceptor` — AOP interceptor applying cache semantics
  - `CaffeineCacheManager` — Caffeine backend
  - `JCacheCacheManager` — JSR-107 backend
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/cache/annotation/Cacheable.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/cache/annotation/EnableCaching.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/cache/interceptor/CacheInterceptor.java`
  - `src/spring-framework/spring-context-support/src/main/java/org/springframework/cache/caffeine/CaffeineCacheManager.java`
  - `src/spring-framework/spring-context-support/src/main/java/org/springframework/cache/jcache/` (package)

#### Task Scheduling and Async Execution

- **Description:** Declarative task scheduling (`@Scheduled` with cron, fixed rate, fixed delay, and one-shot delay semantics) and asynchronous method execution (`@Async`). Supports both imperative and reactive return types (Mono/Flux, Kotlin coroutines). `TaskScheduler` abstraction unifies thread-pool and Quartz-based schedulers. Virtual thread executors (`VirtualThreadTaskExecutor`) are supported from Java 21.
- **Key classes/interfaces:**
  - `@Scheduled` — marks a method for periodic/delayed scheduling
  - `@Async` — marks a method for asynchronous execution
  - `@EnableScheduling` / `@EnableAsync` — activates scheduling/async infrastructure
  - `TaskScheduler` / `ThreadPoolTaskScheduler` / `ConcurrentTaskScheduler`
  - `AsyncAnnotationBeanPostProcessor` — AOP proxy creator for `@Async`
  - `ScheduledAnnotationBeanPostProcessor` — registers `@Scheduled` tasks
  - `VirtualThreadTaskExecutor` — Java 21+ virtual thread executor
  - `SimpleAsyncTaskExecutor` — lightweight per-task threading
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/annotation/Scheduled.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/annotation/Async.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/annotation/ScheduledAnnotationBeanPostProcessor.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/annotation/AsyncAnnotationBeanPostProcessor.java`
  - `src/spring-framework/spring-core/src/main/java/org/springframework/core/task/VirtualThreadTaskExecutor.java`
  - `src/spring-framework/spring-context-support/src/main/java/org/springframework/scheduling/quartz/` (package)

#### Application Events

- **Description:** Publish-subscribe event system embedded in the `ApplicationContext`. Beans publish events via `ApplicationEventPublisher`; listeners declare interest via `@EventListener` (including `@TransactionalEventListener` for transaction-scoped delivery) or by implementing `ApplicationListener`. Async event delivery is supported. Context lifecycle events (started, refreshed, stopped, closed) are published automatically.
- **Key classes/interfaces:**
  - `ApplicationEvent` — base class for all events
  - `ApplicationEventPublisher` — publish interface
  - `@EventListener` — annotation-driven listener registration
  - `@TransactionalEventListener` — listener bound to a transaction phase
  - `SimpleApplicationEventMulticaster` — default multicaster
  - `ContextRefreshedEvent`, `ContextClosedEvent`, `ContextStartedEvent`, `ContextStoppedEvent`, `ContextPausedEvent`, `ContextRestartedEvent`
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/ApplicationEvent.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/event/EventListener.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/event/SimpleApplicationEventMulticaster.java`
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/event/` (package)

#### Resilience: Retry and Concurrency Limiting (new in 7.0)

- **Description:** Native framework-level resilience annotations added in Spring 7.0, inspired by the separate Spring Retry project. `@Retryable` marks methods for automatic retry with configurable exception filters, max attempts, timeout, delay, jitter, and multiplier (exponential backoff). `@ConcurrencyLimit` limits the number of concurrent invocations of a method or class, with optional blocking or rejection policy. Supports both imperative and reactive (Reactor) return types.
- **Key classes/interfaces:**
  - `@Retryable` — retry annotation
  - `@ConcurrencyLimit` — concurrency throttle annotation
  - `@EnableResilientMethods` — activates resilience infrastructure
  - `RetryAnnotationBeanPostProcessor` — creates AOP proxies for `@Retryable`
  - `ConcurrencyLimitBeanPostProcessor` — creates AOP proxies for `@ConcurrencyLimit`
  - `SimpleRetryInterceptor` — AOP advice performing retry logic
  - `MethodRetrySpec` — record describing retry configuration
  - `RetryTemplate` (in `spring-core`) — programmatic retry execution
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/resilience/annotation/Retryable.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/resilience/annotation/ConcurrencyLimit.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/resilience/annotation/EnableResilientMethods.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/resilience/retry/MethodRetrySpec.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/resilience/retry/SimpleRetryInterceptor.java`
  - `src/spring-framework/spring-core/src/main/java/org/springframework/core/retry/RetryTemplate.java`

#### Validation

- **Description:** Unified validation framework. Spring's own `Validator` interface provides programmatic validation with `Errors`/`BindingResult`. Bean Validation (Jakarta Validation API / Hibernate Validator) is integrated via `LocalValidatorFactoryBean` and `MethodValidationPostProcessor`, enabling constraint annotations (`@NotNull`, `@Size`, etc.) on method parameters and return values. `DataBinder` binds request parameters to objects and drives validation.
- **Key classes/interfaces:**
  - `Validator` / `SmartValidator` — Spring validation SPI
  - `LocalValidatorFactoryBean` — integrates Jakarta Bean Validation
  - `MethodValidationPostProcessor` / `MethodValidationInterceptor` — method-level validation via AOP
  - `DataBinder` — binds request parameters, drives validation
  - `Errors` / `BindingResult` — validation error accumulation
  - `ValidationUtils` — utility methods
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/validation/Validator.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/validation/beanvalidation/LocalValidatorFactoryBean.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/validation/beanvalidation/MethodValidationPostProcessor.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/validation/DataBinder.java`

#### Data Formatting and Conversion

- **Description:** Type conversion service (`ConversionService`) providing an extensible converter/formatter registry. Formatters parse text to objects and format objects to text (e.g. date/number formatting). `@NumberFormat`, `@DateTimeFormat` annotations on fields trigger automatic formatting. SpEL and data-binding both use this infrastructure.
- **Key classes/interfaces:**
  - `ConversionService` / `DefaultConversionService` — type conversion
  - `FormattingConversionService` — conversion + formatting
  - `Formatter`, `Printer`, `Parser` — formatting SPI
  - `@NumberFormat`, `@DateTimeFormat` — format annotations
  - `ConversionServiceFactoryBean` — configures conversion service as a bean
- **Source files:**
  - `src/spring-framework/spring-core/src/main/java/org/springframework/core/convert/ConversionService.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/format/annotation/` (package)
  - `src/spring-framework/spring-context/src/main/java/org/springframework/format/support/` (package)

#### JMX Integration

- **Description:** Exposes Spring beans as JMX MBeans with configurable naming, attribute/operation exposure, and notification support. Beans can be proxied and accessed as remote JMX resources. Annotations (`@ManagedResource`, `@ManagedAttribute`, `@ManagedOperation`) drive exposure.
- **Key classes/interfaces:**
  - `MBeanExporter` — exports beans as MBeans
  - `@EnableMBeanExport` — activates auto-detection
  - `MBeanServerFactoryBean` — creates/locates `MBeanServer`
  - `MBeanProxyFactoryBean` — proxies remote MBeans as local Spring beans
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/jmx/export/` (package)
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/EnableMBeanExport.java`

#### AOT (Ahead-of-Time) Processing and GraalVM Native Image Support

- **Description:** Spring Framework 6.0+ includes a comprehensive AOT processing pipeline for generating optimised source code and GraalVM Native Image hints at build time. `ContextAotProcessor` drives the process. `RuntimeHints` accumulates reflection, proxy, serialisation, and resource hints. `BeanRegistrationAotProcessor` / `BeanFactoryInitializationAotProcessor` are extension points for modules to contribute AOT metadata. The resulting generated code allows the application to start without classpath scanning at runtime.
- **Key classes/interfaces:**
  - `AotDetector` — runtime detection of AOT mode
  - `RuntimeHints` / `ReflectionHints` / `ProxyHints` / `ResourceHints` — hint accumulation
  - `RuntimeHintsRegistrar` — SPI for registering hints
  - `ContextAotProcessor` / `ApplicationContextAotGenerator`
  - `BeanRegistrationAotProcessor` / `BeanFactoryInitializationAotProcessor`
  - `GenerationContext` / `GeneratedClasses` / `GeneratedFiles` — code generation infrastructure
  - `SpelCompiler` — byte-code compiled expressions work without reflection
  - `@ImportRuntimeHints` — declarative hint import
- **Source files:**
  - `src/spring-framework/spring-core/src/main/java/org/springframework/aot/AotDetector.java`
  - `src/spring-framework/spring-core/src/main/java/org/springframework/aot/hint/RuntimeHints.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/aot/ContextAotProcessor.java`
  - `src/spring-framework/spring-core/src/main/java/org/springframework/aot/generate/` (package)
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/aot/` (package)

#### Testing Support

- **Description:** Comprehensive test framework integration. Spring TestContext Framework (`TestContextManager`) manages application context caching across test methods. `@SpringJUnitConfig`, `@ContextConfiguration`, `@ActiveProfiles`, `@TestPropertySource`, `@DynamicPropertySource` configure the test context. `MockMvc` and `WebTestClient` perform server-side integration testing without deploying to a real server. `@MockBean` / `@SpyBean` inject Mockito mocks into the context. SQL script execution (`@Sql`), transaction rollback (`@Transactional`), and Bean Override support are included.
- **Key classes/interfaces:**
  - `TestContextManager` — central orchestrator
  - `MockMvc` — Spring MVC test support
  - `WebTestClient` — reactive and MVC test client
  - `@SpringJUnitConfig`, `@ContextConfiguration`, `@ActiveProfiles`, `@TestPropertySource`
  - `@MockBean`, `@SpyBean` — Mockito integration
  - `@Sql` — SQL script execution
  - `@DynamicPropertySource` — dynamic property registration
- **Source files:**
  - `src/spring-framework/spring-test/src/main/java/org/springframework/test/context/TestContextManager.java`
  - `src/spring-framework/spring-test/src/main/java/org/springframework/test/web/servlet/MockMvc.java` (path inferred)
  - `src/spring-framework/spring-test/src/main/java/org/springframework/test/web/reactive/server/WebTestClient.java` (path inferred)
  - `src/spring-framework/spring-test/src/main/resources/META-INF/spring.factories`

#### Resource Abstraction

- **Description:** Uniform access to underlying resources (classpath entries, file system paths, URLs, byte arrays, input streams, module-path resources) through the `Resource` interface. `ResourceLoader` resolves resource descriptors by location prefix (`classpath:`, `file:`, `http://`, `classpath*:`). Used throughout the framework for loading configuration, templates, and static content.
- **Key classes/interfaces:**
  - `Resource` — core interface
  - `ClassPathResource`, `FileSystemResource`, `UrlResource`, `ByteArrayResource`, `PathResource`, `ModuleResource`
  - `ResourceLoader` / `DefaultResourceLoader`
  - `ResourcePatternResolver` / `PathMatchingResourcePatternResolver` — wildcard resolution
- **Source files:**
  - `src/spring-framework/spring-core/src/main/java/org/springframework/core/io/Resource.java`
  - `src/spring-framework/spring-core/src/main/java/org/springframework/core/io/` (package)

#### Object/XML Mapping (OXM)

- **Description:** Marshalling and unmarshalling between Java objects and XML. Unified `Marshaller`/`Unmarshaller` abstraction with JAXB2 and XStream implementations. Used by `spring-webmvc` and `spring-webflux` for XML message conversion.
- **Key classes/interfaces:**
  - `Marshaller` / `Unmarshaller` — OXM abstractions
  - `Jaxb2Marshaller` — JAXB 2/3 implementation
  - `XStreamMarshaller` — XStream implementation
- **Source files:**
  - `src/spring-framework/spring-oxm/src/main/java/org/springframework/oxm/Marshaller.java`
  - `src/spring-framework/spring-oxm/src/main/java/org/springframework/oxm/jaxb/` (package)

#### Mail Support

- **Description:** Abstraction over JavaMail (Jakarta Mail) API for sending email. `JavaMailSender` / `JavaMailSenderImpl` send `MimeMessage` or `SimpleMailMessage` instances. FreeMarker/Thymeleaf template integration for email body generation.
- **Key classes/interfaces:**
  - `MailSender` / `JavaMailSender` / `JavaMailSenderImpl`
  - `SimpleMailMessage` — simple text email model
  - `MimeMessageHelper` — builder for complex `MimeMessage`
- **Source files:**
  - `src/spring-framework/spring-context-support/src/main/java/org/springframework/mail/` (package)
  - `src/spring-framework/spring-context-support/src/main/java/org/springframework/mail/javamail/` (package)

---

## 4. Workflows and Behaviours

#### Spring MVC HTTP Request Processing

- **Type:** User-facing
- **Trigger:** An HTTP request arrives at the web server and is routed to the `DispatcherServlet`.
- **Steps:**
  1. Servlet container (Tomcat/Jetty) receives the request and passes it to `DispatcherServlet.doDispatch()` — `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/DispatcherServlet.java`
  2. `DispatcherServlet` calls each registered `HandlerMapping` (default: `BeanNameUrlHandlerMapping`, `RequestMappingHandlerMapping`, `RouterFunctionMapping`) to find a matching handler — `DispatcherServlet.properties`
  3. `HandlerExecutionChain` is assembled: handler + applicable `HandlerInterceptor`s — `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/HandlerExecutionChain.java`
  4. Interceptors' `preHandle()` methods are called; if any returns `false`, processing stops.
  5. The matching `HandlerAdapter` (default: `RequestMappingHandlerAdapter`) invokes the controller method, resolving arguments (`@RequestBody`, `@PathVariable`, etc.) and applying data binding and validation — `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/RequestMappingHandlerAdapter.java`
  6. The controller method executes and returns a value (`ModelAndView`, `ResponseEntity`, an object for `@ResponseBody`, etc.).
  7. For `@ResponseBody` / `@RestController`, `RequestResponseBodyMethodProcessor` serialises the return value via the appropriate `HttpMessageConverter` — `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/RequestResponseBodyMethodProcessor.java`
  8. For view-based responses, `ViewResolver` resolves the logical view name to a `View`; the `View` renders the response.
  9. Interceptors' `postHandle()` and `afterCompletion()` methods are called.
  10. If an exception is thrown, the `HandlerExceptionResolver` chain (`ExceptionHandlerExceptionResolver` → `ResponseStatusExceptionResolver` → `DefaultHandlerExceptionResolver`) resolves it — `DispatcherServlet.properties`
- **State transitions:** Request → matched handler → interceptors pre-process → controller executes → response written → interceptors post-process → complete (or exception handled)
- **Source files:**
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/DispatcherServlet.java`
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/RequestMappingHandlerAdapter.java`
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/RequestResponseBodyMethodProcessor.java`

#### ApplicationContext Startup (Refresh)

- **Type:** System/background
- **Trigger:** `ApplicationContext.refresh()` called (typically once at application startup).
- **Steps:**
  1. `prepareRefresh()` — sets start time, validates required properties, initialises early `ApplicationListener`s — `src/spring-framework/spring-context/src/main/java/org/springframework/context/support/AbstractApplicationContext.java`
  2. `obtainFreshBeanFactory()` — creates or refreshes the internal `DefaultListableBeanFactory`; loads bean definitions from XML, annotations, or Groovy — `AbstractRefreshableApplicationContext`
  3. `prepareBeanFactory()` — registers standard post-processors (`ApplicationContextAwareProcessor`, `ApplicationListenerDetector`, etc.)
  4. `postProcessBeanFactory()` — hook for subclasses (e.g. `WebApplicationContext` registers servlet-specific scopes)
  5. `invokeBeanFactoryPostProcessors()` — runs all `BeanFactoryPostProcessor`s, crucially `ConfigurationClassPostProcessor` which processes `@Configuration`, `@ComponentScan`, `@Bean`, `@Import` — `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/ConfigurationClassPostProcessor.java`
  6. `registerBeanPostProcessors()` — registers `BeanPostProcessor`s in order
  7. `initMessageSource()`, `initApplicationEventMulticaster()` — sets up i18n and event infrastructure
  8. `onRefresh()` — subclass hook (e.g. WebServer start in Spring Boot)
  9. `registerListeners()` — connects early `ApplicationListener`s
  10. `finishBeanFactoryInitialization()` — instantiates all remaining non-lazy singleton beans
  11. `finishRefresh()` — clears caches, publishes `ContextRefreshedEvent`, starts `Lifecycle` beans
- **State transitions:** UNINITIALIZED → REFRESHING → ACTIVE; ACTIVE → CLOSED on `close()`
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/support/AbstractApplicationContext.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/ConfigurationClassPostProcessor.java`
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/AbstractAutowireCapableBeanFactory.java`

#### Declarative Transaction Execution

- **Type:** User-facing (transparent, triggered by method invocation on a transactional bean)
- **Trigger:** Invocation of a method annotated with `@Transactional` (or matching a transaction attribute source) on a proxied bean.
- **Steps:**
  1. `TransactionInterceptor.invoke()` intercepts the method call via an AOP proxy — `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/interceptor/TransactionInterceptor.java`
  2. `TransactionAttributeSource` (e.g. `AnnotationTransactionAttributeSource`) retrieves the transaction attributes (`propagation`, `isolation`, `timeout`, `readOnly`, `rollbackFor`) — `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/interceptor/AnnotationTransactionAttributeSource.java`
  3. `PlatformTransactionManager.getTransaction()` creates or joins an existing transaction based on the propagation rule — `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/PlatformTransactionManager.java`
  4. The target method executes within the transaction boundary.
  5. On successful return: `PlatformTransactionManager.commit()` is called.
  6. On exception: rollback rules are evaluated; `PlatformTransactionManager.rollback()` is called if the exception matches.
  7. Transaction synchronisation callbacks (registered via `TransactionSynchronizationManager`) fire in BEFORE_COMMIT, AFTER_COMMIT, AFTER_COMPLETION phases.
  8. `@TransactionalEventListener`s fire at the appropriate phase.
- **State transitions:** No transaction → active transaction → (commit | rollback) → no transaction; or nested transaction (REQUIRES_NEW / NESTED propagation)
- **Source files:**
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/interceptor/TransactionInterceptor.java`
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/interceptor/AnnotationTransactionAttributeSource.java`
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/support/TransactionSynchronizationManager.java`

#### Bean Creation and Dependency Injection

- **Type:** System/background
- **Trigger:** A bean is requested from the `BeanFactory` (directly or indirectly during context refresh).
- **Steps:**
  1. `DefaultListableBeanFactory` checks singleton registry; if not present, proceeds to create — `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/DefaultListableBeanFactory.java`
  2. `AbstractAutowireCapableBeanFactory.createBean()` resolves the bean class and runs `InstantiationAwareBeanPostProcessor.postProcessBeforeInstantiation()` (may short-circuit creation) — `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/AbstractAutowireCapableBeanFactory.java`
  3. Bean is instantiated (constructor injection, factory method, or Objenesis for CGLIB subclasses)
  4. `MergedBeanDefinitionPostProcessor.postProcessMergedBeanDefinition()` — collects injection metadata
  5. `populateBean()` — property injection (setter/field); `AutowiredAnnotationBeanPostProcessor` resolves `@Autowired`/`@Value` targets
  6. `initializeBean()` — calls `Aware` interfaces, `BeanPostProcessor.postProcessBeforeInitialization()`, `InitializingBean.afterPropertiesSet()`, custom `init-method`, `BeanPostProcessor.postProcessAfterInitialization()` (where AOP proxies are typically created)
  7. Bean placed in singleton cache
- **State transitions:** UNRESOLVED → UNDER_CREATION (circular dependency tracking) → INITIALIZED
- **Source files:**
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/AbstractAutowireCapableBeanFactory.java`
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/annotation/AutowiredAnnotationBeanPostProcessor.java`

#### @Scheduled Task Execution

- **Type:** System/background
- **Trigger:** ApplicationContext refresh completes; `ScheduledAnnotationBeanPostProcessor` detects beans with `@Scheduled` methods and registers them with the `TaskScheduler`.
- **Steps:**
  1. `ScheduledAnnotationBeanPostProcessor` post-processes each bean after initialisation; it discovers all `@Scheduled` annotations (including repeatable `@Schedules`) — `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/annotation/ScheduledAnnotationBeanPostProcessor.java`
  2. For each scheduled method, a `Runnable` (or reactive publisher subscription) is registered with the `TaskScheduler` according to the trigger type (cron, fixed rate, fixed delay, one-shot delay).
  3. At each trigger firing, the scheduled method is invoked on the target bean. Reactive return types are subscribed; Kotlin suspending functions are adapted via coroutine-reactor bridge.
  4. Errors are logged at WARN level and do not prevent further executions.
- **State transitions:** SCHEDULED → EXECUTING → IDLE (repeating); or SCHEDULED → EXECUTING → DONE (one-shot)
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/annotation/ScheduledAnnotationBeanPostProcessor.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/annotation/ScheduledAnnotationReactiveSupport.java`

#### AOT Build-Time Processing

- **Type:** System/background (build-time pipeline, not runtime)
- **Trigger:** `ContextAotProcessor` is executed during the build (typically via a build plugin) to process the application context definition.
- **Steps:**
  1. `ContextAotProcessor` creates a fresh `GenericApplicationContext`, loads the application configuration, and performs a standard `refresh()` — `src/spring-framework/spring-context/src/main/java/org/springframework/context/aot/ContextAotProcessor.java`
  2. `ApplicationContextAotGenerator` invokes all `BeanFactoryInitializationAotProcessor`s (including `BeanRegistrationsAotProcessor`, `RuntimeHintsBeanFactoryInitializationAotProcessor`) — `src/spring-framework/spring-context/src/main/java/org/springframework/context/aot/ApplicationContextAotGenerator.java`
  3. Each bean's `BeanRegistrationAotProcessor` contributes code fragments for instantiation without classpath scanning — `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/aot/BeanRegistrationAotProcessor.java`
  4. `RuntimeHints` are accumulated from all `RuntimeHintsRegistrar`s and `@ImportRuntimeHints` annotations.
  5. Generated source files (Java), resource files, and GraalVM Native Image configuration files are written to the output directory via `GeneratedFiles` / `FileSystemGeneratedFiles`.
- **State transitions:** Source application context definition → generated AOT source code + native-image hints
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/aot/ContextAotProcessor.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/aot/ApplicationContextAotGenerator.java`
  - `src/spring-framework/spring-core/src/main/java/org/springframework/aot/generate/FileSystemGeneratedFiles.java`
  - `src/spring-framework/spring-core/src/main/java/org/springframework/aot/hint/RuntimeHints.java`

#### Retry Workflow (@Retryable)

- **Type:** User-facing (transparent, triggered by method invocation on a `@Retryable`-proxied bean)
- **Trigger:** Invocation of a method annotated with `@Retryable` on a proxied bean.
- **Steps:**
  1. `SimpleRetryInterceptor` intercepts via AOP — `src/spring-framework/spring-context/src/main/java/org/springframework/resilience/retry/SimpleRetryInterceptor.java`
  2. The interceptor invokes the target method.
  3. On success: returns the result immediately.
  4. On exception: the `MethodRetrySpec` (built from `@Retryable` attributes) is consulted. Exception type is matched against `includes`/`excludes` or the custom `predicate`. If matched and `maxRetries` not exhausted, a delay (with optional jitter and multiplier) is applied.
  5. For reactive return types, Reactor's `retryWhen` operator is used.
  6. Steps 2–4 repeat up to `maxRetries` times within the configured `timeout`.
  7. If all retries exhausted, the final exception propagates to the caller.
  8. A `MethodRetryEvent` is published to the `ApplicationEventPublisher` at each retry — `src/spring-framework/spring-context/src/main/java/org/springframework/resilience/retry/MethodRetryEvent.java`
- **State transitions:** INVOKED → (SUCCESS) | (FAILED → RETRYING → … → SUCCESS | FINAL_FAILURE)
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/resilience/retry/SimpleRetryInterceptor.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/resilience/retry/MethodRetrySpec.java`

---

## 5. Business Rules and Validation

| ID | Rule | Description | Criticality | Source |
|----|------|-------------|-------------|--------|
| BR-001 | Required property validation | Before context refresh completes, any properties declared as required via `ConfigurableEnvironment.setRequiredProperties()` must resolve; a `MissingRequiredPropertiesException` is thrown if not. | Core | `src/spring-framework/spring-core/src/main/java/org/springframework/core/env/AbstractEnvironment.java` |
| BR-002 | Singleton bean uniqueness | Within a single `BeanFactory`, a singleton bean name must be unique; duplicate registration throws `BeanDefinitionOverrideException` unless override is explicitly enabled. | Core | `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/DefaultListableBeanFactory.java` |
| BR-003 | No circular dependency in constructor injection | Circular dependencies among singleton beans when all use constructor injection are not resolvable; the container throws `BeanCurrentlyInCreationException`. Setter/field injection allows some circular wiring. | Core | `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/DefaultSingletonBeanRegistry.java` |
| BR-004 | @Transactional on public methods | By default, `@Transactional` applies only to public methods of proxied beans when using JDK or CGLIB proxies; declaring it on package-private or private methods has no effect without AspectJ LTW. | Core | `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/interceptor/TransactionInterceptor.java` |
| BR-005 | Transaction rollback on RuntimeException by default | Unless custom rollback rules are specified, a transaction rolls back on `RuntimeException` or `Error` but not on checked exceptions. | Core | `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/annotation/Transactional.java` |
| BR-006 | @Scheduled methods must take no arguments | Methods annotated with `@Scheduled` must not accept any parameters; the framework throws an exception at startup if any parameters are present. | Core | `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/annotation/ScheduledAnnotationBeanPostProcessor.java` |
| BR-007 | Exactly one scheduling trigger per @Scheduled | Each `@Scheduled` annotation must specify exactly one of `cron`, `fixedDelay`, or `fixedRate`; an `initialDelay` alone is accepted only for one-shot tasks. Multiple triggers on the same annotation are rejected. | Core | `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/annotation/Scheduled.java` |
| BR-008 | @RequestMapping uniqueness | Two handler methods in the same `DispatcherServlet` context must not produce identical request-mapping conditions (method + path + headers + params + media types); ambiguity throws an exception at startup. | Core | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/RequestMappingHandlerMapping.java` |
| BR-009 | Content-Type negotiation for @RequestBody | When a handler method accepts `@RequestBody`, an incoming request must supply a `Content-Type` header whose media type is supported by at least one `HttpMessageConverter`; otherwise a `415 Unsupported Media Type` response is returned. | Core | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/RequestMappingHandlerAdapter.java` |
| BR-010 | SpEL expression sandbox (SimpleEvaluationContext) | When `SimpleEvaluationContext` is used (e.g. in data binding), access to Java types, constructors, and static methods is blocked; only property access and simple operators are allowed. | Supporting | `src/spring-framework/spring-expression/src/main/java/org/springframework/expression/spel/support/SimpleEvaluationContext.java` |
| BR-011 | Bean Validation constraint enforcement | When `MethodValidationPostProcessor` is active and a method parameter or return value violates a Bean Validation constraint, a `ConstraintViolationException` (or `MethodValidationException` for more detailed reporting) is thrown. | Supporting | `src/spring-framework/spring-context/src/main/java/org/springframework/validation/beanvalidation/MethodValidationPostProcessor.java` |
| BR-012 | @Retryable timeout supersedes maxRetries | If a `timeout` is specified on `@Retryable`, retry attempts cease when the total elapsed time (initial invocation plus retries including delays) exceeds the timeout, even if `maxRetries` has not been exhausted. | Supporting | `src/spring-framework/spring-context/src/main/java/org/springframework/resilience/retry/MethodRetrySpec.java` |
| BR-013 | @ConcurrencyLimit rejection policy | When `@ConcurrencyLimit` is configured with `policy = REJECT` and the concurrency limit is reached, further invocations immediately throw `InvocationRejectedException` rather than blocking. | Supporting | `src/spring-framework/spring-context/src/main/java/org/springframework/resilience/annotation/ConcurrencyLimit.java` |
| BR-014 | Lazy singleton initialisation | Beans declared as `@Lazy` at singleton scope are not instantiated at context refresh; they are created on first access. Any circular dependencies or misconfiguration are deferred until first access, potentially causing runtime failures. | Supporting | `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/Lazy.java` |
| BR-015 | AOT mode enforcement | When `spring.aot.enabled=true` or running in a GraalVM native image, the framework must use pre-generated AOT artefacts; it will not fall back to runtime classpath scanning or reflection-based inference. | Core | `src/spring-framework/spring-core/src/main/java/org/springframework/aot/AotDetector.java` |
| BR-016 | CORS pre-flight request handling | Cross-origin requests to endpoints with `@CrossOrigin` or a global CORS configuration will trigger a pre-flight `OPTIONS` response; requests not matching configured origins/methods/headers are rejected with a `403`. | Supporting | `src/spring-framework/spring-web/src/main/java/org/springframework/web/cors/` (package) |
| BR-017 | Flash attribute redirect lifecycle | `FlashMap` attributes are stored in the HTTP session on redirect, retrieved by the `FlashMapManager` on the subsequent request, and then immediately removed from the session to prevent stale data. | Supporting | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/FlashMapManager.java` |
| BR-018 | @Cacheable conditional evaluation | The `condition` and `unless` SpEL expressions on `@Cacheable` are evaluated per invocation; `condition=false` or `unless=true` bypasses the cache entirely for that invocation. | Peripheral | `src/spring-framework/spring-context/src/main/java/org/springframework/cache/annotation/Cacheable.java` |
| BR-019 | Property placeholder resolution order | Property sources are consulted in priority order (system properties → system environment → application-supplied sources); later sources do not override earlier ones. Custom sources can be inserted at any priority via `ConfigurableEnvironment.getPropertySources()`. | Supporting | `src/spring-framework/spring-core/src/main/java/org/springframework/core/env/MutablePropertySources.java` |
| BR-020 | Multi-release JAR compatibility | Classes compiled for Java 21 and Java 24 targets (e.g. Virtual Thread and Sequenced Collection utilities) are packaged under `META-INF/versions/21` and `META-INF/versions/24`; the JVM selects the highest applicable version at runtime. | Peripheral | `src/spring-framework/spring-core/spring-core.gradle` |

---

## 6. Domain Model

Spring Framework does not model a business domain. Its "domain" is the framework's own meta-model: beans, their definitions, their relationships, and the request/response/message processing model. The entities below are the primary programmatic abstractions.

#### BeanDefinition

- **Purpose:** Describes the configuration metadata for a single Spring-managed bean, including its class, scope, constructor arguments, property values, lifecycle callbacks, and dependencies.
- **Source file:** `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/config/BeanDefinition.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| `beanClassName` | `String` | Fully-qualified class name of the bean | `BeanDefinition.java` |
| `scope` | `String` | Scope: `singleton`, `prototype`, `request`, `session`, etc. | `BeanDefinition.java` |
| `lazyInit` | `boolean` | Whether to defer initialisation until first use | `BeanDefinition.java` |
| `dependsOn` | `String[]` | Explicit dependency order declarations | `BeanDefinition.java` |
| `autowireCandidate` | `boolean` | Whether eligible for dependency injection | `BeanDefinition.java` |
| `primary` | `boolean` | Whether preferred when multiple candidates exist | `BeanDefinition.java` |
| `initMethodName` | `String` | Custom initialisation method name | `AbstractBeanDefinition.java` |
| `destroyMethodName` | `String` | Custom destruction method name | `AbstractBeanDefinition.java` |
| `propertyValues` | `MutablePropertyValues` | Property/setter injection values | `AbstractBeanDefinition.java` |
| `constructorArgumentValues` | `ConstructorArgumentValues` | Constructor injection arguments | `AbstractBeanDefinition.java` |

#### ApplicationContext

- **Purpose:** Central interface for a Spring IoC container; provides bean access, resource loading, event publication, and message resolution.
- **Source file:** `src/spring-framework/spring-context/src/main/java/org/springframework/context/ApplicationContext.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| `id` | `String` | Unique identifier of this context instance | `ApplicationContext.java` |
| `applicationName` | `String` | Name of the deployed application | `ApplicationContext.java` |
| `displayName` | `String` | Human-readable context name | `ApplicationContext.java` |
| `parent` | `ApplicationContext` | Parent context (for hierarchical contexts) | `ApplicationContext.java` |
| `environment` | `Environment` | Environment with profiles and property sources | `ConfigurableApplicationContext.java` |
| `startupDate` | `long` | Millisecond timestamp of the last successful refresh | `AbstractApplicationContext.java` |

#### Resource

- **Purpose:** Abstraction for any underlying resource descriptor (file, classpath entry, URL, byte array, input stream).
- **Source file:** `src/spring-framework/spring-core/src/main/java/org/springframework/core/io/Resource.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| `exists` | `boolean` | Whether the resource physically exists | `Resource.java` |
| `readable` | `boolean` | Whether the content can be read | `Resource.java` |
| `open` | `boolean` | Whether the resource is an open stream (read once) | `Resource.java` |
| `file` | `File` | Backing file handle (if filesystem resource) | `Resource.java` |
| `uri` | `URI` | URI handle | `Resource.java` |
| `url` | `URL` | URL handle | `Resource.java` |
| `filename` | `String` | File name portion of the path | `Resource.java` |
| `description` | `String` | Human-readable description for error output | `Resource.java` |

#### Environment

- **Purpose:** Represents the runtime environment of the application, providing profile activation state and unified property resolution.
- **Source file:** `src/spring-framework/spring-core/src/main/java/org/springframework/core/env/Environment.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| `activeProfiles` | `String[]` | Currently active profiles | `Environment.java` |
| `defaultProfiles` | `String[]` | Profiles active when no active profiles are set | `Environment.java` |
| `propertySources` | `MutablePropertySources` | Ordered list of property sources | `AbstractEnvironment.java` |

#### Message (Messaging)

- **Purpose:** Represents a generic messaging payload with headers, used across JMS, WebSocket, RSocket, and internal messaging.
- **Source file:** `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/Message.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| `payload` | `T` | The message body (generic type) | `Message.java` |
| `headers` | `MessageHeaders` | Immutable map of message metadata | `Message.java` |

#### ProblemDetail

- **Purpose:** RFC 9457 HTTP Problem Details object for structured error responses.
- **Source file:** `src/spring-framework/spring-web/src/main/java/org/springframework/http/ProblemDetail.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| `type` | `URI` | A URI identifying the problem type | `ProblemDetail.java` |
| `title` | `String` | Short summary of the problem type | `ProblemDetail.java` |
| `status` | `int` | HTTP status code | `ProblemDetail.java` |
| `detail` | `String` | Human-readable explanation | `ProblemDetail.java` |
| `instance` | `URI` | URI identifying the specific occurrence | `ProblemDetail.java` |
| `properties` | `Map<String,Object>` | Extension properties (serialised as top-level JSON keys) | `ProblemDetail.java` |

#### MethodRetrySpec

- **Purpose:** Immutable record encoding all retry configuration for a single method, derived from `@Retryable` annotation attributes.
- **Source file:** `src/spring-framework/spring-context/src/main/java/org/springframework/resilience/retry/MethodRetrySpec.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| `includes` | `Collection<Class<? extends Throwable>>` | Exception types that trigger a retry | `MethodRetrySpec.java` |
| `excludes` | `Collection<Class<? extends Throwable>>` | Exception types excluded from retry | `MethodRetrySpec.java` |
| `predicate` | `MethodRetryPredicate` | Custom exception filter | `MethodRetrySpec.java` |
| `maxRetries` | `long` | Maximum number of retry attempts | `MethodRetrySpec.java` |
| `timeout` | `Duration` | Maximum elapsed time across all attempts | `MethodRetrySpec.java` |
| `delay` | `Duration` | Base delay between retries | `MethodRetrySpec.java` |
| `jitter` | `Duration` | Random jitter added to the delay | `MethodRetrySpec.java` |
| `multiplier` | `double` | Exponential back-off multiplier | `MethodRetrySpec.java` |
| `maxDelay` | `Duration` | Maximum delay cap | `MethodRetrySpec.java` |

#### Enumerations

| Enum Name | Values | Source |
|-----------|--------|--------|
| `RequestMethod` | `GET`, `HEAD`, `POST`, `PUT`, `PATCH`, `DELETE`, `OPTIONS`, `TRACE` | `src/spring-framework/spring-web/src/main/java/org/springframework/web/bind/annotation/RequestMethod.java` |
| `ScopedProxyMode` | `DEFAULT`, `NO`, `INTERFACES`, `TARGET_CLASS` | `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/ScopedProxyMode.java` |
| `AdviceMode` | `PROXY`, `ASPECTJ` | `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/AdviceMode.java` |
| `TransactionDefinition.Propagation` (static ints) | `REQUIRED`, `SUPPORTS`, `MANDATORY`, `REQUIRES_NEW`, `NOT_SUPPORTED`, `NEVER`, `NESTED` | `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/TransactionDefinition.java` |
| `TransactionDefinition.Isolation` (static ints) | `DEFAULT`, `READ_UNCOMMITTED`, `READ_COMMITTED`, `REPEATABLE_READ`, `SERIALIZABLE` | `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/TransactionDefinition.java` |
| `FilterType` | `ANNOTATION`, `ASSIGNABLE_TYPE`, `ASPECTJ`, `REGEX`, `CUSTOM` | `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/FilterType.java` |
| `SpelCompilerMode` | `OFF`, `IMMEDIATE`, `MIXED` | `src/spring-framework/spring-expression/src/main/java/org/springframework/expression/spel/SpelCompilerMode.java` |
| `SimpMessageType` | `CONNECT`, `CONNECT_ACK`, `MESSAGE`, `SUBSCRIBE`, `UNSUBSCRIBE`, `HEARTBEAT`, `DISCONNECT`, `DISCONNECT_ACK`, `OTHER` | `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/simp/SimpMessageType.java` |
| `HttpStatus` | Standard HTTP status codes 100–511 (e.g. `OK`, `NOT_FOUND`, `INTERNAL_SERVER_ERROR`) | `src/spring-framework/spring-web/src/main/java/org/springframework/http/HttpStatus.java` |
| `HttpMethod` | `GET`, `HEAD`, `POST`, `PUT`, `PATCH`, `DELETE`, `OPTIONS`, `TRACE` | `src/spring-framework/spring-web/src/main/java/org/springframework/http/HttpMethod.java` |
| `MemberCategory` (AOT) | `PUBLIC_FIELDS`, `DECLARED_FIELDS`, `INTROSPECT_PUBLIC_CONSTRUCTORS`, `INVOKE_PUBLIC_CONSTRUCTORS`, etc. | `src/spring-framework/spring-core/src/main/java/org/springframework/aot/hint/MemberCategory.java` |
| `ExecutableMode` (AOT) | `INTROSPECT`, `INVOKE` | `src/spring-framework/spring-core/src/main/java/org/springframework/aot/hint/ExecutableMode.java` |

#### Relationships

| Entity A | Entity B | Relationship Type | Source |
|----------|----------|-------------------|--------|
| `ApplicationContext` | `BeanFactory` | Extends (is-a); `ApplicationContext` extends `HierarchicalBeanFactory` and `ListableBeanFactory` | `ApplicationContext.java` |
| `ApplicationContext` | `Environment` | Composes; context holds and exposes an `Environment` | `ConfigurableApplicationContext.java` |
| `ApplicationContext` | `ApplicationEventMulticaster` | Composes; context delegates event publication to the multicaster | `AbstractApplicationContext.java` |
| `BeanDefinition` | `DefaultListableBeanFactory` | Many-to-one; factory holds a registry of bean definitions | `DefaultListableBeanFactory.java` |
| `ProxyFactory` | `AopProxyFactory` | Delegates to; chooses JDK or CGLIB proxy | `ProxyCreatorSupport.java` |
| `DispatcherServlet` | `HandlerMapping` | One-to-many; servlet holds an ordered list of mappings | `DispatcherServlet.java` |
| `DispatcherServlet` | `HandlerAdapter` | One-to-many; servlet holds adapters matched by handler type | `DispatcherServlet.java` |
| `DispatcherServlet` | `ViewResolver` | One-to-many; resolves logical view names | `DispatcherServlet.java` |
| `JdbcTemplate` | `DataSource` | Composes; obtains JDBC connections | `JdbcTemplate.java` |
| `JpaTransactionManager` | `EntityManagerFactory` | Composes; creates/manages JPA EntityManagers | `JpaTransactionManager.java` |
| `TransactionInterceptor` | `PlatformTransactionManager` | Delegates to; applies transaction management | `TransactionInterceptor.java` |
| `Message` | `MessageHeaders` | Composes; message payload wrapped with headers | `Message.java` |
| `RetryTemplate` | `RetryPolicy` | Delegates to; policy decides retry eligibility | `RetryTemplate.java` |
| `RetryTemplate` | `BackOff` | Delegates to; computes delay between attempts | `RetryTemplate.java` |
| `WebClient` | `ClientHttpConnector` | Composes; underlies actual HTTP transport (Reactor Netty etc.) | `DefaultWebClient.java` |

---

## 7. Integration Points

| Integration | Type | Endpoint / Target | Direction | Source |
|-------------|------|-------------------|-----------|--------|
| JDBC relational database | database | Any `javax.sql.DataSource`-compatible RDBMS (H2, HSQLDB, Derby, Oracle, PostgreSQL, etc.) | bidirectional | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/JdbcTemplate.java` |
| R2DBC reactive relational database | database | Any R2DBC SPI-compliant driver (H2, PostgreSQL, MySQL, etc.) | bidirectional | `src/spring-framework/spring-r2dbc/src/main/java/org/springframework/r2dbc/core/DatabaseClient.java` |
| JPA / Hibernate ORM | database | JPA 3.2 `EntityManagerFactory` (Hibernate, EclipseLink) | bidirectional | `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/LocalContainerEntityManagerFactoryBean.java` |
| JMS messaging | messaging | Any JMS 3.1 `ConnectionFactory` (ActiveMQ Artemis, IBM MQ, etc.) | bidirectional | `src/spring-framework/spring-jms/src/main/java/org/springframework/jms/core/JmsTemplate.java` |
| WebSocket (JSR-356) | messaging | Tomcat / Jetty / Undertow WebSocket endpoint | bidirectional | `src/spring-framework/spring-websocket/src/main/java/org/springframework/web/socket/` (package) |
| STOMP broker relay | messaging | External STOMP broker (e.g. RabbitMQ, ActiveMQ) via TCP | bidirectional | `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/simp/stomp/` (package) |
| RSocket | messaging | RSocket server/client over TCP or WebSocket | bidirectional | `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/rsocket/RSocketRequester.java` |
| HTTP outbound (RestTemplate) | HTTP client | Any HTTP/HTTPS endpoint | outbound | `src/spring-framework/spring-web/src/main/java/org/springframework/web/client/RestTemplate.java` |
| HTTP outbound (RestClient) | HTTP client | Any HTTP/HTTPS endpoint | outbound | `src/spring-framework/spring-web/src/main/java/org/springframework/web/client/RestClient.java` |
| Reactive HTTP outbound (WebClient) | HTTP client | Any HTTP/HTTPS endpoint via Reactor Netty / Jetty / Apache HttpClient 5 | outbound | `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/function/client/WebClient.java` |
| JavaMail / Jakarta Mail | external system | SMTP/IMAP mail server | outbound | `src/spring-framework/spring-context-support/src/main/java/org/springframework/mail/javamail/JavaMailSenderImpl.java` |
| JMX | external system | Local / remote `MBeanServer` (any JMX-compliant agent) | bidirectional | `src/spring-framework/spring-context/src/main/java/org/springframework/jmx/export/MBeanExporter.java` |
| JNDI | external system | JNDI naming service (app server datasource lookup, EJB) | inbound | `src/spring-framework/spring-context/src/main/java/org/springframework/jndi/` (package) |
| Quartz Scheduler | external system | Quartz `Scheduler` (in-process or clustered) | bidirectional | `src/spring-framework/spring-context-support/src/main/java/org/springframework/scheduling/quartz/SchedulerFactoryBean.java` |
| Micrometer Observation | external system | Micrometer `ObservationRegistry` → any metrics/tracing backend | outbound | Used throughout web, JMS, R2DBC modules; e.g. `src/spring-framework/spring-jms/src/main/java/org/springframework/jms/core/JmsTemplate.java` |
| GraalVM Native Image | external system | GraalVM `native-image` tool at build time | outbound | `src/spring-framework/spring-core/src/main/resources/META-INF/native-image/` (directories) |
| Object/XML mapping (JAXB) | file I/O | XML files / HTTP XML payloads | bidirectional | `src/spring-framework/spring-oxm/src/main/java/org/springframework/oxm/jaxb/Jaxb2Marshaller.java` |
| Classpath resource loading | file I/O | Classpath entries, file system paths, JARs | inbound | `src/spring-framework/spring-core/src/main/java/org/springframework/core/io/ClassPathResource.java` |
| HTTP inbound (Servlet) | HTTP client | `DispatcherServlet` exposed via Servlet 6.1 container | inbound | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/DispatcherServlet.java` |
| HTTP inbound (Reactive) | HTTP client | `DispatcherHandler` exposed via Reactor Netty / Servlet async | inbound | `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/DispatcherHandler.java` |

---

## 8. Reports

No report-generation functionality (e.g. PDF, Excel, CSV export from a data source to a user-facing report) is present in this codebase. Spring Framework itself is infrastructure; it does not contain any reporting business logic.

However, the following view-layer integrations are present that consumer applications may use to implement report generation:

| Report | Type | Purpose | Data Sources | Parameters | Output Format | Source |
|--------|------|---------|-------------|------------|---------------|--------|
| OpenPDF view (infrastructure) | View integration | Renders a PDF response from an `AbstractPdfView` subclass | Any model data | Spring MVC model attributes | PDF (`application/pdf`) | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/view/document/` (package) |
| Apache POI Excel view (infrastructure) | View integration | Renders an Excel spreadsheet from an `AbstractXlsView` / `AbstractXlsxView` subclass | Any model data | Spring MVC model attributes | XLS / XLSX | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/view/document/` (package) |
| FreeMarker template view (infrastructure) | View integration | Renders FreeMarker templates to HTML, email, or any text format | Model attributes, template files | Spring MVC model attributes | HTML / text | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/view/freemarker/` (package) |
| XSLT view (infrastructure) | View integration | Applies XSLT transformation to an XML source | `Source` object in model | XSLT stylesheet path | XML / HTML | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/view/xslt/` (package) |
| RSS/Atom feed view (infrastructure) | View integration | Renders RSS 2.0 or Atom 1.0 feeds using the ROME library | Model `Feed` object | Spring MVC model attributes | `application/rss+xml` / `application/atom+xml` | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/view/feed/` (package) |
| JSON view (infrastructure) | View integration | Serialises model to JSON via Jackson | Any model data | Spring MVC model attributes | `application/json` | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/view/json/` (package) |

The above are framework-provided view types only; the actual report content is entirely consumer-supplied. No standalone reporting pipeline or scheduler-driven report generation exists in this codebase.

---

## 9. Cross-Reference: Application to Data Layer

#### 9.1 Data Access Patterns

- **Primary data access approaches:**
  - **JDBC (imperative):** `JdbcTemplate` / `JdbcClient` — the canonical Spring JDBC approach; connection managed via `DataSource` with transaction synchronisation. Named-parameter variant available via `NamedParameterJdbcTemplate`. Source: `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/`
  - **JPA / Hibernate (ORM):** `LocalContainerEntityManagerFactoryBean` bootstraps a JPA persistence unit; `SharedEntityManagerCreator` creates transaction-scoped `EntityManager` proxies. Source: `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/`
  - **R2DBC (reactive JDBC):** `DatabaseClient` — reactive, non-blocking access via R2DBC SPI. Source: `src/spring-framework/spring-r2dbc/src/main/java/org/springframework/r2dbc/core/`
  - **Stored procedures:** `SimpleJdbcCall` and `CallableStatementCreatorFactory` wrap stored procedure invocation. Source: `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/simple/SimpleJdbcCall.java`
  - **Embedded databases:** `EmbeddedDatabaseBuilder` creates in-memory H2, HSQLDB, or Derby databases; primarily for testing. Source: `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/datasource/embedded/`

#### 9.2 Entity-to-Table Mapping

Spring Framework does not define any application-domain entities and therefore does not include entity-to-table mappings. The ORM integration module (`spring-orm`) provides the infrastructure (JPA persistence unit, entity manager lifecycle) that consumer applications use to define their own entity-to-table mappings via JPA annotations (`@Entity`, `@Table`, `@Column`, etc.) or Hibernate-specific mappings.

| Entity / Class | Database Table(s) | Source |
|---------------|-------------------|--------|
| *(No framework-defined entities — this is infrastructure code only)* | N/A | N/A |

Note: The `framework-docs` module contains illustrative sample code (e.g. `CorporateEvent` DAO, `TestItem` stored procedure) used in documentation. These are documentation examples only and are not production entities. Source: `src/spring-framework/framework-docs/src/main/java/org/springframework/docs/dataaccess/`

#### 9.3 Repository / DAO Methods

Spring Framework does not define application-level repositories or DAOs. It provides the following low-level data access templates and utility classes that consumers use to build repositories:

| Repository / DAO | Key Methods | Purpose | Source |
|-----------------|-------------|---------|--------|
| `JdbcTemplate` | `query()`, `queryForObject()`, `queryForList()`, `queryForMap()`, `update()`, `batchUpdate()`, `execute()` | Execute arbitrary SQL against a `DataSource`; handles connection lifecycle and exception translation | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/JdbcTemplate.java` |
| `JdbcClient` | `sql()`, `.query()`, `.update()`, `.param()` (fluent builder chain) | Fluent JDBC API introduced in 6.1 as a modern alternative to `JdbcTemplate` | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/simple/JdbcClient.java` |
| `NamedParameterJdbcTemplate` | `query()`, `queryForObject()`, `update()`, `batchUpdate()` with `SqlParameterSource` or `Map` | Named-parameter SQL execution wrapping `JdbcTemplate` | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/namedparam/NamedParameterJdbcTemplate.java` |
| `SimpleJdbcInsert` | `execute()`, `executeAndReturnKey()`, `executeBatch()` | Simplified insert into a named table, auto-detecting column metadata | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/simple/SimpleJdbcInsert.java` |
| `SimpleJdbcCall` | `execute()`, `executeFunction()`, `executeObject()` | Invokes stored procedures/functions with parameter metadata auto-detection | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/simple/SimpleJdbcCall.java` |
| `DatabaseClient` (R2DBC) | `sql()`, `.bind()`, `.fetch()`, `.rowsUpdated()`, `.one()`, `.all()` (reactive fluent chain) | Reactive SQL access returning `Mono`/`Flux` | `src/spring-framework/spring-r2dbc/src/main/java/org/springframework/r2dbc/core/DatabaseClient.java` |
| `SharedEntityManagerCreator` (JPA) | Produces `EntityManager` proxy with `find()`, `persist()`, `merge()`, `remove()`, `createQuery()`, etc. | Transaction-scoped JPA entity manager proxy bound to the current transaction | `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/SharedEntityManagerCreator.java` |
| `JmsTemplate` | `send()`, `convertAndSend()`, `receive()`, `receiveAndConvert()`, `browse()` | Send/receive JMS messages; handles session and connection lifecycle | `src/spring-framework/spring-jms/src/main/java/org/springframework/jms/core/JmsTemplate.java` |
