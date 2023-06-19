---
layout: default
title: 3. 문장 속 단어
parent: InflearnAlgorithm
---

# 문자열 자르기
  

## 1. subString()
  
``` java
string.subString(beginIndex, endIndex -1); 
```  

  문자열 시작 인덱스부터 끝 인덱스 -1 까지 잘라 값을 리턴하는 메서드. 
  
  

~~~ java
Strint str = "zottffs";

String result1 = str.subString(0, 2); 
String result2 = str.subString(2); 

system.out.println(result1); // zo
system.out.println(result2); // ttffs
~~~
  
## 2. split()
``` java
string.split("특정문자");
```
  
특정 문자를 기준으로 문자열을 나누어 **배열에** 저장후 리턴하는 메서드 
  
  
  ``` java
  String str = "hello java";

  String[] s = str.split(" ");// 공백으로 문자열 자르기 

  for(String x : s){
    system.out.println(x); 
  }
  ```

## 3. indexOf()
``` java
string.indexOf("특정문자");
string.indexOf("특정문자",beginIndex); 
```

문자나 문자열에서 해당하는 문자의 **처음** 인덱스 값을 반환하고 찾지 못했을 경우 -1을 반환하는 메소드


  ``` java
  String str = "hello java Wolrd";

  System.out.println(str.indexOf("e")); //1
  System.out.println(str.indexOf("l")): //2
  System.out.println(str.indexOf("l", 5); //13
  System.out.println(str.indexOf("t"); //-1
  ```

## 3. lastIndexOf()
``` java
string.lastIndexOf("특정문자");
string.lastIndexOf("특정문자",fromIndex); 
```

문자나 문자열에서 해당하는 문자의 **마지막** 인덱스 값을 반환하고 찾지 못했을 경우 -1을 반환하는 메소드


``` java
String str = "a ab dff ad";
//            012345678910

System.out.println(str.lastIndexOf('a'));   //9
System.out.println(str.lastIndexOf('a', 3));    //2
System.out.println(str.lastIndexOf('j'));   //-1
```