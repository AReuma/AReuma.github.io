---
layout: default
title: Markdown 마크다운 접기
parent: Markdown
---

# Markdown 접기/ 토글 목록 만들기 
  

마크다운에는 문법이 없어 html details 태그를 이용한다. 


## <span style="background-color:skyblue; color: white">Reason</span>    
접기 뒤의 마크다운이 문법이 적용되지 않는 에러가 발생.  
    
    

![details-errorCode.png](..%2F..%2Fassets%2Fimages%2FMarkdown%2Fdetails%2Fdetails-errorCode.png)    
    
![details-error.png](..%2F..%2Fassets%2Fimages%2FMarkdown%2Fdetails%2Fdetails-error.png)    
    

## <span style="background-color:pink; color: white"> Solution </span>

    
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