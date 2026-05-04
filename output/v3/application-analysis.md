<!-- Input files processed:
- src/spring-framework/build.gradle
- src/spring-framework/settings.gradle
- src/spring-framework/gradle.properties
- src/spring-framework/gradle/spring-module.gradle
- src/spring-framework/gradle/ide.gradle
- src/spring-framework/gradle/publications.gradle
- src/spring-framework/framework-platform/framework-platform.gradle
- src/spring-framework/framework-api/framework-api.gradle
- src/spring-framework/framework-bom/framework-bom.gradle
- src/spring-framework/framework-docs/framework-docs.gradle
- src/spring-framework/integration-tests/integration-tests.gradle
- src/spring-framework/buildSrc/build.gradle
- src/spring-framework/buildSrc/settings.gradle
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
- src/spring-framework/spring-aop/src/main/resources/META-INF/spring.factories
- src/spring-framework/spring-r2dbc/src/main/resources/META-INF/spring.factories
- src/spring-framework/spring-test/src/main/resources/META-INF/spring.factories
- src/spring-framework/spring-core/src/main/java/org/springframework/aot/AotDetector.java
- src/spring-framework/spring-core/src/main/java/org/springframework/core/env/Environment.java
- src/spring-framework/spring-core/src/main/java/org/springframework/core/io/Resource.java
- src/spring-framework/spring-core/src/main/java/org/springframework/core/retry/RetryPolicy.java
- src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/BeanFactory.java
- src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/DefaultListableBeanFactory.java
- src/spring-framework/spring-context/src/main/java/org/springframework/context/ApplicationContext.java
- src/spring-framework/spring-context/src/main/java/org/springframework/context/ApplicationEvent.java
- src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/Configuration.java
- src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/ComponentScan.java
- src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/EnableAspectJAutoProxy.java
- src/spring-framework/spring-context/src/main/java/org/springframework/context/support/AbstractApplicationContext.java
- src/spring-framework/spring-context/src/main/java/org/springframework/cache/annotation/EnableCaching.java
- src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/annotation/EnableScheduling.java
- src/spring-framework/spring-context/src/main/java/org/springframework/validation/Validator.java
- src/spring-framework/spring-context-indexer/src/main/java/org/springframework/context/index/processor/CandidateComponentsIndexer.java
- src/spring-framework/spring-aop/src/main/java/org/springframework/aop/Advisor.java
- src/spring-framework/spring-expression/src/main/java/org/springframework/expression/ExpressionParser.java
- src/spring-framework/spring-instrument/src/main/java/org/springframework/instrument/InstrumentationSavingAgent.java
- src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/PlatformTransactionManager.java
- src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/annotation/EnableTransactionManagement.java
- src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/JdbcTemplate.java
- src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/LocalContainerEntityManagerFactoryBean.java
- src/spring-framework/spring-r2dbc/src/main/java/org/springframework/r2dbc/core/DatabaseClient.java
- src/spring-framework/spring-jms/src/main/java/org/springframework/jms/core/JmsTemplate.java
- src/spring-framework/spring-oxm/src/main/java/org/springframework/oxm/Marshaller.java
- src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/Message.java
- src/spring-framework/spring-web/src/main/java/org/springframework/web/bind/annotation/RestController.java
- src/spring-framework/spring-web/src/main/java/org/springframework/web/client/RestClient.java
- src/spring-framework/spring-web/src/main/java/org/springframework/web/service/invoker/HttpServiceProxyFactory.java
- src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/DispatcherServlet.java
- src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/RequestMappingHandlerMapping.java
- src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/view/InternalResourceViewResolver.java
- src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/DispatcherHandler.java
- src/spring-framework/spring-websocket/src/main/java/org/springframework/web/socket/WebSocketSession.java
- src/spring-framework/spring-context-support/src/main/java/org/springframework/scheduling/quartz/SchedulerFactoryBean.java
-->

# Application Analysis: Spring Framework

> **Important notice for downstream PRD generation:** The codebase under `src/spring-framework/` is the **Spring Framework itself** — the open-source, general-purpose Java application framework authored and published by the Spring team at Broadcom (formerly Pivotal/VMware). It is version **7.1.0-SNAPSHOT** and is released under the Apache Licence 2.0. It is **not** a bespoke Defra application. It is a framework library that Defra applications are typically *built upon*. This analysis documents the framework exhaustively as required; downstream PRD authors should treat these capabilities as the platform affordances available to any application that depends on this framework, rather than as business logic specific to a Defra service.

---

## 1. Application Overview

- **Purpose:** Spring Framework is a comprehensive, general-purpose Java application framework and inversion-of-control (IoC) container that provides infrastructure support for building enterprise Java applications across imperative (servlet-based) and reactive programming models.
- **Technology stack:** Java (primary), Kotlin (secondary, optional), Groovy (optional scripting); targets Jakarta EE 11 APIs; built with Gradle 8.x; reactive stack uses Project Reactor.
- **Framework version:** Spring Framework **7.1.0-SNAPSHOT**; Java 17 minimum (multi-release JAR includes Java 21 and Java 24 variant classes); Jakarta EE 11 (`jakarta.*` namespaces throughout). Source: `src/spring-framework/gradle.properties`
- **Module structure:**
  - **`spring-core`** — foundational utilities: resource abstraction, type conversion, reflection utilities, AOT code-generation infrastructure, GraalVM native-image hints, retry policy, ASM bytecode library (repackaged), Objenesis (repackaged), JavaPoet (repackaged). Source: `src/spring-framework/spring-core/spring-core.gradle`
  - **`spring-beans`** — IoC bean definition model, `BeanFactory`, property editors, `BeanWrapper`, annotation-driven injection (`@Autowired`, `@Value`, `@Qualifier`), AOT bean-registration code generation. Source: `src/spring-framework/spring-beans/spring-beans.gradle`
  - **`spring-context`** — `ApplicationContext`, component scanning (`@ComponentScan`), `@Configuration` / `@Bean`, event publishing, scheduling (`@Scheduled`, `@EnableScheduling`), caching (`@Cacheable`, `@EnableCaching`), validation, i18n, JMX export, EL integration, environment/profiles, SpEL integration, load-time weaving. Source: `src/spring-framework/spring-context/spring-context.gradle`
  - **`spring-context-support`** — integration with third-party libraries: Caffeine cache, JSR-107 JCache, FreeMarker, Quartz scheduler, Jakarta Mail. Source: `src/spring-framework/spring-context-support/spring-context-support.gradle`
  - **`spring-context-indexer`** — compile-time annotation processor that produces a `spring.components` index for faster component-scan startup (deprecated as of 6.1 in favour of the AOT engine). Source: `src/spring-framework/spring-context-indexer/spring-context-indexer.gradle`
  - **`spring-aop`** — Aspect-Oriented Programming framework: `Advisor`, `Pointcut`, `ProxyFactory`, AspectJ integration (`@Aspect`, `@EnableAspectJAutoProxy`), JDK dynamic proxy and CGLIB proxy support, pooling/async target sources. Source: `src/spring-framework/spring-aop/spring-aop.gradle`
  - **`spring-aspects`** — compiled-weave AspectJ aspects for `@Configurable` domain objects, `@Transactional` (LTW), `@Async`, JCache, Jakarta Mail. Source: `src/spring-framework/spring-aspects/spring-aspects.gradle`
  - **`spring-expression`** — Spring Expression Language (SpEL): `ExpressionParser`, `Expression`, `EvaluationContext`. Source: `src/spring-framework/spring-expression/spring-expression.gradle`
  - **`spring-instrument`** — Java agent (`InstrumentationSavingAgent`) for class-level instrumentation and load-time weaving; exposes `java.lang.instrument.Instrumentation`. Source: `src/spring-framework/spring-instrument/spring-instrument.gradle`
  - **`spring-tx`** — transaction abstraction: `PlatformTransactionManager`, `ReactiveTransactionManager`, `@Transactional`, `TransactionTemplate`, JTA support, reactive transaction synchronisation. Source: `src/spring-framework/spring-tx/spring-tx.gradle`
  - **`spring-jdbc`** — JDBC abstraction: `JdbcTemplate`, `JdbcClient` (fluent API, since 6.1), `NamedParameterJdbcTemplate`, `SimpleJdbcInsert`, `SimpleJdbcCall`, embedded database support (H2, HSQL, Derby), `RowMapper`, `ResultSetExtractor`, SQL exception translation. Source: `src/spring-framework/spring-jdbc/spring-jdbc.gradle`
  - **`spring-orm`** — ORM integration: Hibernate 7.x, EclipseLink JPA 5.x, `LocalContainerEntityManagerFactoryBean`, `JpaTransactionManager`, open-session-in-view patterns. Source: `src/spring-framework/spring-orm/spring-orm.gradle`
  - **`spring-oxm`** — Object/XML mapping: `Marshaller`/`Unmarshaller` abstraction, JAXB 3.x, XStream integration. Source: `src/spring-framework/spring-oxm/spring-oxm.gradle`
  - **`spring-r2dbc`** — Reactive relational database client: `DatabaseClient`, `R2dbcTransactionManager`, named-parameter binding, R2DBC SPI abstraction. Source: `src/spring-framework/spring-r2dbc/spring-r2dbc.gradle`
  - **`spring-jms`** — JMS integration: `JmsTemplate`, `JmsClient` (fluent API), `DefaultMessageListenerContainer`, `@JmsListener`, Micrometer instrumentation. Source: `src/spring-framework/spring-jms/spring-jms.gradle`
  - **`spring-messaging`** — messaging abstraction: `Message<T>`, `MessageHeaders`, `MessageChannel`, STOMP protocol, RSocket support, SockJS fallback protocol. Source: `src/spring-framework/spring-messaging/spring-messaging.gradle`
  - **`spring-web`** — core web support: HTTP abstractions (`HttpMethod`, `HttpStatus`, `MediaType`, `HttpHeaders`), `RestTemplate`, `RestClient` (fluent, since 6.1), `WebClient` (reactive), `HttpServiceProxyFactory` (declarative HTTP clients via `@HttpExchange`), multipart, CORS, `HttpMessageConverter` framework, `ClientHttpRequestFactory` abstraction. Source: `src/spring-framework/spring-web/spring-web.gradle`
  - **`spring-webmvc`** — Servlet-based MVC: `DispatcherServlet`, `@RequestMapping`, `@RestController`, `@ControllerAdvice`, `HandlerMapping`, `HandlerAdapter`, `ViewResolver`, content negotiation, FreeMarker views, JSP/JSTL views, PDF (OpenPDF), RSS/Atom (ROME), Excel (Apache POI), Groovy template views. Source: `src/spring-framework/spring-webmvc/spring-webmvc.gradle`
  - **`spring-webflux`** — Reactive web: `DispatcherHandler`, `RouterFunction` / `HandlerFunction`, `@RequestMapping` on reactive controllers, `WebClient`, Reactor Netty integration, WebSocket over Reactor, server-sent events. Source: `src/spring-framework/spring-webflux/spring-webflux.gradle`
  - **`spring-websocket`** — WebSocket support: `WebSocketSession`, `WebSocketHandler`, SockJS fallback, STOMP sub-protocol broker, `@MessageMapping`, Jetty/Tomcat/standard WebSocket adapters. Source: `src/spring-framework/spring-websocket/spring-websocket.gradle`
  - **`spring-test`** — testing support: Spring TestContext Framework, `MockMvc` (servlet MVC testing), `WebTestClient` (reactive testing), `MockMvcTester` (AssertJ-based), bean override (`@MockitoBean`, `@MockitoSpyBean`, `@TestBean`), `@Sql`, transaction test support, `@DirtiesContext`. Source: `src/spring-framework/spring-test/spring-test.gradle`
  - **`spring-core-test`** — internal test utilities for runtime hints verification; includes `RuntimeHintsAgent` (Java agent for hint recording during test execution). Source: `src/spring-framework/spring-core-test/spring-core-test.gradle`
  - **`framework-api`** — aggregate API module (no production code; groups published API artefacts). Source: `src/spring-framework/framework-api/framework-api.gradle`
  - **`framework-bom`** — Bill of Materials POM for consumer dependency version alignment. Source: `src/spring-framework/framework-bom/framework-bom.gradle`
  - **`framework-platform`** — internal Gradle platform module that governs all third-party dependency versions used across the framework build. Source: `src/spring-framework/framework-platform/framework-platform.gradle`
  - **`framework-docs`** — documentation module containing compiled Java code examples used in the reference manual. Source: `src/spring-framework/framework-docs/framework-docs.gradle`
  - **`integration-tests`** — cross-module integration test suite. Source: `src/spring-framework/integration-tests/integration-tests.gradle`

- **External dependencies** (selected from `src/spring-framework/framework-platform/framework-platform.gradle`):
  - `commons-logging:commons-logging:1.3.5` — logging facade (mandatory runtime dependency)
  - `org.jspecify:jspecify:1.0.0` — null-safety annotations (`@Nullable`, `@NonNull`)
  - `io.projectreactor:reactor-bom:2025.0.5` (Reactor Core, Reactor Netty, Reactor Test)
  - `io.micrometer:micrometer-bom:1.16.5` — observability metrics and tracing API
  - `io.netty:netty-bom:4.2.12.Final` — non-blocking I/O for WebFlux / Reactor Netty
  - `com.fasterxml.jackson:jackson-bom:2.21.2` — JSON/XML/YAML/binary serialisation (Jackson 2.x)
  - `tools.jackson:jackson-bom:3.1.1` — Jackson 3.x (next-generation, parallel support)
  - `org.aspectj:aspectjweaver:1.9.25` — AspectJ weaver (optional)
  - `org.hibernate.orm:hibernate-core:7.3.2.Final` — ORM persistence provider (optional)
  - `org.hibernate.validator:hibernate-validator:9.1.0.Final` — Bean Validation provider (optional)
  - `io.r2dbc:r2dbc-spi:1.0.0.RELEASE` — Reactive Relational Database Connectivity SPI
  - `org.quartz-scheduler:quartz:2.3.2` — job scheduling (optional)
  - `org.freemarker:freemarker:2.3.34` — FreeMarker template engine (optional)
  - `org.apache.poi:poi-ooxml:5.5.1` — Excel view support (optional)
  - `com.github.librepdf:openpdf:1.3.43` — PDF view support (optional)
  - `com.rometools:rome:1.19.0` — RSS/Atom feed support (optional)
  - `org.apache.activemq:artemis-jakarta-client:2.42.0` — JMS broker client (test/optional)
  - `io.rsocket:rsocket-bom:1.1.5` — RSocket protocol support (optional)
  - `com.github.ben-manes.caffeine:caffeine:3.2.3` — in-memory cache (optional)
  - `jakarta.servlet:jakarta.servlet-api:6.1.0` — Servlet 6.1 API
  - `jakarta.websocket:jakarta.websocket-api:2.2.0` — WebSocket 2.2 API
  - `jakarta.persistence:jakarta.persistence-api:3.2.0` — JPA 3.2
  - `jakarta.jms:jakarta.jms-api:3.1.0` — JMS 3.1
  - `jakarta.validation:jakarta.validation-api:3.1.0` — Bean Validation 3.1
  - `jakarta.transaction:jakarta.transaction-api:2.0.1` — JTA 2.0
  - `org.eclipse.jetty:jetty-bom:12.1.7` — Jetty 12.1 (embedded server, optional)
  - `org.apache.tomcat.embed:tomcat-embed-core:11.0.20` — Tomcat 11 (embedded, optional)
  - `org.jetbrains.kotlin:kotlin-reflect` / `kotlin-stdlib` (Kotlin 2.3.20) — Kotlin support (optional)
  - `org.jetbrains.kotlinx:kotlinx-coroutines-bom:1.10.2` — Kotlin coroutines (optional)
  - `org.jetbrains.kotlinx:kotlinx-serialization-bom:1.11.0` — Kotlin serialisation (optional)
  - `io.vavr:vavr:0.11.0` — functional programming types for transaction return-value handling (optional)
  - `org.crac:crac:1.4.0` — CRaC (Coordinated Restore at Checkpoint) lifecycle (optional)
  - `io.smallrye.reactive:mutiny:1.10.0` — Mutiny reactive types adaptor (optional)
  - `io.reactivex.rxjava3:rxjava:3.1.12` — RxJava 3 adaptor (optional)
  - `org.eclipse.persistence:org.eclipse.persistence.jpa:5.0.0` — EclipseLink JPA (optional)

- **Configuration summary:**
  - No runtime `application.properties` or `application.yml` exists — this is a library, not a self-contained application. Configuration is supplied entirely by downstream consumer applications.
  - `gradle.properties` sets: `version=7.1.0-SNAPSHOT`, `kotlinVersion=2.3.20`, `byteBuddyVersion=1.17.6`, JVM max heap 2 GB, parallel Gradle build enabled, Gradle build caching enabled. Source: `src/spring-framework/gradle.properties`
  - `spring-core` ships a `SpringProperties` mechanism allowing consumers to configure framework flags (e.g., `spring.aot.enabled`) via JVM system properties or a `spring.properties` file on the classpath. Source: `src/spring-framework/spring-core/src/main/java/org/springframework/core/SpringProperties.java`
  - AOT mode is activated by the `spring.aot.enabled` system property or automatically inside a GraalVM native image. Source: `src/spring-framework/spring-core/src/main/java/org/springframework/aot/AotDetector.java`
  - The `spring-test` module registers default `TestExecutionListener` implementations via `META-INF/spring.factories`, including listeners for dependency injection, transaction management, JDBC SQL scripts, dirty-context, Micrometer observation registry, and Mockito bean override. Source: `src/spring-framework/spring-test/src/main/resources/META-INF/spring.factories`
  - The `spring-aop` module registers `ScopedProxyBeanRegistrationContributionProvider` via `META-INF/spring.factories` for AOT scoped-proxy code generation. Source: `src/spring-framework/spring-aop/src/main/resources/META-INF/spring.factories`
  - The `spring-r2dbc` module registers `BuiltInBindMarkersFactoryProvider` via `META-INF/spring.factories` for R2DBC bind-marker dialect resolution. Source: `src/spring-framework/spring-r2dbc/src/main/resources/META-INF/spring.factories`
  - The multi-release JAR in `spring-core` provides Java 21 virtual-thread-aware classes and Java 24 classes via the `org.springframework.build.multiReleaseJar` Gradle plugin. Source: `src/spring-framework/spring-core/spring-core.gradle`
  - The `spring-instrument` JAR manifest declares `Premain-Class` and `Agent-Class` as `InstrumentationSavingAgent`, enabling use as a Java agent. Source: `src/spring-framework/spring-instrument/spring-instrument.gradle`

---

## 2. User Roles and Access Control

| Role | Permissions / Access | Source |
|------|---------------------|--------|
| N/A — framework library | Spring Framework does not define application-level user roles; it provides the infrastructure (AOP integration points, `Principal` access in web layers) that downstream applications use to implement their own role and permission models. | — |

- **Authentication mechanism:** Not implemented at framework level. Spring Framework exposes hooks — `java.security.Principal` is accessible via `WebSocketSession.getPrincipal()` (`src/spring-framework/spring-websocket/src/main/java/org/springframework/web/socket/WebSocketSession.java`) and via `HttpServletRequest` in the MVC layer — but authentication is the responsibility of Spring Security (a separate project) or the servlet container.
- **Authorisation approach:** Not implemented at framework level. Method-level and URL-level authorisation is the concern of Spring Security, which integrates with Spring Framework's AOP infrastructure. The framework itself exposes AOP pointcut and advice mechanisms that Spring Security uses internally.

> **Note for LAP analysts:** If a Defra application built on this framework is under analysis, security configuration will reside in that application's own source tree, not in this framework codebase.

---

## 3. Features and Capabilities

#### Inversion of Control / Dependency Injection Container

- **Description:** Central IoC container managing the full lifecycle of application beans. Supports constructor injection, setter injection, and field injection. Bean definitions may be declared in XML, via annotations (`@Component`, `@Service`, `@Repository`, `@Controller`), or via Java `@Configuration` classes with `@Bean` methods. The container resolves dependencies, applies scope (singleton, prototype, request, session, application, websocket), and fires lifecycle callbacks (`@PostConstruct`, `@PreDestroy`, `InitializingBean`, `DisposableBean`). `DefaultListableBeanFactory` is the primary concrete implementation.
- **Key classes/interfaces:** `BeanFactory`, `ApplicationContext`, `DefaultListableBeanFactory`, `AnnotationConfigApplicationContext`, `AbstractApplicationContext`, `BeanDefinition`, `@Bean`, `@Configuration`, `@ComponentScan`, `@Autowired`, `@Value`, `@Qualifier`, `@Lazy`
- **Source files:**
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/BeanFactory.java`
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/DefaultListableBeanFactory.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/ApplicationContext.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/support/AbstractApplicationContext.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/Configuration.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/ComponentScan.java`
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/annotation/AutowiredAnnotationBeanPostProcessor.java`

#### Aspect-Oriented Programming (AOP)

- **Description:** Declarative cross-cutting concerns (logging, security, transactions, caching, retry) via AspectJ-style `@Aspect` classes and programmatic `ProxyFactory` / `Advisor` APIs. Supports JDK dynamic proxies (for interface-based targets) and CGLIB subclass proxies (for concrete classes). `@EnableAspectJAutoProxy` activates auto-detection of `@Aspect` beans. AspectJ load-time weaving is available via `spring-instrument` agent. The `spring-aspects` module provides pre-compiled AspectJ aspects for domain-object dependency injection (`@Configurable`) and other cross-cutting concerns.
- **Key classes/interfaces:** `Advisor`, `Pointcut`, `Advice`, `ProxyFactory`, `AopProxy`, `AspectJExpressionPointcut`, `AnnotationAwareAspectJAutoProxyCreator`, `@Aspect`, `@Before`, `@After`, `@Around`, `@AfterReturning`, `@AfterThrowing`
- **Source files:**
  - `src/spring-framework/spring-aop/src/main/java/org/springframework/aop/Advisor.java`
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/EnableAspectJAutoProxy.java`
  - `src/spring-framework/spring-aop/src/main/java/org/springframework/aop/framework/ProxyFactory.java`

#### Spring Expression Language (SpEL)

- **Description:** Powerful expression language for querying and manipulating an object graph at runtime. Used internally by the framework in `@Value` property injection, cache key expressions (`@Cacheable(key="...")`), `@PreAuthorize` (Spring Security), and `@Scheduled(cron="...")`. Supports literals, property access, method invocation, arithmetic, relational, and logical operators, regular expressions, collection projections, template expressions, and operator overloading (Kotlin).
- **Key classes/interfaces:** `ExpressionParser`, `Expression`, `EvaluationContext`, `StandardEvaluationContext`, `SpelExpressionParser`
- **Source files:**
  - `src/spring-framework/spring-expression/src/main/java/org/springframework/expression/ExpressionParser.java`

#### Environment Abstraction and Profiles

- **Description:** `Environment` models the runtime environment as a set of named profiles and a hierarchy of property sources. Profiles allow conditional bean registration (`@Profile`). Properties are resolved from multiple sources (system properties, OS environment variables, `application.properties`, JNDI, servlet context parameters, etc.) with a configurable priority order.
- **Key classes/interfaces:** `Environment`, `ConfigurableEnvironment`, `PropertySource`, `PropertySources`, `@Profile`, `@PropertySource`, `StandardEnvironment`
- **Source files:**
  - `src/spring-framework/spring-core/src/main/java/org/springframework/core/env/Environment.java`

#### Resource Abstraction

- **Description:** Unified `Resource` interface abstracts access to any addressable resource regardless of underlying storage (classpath, filesystem, URL, byte array, etc.). `ResourceLoader` resolves resource strings. `PathMatchingResourcePatternResolver` supports Ant-style glob patterns for multi-resource loading.
- **Key classes/interfaces:** `Resource`, `ResourceLoader`, `ResourcePatternResolver`, `ClassPathResource`, `FileSystemResource`, `UrlResource`, `PathMatchingResourcePatternResolver`
- **Source files:**
  - `src/spring-framework/spring-core/src/main/java/org/springframework/core/io/Resource.java`

#### Event Publishing

- **Description:** Application-level publish/subscribe event model. `ApplicationEventPublisher` (implemented by `ApplicationContext`) broadcasts `ApplicationEvent` subclasses to `ApplicationListener` beans or `@EventListener`-annotated methods. Supports synchronous and asynchronous (`@Async`) event delivery, transactional event listeners (`@TransactionalEventListener`), and arbitrary payload events (any POJO can be published since Spring 4.2).
- **Key classes/interfaces:** `ApplicationEvent`, `ApplicationEventPublisher`, `ApplicationListener<E>`, `@EventListener`, `@TransactionalEventListener`
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/ApplicationEvent.java`

#### Transaction Management

- **Description:** Portable transaction abstraction across JDBC, JPA, JTA, R2DBC, and JMS. `PlatformTransactionManager` is the imperative entry point; `ReactiveTransactionManager` serves reactive stacks. `@Transactional` enables declarative demarcation via AOP. Supports propagation (REQUIRED, REQUIRES_NEW, SUPPORTS, NOT_SUPPORTED, MANDATORY, NEVER, NESTED), isolation levels, read-only optimisation, and rollback rules. `TransactionTemplate` provides programmatic control. `@EnableTransactionManagement` activates processing.
- **Key classes/interfaces:** `PlatformTransactionManager`, `ReactiveTransactionManager`, `TransactionDefinition`, `TransactionStatus`, `@Transactional`, `TransactionTemplate`, `JtaTransactionManager`, `@EnableTransactionManagement`
- **Source files:**
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/PlatformTransactionManager.java`
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/annotation/EnableTransactionManagement.java`

#### JDBC Data Access

- **Description:** Template-method-based JDBC access that eliminates boilerplate connection handling, exception translation, and resource cleanup. `JdbcTemplate` is the central delegate. `JdbcClient` (since 6.1) provides a fluent modern API. `NamedParameterJdbcTemplate` adds named-parameter support. `SimpleJdbcInsert` and `SimpleJdbcCall` simplify INSERT and stored-procedure invocations. The `SQLExceptionTranslator` converts vendor-specific `SQLException` codes to Spring's technology-agnostic `DataAccessException` hierarchy.
- **Key classes/interfaces:** `JdbcTemplate`, `JdbcClient`, `NamedParameterJdbcTemplate`, `RowMapper`, `ResultSetExtractor`, `PreparedStatementCreator`, `DataAccessException`, `SQLExceptionTranslator`, `SimpleJdbcInsert`, `SimpleJdbcCall`, `EmbeddedDatabaseBuilder`
- **Source files:**
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/JdbcTemplate.java`
  - `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/simple/JdbcClient.java`

#### ORM / JPA Integration

- **Description:** Integration layer over JPA 3.2 and Hibernate 7.x. `LocalContainerEntityManagerFactoryBean` bootstraps a container-managed `EntityManagerFactory` within the Spring `ApplicationContext`. `JpaTransactionManager` integrates JPA transactions with Spring's transaction abstraction. `SharedEntityManagerCreator` produces thread-safe `EntityManager` proxies. EclipseLink JPA 5.x is also supported. Open-session-in-view filter and interceptor patterns are provided for web tiers.
- **Key classes/interfaces:** `LocalContainerEntityManagerFactoryBean`, `LocalEntityManagerFactoryBean`, `JpaTransactionManager`, `SharedEntityManagerCreator`, `JpaVendorAdapter`, `HibernateJpaVendorAdapter`, `EclipseLinkJpaVendorAdapter`
- **Source files:**
  - `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/LocalContainerEntityManagerFactoryBean.java`

#### Reactive Database Access (R2DBC)

- **Description:** Non-blocking reactive database access using the R2DBC SPI. `DatabaseClient` provides a fluent, reactive API over any R2DBC-compatible driver. `R2dbcTransactionManager` integrates with `ReactiveTransactionManager`. Named parameters, bind-marker dialect resolution (via `spring.factories`), and row-mapping are supported.
- **Key classes/interfaces:** `DatabaseClient`, `R2dbcTransactionManager`, `BindMarkersFactory`, `RowsFetchSpec`, `GenericExecuteSpec`
- **Source files:**
  - `src/spring-framework/spring-r2dbc/src/main/java/org/springframework/r2dbc/core/DatabaseClient.java`

#### JMS Messaging

- **Description:** Simplifies synchronous and asynchronous JMS 3.1 interactions. `JmsTemplate` handles synchronous send/receive. `JmsClient` (since 6.1) provides a fluent API. `DefaultMessageListenerContainer` drives asynchronous message consumption with configurable concurrency and transaction participation. `@JmsListener` enables annotation-driven listener registration. Micrometer instrumentation for JMS publish and process operations is integrated.
- **Key classes/interfaces:** `JmsTemplate`, `JmsClient`, `DefaultMessageListenerContainer`, `MessageListenerAdapter`, `@JmsListener`, `@EnableJms`, `MessageConverter`, `SimpleMessageConverter`
- **Source files:**
  - `src/spring-framework/spring-jms/src/main/java/org/springframework/jms/core/JmsTemplate.java`

#### Object/XML Marshalling (OXM)

- **Description:** Technology-agnostic `Marshaller` / `Unmarshaller` abstraction for XML serialisation. Implementations provided for JAXB 3.x and XStream. Used internally by Spring Web's XML `HttpMessageConverter`.
- **Key classes/interfaces:** `Marshaller`, `Unmarshaller`, `Jaxb2Marshaller`, `XStreamMarshaller`
- **Source files:**
  - `src/spring-framework/spring-oxm/src/main/java/org/springframework/oxm/Marshaller.java`

#### Servlet MVC (Spring Web MVC)

- **Description:** Full-featured, annotation-driven MVC framework for servlet-based web applications. `DispatcherServlet` is the front-controller that delegates to `HandlerMapping` (route resolution), `HandlerAdapter` (controller invocation), `HandlerExceptionResolver` (error handling), and `ViewResolver` (view selection). Controller methods are declared with `@RequestMapping` and its specialisations. Content negotiation supports JSON (Jackson 2 and 3), XML (JAXB/Jackson-XML), YAML, Protobuf, form data, and multipart. View technologies include JSP/JSTL, FreeMarker, Groovy templates, PDF, Excel, RSS/Atom, and XSLT. API versioning is supported via `DefaultApiVersionStrategy`.
- **Key classes/interfaces:** `DispatcherServlet`, `@Controller`, `@RestController`, `@RequestMapping`, `@ControllerAdvice`, `@ExceptionHandler`, `RequestMappingHandlerMapping`, `RequestMappingHandlerAdapter`, `HandlerInterceptor`, `ViewResolver`, `InternalResourceViewResolver`, `ModelAndView`, `RedirectAttributes`
- **Source files:**
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/DispatcherServlet.java`
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/RequestMappingHandlerMapping.java`
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/view/InternalResourceViewResolver.java`

#### Reactive Web (Spring WebFlux)

- **Description:** Reactive, non-blocking web framework built on Project Reactor. `DispatcherHandler` is the reactive counterpart of `DispatcherServlet`. Supports annotation-based (same `@RequestMapping` family, returning `Mono<T>` / `Flux<T>`) and functional (router functions `RouterFunction<ServerResponse>`) programming models. Runs on Reactor Netty (default), Tomcat, Jetty, or Undertow via reactive adapters. Server-Sent Events and streaming are natively supported.
- **Key classes/interfaces:** `DispatcherHandler`, `RouterFunction`, `HandlerFunction`, `ServerRequest`, `ServerResponse`, `@EnableWebFlux`, `WebHttpHandlerBuilder`, `ServerWebExchange`
- **Source files:**
  - `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/DispatcherHandler.java`

#### HTTP Client Abstractions

- **Description:** Multiple levels of HTTP client abstraction. `RestTemplate` is the classic synchronous template. `RestClient` (since 6.1) provides a fluent, synchronous API over pluggable `ClientHttpRequestFactory` implementations (JDK `HttpClient`, Apache HttpComponents 5, Jetty). `WebClient` provides a reactive, non-blocking client. `HttpServiceProxyFactory` generates type-safe client proxies from interfaces annotated with `@HttpExchange`, supporting both `RestClient` and `WebClient` adapters.
- **Key classes/interfaces:** `RestTemplate`, `RestClient`, `WebClient`, `HttpServiceProxyFactory`, `@HttpExchange`, `ClientHttpRequestFactory`, `HttpMessageConverter`
- **Source files:**
  - `src/spring-framework/spring-web/src/main/java/org/springframework/web/client/RestClient.java`
  - `src/spring-framework/spring-web/src/main/java/org/springframework/web/service/invoker/HttpServiceProxyFactory.java`

#### WebSocket and STOMP Messaging

- **Description:** Full WebSocket support for both servlet-based and reactive stacks. `WebSocketSession` abstracts individual connections. SockJS fallback is provided for environments where WebSocket is unavailable. STOMP sub-protocol support enables message-broker integration with `@MessageMapping`, `@SendTo`, and `@SubscribeMapping` controller methods. Supports simple in-memory broker and external brokers (ActiveMQ, RabbitMQ) via relay. Jetty, Tomcat, and standard (JSR-356) WebSocket containers are supported.
- **Key classes/interfaces:** `WebSocketSession`, `WebSocketHandler`, `SockJsClient`, `StompBrokerRelayMessageHandler`, `@MessageMapping`, `@EnableWebSocketMessageBroker`
- **Source files:**
  - `src/spring-framework/spring-websocket/src/main/java/org/springframework/web/socket/WebSocketSession.java`

#### Caching Abstraction

- **Description:** Technology-agnostic caching API with annotation-driven method caching via `@Cacheable`, `@CachePut`, `@CacheEvict`, and `@Caching`. `CacheManager` is the SPI; implementations include `ConcurrentMapCacheManager` (in-memory), `CaffeineCacheManager`, `JCacheCacheManager` (JSR-107), and `TransactionAwareCacheManagerProxy`. `@EnableCaching` activates the infrastructure via AOP.
- **Key classes/interfaces:** `CacheManager`, `Cache`, `@Cacheable`, `@CachePut`, `@CacheEvict`, `@EnableCaching`, `CaffeineCacheManager`, `JCacheCacheManager`
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/cache/annotation/EnableCaching.java`

#### Task Scheduling and Asynchronous Execution

- **Description:** Annotation-driven scheduled task execution (`@Scheduled`, `@EnableScheduling`) with cron, fixed-rate, and fixed-delay triggers. Compatible with virtual threads on JDK 21+. `@Async` delegates method calls to a configured `Executor`. Quartz integration (`SchedulerFactoryBean`) provides enterprise-grade job scheduling with JDBC persistence. `TaskExecutor` / `TaskScheduler` SPI abstracts thread pool management.
- **Key classes/interfaces:** `@Scheduled`, `@EnableScheduling`, `@Async`, `@EnableAsync`, `TaskExecutor`, `TaskScheduler`, `ScheduledTaskRegistrar`, `SchedulerFactoryBean`, `ThreadPoolTaskExecutor`, `ThreadPoolTaskScheduler`
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/annotation/EnableScheduling.java`
  - `src/spring-framework/spring-context-support/src/main/java/org/springframework/scheduling/quartz/SchedulerFactoryBean.java`

#### Validation

- **Description:** Application-layer `Validator` SPI decoupled from any tier. `SmartValidator` adds group-based validation. `DataBinder` combines property binding and validation. Deep integration with Jakarta Bean Validation 3.1 (`@Valid`, `@Validated`, method-level validation via `MethodValidationInterceptor`). Spring MVC and WebFlux automatically apply validation to `@RequestBody`, `@ModelAttribute`, and handler method parameters.
- **Key classes/interfaces:** `Validator`, `SmartValidator`, `Errors`, `BindingResult`, `DataBinder`, `MethodValidationInterceptor`, `LocalValidatorFactoryBean`
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/validation/Validator.java`

#### AOT (Ahead-of-Time) Compilation and GraalVM Native Image Support

- **Description:** Since Spring 6.0, the framework includes an AOT engine that analyses the application at build time to generate `RuntimeHints` (reflection, resource, serialisation, and JDK proxy hints) and pre-initialised bean registration code. This enables deployment as a GraalVM native executable. `AotDetector` controls whether AOT artefacts are used at runtime. `FileNativeConfigurationWriter` writes GraalVM configuration JSON files. `RuntimeHintsRegistrar` is the extension point for libraries and applications to register hints. JavaPoet is repackaged inside `spring-core` as `org.springframework.javapoet` for source generation.
- **Key classes/interfaces:** `AotDetector`, `RuntimeHints`, `RuntimeHintsRegistrar`, `GenerationContext`, `BeanRegistrationAotProcessor`, `BeanFactoryInitializationAotProcessor`, `FileNativeConfigurationWriter`, `@Reflective`, `@RegisterReflection`
- **Source files:**
  - `src/spring-framework/spring-core/src/main/java/org/springframework/aot/AotDetector.java`
  - `src/spring-framework/spring-core/src/main/java/org/springframework/aot/hint/RuntimeHints.java`
  - `src/spring-framework/spring-core/src/main/java/org/springframework/aot/generate/GenerationContext.java`
  - `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/aot/BeanRegistrationAotProcessor.java`

#### Retry Policy (since Spring 7.0)

- **Description:** `RetryPolicy` is a strategy interface for defining retry behaviour for transient failure recovery. `RetryTemplate` executes retryable operations. The fluent builder API supports configurable back-off (fixed, exponential with optional jitter), maximum retries, timeout, include/exclude exception type filters, and custom predicates. Default retry count is 3; default delay is 1,000 ms; default multiplier is 1.0 (fixed delay).
- **Key classes/interfaces:** `RetryPolicy`, `RetryTemplate`, `RetryPolicy.Builder`, `FixedBackOff`, `ExponentialBackOff`, `@Retryable`
- **Source files:**
  - `src/spring-framework/spring-core/src/main/java/org/springframework/core/retry/RetryPolicy.java`

#### Observability (Micrometer Integration)

- **Description:** First-class integration with Micrometer Observation API. HTTP server (MVC and WebFlux) and client (`RestClient`, `WebClient`) requests are instrumented with spans and metrics. JMS publish and process operations are instrumented via Micrometer Jakarta 9 bridge. Task scheduler observations are supported. Convention-based customisation of observation names and tags is provided via `ObservationConvention`.
- **Key classes/interfaces:** `ObservationRegistry`, `ClientRequestObservationConvention`, `ServerRequestObservationConvention`, `JmsInstrumentation`, `MicrometerObservationRegistryTestExecutionListener`
- **Source files:**
  - `src/spring-framework/spring-web/src/main/java/org/springframework/web/client/RestClient.java`
  - `src/spring-framework/spring-jms/src/main/java/org/springframework/jms/core/JmsTemplate.java`

#### Spring TestContext Framework

- **Description:** Comprehensive testing support integrating with JUnit 5 (Jupiter), JUnit 4, and TestNG. The `TestContext Framework` loads and caches `ApplicationContext` instances across tests. `TestExecutionListener` implementations handle dependency injection, transaction management, SQL script execution, dirty-context management, and event publication. `MockMvc` enables integration testing of Spring MVC controllers without a running server. `MockMvcTester` provides AssertJ-style assertions (since 6.2). `WebTestClient` tests reactive web. Bean override (`@MockitoBean`, `@MockitoSpyBean`, `@TestBean`) enables fine-grained mocking within the Spring context.
- **Key classes/interfaces:** `@SpringJUnitConfig`, `MockMvc`, `MockMvcTester`, `WebTestClient`, `@MockitoBean`, `@TestBean`, `@Sql`, `@DirtiesContext`, `TestExecutionListener`
- **Source files:**
  - `src/spring-framework/spring-test/src/main/resources/META-INF/spring.factories`

#### Load-Time Weaving and Class Instrumentation

- **Description:** `InstrumentationSavingAgent` is a Java agent that captures the JVM `Instrumentation` handle for use by `InstrumentationLoadTimeWeaver`. This enables AspectJ LTW-based weaving of domain objects (`@Configurable`) without compile-time instrumentation. The agent is declared in the `spring-instrument` JAR's manifest.
- **Key classes/interfaces:** `InstrumentationSavingAgent`, `InstrumentationLoadTimeWeaver`, `LoadTimeWeaver`
- **Source files:**
  - `src/spring-framework/spring-instrument/src/main/java/org/springframework/instrument/InstrumentationSavingAgent.java`

---

## 4. Workflows and Behaviours

#### HTTP Request Processing (Servlet MVC)

- **Type:** user-facing
- **Trigger:** Incoming HTTP request received by the servlet container and forwarded to `DispatcherServlet`.
- **Steps:**
  1. `DispatcherServlet.doDispatch()` resolves the request locale and determines whether multipart processing is required via `MultipartResolver`. Source: `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/DispatcherServlet.java`
  2. Each registered `HandlerMapping` is consulted (in order) to produce a `HandlerExecutionChain` wrapping the matched handler and applicable `HandlerInterceptor` instances. Default mappings are `BeanNameUrlHandlerMapping` and `RequestMappingHandlerMapping`.
  3. Pre-handle interceptors are invoked (`HandlerInterceptor.preHandle`). If any returns `false`, processing stops.
  4. The appropriate `HandlerAdapter` invokes the handler. `RequestMappingHandlerAdapter` calls the `@RequestMapping` controller method, resolving arguments via argument resolvers and processing the return value via return value handlers.
  5. Post-handle interceptors are invoked (`HandlerInterceptor.postHandle`).
  6. If a `ModelAndView` is produced, `DispatcherServlet` selects a `ViewResolver` and renders the view.
  7. After-completion interceptors are invoked (`HandlerInterceptor.afterCompletion`).
  8. Exceptions are routed to `HandlerExceptionResolver` implementations (including `@ControllerAdvice` / `@ExceptionHandler` methods).
- **State transitions:** Stateless HTTP cycle; no durable state is persisted by the framework itself.
- **Source files:**
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/DispatcherServlet.java`
  - `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/RequestMappingHandlerMapping.java`

#### HTTP Request Processing (Reactive WebFlux)

- **Type:** user-facing
- **Trigger:** Incoming HTTP request received by a reactive HTTP server (Reactor Netty, Tomcat async, Jetty async) and adapted into a `ServerWebExchange`.
- **Steps:**
  1. `WebHttpHandlerBuilder` assembles a reactive processing chain of `WebFilter`, `WebExceptionHandler`, and `DispatcherHandler`. Source: `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/DispatcherHandler.java`
  2. `DispatcherHandler.handle(ServerWebExchange)` returns `Mono<Void>`. It iterates registered `HandlerMapping` implementations reactively.
  3. The matched `HandlerAdapter` invokes the handler, returning `Mono<HandlerResult>`.
  4. A `HandlerResultHandler` writes the result to the response (JSON, view, SSE stream, etc.).
  5. Pre-flight CORS requests are handled by `PreFlightRequestHandler`.
  6. Exceptions propagate as Reactor error signals and are caught by `WebExceptionHandler` beans.
- **State transitions:** Non-blocking reactive pipeline; all steps are composed as Reactor operators.
- **Source files:**
  - `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/DispatcherHandler.java`

#### Declarative Transaction Demarcation

- **Type:** system/background
- **Trigger:** Invocation of a method annotated with `@Transactional` on a Spring-managed bean through an AOP proxy.
- **Steps:**
  1. `TransactionInterceptor` intercepts the method call. Source: `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/interceptor/TransactionInterceptor.java`
  2. `PlatformTransactionManager.getTransaction()` is called with the resolved `TransactionDefinition` (propagation, isolation, timeout, read-only flag).
  3. The underlying method executes within the transaction boundary.
  4. On normal completion, `PlatformTransactionManager.commit()` is called.
  5. On an unchecked exception (or checked exceptions listed in `rollbackFor`), `PlatformTransactionManager.rollback()` is called.
  6. Transaction synchronisation callbacks are fired (`TransactionSynchronization`).
- **State transitions:** `ACTIVE` → `COMMITTED` or `ACTIVE` → `ROLLED_BACK`.
- **Source files:**
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/PlatformTransactionManager.java`
  - `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/interceptor/TransactionInterceptor.java`

#### ApplicationContext Refresh (Bootstrap) Lifecycle

- **Type:** system/background
- **Trigger:** Call to `ApplicationContext.refresh()` during application startup.
- **Steps:**
  1. Prepare the bean factory: register environment beans, apply `BeanFactoryPostProcessor` beans (e.g., `PropertySourcesPlaceholderConfigurer`).
  2. Invoke `BeanDefinitionRegistryPostProcessor` implementations (e.g., `ConfigurationClassPostProcessor` processes `@Configuration` classes, `@ComponentScan`, `@Import`, `@Bean`).
  3. Instantiate all non-lazy singleton beans; perform dependency injection, fire `@PostConstruct` and `InitializingBean.afterPropertiesSet()`.
  4. Publish `ContextRefreshedEvent` to all `ApplicationListener` beans.
  5. `SmartLifecycle` beans are started in ascending phase order.
- **State transitions:** `CREATED` → `REFRESHING` → `ACTIVE` → `CLOSED` (on `close()`).
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/context/support/AbstractApplicationContext.java`

#### Scheduled Task Execution

- **Type:** system/background
- **Trigger:** Container start-up when `@EnableScheduling` is present; thereafter fired by the configured `TaskScheduler` on cron, fixed-rate, or fixed-delay triggers.
- **Steps:**
  1. `ScheduledAnnotationBeanPostProcessor` scans all beans for `@Scheduled` methods. Source: `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/annotation/ScheduledAnnotationBeanPostProcessor.java`
  2. Tasks are registered with `ScheduledTaskRegistrar` against the resolved `TaskScheduler`.
  3. The scheduler fires tasks on the configured interval in pool threads (or virtual threads on JDK 21+).
  4. Exceptions are logged; the scheduler is not interrupted.
- **Source files:**
  - `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/annotation/EnableScheduling.java`

#### JMS Asynchronous Message Consumption

- **Type:** system/background
- **Trigger:** `DefaultMessageListenerContainer` starts polling a JMS destination after `ApplicationContext` refresh.
- **Steps:**
  1. Container establishes a JMS `Connection` and starts `Session`-based polling threads (configurable concurrency).
  2. A `MessageConsumer` receives a `Message` from the queue or topic.
  3. The message is dispatched to the registered `MessageListener` or `@JmsListener`-annotated method.
  4. If `sessionTransacted=true`, the session is committed on success or rolled back on exception.
  5. Micrometer observation spans are created for the process operation. Source: `src/spring-framework/spring-jms/src/main/java/org/springframework/jms/core/JmsTemplate.java`
- **Source files:**
  - `src/spring-framework/spring-jms/src/main/java/org/springframework/jms/listener/DefaultMessageListenerContainer.java`

#### AOT Build-Time Processing

- **Type:** system/background
- **Trigger:** Execution of the Spring AOT Gradle/Maven plugin during the build phase (before native image compilation).
- **Steps:**
  1. The AOT engine refreshes a limited `ApplicationContext` using class analysis.
  2. `BeanRegistrationAotProcessor` and `BeanFactoryInitializationAotProcessor` implementations are invoked to collect `RuntimeHints` and generate `BeanRegistrationCode`. Source: `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/aot/BeanRegistrationAotProcessor.java`
  3. `FileNativeConfigurationWriter` writes `reflect-config.json`, `resource-config.json`, `proxy-config.json`, and `serialization-config.json` for GraalVM. Source: `src/spring-framework/spring-core/src/main/java/org/springframework/aot/nativex/FileNativeConfigurationWriter.java`
  4. Generated Java source files (using repackaged JavaPoet) are output for compilation into AOT-initialised classes.
  5. `native-image` consumes these artefacts to produce a standalone native executable.
- **Source files:**
  - `src/spring-framework/spring-core/src/main/java/org/springframework/aot/AotDetector.java`
  - `src/spring-framework/spring-core/src/main/java/org/springframework/aot/nativex/FileNativeConfigurationWriter.java`

#### WebSocket Handshake and STOMP Session

- **Type:** user-facing
- **Trigger:** HTTP `Upgrade` request from a WebSocket-capable client.
- **Steps:**
  1. `HttpSessionHandshakeInterceptor` (or custom interceptor) populates session attributes.
  2. The appropriate `RequestUpgradeStrategy` (Tomcat, Jetty, or standard JSR-356) upgrades the HTTP connection to WebSocket.
  3. A `WebSocketSession` is created and passed to the registered `WebSocketHandler`. Source: `src/spring-framework/spring-websocket/src/main/java/org/springframework/web/socket/WebSocketSession.java`
  4. For STOMP: `StompSubProtocolHandler` decodes STOMP frames; `@MessageMapping` methods are invoked.
  5. SockJS fallback negotiates an alternative transport (long-polling, iframe eventsource) if WebSocket is unavailable.
- **Source files:**
  - `src/spring-framework/spring-websocket/src/main/java/org/springframework/web/socket/WebSocketSession.java`

---

## 5. Business Rules and Validation

| ID | Rule | Description | Criticality | Source |
|----|------|-------------|-------------|--------|
| BR-01 | Bean name uniqueness | Each bean registered in the `ApplicationContext` must have a unique name. Duplicate registration raises `BeanDefinitionOverrideException` unless `allowBeanDefinitionOverriding` is explicitly enabled. | Core | `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/DefaultListableBeanFactory.java` |
| BR-02 | Singleton scope re-use | A singleton-scoped bean is created once and shared across all injection points. Mutable state inside singletons must be thread-safe. | Core | `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/DefaultSingletonBeanRegistry.java` |
| BR-03 | Circular dependency restriction | Constructor-injection circular dependencies are forbidden and raise `BeanCurrentlyInCreationException`. Setter/field injection circularity is resolved via early exposure of partially-initialised singleton references (three-level cache). | Core | `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/AbstractAutowireCapableBeanFactory.java` |
| BR-04 | Transaction rollback rules | By default, `@Transactional` rolls back on unchecked exceptions (`RuntimeException` and `Error`) and commits on checked exceptions. `rollbackFor` / `noRollbackFor` attributes override this. | Core | `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/annotation/Transactional.java` |
| BR-05 | Transaction propagation semantics | `REQUIRED` (default) joins an existing transaction or creates one. `REQUIRES_NEW` always suspends any existing transaction. `SUPPORTS` participates if present, else runs non-transactionally. `MANDATORY` requires an existing transaction, else throws. `NEVER` must not run in a transaction. `NOT_SUPPORTED` suspends current transaction. `NESTED` creates a savepoint. | Core | `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/TransactionDefinition.java` |
| BR-06 | AOP proxy self-invocation bypass | Calling one advised method (e.g., `@Transactional`) from within the same bean instance bypasses the AOP proxy; the advice is not applied. Applications requiring self-invocation must use `AopContext.currentProxy()` or inject a self-reference. | Supporting | `src/spring-framework/spring-aop/src/main/java/org/springframework/aop/framework/AopContext.java` |
| BR-07 | Single-threaded scheduler by default | All `@Scheduled` tasks share a single-threaded scheduler unless a custom `TaskScheduler` is configured. Long-running tasks block subsequent invocations. | Supporting | `src/spring-framework/spring-context/src/main/java/org/springframework/scheduling/annotation/ScheduledAnnotationBeanPostProcessor.java` |
| BR-08 | RetryPolicy configuration constraints | When a custom `BackOff` strategy is supplied to `RetryPolicy.Builder`, the `maxRetries`, `delay`, `jitter`, `multiplier`, and `maxDelay` options must not also be set; the `build()` method raises `IllegalStateException` if this constraint is violated. | Supporting | `src/spring-framework/spring-core/src/main/java/org/springframework/core/retry/RetryPolicy.java` |
| BR-09 | RetryPolicy defaults | Default `RetryPolicy` retries up to 3 times with a 1,000 ms fixed delay and no timeout. | Supporting | `src/spring-framework/spring-core/src/main/java/org/springframework/core/retry/RetryPolicy.java` |
| BR-10 | AOT mode enforcement | When `spring.aot.enabled=true` or running inside a GraalVM native image, the framework must use pre-generated AOT artefacts. If artefacts are absent, the recommended behaviour is to throw an exception rather than fall back to dynamic reflection. | Supporting | `src/spring-framework/spring-core/src/main/java/org/springframework/aot/AotDetector.java` |
| BR-11 | Bean Validation on web method parameters | `@Valid` / `@Validated` on controller method parameters triggers Jakarta Bean Validation. Constraint violations raise `MethodArgumentNotValidException` (MVC) or `WebExchangeBindException` (WebFlux), producing a 400 Bad Request response by default. | Supporting | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/mvc/method/annotation/RequestResponseBodyMethodProcessor.java` |
| BR-12 | Content negotiation — 406 response | `DispatcherServlet` selects response media type through `ContentNegotiationManager`. If no acceptable type can be produced for the client's `Accept` header, a 406 Not Acceptable response is returned. | Supporting | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/DispatcherServlet.java` |
| BR-13 | CORS pre-flight handling | Cross-Origin preflight (`OPTIONS`) requests are handled by the framework before controller methods are invoked. CORS configuration (allowed origins, methods, headers) must be declared via `@CrossOrigin` or a global `CorsConfigurationSource`. | Peripheral | `src/spring-framework/spring-web/src/main/java/org/springframework/web/cors/CorsConfiguration.java` |
| BR-14 | CandidateComponentsIndexer deprecation | The compile-time `CandidateComponentsIndexer` annotation processor is deprecated since Spring 6.1 and scheduled for removal. New projects must rely on the AOT engine instead. | Peripheral | `src/spring-framework/spring-context-indexer/src/main/java/org/springframework/context/index/processor/CandidateComponentsIndexer.java` |
| BR-15 | R2DBC bind-marker dialect resolution | The `BindMarkersFactoryResolver` selects the correct bind-marker dialect (positional `?`, named `:name`, or `$1`) based on the `ConnectionFactory` driver. Built-in providers are registered via `META-INF/spring.factories`. | Peripheral | `src/spring-framework/spring-r2dbc/src/main/resources/META-INF/spring.factories` |

---

## 6. Domain Model

> **Note:** Spring Framework is a general-purpose infrastructure library and does not model a business domain. The entities below are framework abstractions — the core vocabulary that applications built on this framework use and extend.

#### BeanFactory

- **Purpose:** Root container interface for accessing and managing Spring beans. Provides bean retrieval by name, type, and annotation; manages bean scopes; performs type conversion.
- **Source file:** `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/BeanFactory.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| (interface methods) | — | `getBean(String)`, `getBean(Class<T>)`, `containsBean(String)`, `isSingleton(String)`, `isPrototype(String)`, `getType(String)`, `getAliases(String)` | `BeanFactory.java` |

#### ApplicationContext

- **Purpose:** Extends `BeanFactory` to add event publishing, message resolution (i18n), resource loading, environment access, and parent-context hierarchies. The central runtime object in any Spring application.
- **Source file:** `src/spring-framework/spring-context/src/main/java/org/springframework/context/ApplicationContext.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| id | `String` | Unique identifier for this context instance | `ApplicationContext.java` |
| applicationName | `String` | Deployed application name | `ApplicationContext.java` |
| displayName | `String` | Human-readable context name | `ApplicationContext.java` |
| startupDate | `long` | Timestamp (epoch ms) of context refresh | `ApplicationContext.java` |
| parent | `ApplicationContext` (nullable) | Parent context for hierarchical contexts | `ApplicationContext.java` |

#### BeanDefinition

- **Purpose:** Metadata descriptor for a bean: class name, scope, lazy-init flag, constructor arguments, property values, init/destroy method names, and dependency declarations.
- **Source file:** `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/config/BeanDefinition.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| beanClassName | `String` (nullable) | Fully qualified class name | `BeanDefinition.java` |
| scope | `String` | `singleton`, `prototype`, `request`, `session`, etc. | `BeanDefinition.java` |
| lazyInit | `boolean` | Whether to defer instantiation | `BeanDefinition.java` |
| role | `int` | `ROLE_APPLICATION(0)`, `ROLE_SUPPORT(1)`, `ROLE_INFRASTRUCTURE(2)` | `BeanDefinition.java` |

#### Environment

- **Purpose:** Models the runtime environment: active and default profiles; hierarchical property sources for resolving `${...}` placeholders and `@Value` expressions.
- **Source file:** `src/spring-framework/spring-core/src/main/java/org/springframework/core/env/Environment.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| activeProfiles | `String[]` | Profiles currently active | `Environment.java` |
| defaultProfiles | `String[]` | Profiles active when no explicit profile is set | `Environment.java` |

#### Resource

- **Purpose:** Abstraction over any addressable resource (file, classpath entry, URL, byte array, etc.). Provides `getInputStream()`, `getURL()`, `getURI()`, `getFile()`, `exists()`, `contentLength()`, `lastModified()`.
- **Source file:** `src/spring-framework/spring-core/src/main/java/org/springframework/core/io/Resource.java`

#### ApplicationEvent

- **Purpose:** Base class for all application events. Carries a timestamp and the event source object. Consumers extend this class for domain-specific events.
- **Source file:** `src/spring-framework/spring-context/src/main/java/org/springframework/context/ApplicationEvent.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| timestamp | `long` | Epoch milliseconds when the event occurred | `ApplicationEvent.java` |
| source | `Object` | Object that triggered the event (inherited from `EventObject`) | `ApplicationEvent.java` |

#### Message

- **Purpose:** Generic message abstraction (spring-messaging). Immutable value carrying a typed payload and a `MessageHeaders` map. Used in STOMP, JMS, WebSocket, and RSocket messaging layers.
- **Source file:** `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/Message.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| payload | `T` | Message body | `Message.java` |
| headers | `MessageHeaders` | Immutable metadata map (id, timestamp, content-type, etc.) | `Message.java` |

#### RetryPolicy

- **Purpose:** Strategy interface defining whether and how a failed operation should be retried. Provides a fluent `Builder` for common configuration. Default behaviour: 3 retries, 1,000 ms fixed delay, applies to all exception types, no timeout.
- **Source file:** `src/spring-framework/spring-core/src/main/java/org/springframework/core/retry/RetryPolicy.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| DEFAULT_MAX_RETRIES | `long` (3) | Default maximum retry count | `RetryPolicy.Builder` |
| DEFAULT_DELAY | `long` (1000 ms) | Default base delay in milliseconds | `RetryPolicy.Builder` |
| DEFAULT_MAX_DELAY | `long` (`Long.MAX_VALUE`) | Default upper bound on exponential delay | `RetryPolicy.Builder` |
| DEFAULT_MULTIPLIER | `double` (1.0) | Default back-off multiplier (1.0 = fixed delay) | `RetryPolicy.Builder` |

#### WebSocketSession

- **Purpose:** Abstraction over a single live WebSocket connection. Provides session identification, URI, handshake headers, principal, local and remote addresses, attribute map, and message-send / close operations.
- **Source file:** `src/spring-framework/spring-websocket/src/main/java/org/springframework/web/socket/WebSocketSession.java`

| Property / Field | Type | Description | Source |
|-----------------|------|-------------|--------|
| id | `String` | Unique session identifier | `WebSocketSession.java` |
| uri | `URI` (nullable) | URI used to open the connection | `WebSocketSession.java` |
| handshakeHeaders | `HttpHeaders` | HTTP headers from the handshake request | `WebSocketSession.java` |
| attributes | `Map<String, Object>` | Session-scoped attribute map | `WebSocketSession.java` |
| principal | `Principal` (nullable) | Authenticated user principal | `WebSocketSession.java` |

#### Enumerations

| Enum Name | Values | Source |
|-----------|--------|--------|
| `HttpMethod` | `GET`, `HEAD`, `POST`, `PUT`, `PATCH`, `DELETE`, `OPTIONS`, `TRACE` | `src/spring-framework/spring-web/src/main/java/org/springframework/http/HttpMethod.java` |
| `HttpStatus` | Full RFC HTTP status code enumeration (1xx–5xx), e.g. `OK(200)`, `NOT_FOUND(404)`, `INTERNAL_SERVER_ERROR(500)` | `src/spring-framework/spring-web/src/main/java/org/springframework/http/HttpStatus.java` |
| `TransactionDefinition` propagation constants | `PROPAGATION_REQUIRED(0)`, `PROPAGATION_SUPPORTS(1)`, `PROPAGATION_MANDATORY(2)`, `PROPAGATION_REQUIRES_NEW(3)`, `PROPAGATION_NOT_SUPPORTED(4)`, `PROPAGATION_NEVER(5)`, `PROPAGATION_NESTED(6)` | `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/TransactionDefinition.java` |
| `TransactionDefinition` isolation constants | `ISOLATION_DEFAULT(-1)`, `ISOLATION_READ_UNCOMMITTED(1)`, `ISOLATION_READ_COMMITTED(2)`, `ISOLATION_REPEATABLE_READ(4)`, `ISOLATION_SERIALIZABLE(8)` | `src/spring-framework/spring-tx/src/main/java/org/springframework/transaction/TransactionDefinition.java` |
| `MemberCategory` (AOT hints) | `PUBLIC_FIELDS`, `DECLARED_FIELDS`, `INTROSPECT_PUBLIC_CONSTRUCTORS`, `INVOKE_PUBLIC_CONSTRUCTORS`, `INTROSPECT_DECLARED_CONSTRUCTORS`, `INVOKE_DECLARED_CONSTRUCTORS`, `INTROSPECT_PUBLIC_METHODS`, `INVOKE_PUBLIC_METHODS`, `INTROSPECT_DECLARED_METHODS`, `INVOKE_DECLARED_METHODS` | `src/spring-framework/spring-core/src/main/java/org/springframework/aot/hint/MemberCategory.java` |
| `ExecutableMode` (AOT hints) | `INTROSPECT`, `INVOKE` | `src/spring-framework/spring-core/src/main/java/org/springframework/aot/hint/ExecutableMode.java` |
| `AdviceMode` | `PROXY`, `ASPECTJ` | `src/spring-framework/spring-context/src/main/java/org/springframework/context/annotation/AdviceMode.java` |
| `Autowire` | `NO`, `BY_NAME`, `BY_TYPE`, `CONSTRUCTOR` | `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/annotation/Autowire.java` |
| `BeanDefinition` role constants | `ROLE_APPLICATION(0)`, `ROLE_SUPPORT(1)`, `ROLE_INFRASTRUCTURE(2)` | `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/config/BeanDefinition.java` |

#### Relationships

| Entity A | Entity B | Relationship Type | Source |
|----------|----------|-------------------|--------|
| `ApplicationContext` | `BeanFactory` | Extends (is-a; adds lifecycle and event features) | `src/spring-framework/spring-context/src/main/java/org/springframework/context/ApplicationContext.java` |
| `ApplicationContext` | `Environment` | Provides (exposes via `getEnvironment()`) | `src/spring-framework/spring-context/src/main/java/org/springframework/context/ApplicationContext.java` |
| `ApplicationContext` | `ApplicationEventPublisher` | Implements (self-publishes events) | `src/spring-framework/spring-context/src/main/java/org/springframework/context/ApplicationContext.java` |
| `BeanFactory` | `BeanDefinition` | Manages (holds registry of definitions) | `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/DefaultListableBeanFactory.java` |
| `BeanDefinition` | Bean instance | Creates (factory produces instances from definitions) | `src/spring-framework/spring-beans/src/main/java/org/springframework/beans/factory/support/AbstractAutowireCapableBeanFactory.java` |
| `Message` | `MessageHeaders` | Has-a (composed; immutable) | `src/spring-framework/spring-messaging/src/main/java/org/springframework/messaging/Message.java` |
| `RetryPolicy` | `BackOff` | Has-a (pluggable back-off strategy) | `src/spring-framework/spring-core/src/main/java/org/springframework/core/retry/RetryPolicy.java` |
| `JdbcTemplate` | `DataSource` | Uses (injected dependency) | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/JdbcTemplate.java` |
| `JpaTransactionManager` | `EntityManagerFactory` | Uses (injected dependency) | `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/JpaTransactionManager.java` |
| `DispatcherServlet` | `HandlerMapping` | Uses (ordered list; consulted sequentially) | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/DispatcherServlet.java` |
| `DispatcherServlet` | `HandlerAdapter` | Uses (ordered list) | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/DispatcherServlet.java` |
| `DispatcherServlet` | `ViewResolver` | Uses (ordered list) | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/DispatcherServlet.java` |
| `DispatcherHandler` | `HandlerMapping` | Uses (reactive; list of) | `src/spring-framework/spring-webflux/src/main/java/org/springframework/web/reactive/DispatcherHandler.java` |
| `HttpServiceProxyFactory` | `HttpExchangeAdapter` | Uses (pluggable transport strategy) | `src/spring-framework/spring-web/src/main/java/org/springframework/web/service/invoker/HttpServiceProxyFactory.java` |
| `LocalContainerEntityManagerFactoryBean` | `PersistenceUnitManager` | Uses (lifecycle integration) | `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/LocalContainerEntityManagerFactoryBean.java` |
| `ApplicationEvent` | `ApplicationContext` | Published by (source is the context or an application component) | `src/spring-framework/spring-context/src/main/java/org/springframework/context/ApplicationEvent.java` |

---

## 7. Integration Points

| Integration | Type | Endpoint / Target | Direction | Source |
|-------------|------|-------------------|-----------|--------|
| JDBC relational databases | JDBC / `javax.sql.DataSource` | Any JDBC-compatible database (Oracle, PostgreSQL, H2, HSQLDB, Derby, etc.) | Bidirectional (query and update) | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/JdbcTemplate.java` |
| JPA / Hibernate ORM | JPA 3.2 SPI | Entity persistence provider (Hibernate 7.3, EclipseLink 5.0) | Bidirectional | `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/LocalContainerEntityManagerFactoryBean.java` |
| R2DBC reactive databases | R2DBC SPI 1.0 | Any R2DBC-compatible driver (H2, PostgreSQL, Oracle, etc.) | Bidirectional (reactive) | `src/spring-framework/spring-r2dbc/src/main/java/org/springframework/r2dbc/core/DatabaseClient.java` |
| JMS messaging | Jakarta JMS 3.1 API | Any JMS broker (ActiveMQ Artemis 2.42, IBM MQ, RabbitMQ, etc.) | Bidirectional (send and receive) | `src/spring-framework/spring-jms/src/main/java/org/springframework/jms/core/JmsTemplate.java` |
| STOMP over WebSocket / TCP relay | STOMP protocol | External STOMP broker (ActiveMQ, RabbitMQ) | Bidirectional | `src/spring-framework/spring-websocket/src/main/java/org/springframework/web/socket/messaging/StompBrokerRelayMessageHandler.java` |
| RSocket | RSocket binary protocol | Any RSocket endpoint | Bidirectional | `src/spring-framework/spring-messaging/spring-messaging.gradle` (`io.rsocket:rsocket-core`) |
| HTTP REST services (client) | HTTP/1.1 and HTTP/2 | Any REST API endpoint | Outbound | `src/spring-framework/spring-web/src/main/java/org/springframework/web/client/RestClient.java` |
| Apache HttpComponents 5 | HTTP client library | External HTTP servers | Outbound | `src/spring-framework/spring-web/spring-web.gradle` |
| Reactor Netty | Netty-based HTTP server/client | Network I/O layer | Bidirectional | `src/spring-framework/spring-webflux/spring-webflux.gradle` |
| GraalVM Native Image | AOT compilation toolchain | `native-image` compiler | Outbound (configuration JSON files) | `src/spring-framework/spring-core/src/main/java/org/springframework/aot/nativex/FileNativeConfigurationWriter.java` |
| Micrometer | Observation / metrics / tracing API | Monitoring backend (Prometheus, DataDog, Zipkin, etc.) | Outbound | `src/spring-framework/spring-context/spring-context.gradle`, `src/spring-framework/spring-web/spring-web.gradle`, `src/spring-framework/spring-jms/spring-jms.gradle` |
| Jakarta Mail | `jakarta.mail` API | SMTP mail server | Outbound | `src/spring-framework/spring-context-support/src/main/java/org/springframework/mail/javamail/JavaMailSenderImpl.java` |
| Quartz Scheduler | `org.quartz` API 2.3.2 | Quartz `Scheduler` (in-memory or JDBC job store) | Bidirectional | `src/spring-framework/spring-context-support/src/main/java/org/springframework/scheduling/quartz/SchedulerFactoryBean.java` |
| AspectJ LTW | Java agent / class transformer | JVM class-loading pipeline | Inbound (class transformation at load time) | `src/spring-framework/spring-instrument/src/main/java/org/springframework/instrument/InstrumentationSavingAgent.java` |
| JMX | `javax.management` API | JMX MBean server (local or remote) | Bidirectional | `src/spring-framework/spring-context/src/main/java/org/springframework/jmx/export/MBeanExporter.java` |
| Jakarta EL 6.0 | Expression Language API | Expression evaluation in templates and bean validation | Internal | `src/spring-framework/spring-context/spring-context.gradle` |
| Jakarta Faces (JSF) 4.1 | JSF lifecycle API | JSF lifecycle integration for Spring beans | Bidirectional | `src/spring-framework/spring-web/spring-web.gradle` |
| FreeMarker 2.3.34 | Template engine | Template rendering for MVC and WebFlux views | Inbound (template → response) | `src/spring-framework/spring-webmvc/spring-webmvc.gradle`, `src/spring-framework/spring-webflux/spring-webflux.gradle` |
| Jackson 2.21 / 3.1 (JSON/XML/YAML/CBOR/Smile) | `com.fasterxml.jackson` / `tools.jackson` | JSON/XML/binary (de)serialisation | Bidirectional | `src/spring-framework/spring-web/spring-web.gradle`, `src/spring-framework/spring-webmvc/spring-webmvc.gradle` |
| Apache POI 5.5.1 | `org.apache.poi` | Excel (.xlsx) view generation | Outbound | `src/spring-framework/spring-webmvc/spring-webmvc.gradle` |
| OpenPDF 1.3.43 | `com.github.librepdf:openpdf` | PDF view generation | Outbound | `src/spring-framework/spring-webmvc/spring-webmvc.gradle` |
| ROME 1.19.0 | `com.rometools:rome` | RSS and Atom feed views | Outbound | `src/spring-framework/spring-webmvc/spring-webmvc.gradle` |
| CRaC 1.4.0 | `org.crac:crac` | JVM Coordinated Restore at Checkpoint lifecycle hooks | Bidirectional | `src/spring-framework/spring-context/spring-context.gradle` |
| Kotlin coroutines 1.10.2 | `kotlinx-coroutines-reactor` | Suspension-point adaptation for reactive pipelines | Bidirectional | Multiple module gradle files |
| Kotlin serialisation 1.11.0 | `kotlinx-serialization-*` | Kotlin data class (de)serialisation for HTTP responses | Bidirectional | `src/spring-framework/spring-web/spring-web.gradle`, `src/spring-framework/spring-webmvc/spring-webmvc.gradle` |

---

## 8. Reports

Spring Framework does not contain any report generation feature of its own as a platform concern. It provides view infrastructure classes that downstream applications can extend to render reports as HTTP responses. No embedded report definition language, report scheduler, or data-warehouse query is present in this codebase.

| Report | Type | Purpose | Data Sources | Parameters | Output Format | Source |
|--------|------|---------|-------------|------------|---------------|--------|
| PDF HTTP response views | View infrastructure | Allows downstream application controllers to stream generated PDF documents to the HTTP response | Application-supplied Spring MVC model map | Controller-defined | `application/pdf` | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/view/document/AbstractPdfView.java` |
| Excel HTTP response views | View infrastructure | Allows downstream application controllers to stream `.xlsx` workbooks to the HTTP response | Application-supplied Spring MVC model map | Controller-defined | `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet` | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/view/document/AbstractXlsxView.java` |
| Atom feed views | View infrastructure | Serves Atom feeds over HTTP | Application-supplied Spring MVC model map | Controller-defined | `application/atom+xml` | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/view/feed/AbstractAtomFeedView.java` |
| RSS feed views | View infrastructure | Serves RSS feeds over HTTP | Application-supplied Spring MVC model map | Controller-defined | `application/rss+xml` | `src/spring-framework/spring-webmvc/src/main/java/org/springframework/web/servlet/view/feed/AbstractRssFeedView.java` |

---

## 9. Cross-Reference: Application to Data Layer

### 9.1 Data Access Patterns

Spring Framework provides four distinct data access patterns for relational data plus one for reactive relational data:

1. **`JdbcTemplate` / `JdbcClient` (spring-jdbc):** Template-method pattern. The caller provides SQL and callback objects (`RowMapper`, `ResultSetExtractor`, `PreparedStatementSetter`). The template manages connection acquisition, `PreparedStatement` creation, result iteration, and `DataAccessException` translation. `JdbcClient` (since 6.1) wraps `JdbcTemplate` with a fluent, method-chained API.
2. **`NamedParameterJdbcTemplate` (spring-jdbc):** Wraps `JdbcTemplate`, replacing positional `?` placeholders with named parameters (`:paramName`) supplied via `SqlParameterSource` or `Map<String, ?>`.
3. **`SimpleJdbcInsert` / `SimpleJdbcCall` (spring-jdbc):** Metadata-driven helpers that introspect database table and procedure metadata at first use, generating INSERT statements or stored-procedure invocations with minimal configuration.
4. **JPA via `LocalContainerEntityManagerFactoryBean` (spring-orm):** Full JPA container bootstrap, `SharedEntityManagerCreator` proxies, and `JpaTransactionManager`. Application DAOs use `EntityManager` directly or via Spring Data (a separate project).
5. **`DatabaseClient` (spring-r2dbc):** Reactive non-blocking client. Fluent API returning `Mono<T>` / `Flux<T>`. Row mapping is performed via `BiFunction<Row, RowMetadata, T>` lambdas.

### 9.2 Entity-to-Table Mapping

Spring Framework does not define any business entities or database tables. The ORM layer (`spring-orm`) mediates between JPA `@Entity`-annotated classes (defined by downstream applications) and their database tables through a JPA persistence provider (Hibernate 7.3 or EclipseLink 5.0). The JDBC layer (`spring-jdbc`) operates on raw SQL without an object-to-table mapping layer; any mapping is performed by application-supplied `RowMapper` implementations.

| Entity / Class | Database Table(s) | Source |
|---------------|-------------------|--------|
| No framework-level entities defined | N/A — all entity-to-table mappings are defined in downstream application code and JPA `persistence.xml` / annotation metadata | `src/spring-framework/spring-orm/src/main/java/org/springframework/orm/jpa/LocalContainerEntityManagerFactoryBean.java` |

### 9.3 Repository / DAO Methods

Spring Framework ships no repository or DAO implementations for application business data. It provides the *infrastructure* that application-layer DAOs use. The following table documents the principal framework-level data access methods.

| Repository / DAO | Key Methods | Purpose | Source |
|-----------------|-------------|---------|--------|
| `JdbcTemplate` | `query(String, RowMapper<T>)`, `queryForObject(String, Class<T>)`, `queryForList(String)`, `update(String, Object...)`, `batchUpdate(String, List<Object[]>)`, `execute(String)` | Synchronous SQL execution with automatic resource management and exception translation | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/JdbcTemplate.java` |
| `JdbcClient` | `sql(String).query().list()`, `sql(String).param(...).update()`, `sql(String).query().single()` | Fluent, modern synchronous SQL API (since 6.1) | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/simple/JdbcClient.java` |
| `NamedParameterJdbcTemplate` | `query(String, SqlParameterSource, RowMapper<T>)`, `queryForObject(String, SqlParameterSource, Class<T>)`, `update(String, SqlParameterSource)`, `batchUpdate(String, SqlParameterSource[])` | Named-parameter SQL execution | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/namedparam/NamedParameterJdbcTemplate.java` |
| `SimpleJdbcInsert` | `execute(Map<String,?>)`, `executeAndReturnKey(Map<String,?>)`, `executeBatch(Map<String,?>[])` | Metadata-driven INSERT with optional generated key retrieval | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/simple/SimpleJdbcInsert.java` |
| `SimpleJdbcCall` | `execute(Map<String,?>)`, `executeObject(Class<T>, Map<String,?>)`, `executeFunction(Class<T>, Map<String,?>)` | Stored procedure and database function invocation | `src/spring-framework/spring-jdbc/src/main/java/org/springframework/jdbc/core/simple/SimpleJdbcCall.java` |
| `DatabaseClient` | `sql(String).bind(...).fetch().all()`, `sql(String).bind(...).fetch().one()`, `sql(String).bind(...).rowsUpdated()` | Reactive non-blocking SQL execution returning `Flux<T>` / `Mono<Long>` | `src/spring-framework/spring-r2dbc/src/main/java/org/springframework/r2dbc/core/DatabaseClient.java` |
| `JmsTemplate` | `send(Destination, MessageCreator)`, `convertAndSend(String, Object)`, `receive(String)`, `receiveAndConvert(String)`, `browse(String, BrowserCallback<T>)` | Synchronous JMS send, receive, and queue browse | `src/spring-framework/spring-jms/src/main/java/org/springframework/jms/core/JmsTemplate.java` |
