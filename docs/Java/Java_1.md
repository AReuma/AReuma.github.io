---
layout: default
title: BufferedReader 와 BufferedWriter
parent: Java
---

# [Java] BufferedReader 와 BufferedWriter 사용법
  

## 1. BufferedReader
  
BufferedReader는 Scanner와 유사하나 처리속도가 더 빠름. 

## 사용법
``` java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
String str = br.readLine(); //String
int n = Integer.parseInt(br.readLine()); //int
```

readLine()은 String 타입으로 값을 리턴한다.  
따라서 다른 값을 받기 위해서는 형 변환이 필수이다.
  
## 2. StringTokenizer  

BufferedReader의 공백 단위로 데이터를 가공하기 위해서 사용되는 클래스

## 방법 1 - StringTokenizer
``` java
StringTokenizer st = new StringTokenizer(str); // str = abcd efgh

String str1 = st.nextToken();
String str2 = st.nextToken();

System.out.println("str1: "+str1); // abcd
System.out.println("str2: "+str2); // efgh
```

## 방법 2 - 특정 문자를 기준으로 자르기
``` java
String[] strArr = str.split(" "); // str = abcd efgh
System.out.println(Arrays.toString(strArr)); // [abce, efgh]
```
  
## 3. BufferedWriter
BufferedWriter는 System.out.println 유사하나 처리속도가 더 빠름.
``` java
bw.write("hello reuma Blog!");
bw.flush();
bw.close();
```

### BufferedWriter 의 경우 버퍼를 잡아 놓았기 때문에 <span style="color: red">flush() / close() 를 반드시 호출해 주어 뒤처리를 해주어야 한다.</span>
호출하지 않을 경우 값이 적히지 않는 오류가 발생함. 