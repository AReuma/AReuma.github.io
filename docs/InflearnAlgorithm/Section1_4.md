---
layout: default
title: 4. 단어 뒤집기(StringBuilder 이용법 또는 직접 뒤집기)
parent: InflearnAlgorithm
---
# 단어 뒤집기


## 1. StringBuilder와 String의 차이점 
  
### String은 새로운 객체가 계속 만들어짐 
### StringBuilder는 새로운 객체를 만들지 않아도 됨.

``` java
두개의 String 객체를 연산을 할때

String str1 = "abc"; // abc를 변수에 저장한 상태.
String str2 = "def";

String str3 = str1 + str2; // 새로운 String을 생성한다.

그럼 여기서 
String str4 = "abc";
str4 += "def";  // 새로운 String을 생성한건 아니지 않나?



StringBuilder sb = new StringBuilder();
sb.append("abc"); // abc라는 값이 변수에 저장되어있는 상태가 아님. 
sb.append("def");

System.out.println(sb.toString()); // str3보다 str4랑 같은게 아닌가..?
```  

https://developer-talk.tistory.com/774
  
동작 과정에서의 차이점이 있다고 한다.  
이 블로그에 잘 정리 되어있음.  
  
## 2. StringBuilder 클래스 사용법

``` java
StringBuilder sb = new StringBuilder();
sb.append("abc");
sb.append("def");

System.out.println(sb.toString()); //abcdef
```   
  
  

### **1) equals() 문자열 비교**  

``` java
StringBuilder sb = new StringBuilder("Happy");
sb.append("Day");

System.out.println(sb.equals("HappyDay")); // false
System.out.println(sb.toString().equals("HappyDay")); // true
```  
같은 문자열을 비교했을때 첫번째 출력과 두번쨰 출력이 다르게 나온 이유는  
StringBuilder랑 String이랑 비교를 했기 때문.  
  
그래서 비교를 원할때는 StringBuilder로 만든 문자열을 String으로 변환해야함. 


### **2) insert(인덱스, 값) 특정 인덱스에 값을 삽입**
``` java
StringBuilder sb = new StringBuilder("Happy");
sb.insert(1,"Day");

System.out.println(sb); //HDayappy
```  


### **3) delete(시작 인덱스, 마지막 인덱스) 시작 인덱스부터 마지막 인덱스-1까지 깂을 삭제**
``` java
StringBuilder sb = new StringBuilder("HappyDay");
sb.delete(1,5);

System.out.println(sb); //HDay
```  


### **i4) ndexOf(특정문자) 특정 문자의 인덱스 출력**
``` java
StringBuilder sb = new StringBuilder("HappyDay");

System.out.println(sb.indexOf("H"));    //0
```  


### **5) subString(시작 인덱스, 마지막 인덱스) 시작 인덱스부터 마지막인덱스까지 값 자르기**
``` java
StringBuilder sb = new StringBuilder("HappyDay");

System.out.println(sb.substring(1));    //appyDay
System.out.println(sb.substring(0,5));  //Happy
```  


### **6) length() 문자열 길이**
``` java
StringBuilder sb = new StringBuilder("HappyDay");
  
System.out.println(sb.length());    //8
```  


### **7) replace(시작 인덱스, 마지막 인덱스, 값) 시작 인덱스부터 마지막 인덱스-1까지의 값과 변경**
``` java
StringBuilder sb = new StringBuilder("HappyDay");
System.out.println(sb.replace(0, 5, "Reuma"));
```  


### **8) reverse() 글자 순서 뒤집기**
``` java
StringBuilder sb = new StringBuilder("HappyDay");

System.out.println(sb.reverse());   //yaDyppaH
```  
  
