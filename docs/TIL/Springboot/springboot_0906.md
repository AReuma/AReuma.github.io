---
layout: default
title: 23.09.06 TIL
parent: TIL
---

# 23.09.06 TIL: DTO/VO/Entity 


> 🗓 날짜 : 2023.09.06   
> 📚 할 일 : 개인 프로젝트 진행, 블로그 작성하기, 강의듣기   
> 📝 오늘의 목표:  강의 완강, [SELLMS], [SEELP] 진행   
> ⌛ 공부시간 : 9:30 ~

  
&nbsp;

## 1. DTO/VO/Entity
  
### DTO: 데이터 전달용
Data Transfer Object  
순수하게 데이터를담아 계층 간으로 전달히는 객체  
getter와 setter를 제외하고 다른 로직을 갖지않는 객체  
  
전달 할 내용을 담아서 전달되기때문에 다른 로직은 굳이 필요가 없다.  
    
```java
@RequiredArgsConstructor
@Getter
public class FindIdPwResponseDto {

    private final String num;

    private final String email;

    private final String socialType;
}
```

### VO: 값 표현용
Value Object  
값 그자체를 나타내는 객체  
값으로만 비교하는 객체  
DTO와 다르게 로직을 포함할 수 있다.  

![timeVO.png](/assets/images/TIL/springboot/0906/timeVO.png)
&nbsp;
  
VO는 값으로만 비교하기때문에 속성이 같으면 두 인스턴스는 같은 인스턴스이다.  
  
즉, 똑같은 속성인 인스턴스를 비교하면 항상 참이 나와야한다.  
테스트 코드를 작성해서 확인하면 실패가 나온다.  

![timeVOTestFail.png](/assets/images/TIL/springboot/0906/timeVOTestFail.png)  
&nbsp;
  
그래서 값만 비교할 수 있도록 equals()와 hasCode()를 오버라이딩해줘야한다.  
![timeVO-override.png](/assets/images/TIL/springboot/0906/timeVO-override.png)
&nbsp;
  
![timeVOTestSuccess.png](/assets/images/TIL/springboot/0906/timeVOTestSuccess.png)  
&nbsp;  
  
### Entity
실제 DB의 테이블과 매핑되는 클래스  
id를 통해 각각의 엔티티를 구분한다.  


![entity-image.png](/assets/images/TIL/springboot/0906/entity-image.png)
&nbsp;

## 2. DTO를 사용하는 이유  
  
DTO를 생성하지 않고 엔티티로 데이터를 주고받게 되면, 앤티티에 API 검증을 위한 로직이 들어가야한다.  
하나의 엔티티를 위한 API가 많이 만들어지는데 그 요청 사항을 하나의 엔티티에 담기는 어렵다.  
또 엔티티가 변경되면 API 스펙이 변경된다.  
  
그래서 DTO를 사용해서 데이터를 주고받는다. 

  
## 3. VO와 Entity의 차이점
  
VO는 값 자체를 표현하는 용도라 **불변 객체**이다.  
생성 후 상태 변경이 없다.  
  
Entity는 **가변 객체**로 생성 후 상태를 변경할 수 있다.  

|          | DTO                  | VO          | Entity           |
|----------|----------------------|-------------|------------------|
| 용도       | 레이어간의 데이터 전송         | 의미 있는 값을 표현 | DB 테이블과 매핑되는 클래스 |
| 가변/불변    | 가변객체 (setter가 있을 경우) | 불변객체        | 가변객체             |
| 로직 포함 여부 | 포함 불가능               | 포함 가능       | 포함 가능            |


## 3. 변경 감지와 병합 (merge) 
  
### 준영속성 엔티티  
영속성 컨텍스트가 관리 하지 않는 엔티티. -> JPA가 관리하지 않는 엔티티  
  
영속성 엔티티는 값이 변경이 되면 틀랜잭션 커밋 시점에 변경감지가 동작해서 알아서 쿼리가 실행되지만 준영속성 엔티티는 따로 쿼리를 날리는 조치를 해야한다.  

### 준영속성 엔티티 변경  

1)변경 감지 기능 사용
> 영속성컨텍스트에서 엔티티를 다시 조회해 수정.  
  
2) 병합 사용
> 준영속 엔티티를 영속 상태로 변경해서 사용.  
  
변경 감지를 사용하면 속성을 선택해서 값을 변경할 수 있으나 병합은 모든 속성이 한번에 변경이 된다.
  
&nbsp;
&nbsp;



<hr>
[참고 자료]    

* [실전! 스프링 부트와 JPA 활용2 - API 개발과 성능 최적화](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-JPA-API%EA%B0%9C%EB%B0%9C-%EC%84%B1%EB%8A%A5%EC%B5%9C%EC%A0%81%ED%99%94/dashboard)  
* [https://www.youtube.com/watch?v=J_Dr6R0Ov8E&t=384s](https://www.youtube.com/watch?v=J_Dr6R0Ov8E&t=384s)  
* [https://www.youtube.com/watch?v=z5fUkck_RZM](https://www.youtube.com/watch?v=z5fUkck_RZM)



