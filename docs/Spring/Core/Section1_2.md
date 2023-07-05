---
layout: default
title: 2. 좋은 객체 지향 설계의 5가지 원칙(SOLID)
parent: Spring
---

# 좋은 객체 지향 설계의 5가지 원칙(SOLID)
  

## 1. SOLID
  
![SOLID.png](/assets/images/Spring/core/Section2_1.png)
  
## 1. SRP: 단일 책임 원칙
  
한 클래스는 하나의 책임만을 가져야한다.  
  
>변경이 있을때 파급 효과가 적을수록 잘 지켜진것이다.
  
## 2. OCP: 개방-폐쇄 원칙

소프트웨어 요소는 확장에는 열려있고 변경에는 닫혀있어야한다.  
인터페이스를 이용해 구현한 경우 새로운 클래스를 만드는건 기존 코드 변경이 아님. 

> 문제점  
> 구현 객체를 변경하면 클라이언트가 코드를 변경해야함. 
``` java
MemberRepository m = new MemoryMemberRepository(); // 기준 코드 
MemberRepository m = new jdbcMemberRepository(); // 변경 코드 
``` 
>다다형성을 이용해서 변경을 하지만 OCP가 깨지는 상황이 발생. 
  
## 3. LSP: 리스코프 치환 원칙
  
다형성에서 하위 클래스는 인터페이스 규약을 지켜야한다.  
컴파일 성공 여부의 문제가 아니라 엑셀을 밟으면 앞으로 이동 등 기본적인 상식을 지켜야함. 

## 4. ISP: 인터페이스 분리 원칙

특정 클라이언트를 위한 인터페이스 여러개가 범용 인터페이스 하나보다 좋다.  

>클라이언트 -> 자동차 -> 정비, 운전  
>인터페이스가 명확해진다.  
> 정비와 운전을 변경해도 클라이언트에는 영향이 없다. 
  
## 5. DIP: 의존 관계 역전 원칙

구체화에 의존하지 않고 추상화에 의존해야하는 원칙  
인터페이스만을 알아야하고 인터페이스를 상속한 것이 어떤 역할을 하는지 세세히 알 필요 없다. 
``` java
MemberRepository m = new MemoryMemberRepository();
// MemberRepository 와 MemoryMemberRepository 둘 다 의존하고 있음. 
``` 

<mark style="background-color: skyblue">다형성만으로는 OCP와 DIP를 지킬 수 없다.</mark>  
### Spirng은 객체지향을 통해서 다형성 + OCP + DIP를 가능하게 한다. 


<hr>  

![필기1](/assets/images/Spring/core/Section2_2.png)  
  

![필기2](/assets/images/Spring/core/Section2_3.jpg)