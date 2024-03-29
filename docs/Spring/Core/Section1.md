---
layout: default
title: 1. 객체 지향 설계와 스프링_1
parent: 스프링 핵심 원리
grand_parent: Spring
---

# 객체 지향 설계와 스프링_1
  

## 1. 스프링이란?  
  
JAVA를 사용하는 프레임워크  
-> JAVA를 이용해서 웹 사이트를 쉽고 빠르게 개발하기 위한 구조/틀
  
## 2. 스프링이 만들어진 이유
  
스프링은 JAVA 언어 기반의 프레임 워크  
JAVA의 가장 큰 특징은 객체지향 언어  
  
>객체지향의 특징을 살려서 애플리케이션을 개발하기 위해서 만들어 졌다.
  
## 3. 좋은 객체지향 프로그래밍이란?
  
### 1) 객체 지향 프로그래밍이란?  
객체들의 모임으로, 각각의 객체들의 역할이 무엇인지 정의해 `객체들간의 상호작용`을 통해 프로그램을 만드는 것을 말함. 
  
### 2) 객체지향의 특징
객체지향의 특징으로는 `추상화`, `캡슐화`, `상속`, `다형성`이 있다.  

#### 추상화란?  
클래스들의 공통적인 특성들을 묶어 표현하는 것.  
### 캡슐화란?  
객체에 필요한 데이터나 기능(메소드)을 책임 있는 객체에 그룹화 시키는 것.  
### 상속  
부모 클래스에 정의된 변수 및 메서드를 자식 클래스에서 상속받아서 사용하는 것.  
-> 중복되는 코드를 없애기 위해서 사용함.  
### 다형성  
다양한 형태로 표현이 가능한것.  
> 오버라이딩  
> 오버로딩
  
객체 지향의 핵심인 다형성  

역활과 구현으로 분리하는거라고 생각하면 된다. 
예를 들어서 운전자(클라이언트)와 자동차가 있다고 하면, 운전자는 자동차가 변경이 되어도 운전 면허증을 다시 취득할 필요가 없다.  
운전자는 자동차의 역할에만 의존을 하고 있는 상태이다.  
운전자는 자동차의 내부가 어떻게 생겨먹어서 앞으로 가는지 몰라도 됨.
  
역할과 구현을 분리하는 이유는 운전자를 위해서 분리를 하는것.  
다형성이 제대로 구현이 된다면 <mark style="background-color: skyblue">클라이언트에게 영향을 주지않고 새로운 기능을 제공 가능해짐.</mark>  
  
### 3) 역할과 구현으로 분리  
역할과 구현으로 분리가 되면  
* 단순해지고 유연해지며 변경이 편리해짐.
* 클라이언트가 대상의 역할만 알면 됨. 
* 클라이언트가 구현대상의 내부 구조를 몰라도 됨. 
* 클라이언트는 구현대상의 내부 구조가 변경 되어도 영향을 받지않음. 
  
  
역할과 구현을 분리하는게 객체를 설계할때 중요하다.  
<mark style="background-color: skyblue">역할: 인터페이스<br/>구현: 인터페이스를 구현한 클래스, 구현 객체</mark>  
  
  
  
<hr>  

![필기1](/assets/images/Spring/core/Section1_1.jpg)  
  

![필기2](/assets/images/Spring/core/Section1_2.jpg)