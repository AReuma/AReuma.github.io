---
layout: default
title:  Builder 패턴으로 인한 NullPointerException 
parent: Issue
---

# Builder 패턴으로 인한 NullPointerException

## <span style="background-color:skyblue; color: white">Reason</span>
![NullPointerException.png](/assets/images/Issue/Issue6/NullPointerException.png)
    
Product 클래스에 있는 ProductOptionList에 값을 추가할때 NullPointerException 발생.  
  



## <span style="background-color:pink; color: white"> Solution </span> 
  
빌더 패턴을 이용하면 미리 지정해준 값을 무시하고 자동초기값으로 생성이 된다.  
  
엔티티에서 new ArrayList로 초기화 했으나 무시했기때문에 NullPointerException 발생.  

### 해결방법 1  
  
![builderDefault.png](/assets/images/Issue/Issue6/builderDefault.png)
  
  
### 해별방법 2  
  
![createProduct.png](/assets/images/Issue/Issue6/createProduct.png)
<hr/>  

[참고블로그](https://bbeomgeun.tistory.com/174#%ED%--%B-%EB%-E%--%EC%-A%A-%--%ED%--%--%EB%--%-C%--%EC%B-%--%EA%B-%B-%ED%--%--)  

