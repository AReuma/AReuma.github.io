---
layout: default
title: Swagger 설정
parent: Bossi
grand_parent: Project
---

# 1. Swagger 란?

 ![logo.png](/assets/images/Project/Bossi/swagger/swagger-logo.png)
 
 
> Open Api Specification(OAS)를 위한 프레임 워크  
> API들이 가지고 있는 specification(스펙/spec/명세)를 관리할 수 있는 프로젝트
  
  
# 2. Swagger 설정
    
## 1) 개발환경    
> spring boot  3.0.4  
> Swagger 3.0.0  
> Java 17  
> Gradle
  
  
## 2) 의존성 추가 
  
* application.ymal 추가 
   
```java
spring:
  mvc:
    path match:
      matching-strategy: ant_path_matcher
```    
    

### Swagger 2.9.2  

* swagger 2.9.2 시도 

![swagger-2.9.2.png](/assets/images/Project/Bossi/swagger/swagger-2.9.2.png)
     
![swagger-ui-2.9.2.png](/assets/images/Project/Bossi/swagger/swagger-ui-2.9.2.png)
  
```java
implementation group: 'io.springfox', name: 'springfox-swagger-ui', version: '2.9.4'
implementation group: 'io.springfox', name: 'springfox-boot-starter', version: '2.9.4'
```

* 에러 발생  

![swagger-error-2.9.2.png](/assets/images/Project/Bossi/swagger/swagger-error-2.9.2.png)
    
* 해결 
> Spring boot 2.6버전 하위 - Swagger 2.x.x  
> Spring boot 2.6버전 상위 - Swagger 3.x.x  
    

### Swagger 3.0.0
    
* swagger 3.0.0 시도  
```java
implementation group: 'io.springfox', name: 'springfox-swagger-ui', version: '3.0.0'
implementation group: 'io.springfox', name: 'springfox-boot-starter', version: '3.0.0'
```
  
  
* 에러 발생 -1   
![whitelabelErrorPage.png](/assets/images/Project/Bossi/swagger/whitelabelErrorPage.png)
      

* 해결 
> Spring boot 3.x.x 부터는 Springfox 대신 Springdoc를 사용해야함. 

```java
//implementation group: 'io.springfox', name: 'springfox-swagger-ui', version: '3.0.0' -> swagger 3.0 이상은 사용x

implementation group: 'io.springfox', name: 'springfox-boot-starter', version: '3.0.0'  
implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.0.2'
``` 
참고 사이트  
https://velog.io/@layl__a/Spring-Boot-3.x-%EB%B2%84%EC%A0%84-%EC%9D%B4%ED%9B%84%EC%97%90%EC%84%9C-Swagger-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94


* 에러 발생 -2  
  
![swagger-validation.png](/assets/images/Project/Bossi/swagger/swagger-validation.png)

* 해결 

```java
implementation 'org.springframework.boot:spring-boot-starter-validation'
```   
참고 사이트
https://stackoverflow.com/questions/36329001/unable-to-create-a-configuration-because-no-bean-validation-provider-could-be-f  


<details>
<summary>에러 코드</summary> 
> jakarta.validation.NoProviderFoundException: Unable to create a Configuration, because no Jakarta Bean Validation provider could be found. Add a provider like Hibernate Validator (RI) to your classpath.
> at jakarta.validation.Validation$GenericBootstrapImpl.configure(Validation.java:291) ~[jakarta.validation-api-3.0.2.jar:na]
> at jakarta.validation.Validation.buildDefaultValidatorFactory(Validation.java:103) ~[jakarta.validation-api-3.0.2.jar:na]
> at org.hibernate.cfg.beanvalidation.TypeSafeActivator.getValidatorFactory(TypeSafeActivator.java:479) ~[hibernate-core-6.1.7.Final.jar:6.1.7.Final]
> at org.hibernate.cfg.beanvalidation.TypeSafeActivator.activate(TypeSafeActivator.java:82) ~[hibernate-core-6.1.7.Final.jar:6.1.7.Final]
> at java.base/jdk.internal.reflect.DirectMethodHandleAccessor.invoke(DirectMethodHandleAccessor.java:104) ~[na:na]
> at java.base/java.lang.reflect.Method.invoke(Method.java:577) ~[na:na]
> at org.hibernate.cfg.beanvalidation.BeanValidationIntegrator.integrate(BeanValidationIntegrator.java:137) ~[hibernate-core-6.1.7.Final.jar:6.1.7.Final]
> at org.hibernate.internal.SessionFactoryImpl.<init>(SessionFactoryImpl.java:287) ~[hibernate-core-6.1.7.Final.jar:6.1.7.Final]
> at org.hibernate.boot.internal.SessionFactoryBuilderImpl.build(SessionFactoryBuilderImpl.java:415) ~[hibernate-core-6.1.7.Final.jar:6.1.7.Final]
> at org.hibernate.jpa.boot.internal.EntityManagerFactoryBuilderImpl.build(EntityManagerFactoryBuilderImpl.java:1423) ~[hibernate-core-6.1.7.Final.jar:6.1.7.Final]
> at org.springframework.orm.jpa.vendor.SpringHibernateJpaPersistenceProvider.createContainerEntityManagerFactory(SpringHibernateJpaPersistenceProvider.java:66) ~[spring-orm-6.0.6.jar:6.0.6]
> at org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean.createNativeEntityManagerFactory(LocalContainerEntityManagerFactoryBean.java:376) ~[spring-orm-6.0.6.jar:6.0.6]
> at org.springframework.orm.jpa.AbstractEntityManagerFactoryBean.buildNativeEntityManagerFactory(AbstractEntityManagerFactoryBean.java:409) ~[spring-orm-6.0.6.jar:6.0.6]
> at org.springframework.orm.jpa.AbstractEntityManagerFactoryBean.afterPropertiesSet(AbstractEntityManagerFactoryBean.java:396) ~[spring-orm-6.0.6.jar:6.0.6]
> at org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean.afterPropertiesSet(LocalContainerEntityManagerFactoryBean.java:352) ~[spring-orm-6.0.6.jar:6.0.6]
> at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.invokeInitMethods(AbstractAutowireCapableBeanFactory.java:1808) ~[spring-beans-6.0.6.jar:6.0.6]
> at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1758) ~[spring-beans-6.0.6.jar:6.0.6]
> at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:599) ~[spring-beans-6.0.6.jar:6.0.6]
> at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:521) ~[spring-beans-6.0.6.jar:6.0.6]
> at org.springframework.beans.factory.support.AbstractBeanFactory.lambda$doGetBean$0(AbstractBeanFactory.java:326) ~[spring-beans-6.0.6.jar:6.0.6]
> at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:234) ~[spring-beans-6.0.6.jar:6.0.6]
> at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:324) ~[spring-beans-6.0.6.jar:6.0.6]
> at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:200) ~[spring-beans-6.0.6.jar:6.0.6]
> at org.springframework.context.support.AbstractApplicationContext.getBean(AbstractApplicationContext.java:1132) ~[spring-context-6.0.6.jar:6.0.6]
> at org.springframework.context.support.AbstractApplicationContext.finishBeanFactoryInitialization(AbstractApplicationContext.java:907) ~[spring-context-6.0.6.jar:6.0.6]
> at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:584) ~[spring-context-6.0.6.jar:6.0.6]
> at org.springframework.boot.web.servlet.context.ServletWebServerApplicationContext.refresh(ServletWebServerApplicationContext.java:146) ~[spring-boot-3.0.4.jar:3.0.4]
> at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:732) ~[spring-boot-3.0.4.jar:3.0.4]
> at org.springframework.boot.SpringApplication.refreshContext(SpringApplication.java:434) ~[spring-boot-3.0.4.jar:3.0.4]
> at org.springframework.boot.SpringApplication.run(SpringApplication.java:310) ~[spring-boot-3.0.4.jar:3.0.4]
> at org.springframework.boot.SpringApplication.run(SpringApplication.java:1304) ~[spring-boot-3.0.4.jar:3.0.4]
> at org.springframework.boot.SpringApplication.run(SpringApplication.java:1293) ~[spring-boot-3.0.4.jar:3.0.4]
> at com.example.bossi.BossiApplication.main(BossiApplication.java:11) ~[main/:na]
</details>   
  
* 에러 발생 -3  
    
![swagger-error500.png](/assets/images/Project/Bossi/swagger/swagger-error500.png)

  
* 해결
의존성 추가
```java
implementation group: 'io.swagger.core.v3', name: 'swagger-core', version: '2.2.8'
```
    
참고 사이트  

https://stackoverflow.com/questions/75732794/spring-boot-3-and-swagger-ui-java-lang-nosuchmethoderror-io-swagger-v3-oas-ann

<details>
<summary>에러 코드</summary>   

> java.lang.NoSuchMethodError: 'boolean io.swagger.v3.oas.models.media.Schema.getExampleSetFlag()'
> at io.swagger.v3.core.jackson.SchemaSerializer.serialize(SchemaSerializer.java:35) ~[swagger-core-jakarta-2.2.7.jar:2.2.7]
> at io.swagger.v3.core.jackson.SchemaSerializer.serialize(SchemaSerializer.java:13) ~[swagger-core-jakarta-2.2.7.jar:2.2.7]
> at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider._serialize(DefaultSerializerProvider.java:480) ~[jackson-databind-2.14.2.jar:2.14.2]
> at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:319) ~[jackson-databind-2.14.2.jar:2.14.2]
> at com.fasterxml.jackson.databind.ObjectWriter$Prefetch.serialize(ObjectWriter.java:1572) ~[jackson-databind-2.14.2.jar:2.14.2]
> at com.fasterxml.jackson.databind.ObjectWriter._writeValueAndClose(ObjectWriter.java:1273) ~[jackson-databind-2.14.2.jar:2.14.2]
> at com.fasterxml.jackson.databind.ObjectWriter.writeValueAsString(ObjectWriter.java:1140) ~[jackson-databind-2.14.2.jar:2.14.2]
> at io.swagger.v3.core.util.Json.pretty(Json.java:24) ~[swagger-core-jakarta-2.2.7.jar:2.2.7]
> at io.swagger.v3.core.jackson.ModelResolver.clone(ModelResolver.java:937) ~[swagger-core-jakarta-2.2.7.jar:2.2.7]
> at io.swagger.v3.core.jackson.ModelResolver.resolve(ModelResolver.java:656) ~[swagger-core-jakarta-2.2.7.jar:2.2.7]
> at org.springdoc.core.converters.AdditionalModelsConverter.resolve(AdditionalModelsConverter.java:155) ~[springdoc-openapi-starter-common-2.0.2.jar:2.0.2]
> at org.springdoc.core.converters.FileSupportConverter.resolve(FileSupportConverter.java:69) ~[springdoc-openapi-starter-common-2.0.2.jar:2.0.2]
> at org.springdoc.core.converters.ResponseSupportConverter.resolve(ResponseSupportConverter.java:79) ~[springdoc-openapi-starter-common-2.0.2.jar:2.0.2]
> at org.springdoc.core.converters.SchemaPropertyDeprecatingConverter.resolve(SchemaPropertyDeprecatingConverter.java:92) ~[springdoc-openapi-starter-common-2.0.2.jar:2.0.2]
> at org.springdoc.core.converters.PolymorphicModelConverter.resolve(PolymorphicModelConverter.java:77) ~[springdoc-openapi-starter-common-2.0.2.jar:2.0.2]
> at org.springdoc.core.converters.PageableOpenAPIConverter.resolve(PageableOpenAPIConverter.java:93) ~[springdoc-openapi-starter-common-2.0.2.jar:2.0.2]
> at org.springdoc.core.converters.SortOpenAPIConverter.resolve(SortOpenAPIConverter.java:83) ~[springdoc-openapi-starter-common-2.0.2.jar:2.0.2]
> at io.swagger.v3.core.converter.ModelConverterContextImpl.resolve(ModelConverterContextImpl.java:97) ~[swagger-core-jakarta-2.2.7.jar:2.2.7]
> at io.swagger.v3.core.converter.ModelConverters.resolveAsResolvedSchema(ModelConverters.java:110) ~[swagger-core-jakarta-2.2.7.jar:2.2.7]
> at org.springdoc.core.utils.SpringDocAnnotationsUtils.extractSchema(SpringDocAnnotationsUtils.java:122) ~[springdoc-openapi-starter-common-2.0.2.jar:2.0.2]
> at org.springdoc.core.service.GenericParameterService.calculateSchema(GenericParameterService.java:373) ~[springdoc-openapi-starter-common-2.0.2.jar:2.0.2]
> at org.springdoc.core.service.RequestBodyService.buildRequestBody(RequestBodyService.java:281) ~[springdoc-openapi-starter-common-2.0.2.jar:2.0.2]
> at org.springdoc.core.service.RequestBodyService.calculateRequestBodyInfo(RequestBodyService.java:257) ~[springdoc-openapi-starter-common-2.0.2.jar:2.0.2]
> at org.springdoc.core.service.AbstractRequestService.build(AbstractRequestService.java:343) ~[springdoc-openapi-starter-common-2.0.2.jar:2.0.2]
> at org.springdoc.api.AbstractOpenApiResource.calculatePath(AbstractOpenApiResource.java:504) ~[springdoc-openapi-starter-common-2.0.2.jar:2.0.2]
> at org.springdoc.api.AbstractOpenApiResource.calculatePath(AbstractOpenApiResource.java:664) ~[springdoc-openapi-starter-common-2.0.2.jar:2.0.2]
> at org.springdoc.webmvc.api.OpenApiResource.lambda$calculatePath$11(OpenApiResource.java:235) ~[springdoc-openapi-starter-webmvc-api-2.0.2.jar:2.0.2]
> at java.base/java.util.Optional.ifPresent(Optional.java:178) ~[na:na]
> at org.springdoc.webmvc.api.OpenApiResource.calculatePath(OpenApiResource.java:216) ~[springdoc-openapi-starter-webmvc-api-2.0.2.jar:2.0.2]
> at org.springdoc.webmvc.api.OpenApiResource.lambda$getPaths$2(OpenApiResource.java:186) ~[springdoc-openapi-starter-webmvc-api-2.0.2.jar:2.0.2]
> at java.base/java.util.Optional.ifPresent(Optional.java:178) ~[na:na]
> at org.springdoc.webmvc.api.OpenApiResource.getPaths(OpenApiResource.java:165) ~[springdoc-openapi-starter-webmvc-api-2.0.2.jar:2.0.2]
> at org.springdoc.api.AbstractOpenApiResource.getOpenApi(AbstractOpenApiResource.java:366) ~[springdoc-openapi-starter-common-2.0.2.jar:2.0.2]
> at org.springdoc.webmvc.api.OpenApiResource.openapiJson(OpenApiResource.java:140) ~[springdoc-openapi-starter-webmvc-api-2.0.2.jar:2.0.2]
> at org.springdoc.webmvc.api.OpenApiWebMvcResource.openapiJson(OpenApiWebMvcResource.java:117) ~[springdoc-openapi-starter-webmvc-api-2.0.2.jar:2.0.2]
> at java.base/jdk.internal.reflect.DirectMethodHandleAccessor.invoke(DirectMethodHandleAccessor.java:104) ~[na:na]
> at java.base/java.lang.reflect.Method.invoke(Method.java:577) ~[na:na]
> at org.springframework.web.method.support.InvocableHandlerMethod.doInvoke(InvocableHandlerMethod.java:207) ~[spring-web-6.0.6.jar:6.0.6]
> at org.springframework.web.method.support.InvocableHandlerMethod.invokeForRequest(InvocableHandlerMethod.java:152) ~[spring-web-6.0.6.jar:6.0.6]
> at org.springframework.web.servlet.mvc.method.annotation.ServletInvocableHandlerMethod.invokeAndHandle(ServletInvocableHandlerMethod.java:117) ~[spring-webmvc-6.0.6.jar:6.0.6]
> at org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter.invokeHandlerMethod(RequestMappingHandlerAdapter.java:884) ~[spring-webmvc-6.0.6.jar:6.0.6]
> at org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter.handleInternal(RequestMappingHandlerAdapter.java:797) ~[spring-webmvc-6.0.6.jar:6.0.6]
> at org.springframework.web.servlet.mvc.method.AbstractHandlerMethodAdapter.handle(AbstractHandlerMethodAdapter.java:87) ~[spring-webmvc-6.0.6.jar:6.0.6]
> at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:1081) ~[spring-webmvc-6.0.6.jar:6.0.6]
> at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:974) ~[spring-webmvc-6.0.6.jar:6.0.6]
> at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:1011) ~[spring-webmvc-6.0.6.jar:6.0.6]
> at org.springframework.web.servlet.FrameworkServlet.doGet(FrameworkServlet.java:903) ~[spring-webmvc-6.0.6.jar:6.0.6]
> at jakarta.servlet.http.HttpServlet.service(HttpServlet.java:705) ~[tomcat-embed-core-10.1.5.jar:6.0]
> at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:885) ~[spring-webmvc-6.0.6.jar:6.0.6]
> at jakarta.servlet.http.HttpServlet.service(HttpServlet.java:814) ~[tomcat-embed-core-10.1.5.jar:6.0]
> at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:223) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:158) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.tomcat.websocket.server.WsFilter.doFilter(WsFilter.java:53) ~[tomcat-embed-websocket-10.1.5.jar:10.1.5]
> at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:185) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:158) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:110) ~[spring-web-6.0.6.jar:6.0.6]
> at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:185) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:158) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.springframework.web.servlet.resource.ResourceUrlEncodingFilter.doFilter(ResourceUrlEncodingFilter.java:66) ~[spring-webmvc-6.0.6.jar:6.0.6]
> at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:185) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:158) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.springframework.security.web.FilterChainProxy.lambda$doFilterInternal$3(FilterChainProxy.java:231) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:365) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.access.intercept.AuthorizationFilter.doFilter(AuthorizationFilter.java:100) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.access.ExceptionTranslationFilter.doFilter(ExceptionTranslationFilter.java:126) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.access.ExceptionTranslationFilter.doFilter(ExceptionTranslationFilter.java:120) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.session.SessionManagementFilter.doFilter(SessionManagementFilter.java:131) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.session.SessionManagementFilter.doFilter(SessionManagementFilter.java:85) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.authentication.AnonymousAuthenticationFilter.doFilter(AnonymousAuthenticationFilter.java:100) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.servletapi.SecurityContextHolderAwareRequestFilter.doFilter(SecurityContextHolderAwareRequestFilter.java:179) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.savedrequest.RequestCacheAwareFilter.doFilter(RequestCacheAwareFilter.java:63) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.authentication.ui.DefaultLogoutPageGeneratingFilter.doFilterInternal(DefaultLogoutPageGeneratingFilter.java:58) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar:6.0.6]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.authentication.ui.DefaultLoginPageGeneratingFilter.doFilter(DefaultLoginPageGeneratingFilter.java:188) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.authentication.ui.DefaultLoginPageGeneratingFilter.doFilter(DefaultLoginPageGeneratingFilter.java:174) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.authentication.AbstractAuthenticationProcessingFilter.doFilter(AbstractAuthenticationProcessingFilter.java:227) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.authentication.AbstractAuthenticationProcessingFilter.doFilter(AbstractAuthenticationProcessingFilter.java:221) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar:6.0.2]
> at com.example.bossi.filter.CustomAuthorizationFilter.checkAccessTokenAndAuthentication(CustomAuthorizationFilter.java:103) ~[main/:na]
> at com.example.bossi.filter.CustomAuthorizationFilter.doFilterInternal(CustomAuthorizationFilter.java:72) ~[main/:na]
> at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar:6.0.6]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.authentication.AbstractAuthenticationProcessingFilter.doFilter(AbstractAuthenticationProcessingFilter.java:227) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.authentication.AbstractAuthenticationProcessingFilter.doFilter(AbstractAuthenticationProcessingFilter.java:221) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.oauth2.client.web.OAuth2AuthorizationRequestRedirectFilter.doFilterInternal(OAuth2AuthorizationRequestRedirectFilter.java:181) ~[spring-security-oauth2-client-6.0.2.jar:6.0.2]
> at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar:6.0.6]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.authentication.logout.LogoutFilter.doFilter(LogoutFilter.java:107) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.authentication.logout.LogoutFilter.doFilter(LogoutFilter.java:93) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.web.filter.CorsFilter.doFilterInternal(CorsFilter.java:91) ~[spring-web-6.0.6.jar:6.0.6]
> at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar:6.0.6]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.header.HeaderWriterFilter.doHeadersAfter(HeaderWriterFilter.java:90) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.header.HeaderWriterFilter.doFilterInternal(HeaderWriterFilter.java:75) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar:6.0.6]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.context.SecurityContextHolderFilter.doFilter(SecurityContextHolderFilter.java:82) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.context.SecurityContextHolderFilter.doFilter(SecurityContextHolderFilter.java:69) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.context.request.async.WebAsyncManagerIntegrationFilter.doFilterInternal(WebAsyncManagerIntegrationFilter.java:62) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar:6.0.6]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.session.DisableEncodeUrlFilter.doFilterInternal(DisableEncodeUrlFilter.java:42) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar:6.0.6]
> at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:374) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.FilterChainProxy.doFilterInternal(FilterChainProxy.java:233) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.security.web.FilterChainProxy.doFilter(FilterChainProxy.java:191) ~[spring-security-web-6.0.2.jar:6.0.2]
> at org.springframework.web.filter.DelegatingFilterProxy.invokeDelegate(DelegatingFilterProxy.java:352) ~[spring-web-6.0.6.jar:6.0.6]
> at org.springframework.web.filter.DelegatingFilterProxy.doFilter(DelegatingFilterProxy.java:268) ~[spring-web-6.0.6.jar:6.0.6]
> at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:185) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:158) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.springframework.web.filter.RequestContextFilter.doFilterInternal(RequestContextFilter.java:100) ~[spring-web-6.0.6.jar:6.0.6]
> at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar:6.0.6]
> at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:185) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:158) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.springframework.web.filter.FormContentFilter.doFilterInternal(FormContentFilter.java:93) ~[spring-web-6.0.6.jar:6.0.6]
> at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar:6.0.6]
> at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:185) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:158) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:201) ~[spring-web-6.0.6.jar:6.0.6]
> at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:116) ~[spring-web-6.0.6.jar:6.0.6]
> at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:185) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:158) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:177) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:97) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:542) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:119) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:92) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:78) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:357) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.coyote.http11.Http11Processor.service(Http11Processor.java:400) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.coyote.AbstractProcessorLight.process(AbstractProcessorLight.java:65) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.coyote.AbstractProtocol$ConnectionHandler.process(AbstractProtocol.java:859) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.tomcat.util.net.NioEndpoint$SocketProcessor.doRun(NioEndpoint.java:1734) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.tomcat.util.net.SocketProcessorBase.run(SocketProcessorBase.java:52) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.tomcat.util.threads.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1191) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.tomcat.util.threads.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:659) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at org.apache.tomcat.util.threads.TaskThread$WrappingRunnable.run(TaskThread.java:61) ~[tomcat-embed-core-10.1.5.jar:10.1.5]
> at java.base/java.lang.Thread.run(Thread.java:833) ~[na:na]
</details>  

## 3) 접속 사이트 
> http://localhost:{port}/swagger-ui/index.html
    
## 4) Swagger Config 설정 
```java
@Configuration
public class SwaggerConfig {
    private static final String API_NAME = "Bossi API";
    private static final String API_VERSION = "0.1";
    private static final String API_DESCRIPTION = "Bossi 웹 어플리케이션 API입니다.";

    @Bean
    public Docket api() {
        return new Docket(DocumentationType.OAS_30)
                .apiInfo(apiInfo())
                .select()
                .apis(RequestHandlerSelectors.basePackage("com.example.bossi"))
                .paths(PathSelectors.any())
                .build();
    }

    private ApiInfo apiInfo() {
        return new ApiInfoBuilder()
                .title(API_NAME)
                .description(API_DESCRIPTION)
                .version(API_DESCRIPTION)
                .build();
    }
}
```

![swagger-ui.png](/assets/images/Project/Bossi/swagger/swagger-ui-error.png)

* 에러 발생 
ApiInfoVuilder()를 통해 API에 대한 정보를 설정 시도함.  
Swagger 상단의 제목, 버전, 설명을 추가했으나 접속했을때 보이지않는 에러가 발생함. 
    
* 에러 해결 
OpenAPI been 등록해서 제목, 버전, 설명을 추가함. 
    
![swagger-ui.png](/assets/images/Project/Bossi/swagger/swagger-ui.png)
```java
@Configuration
public class SwaggerConfig {
    private static final String API_NAME = "Bossi API";
    private static final String API_VERSION = "0.0.1";
    private static final String API_DESCRIPTION = "Bossi 웹 어플리케이션 API입니다.";

    @Bean
    public Docket api() {
        return new Docket(DocumentationType.OAS_30)
                //.apiInfo(apiInfo())
                .select()
                .apis(RequestHandlerSelectors.basePackage("com.example.bossi"))
                .paths(PathSelectors.any())
                .build();
    }

    @Bean
    public OpenAPI openAPI(){
        Info info = new Info()
                .title(API_NAME)
                .version(API_VERSION)
                .description(API_DESCRIPTION)
                .contact(new Contact().url("https://areuma.github.io/").email("kuuniin@gmail.com"))
                ;

        return new OpenAPI().components(new Components()).info(info);
    }
}
```