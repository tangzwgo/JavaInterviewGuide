## spring-core
@NonNullApi：

@Nullable：

@NonNullFields：

@UsesSunMisc：

@NonNull：

@AliasFor：
- value
- attribute
- annotation

@Order：
- value:
 
~~@UsesSunHttpServer~~

~~@UsesJava7~~

~~@UsesJava8~~

## spring-beans
@Autowired：
- required

@Required：

@Lookup：
- value

@Qualifier：
- value

@Configurable：
- value
- autowire
- dependencyCheck
- preConstruction

@Value：
- value

## spring-context
@ManagedAttribute：
- defaultValue
- description
- currencyTimeLimit
- persistPolicy
- persistPeriod

@ManagedNotifications：
- value

@ManagedOperationParameter：
- name
- description

@ManagedMetric：
- category
- currencyTimeLimit
- description
- displayName
- metricType
- persistPeriod
- persistPolicy
- unit

@ManagedOperation：
- description
- currencyTimeLimit

@ManagedOperationParameters：
- value

@ManagedResource：
- value
- objectName
- description
- currencyTimeLimit
- log
- logFile
- persistPolicy
- persistPeriod
- persistName
- persistLocation

@ManagedNotification：
- name
- description
- notificationTypes

@ComponentScans：
- value

@Bean：
- value
- name
- autowire
- autowireCandidate
- initMethod
- destroyMethod

@Scope：
- value
- scopeName
- proxyMode

@Description：
- value

@Scheduled：
- cron
- zone
- fixedDelay
- fixedDelayString
- fixedRate
- fixedRateString
- initialDelay
- initialDelayString

@Lazy：
- value

@EnableCaching：
- proxyTargetClass
- mode
- order

@CacheEvict：
- value
- cacheNames
- key
- keyGenerator
- cacheManager
- cacheResolver
- condition
- allEntries
- beforeInvocation

@CachePut：
- value
- cacheNames
- key
- keyGenerator
- cacheManager
- cacheResolver
- condition
- unless

@Cacheable：
- value
- cacheNames
- key
- keyGenerator
- cacheManager
- cacheResolver
- condition
- unless
- sync

@Caching：
- cacheable
- put
- evict

@CacheConfig：
- cacheNames
- keyGenerator
- cacheManager
- cacheResolver

@DateTimeFormat：
- style
- iso
- pattern

@NumberFormat：
- style
- pattern

@EventListener：
- value
- classes
- condition

@Primary：

@DependsOn：
- value

@EnableLoadTimeWeaving：
- aspectjWeaving

@PropertySource：
- name
- value
- ignoreResourceNotFound
- encoding
- factory

@Configuration：
- value
- proxyBeanMethods

@Role：
- value

@Conditional：
- value

@EnableAsync：
- annotation
- proxyTargetClass
- mode
- order

@Schedules：
- value

@EnableMBeanExport：
- defaultDomain
- server
- registration

@PropertySources：
- value

@Async：
- value

@EnableAspectJAutoProxy：
- proxyTargetClass
- exposeProxy

@Profile：
- value

@Import：
- value

@ComponentScan：
- value
- basePackages
- basePackageClasses
- nameGenerator
- scopeResolver
- scopedProxy
- resourcePattern
- useDefaultFilters
- includeFilters
- excludeFilters
- lazyInit

@Filter：
- type
- value
- classes
- pattern

@EnableScheduling：

@ImportResource：
- value
- locations
- reader

@Validated：
- value

@Service：
- value

@Indexed：

@Repository：
- value

@Controller：
- value

@Component：
- value

## spring-context-indexer
无

## spring-context-support
无

## spring-expression
无

## spring-aop
无

## spring-aspects
@EnableSpringConfigured

## spring-instrument
无

## spring-messaging
@Header：
- value
- name
- required
- defaultValue

@MessageMapping：
- value

@Payload：
- value
- expression
- required

@MessageExceptionHandler：
- value

@Headers：

@SubscribeMapping：
- value

@ConnectMapping：
- value

@SendToUser：
- value
- destinations
- broadcast

@DestinationVariable：
- value

@SendTo：
- value

## spring-jdbc
无

## spring-orm
无

## spring-oxm
无

## spring-jms
@EnableJms：

@JmsListener：
- id
- containerFactory
- destination
- subscription
- selector
- concurrency

@JmsListeners：
- value

## spring-tx
@Transactional：
- value
- transactionManager
- propagation
- isolation
- timeout
- readOnly
- rollbackFor
- rollbackForClassName
- noRollbackFor
- noRollbackForClassName

@TransactionalEventListener：
- phase
- fallbackExecution
- value
- classes
- condition

@EnableTransactionManagement：
- proxytargetClass
- mode
- order

## spring-web
@RestController：
- value

@RequestMapping：
- name
- value
- path
- method
- params
- headers
- consumes
- produces

@GetMapping：
- name
- value
- path
- params
- headers
- consumes
- produces

@PostMapping：
- name
- value
- path
- params
- headers
- consumes
- produces

@PatchMapping：
- name
- value
- path
- params
- headers
- consumes
- produces

@DeleteMapping：
- name
- value
- path
- params
- headers
- consumes
- produces

@PutMapping：
- name
- value
- path
- params
- headers
- consumes
- produces

@Mapping：

@RequestParam：
- value
- name
- required
- defaultValue

@RequestBody：
- required

@ResponseBody：

@ResponseStatus：
- value
- code
- reason

@ExceptionHandler：
- value

@RequestHander：
- value
- name
- required
- defaultValue

@RestControllerAdvice：
- value
- basePackages
- basePackageClasses
- assignableTypes
- annotations

@ControllerAdvice：
- value
- basePackages
- basePackageClasses
- assignableTypes
- annotations

@SessionScope：
- proxyMode

@RequestScope：
- proxyMode

@ApplicationScope：
- proxyMode

@ModelAttribute：
- value
- name
- binding

@SessionAttributes：
- value
- names
- types

@SessionAttribute：
- value
- name
- required

@RequestAttribute：
- value
- name
- required

@RequestPart：
- value
- name
- required

@PathVariable：
- value
- name
- required

@MatrixVariable：
- value
- name
- pathVar
- required
- defaultValue

@CookieValue：
- value
- name
- required
- defaultValue

@InitBinder：
- value

@CrossOrigin：
- value
- origins
- allowedHeaders
- exposedHeaders
- methods
- allowCredentials
- maxAge

## spring-webmvc
@EnableWebMvc：

## spring-websocket
@EnableWebSocketMessageBroker：

@EnableWebSocket：

## spring-webflux
@EnableWebFlux：

## spring-jcl
无

## spring-test
@TestConstructor：
- autowireMode

@BootstrapWith：
- value

@ContextConfiguration：
- value
- locations
- classes
- initializers
- inheritLocations
- inheritInitializers
- loader
- name

@TestExecutionListeners：
- value
- listeners
- inheritListeners
- mergeMode

@TestPropertySource：
- value
- locations
- inheritLocations
- properties
- inheritProperties

@SpringJUnitConfig：
- value
- classes
- locations
- initializers
- inheritLocations
- inheritInitializers
- name

@WebAppConfiguration：
- value

@EnabledIf：
- value
- expression
- reason
- loadContext

@DisabledIf：
- value
- expression
- reason
- loadContext

@SpringJUnitWebConfig：
- value
- classes
- locations
- initializers
- inheritLocations
- inheritInitializers
- name
- resourcePath

@SqlMergeMode：
- value

@SqlGroup：
- value

@Sql：
- value
- scripts
- statements
- executionPhase
- config

@SqlConfig：
- dataSource
- transactionManager
- transactionMode
- encoding
- separator
- commentPrefix
- commentPrefixes
- blockCommentStartDelimiter
- blockCommentEndDelimiter
- errorMode

@AfterTransaction：

@BeforeTransaction：

@TestPropertySources：
- value

@BeforeTestMethod：
- value

@BeforeTestExecution：
- value

@DirtiesContext：
- methodMode
- classMode
- hierarchyMode

@AfterTestClass：
- value

@Timed：
- millis

@Commit：

@ActiveProfiles：
- value
- profiles
- resolver
- inheritProfiles

@PrepareTestInstance：
- value

@AfterTestMethod：
- value

@ProfileValueSourceConfiguration：
- value

@BeforeTestClass：
- value

@IfProfileValue：
- name
- value
- values

@AfterTestExecution：
- value

@Repeat：
- value

@ContextHierarchy：
- value

@Rollback：
- value