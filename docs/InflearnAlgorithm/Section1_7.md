---
layout: default
title: 7. 회문문자열
parent: InflearnAlgorithm
---

# 회문문자열
  
## 문자열 비교하기

## string.equals()
``` java
String str1 = "abc";
String str2 = "aBc";

System.out.println(str1.equals("abc")); //true
System.out.println(str1.equals(str2)); //false
```

* #### 비교연산자 **"=="** 와 **"equals()"**의 차이점
* ##### "=="는 비교하는 대상의 주소값을 비교 
* ##### "equals()"는 비교하는 대상의 내용 자체를 비교 

## 2. string.equalsIgnoreCase()
``` java
String str1 = "abc";
String str2 = "aBc";

System.out.println(str1.equalsIgnoreCase(str2)); // true
```

대소문자 구별없이 문자열 비교
