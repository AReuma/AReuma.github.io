---
layout: default
title: 3. 문장 속 단어
parent: InflearnAlgorithm
---

# 문자 자르기
  

## 1. subString 
  
``` java
string.subString(beginIndex, endIndex -1); 
```  

  문자열 시작 인덱스부터 끝 인덱스 -1 까지 자른다. 
  
  

~~~ java
Strint str = "zottffs";

String result1 = str.subString(0, 2); 
String result2 = str.subString(2); 

system.out.println(result1); // zo
system.out.println(result2); // ttffs
~~~
  
## 2. split
``` java
string.split("특정문자");
```
  
특정 문자를 기준으로 문자열 자르기
  
  
  ``` java
  String str = "hello java";

  String[] s = str.split(" ");// 공백으로 문자열 자르기 

  for(String x : s){
    system.out.println(x); 
  }
  ```