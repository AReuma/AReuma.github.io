---
layout: default
title: Jekyll 테마를 이용해 Github 블로그 생성
parent: Etc
---

### 1. Jekyll Theme 설정 
 - https://jekyll-themes.com/free/
 - http://jekyllthemes.org/
 - https://github.com/topics/jekyll-theme

 ### 2. 원하는 테마를 .zip 으로 다운로드 

 ![zip다운로드](../../assets/images/Etc/JekyllTheme/gitZipDownload.png)

### 3. 다운 받은 테마 압축풀기

![zip압축풀기](../../assets/images/Etc/JekyllTheme/justThe.png)

### 4. github에 'username.github.io' repo 생성 

![repo생성](../../assets/images/Etc/JekyllTheme/makeRepo.png)

``` HTTP
 git clone https://github.com/AReuma/AReuma.github.io.git
```

### 5. 내려받은 폴더에 압축 푼 파일 넣기

![파일생성](../../assets/images/Etc/JekyllTheme/github_io.png)

### 6. _config 파일 변경 

![config_1](../../assets/images/Etc/JekyllTheme/config1.png)
![config_2](../../assets/images/Etc/JekyllTheme/config2.png)
![config_3](../../assets/images/Etc/JekyllTheme/config3.png)

### 7. docs 폴더 문서 삭제 

![docs폴더](../../assets/images/Etc/JekyllTheme/docs.png)
 블로그 내용이 docs 폴더 밑에 저장되기 때문에 default로 설정된 문서 삭제

### 8. 원하는 색상으로 변경 
 기본적으로 설정된 색상은 보라색 
 ![blogColor1](../../assets/images/Etc/JekyllTheme/defaultBlog.png)

원하는 색상인 파란색으로 변경 
 ![blogColor2](../../assets/images/Etc/JekyllTheme/chageBlogColor.png)

 gitHub에서 
 AReuma.github.io > _sass > support > _variables.scss

![colorChange](../../assets/images/Etc/JekyllTheme/color.png)

``` HTTP
 $link-color: 원하는 색상; 
 $btn-primary-color: 원하는 색상;
```


