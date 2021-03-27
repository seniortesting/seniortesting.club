---
title: spring技术问题整理
tags: []
keywords: ''
categories: []
abbrlink: 7670b080
date: 2021-03-26 20:38:51
description:
cover:
top_img:
---



整理一些常用的spring技术问题

## 自定义自己的application.yml中的配置信息

```java
         <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-configuration-processor</artifactId>
            <optional>true</optional>
        </dependency>

```

## spring security securedEnabled /jsr250Enabled  / prePostEnabled

## resttemplate获取的json对象是泛型的会自动转换为map对象，如何转为正确的实体类？

```
// 泛型的数据返回值
        ParameterizedTypeReference<WebResponse<WeixinUserInfoResponse>> webResponseParameterizedTypeReference =
                new ParameterizedTypeReference<WebResponse<WeixinUserInfoResponse>>() {
                };
        ResponseEntity<WebResponse<WeixinUserInfoResponse>> responseEntity = restTemplate.
                exchange(userInfoRequestUrl, HttpMethod.GET, null, webResponseParameterizedTypeReference);
        // 获取正确了token值
        WebResponse<WeixinUserInfoResponse> webResponse = responseEntity.getBody();
```

## spring quartz任务调度超时

[参考博客](https://www.cnblogs.com/daxin/p/3919927.html)

```yaml
        jobStore:
            class: org.quartz.impl.jdbcjobstore.JobStoreTX
            driverDelegateClass: org.quartz.impl.jdbcjobstore.StdJDBCDelegate
            tablePrefix: QRTZ_
            # 调度引擎比较忙得时候出现这个问题
            # 当前线程有10个，但是现在有12个任务需要在13:00处理，所以有两个任务需要延迟处理，
            # 如果延迟到13:60，就是延迟了60分钟， 大于下面的50分钟，所以就是misfire的。
            # 如果延迟到13:40 ，触发器发现小于50秒，调度引擎认为这个延迟时间可以忍受，所以不算超时(Misfires)
            misfireThreshold: 50000
            # 集群配置
            isClustered: false
            clusterCheckinInterval: 50000

```

## springboot 配置全局404详细步骤及说明

- `application.xml`中配置如下

```yml
server:
  error:
    whitelabel:
      enabled: false
    include-exception: true
    include-stacktrace: on_trace_param

```

说明：`server.error.whitelabel.enabled`,是为了去掉springboot的自动配置，它的自动配置代码如下：

```java
org.springframework.boot.autoconfigure.web.servlet.error.ErrorMvcAutoConfiguration.WhitelabelErrorViewConfiguration

 @Configuration
 @ConditionalOnProperty(prefix = "server.error.whitelabel", name = "enabled", matchIfMissing = true)
 @Conditional(ErrorTemplateMissingCondition.class)
 protected static class WhitelabelErrorViewConfiguration {

  private final StaticView defaultErrorView = new StaticView();

  @Bean(name = "error")
  @ConditionalOnMissingBean(name = "error")
  public View defaultErrorView() {
   return this.defaultErrorView;
  }

  // If the user adds @EnableWebMvc then the bean name view resolver from
  // WebMvcAutoConfiguration disappears, so add it back in to avoid disappointment.
  @Bean
  @ConditionalOnMissingBean
  public BeanNameViewResolver beanNameViewResolver() {
   BeanNameViewResolver resolver = new BeanNameViewResolver();
   resolver.setOrder(Ordered.LOWEST_PRECEDENCE - 10);
   return resolver;
  }

 }

```

`server.error.include-exception` 用于实例化一个bean可以获取对应的404发生的时候获取对应的错误信息:

```java
 @Bean
 @ConditionalOnMissingBean(value = ErrorAttributes.class, search = SearchStrategy.CURRENT)
 public DefaultErrorAttributes errorAttributes() {
  return new DefaultErrorAttributes(
    this.serverProperties.getError().isIncludeException());
 }

 @Bean
 @ConditionalOnMissingBean(value = ErrorController.class, search = SearchStrategy.CURRENT)
 public BasicErrorController basicErrorController(ErrorAttributes errorAttributes) {
  return new BasicErrorController(errorAttributes, this.serverProperties.getError(),
    this.errorViewResolvers);
 }

```

- `application.yml`中还需要配置如下信息：

```

spring:
  mvc:
    favicon:
      enabled: false
    throw-exception-if-no-handler-found: true
```

- 重写一个controller实现`ErrorController`, 因为`ErrorMvcAutoConfiguration`会查找所有实现了`ErrorController` 的bean，如果没有就使用自己的`BasicErrorController`:

```java
@Bean
 @ConditionalOnMissingBean(value = ErrorController.class, search = SearchStrategy.CURRENT)
 public BasicErrorController basicErrorController(ErrorAttributes errorAttributes) {
  return new BasicErrorController(errorAttributes, this.serverProperties.getError(),
    this.errorViewResolvers);
 }

```

所以重写的一个自定义的ErrorController如下：

```java

/**
 * @author Walter
 * @see org.springframework.boot.autoconfigure.web.servlet.error.ErrorMvcAutoConfiguration
 * @see org.springframework.boot.autoconfigure.web.ErrorProperties
 * @see org.springframework.boot.autoconfigure.web.ServerProperties
 */
@RestController
@Slf4j
public class GlobalNotFoundErrorController implements ErrorController {
    private static final String PATH = "/error";

    private ErrorAttributes errorAttributes;

    public GlobalNotFoundErrorController(ErrorAttributes errorAttributes) {
        this.errorAttributes = errorAttributes;
    }

    @Override
    public String getErrorPath() {
        return PATH;
    }

    @RequestMapping(value = PATH)
    public WebResponse handle404Exception(HttpServletRequest request) {
        WebResponse response = WebResponse.getResponse();
        final String requestURI = request.getRequestURI();
        WebRequest webRequest = new ServletWebRequest(request);
        Map<String, Object> body = errorAttributes.getErrorAttributes(webRequest, true);
        log.error("没有找到请求地址: {},异常返回结果: {}", requestURI, body);
        /* int internalStatusCode = (int) body.get("active"); */
        body.remove("active");
        body.remove("timestamp");
        body.remove("message");
//        HttpStatus active = getStatus(request);
        response.fail(WebResponseCode.FAILED, body, requestURI);
        return response;
    }
}

```

## springboot 异步/多线程处理 async

### 多线程的几个概念

- coreSize 核心线程 ，这里设置为 **8**
- queueCapacity 当核心线程都在跑任务，还有多余的任务会存到此处，这里设置为 **20**
- maxSize 如果queueCapacity存满了，还有任务就会启动更多的线程，直到线程数达到maxPoolSize。如果还有任务，则根据拒绝策略进行处理。
，这里设置为 **15** ，超过将会按照**拒绝策略**进行处理
- keepAlive 线程存活时间

> 所以以上的设置，保证了最大只有15个线程在跑任务

1. 当线程数量<8的时候，如果有新的线程需要执行，则以前的线程不会销毁重复利用，直到启动的线程达到8个的时候，才会重复利用核心线程
2. 也就是说如果启动的线程是<=28个，总运行这28的线程的一直是线程池中的8个核心线程交替执行这些线程。
1. 当启动的线程>28个，此时启动新的线程,直到总线程数量达到maxSize
2. 当启动的运行总线程> 15个的时候，此处会安装下面的拒绝策略进行处理线程

拒绝策略如下：

1. 由任务调用线程执行   `new ThreadPoolExecutor.CallerRunsPolicy();`
2. 抛异常    `new ThreadPoolExecutor.AbortPolicy();`
3. 多余的直接抛弃   `new ThreadPoolExecutor.DiscardPolicy();`
4. 根据FIFO（先进先出）抛弃队列里任务  `new ThreadPoolExecutor.DiscardOldestPolicy();`

而跟进代码发现：`TaskExecutionAutoConfiguration`类实现了`ThreadPoolTaskExecutor` bean,我一直都是用的是`TaskExecutor`，直到最近我发现这个bean异步操作后不能返回异步的结果。
所以这里推荐的还是使用`ThreadPoolTaskExecutor` 和`AsyncTaskExecutor`,二者都可以返回多线程执行的结果。如下所示：

![async task](./img/async-task.png)

::: warning 空闲的coreSize线程
空闲的线程不占用内存，参考文档：[stackoverflow](https://stackoverflow.com/questions/43795545/is-idle-thread-taking-cpu-execute-time-in-java-executors)
:::

### ThreadPoolTaskExecutor 等待所有的线程执行完成 `future.get()`

```java

@Service
@Slf4j
public class AsyncService {

    @Autowired
    private ThreadPoolTaskExecutor taskExecutor;

    public void longTask() throws ExecutionException, InterruptedException {
        List<ListenableFuture<Integer>> alllist = Lists.newArrayList();
        IntStream.range(0, 200).forEach(intValue->{
            ListenableFuture<Integer> thread = taskExecutor.submitListenable(() -> {
                String name = Thread.currentThread().getName();
                log.info("线程： {}", name);
                Thread.sleep(5 * 1000);
                log.info("结束: {}", name);
                return intValue;
            });
            alllist.add(thread);
        });
        log.info("Waiting for everything to finish...");
        for (ListenableFuture<Integer> future : alllist) {
            // 此处的get方法会等待该线程执行完成
            Integer threadIndex = future.get();
            log.info("thread: {}, is done: {}", threadIndex, future.isDone());
        }

    }
}

```

## Unit测试中`ThreadPoolTaskExecutor`中任务退出

> 因为@Test中的主线程已经退出，所以其他的异步线程池不能继续进行。

## springboot jar vs tomcat war

Hence the famous:

> 'Make JAR, not WAR.' — Josh Long

## 配置`RestTemplate`支持更多的数据类型转换

在请求http的时候，可能返回的不会是通常的json类型，就是application/json，这种方式我们采用springboot类型的RestTemplate会报错，找不到对应的ResponseType对应的转换器，所以下面的配置可以采用`MappingJackson2HttpMessageConverter`转换所有的数据类型：

```java
  @Bean
    public RestTemplate restTemplate(RestTemplateBuilder builder) {
        RestTemplate restTemplate = builder.build();
        List<HttpMessageConverter<?>> messageConverters = restTemplate.getMessageConverters();
        //放到第一个,使得以前的配置不生效
        MappingJackson2HttpMessageConverter jackson2HttpMessageConverter = new MappingJackson2HttpMessageConverter();
        jackson2HttpMessageConverter.setSupportedMediaTypes(Lists.newArrayList(
                MediaType.APPLICATION_JSON,
                MediaType.APPLICATION_JSON_UTF8,
                // 支持所有的返回JSON数据,数据类型可以反序列化：  Content-Type: text/javascript;charset=utf-8
                // 不再使用，因为可能会引起其他的意外问题，反序列化最好转为String.class,不要使用Map.class 或者List.class
                MediaType.ALL
        ));
        jackson2HttpMessageConverter.setObjectMapper(JacksonUtils.getObjectMapper());
        jackson2HttpMessageConverter.setPrettyPrint(false);
        messageConverters.removeIf(m -> m.getClass().getName().equals(MappingJackson2HttpMessageConverter.class.getName()));
        messageConverters.add(0, jackson2HttpMessageConverter);

        return restTemplate;
    }

```

## springboot application.yml配置integer变量

参考： <https://blog.csdn.net/blueheart20/article/details/81480864>

```

Failed to bind properties under 'dubbo.protocol.port' to java.lang.Integer:

    Property: dubbo.protocol.port
    Value: (java.lang.Integer)${server.port}
    Origin: class path resource [application.yml]:136:11
    Reason: failed to convert java.lang.String to java.lang.Integer

```

这些变量字符在进行maven的`clean install`的时候回替换成对应的变量，可以通过执行maven的`clean install`命令后采用解压缩包打开对应的war查看
对应的`application.yml`中的配置，会发现里面的变量已经被替换。 在`pom.xml`中进行如下配置：

```
 <resources>
        <resource>
            <directory>src/main/resources</directory>
            <filtering>true</filtering>
        </resource>
</resources>
```

## Cacheable注解

- org.springframework.cache.interceptor.CacheInterceptor
- org.springframework.cache.interceptor.CacheInterceptor#invoke
- org.springframework.cache.interceptor.CacheAspectSupport#execute(org.springframework.cache.interceptor.CacheOperationInvoker, java.lang.Object, java.lang.reflect.Method, java.lang.Object[])

- org.springframework.cache.interceptor.CacheAspectSupport#execute(org.springframework.cache.interceptor.CacheOperationInvoker, java.lang.reflect.Method, org.springframework.cache.interceptor.CacheAspectSupport.CacheOperationContexts)

核心代码

```java
        if (contexts.isSynchronized()) {
   CacheOperationContext context = contexts.get(CacheableOperation.class).iterator().next();
   if (isConditionPassing(context, CacheOperationExpressionEvaluator.NO_RESULT)) {
    Object key = generateKey(context, CacheOperationExpressionEvaluator.NO_RESULT);
    Cache cache = context.getCaches().iterator().next();
    try {
     return wrapCacheValue(method, cache.get(key, () -> unwrapReturnValue(invokeOperation(invoker))));
    }
    catch (Cache.ValueRetrievalException ex) {
     // The invoker wraps any Throwable in a ThrowableWrapper instance so we
     // can just make sure that one bubbles up the stack.
     throw (CacheOperationInvoker.ThrowableWrapper) ex.getCause();
    }
   }
   else {
    // No caching required, only call the underlying method
    return invokeOperation(invoker);
   }
  }

```

进入redis中的缓存获取：`org.springframework.data.redis.cache.RedisCache#get`,这个是redis与数据库封装的类，还有参考类: `org.springframework.cache.support.AbstractValueAdaptingCache#get(java.lang.Object)` 这个是redis的相关操作类

```java
    public synchronized <T> T get(Object key, Callable<T> valueLoader) {

  ValueWrapper result = get(key);

  if (result != null) {
   return (T) result.get();
  }

  T value = valueFromLoader(key, valueLoader);
  put(key, value);
  return value;
 }

```
