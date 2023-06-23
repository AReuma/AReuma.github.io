---
layout: default
title: 9. 숫자만 추출
parent: InflearnAlgorithm
---

# 숫자만 추출
  
## Integer.parseInt()
``` java
String str = "0123";

System.out.println(str); //0123
System.out.println(Integer.parseInt(str)); //123
```

문자열을 int 변환

## 2. Character.isDigit(x)
``` java
String str = "01d";

for(char x : str.toCharArray()){
    if(Character.isDigit(x)){
        System.out.println("숫자");
    }else System.out.println("숫자아님");
}
```

특정 문자가 숫자인지 판별
