---
layout: default
title: Markdown 마크다운 접기
parent: Markdown
---

# Markdown 접기/ 토글 목록 만들기 
  

마크다운에는 문법이 없어 html details 태그를 이용한다. 


## <span style="background-color:skyblue; color: white">Reason</span>    
접기 뒤의 마크다운이 문법이 적용되지 않는 에러가 발생.  
    
    

![details-errorCode.png](/assets/images/Markdown/details/details-errorCode.png)    
    
![details-error.png](/assets/images/Markdown/details/details-error.png)    
    

## <span style="background-color:pink; color: white"> Solution </span>

    
> div markdown=”1” 은 jekyll에서 html사이에 markdown을 인식 하기 위해 작성한 태그 

```html
<details>
    <summary>제목</summary>
    <div markdown="1">
        
        * markdown
        * spring 
        * vue
        
    </div>
</details>
```

<details>
<summary>제목</summary>
<div markdown="1">

* markdown
* spring 
* vue 

</div>
</details>      
    


![details.png](..%2F..%2Fassets%2Fimages%2FMarkdown%2Fdetails%2Fdetails.png)    
    
[참고 블로그](https://inasie.github.io/it%EC%9D%BC%EB%B0%98/%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4-expander-control/)