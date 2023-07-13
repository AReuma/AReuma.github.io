---
layout: default
title: 대소문자 변환
parent: InflearnAlgorithm
---

# 대소문자 변환


## 1. Character 클래스 
  
### 문자 데이터에 대한 다양한 처리를 위한 상수 및 메서드를 제공 
  

## 2. Character.isLowerCase()
``` java
char c = 'a';

System.out.print(Character.isLowerCase(c));   //true
```

문자가 소문자인지 판별

## 3. Character.isUpperCase()
``` java
char c = 'a';

System.out.print(Character.isUpperCase(c));   //false
```

문자가 대문자인지 판별

## 4. Character.toUpperCase()
``` java
char c = 'a';

System.out.print(Character.toUpperCase(c)); //A
```

문자를 대문자로 변환

## 5. Character.toLowerCase()
``` java
char c = 'A';

System.out.print(Character.toLowerCase(c)); //a
```

문자를 소문자로 변환