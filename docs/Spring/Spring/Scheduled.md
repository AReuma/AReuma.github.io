---
layout: default
title: @Scheduled를 이용해 일정 시간마다 실행하기
parent: Spring,Springboot
grand_parent: Spring
---

# @Scheduled 
  
프로젝트를 진행하면서 어떤 시간이 지나면 delete 쿼리를 날리도록 구현하고 싶었다.   
인터넷에 찾아보니 @Scheduled 어노테이션을 사용하면 된다고 한다.  
  
## 1. @Scheduled란?  
메서드나 클래스를 정기적으로 실행 할 수 있도록 해주는 어노테이션  
  
```java
@Scheduled(fixedRate = 1000)
public void scheduledMethod(){
    // 정기적으로 실행할 작업
}
```  
  
@Scheduled 속성을 가지고 언제 메서드가 실행할지 정할 수 있다.  
  
## 2. @Scheduled 속성  
  
### 1) fixedRate   
  

````java
@Scheduled(fixedRate = 1000) // 1초마다 실행됨 
public void scheduledMethod(){
    // 정기적으로 실행할 작업
}
````  
  
ms 단위  
fixedRate는 이전 작업의 시작 시점으로부터 정의 된 시간이 지난 후 작업을 실행  



### 2) fixedDelay


````java
@Scheduled(fixedDelay = 1000) // 1초마다 실행됨 
public void scheduledMethod(){
    // 정기적으로 실행할 작업
}
````  

ms 단위  
fixedDelay는 이전 작업의 끝난 시점으로부터 정의 된 시간이 지난 후 작업을 실행  


### 3) fixedDelayString


````java
@Scheduled(fixedDelayString = "1000") // 1초마다 실행됨 
public void scheduledMethod(){
    // 정기적으로 실행할 작업
}
````  

fixedDelay와 실행은 같지만 문자열로 시간을 표현한다.  


### 4) fixedRateString


````java
@Scheduled(fixedRateString = 1000) // 1초마다 실행됨 
public void scheduledMethod(){
    // 정기적으로 실행할 작업
}
````  

fixedRate와 실행은 같지만 문자열로 시간을 표현한다.


### 5) initialDelay


````java
@Scheduled(fixedRate = 1000, initialDelay = 3000) // 1초마다 실행됨 
public void scheduledMethod(){
    // 정기적으로 실행할 작업
}
````  

ms 단위  
initialDelay는 스케줄러에서 메서드가 등록되자마자 수행하는게 아니라 초기 지연시간을 지정하는것    


### 6) initialDelayString


````java
@Scheduled(fixedRate = 1000) // 1초마다 실행됨 
public void scheduledMethod(){
    // 정기적으로 실행할 작업
}
````  

initialDelay와 실행은 같지만 문자열로 시간을 표현한다.  


### 7) cron


````java
@Scheduled(cron = "* * * * * *") // 1초마다 실행됨 
public void scheduledMethod(){
    // 정기적으로 실행할 작업
}
````  

@Scheduled(cron = 초 분 시간 일 월 요일)  
  

  
## 3. @Scheduled 사용법  
  
```java
@EnableScheduling
@SpringBootApplication(exclude = SecurityAutoConfiguration.class)
public class BossiApplication {

	public static void main(String[] args) {
		SpringApplication.run(BossiApplication.class, args);
	}

}
```    
Application Class에 @EnableScheduling 어노테이션을 추가  
  

  
```java
@Service
@RequiredArgsConstructor
public class DataCleanupScheduler {
    private final ManagerService managerService;

    @Scheduled(cron = "0 0 0 * * *") // 매일 12시에 실행됨.
    public void cleanupExpireDate() {
        managerService.call();
    }
}
```  
  
스케줄링 할 클래스를 만들어서 작업을 설정하면 된다.  
@Service나 @Component 어노테이션을 사용해서 스프링 빈에 등록되도록 해야한다.  
사용하지 않으면 스프링이 관리하지않게 되어서 실행이 되지 않는다.  
  
  
## 4. 실행 중 발생한 에러    

[@Scheduled 사용 시 @Transactional 메소드 사용으로 인한 에러](https://areuma.github.io/docs/Issue/issue5/)

  
&nbsp;
<hr/>  

[참고 자료]  

[https://dev-coco.tistory.com/176](https://dev-coco.tistory.com/176)  
