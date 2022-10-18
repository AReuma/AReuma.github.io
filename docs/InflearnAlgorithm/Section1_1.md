---
layout: default
title: 문자 찾기 
parent: InflearnAlgorithm
---

# 문자 찾기 
  

## toUpperCase 
``` java
string.toUpperCase();
문자열을 대문자로 변환해서 반환 
```  
  
## toLowerCase
``` java
string.toLowerCase();
문자열을 소문자로 변환해서 반환
```
  
## toCharArray
``` java
str.toCharArray();
문자열을 문자로 나눠 char 타입 배열 생성
```

- 예1)
    ``` java
    String str = "Hello World";
    char[] arr = str.toCharArray();
    ```
  
- 예2)
    ~~~ java
    for(char c : str.toCharArray){
        system.out.println(c);
    }
    ~~~
  
## charAt
``` java
string.charAt(index);
문자열을 char 타입으로 한 글자만 받는 함수
```