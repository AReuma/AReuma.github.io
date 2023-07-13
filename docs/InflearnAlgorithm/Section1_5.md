---
layout: default
title: 특정 문자 뒤집기
parent: InflearnAlgorithm
---

# 특정 문자 뒤집기


## 1. Character.isAlphabetic()
``` java
System.out.print(Character.isAlphabetic('a'));   //true
System.out.print(Character.isAlphabetic('가'));   //true
System.out.print(Character.isAlphabetic('#'));   //false
System.out.print(Character.isAlphabetic(2));   //false
```

특정 값이 문자인지 판별 
* 알파벳과 특수문자는 구별 가능
* 알파벳과 한글은 구별 불가능

## 2. String.valueOf()
``` java
String answer = "";
char[] s = {'a', 'b', 'c'};

answer = String.valueOf(s);

System.out.print(answer);   //abc
```

특정 값을 문자열로 변환
