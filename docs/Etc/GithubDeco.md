---
layout: default
title: Github Readme/ Profile 꾸미기 
parent: Etc
---

![githubProfile](../../assets/images/Etc/GithubDeco/githubReadme.png)  
  
## 1. Repository 생성
  
![repository](../../assets/images/Etc/GithubDeco/repository.png)

아이디와 똑같은 이름과 똑같이 repository를 생성.  
Add a README file 선택 
  
## 2. 마크다운 내용 작성   
.md 파일 미리보기 지원하는 사이트 
[https://dillinger.io/](https://dillinger.io/) 
    
![미리보기](../../assets/images/Etc/GithubDeco/preview.png)


### 1. 헤더 꾸미기 
  
![header](../../assets/images/Etc/GithubDeco/header.png)

[https://github.com/kyechan99/capsule-render#waving](https://github.com/kyechan99/capsule-render#waving) 
  
  github에 따라서 원하는 헤더로 선택

 ~~~ html
 ![header](https://capsule-render.vercel.app/api?type=transparent&&fontColor=색상&height=300&section=header&text=내용&fontSize=100)
 ~~~

 - 원하는 색상은 헥사코드 (아래에 들어가 원하는 색상 선택)
 ~~~
 [https://encycolorpedia.kr/00076b](https://encycolorpedia.kr/00076b)
 ~~~
  

### 2. 뱃지 
  
![badge](../../assets/images/Etc/GithubDeco/badge.png)
  
- 아이콘 
[https://simpleicons.org/?q=instarg](https://simpleicons.org/?q=instarg)
  
- 뱃지 
[https://shields.io/](https://shields.io/)


~~~ html
<img src="https://img.shields.io/badge/문자-색코드?style=flat-square&logo=이미지 이름&logoColor=white"/></a>
~~~
  
~~~ html
![JAVA](https://img.shields.io/badge/문자-색코드?style=flat-square&logo=이미지 이름&logoColor=white)  
~~~

  
### 3. Github Stats
![githubStats](../../assets/images/Etc/GithubDeco/githubStats.png)  

- github stats 페이지
[https://github.com/anuraghazra/github-readme-stats/blob/master/docs/readme_kr.md](https://github.com/anuraghazra/github-readme-stats/blob/master/docs/readme_kr.md)
  
 위의 깃허브를 따라서 github stats 설정.  
 색상도 마음대로 커스텀 가능. 

 ~~~ html
 ![GitHub stats](https://github-readme-stats.vercel.app/api?username=아아디&show_icons=true&title_color=색상&text_color=색상&icon_color=색상&bg_color=색상&locale=언어)
 ~~~

### 4. 백준 Solved.ac 
  
![backjoon](../../assets/images/Etc/GithubDeco/backjoon.png)
  

[https://github.com/mazassumnida/mazassumnida](https://github.com/mazassumnida/mazassumnida)
  

~~~ html
[![Solved.ac Profile](http://mazassumnida.wtf/api/v2/generate_badge?boj=아이디)](https://solved.ac/아이디/)
~~~

  
## README 오류해결 
  
![githubError](../../assets/images/Etc/GithubDeco/githubError.png)
  
가운데 정렬을 하기 위해서 align을 사용했으나, 마크다운 + html 사용해서 에러발생. 
  
``` html
<p align="center"> </p>
```
  
[https://www.ttmkt.com/kr/tools/markdown-to-html/](https://www.ttmkt.com/kr/tools/markdown-to-html/)  

위의 사이트에 들어가서 html을 마크다운으로 변경 후 README에 입력


  

## 완성 코드 

~~~ html
![header](https://capsule-render.vercel.app/api?type=transparent&&fontColor=003458&height=300&section=header&text=Areuma&fontSize=100)

# 🛠 Used Tool & Skill 🛠
## Platforms & Languages

<center>
    ![JAVA](https://img.shields.io/badge/Java-007396?style=flat-square&logo=Java&logoColor=white)   ![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=Python&logoColor=white) ![Spring](https://img.shields.io/badge/Spring-6DB33F?style=flat-square&logo=Spring&logoColor=white) ![SpringBoot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=Spring%20Boot&logoColor=white) 
    ![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=HTML5&logoColor=white) ![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=CSS3&logoColor=white)    ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=JavaScript&logoColor=white)    ![Vue.js](https://img.shields.io/badge/Vue.js-4FC08D?style=flat-square&logo=Vue.js&logoColor=white) ![Vuetify](https://img.shields.io/badge/Vuetify-1867C0?style=flat-square&logo=Vuetify&logoColor=white)  ![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=MySQL&logoColor=white) ![Oracle](https://img.shields.io/badge/Oracle-F80000.svg?&style=flat-square&logo=Oracle&logoColor=white)
</center>  

<h3 align="center">Tool </h3>
<p align="center">
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=Git&logoColor=white) ![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=GitHub&logoColor=white) ![Notion](https://img.shields.io/badge/Notion-000000?style=flat-square&logo=Notion&logoColor=white) ![IntelliJ_IDEA](https://img.shields.io/badge/IntelliJ_IDEA-000000?style=flat-square&logo=IntelliJ%20IDEA&logoColor=white) ![Visual Studio Code](https://img.shields.io/badge/Visual%20Studio%20Code-007ACC.svg?&style=flat-square&logo=Visual%20Studio%20Code&logoColor=white) 
</p>

<h1 align="center"> 🌟 Contacts 🌟 </h2>

<p align="center">
[![Tistory](https://img.shields.io/badge/Tistory-000000?style=flat-square&logo=Tistory&logoColor=white)](https://meur.tistory.com/)  [![Twitter](https://img.shields.io/badge/Twitter-1DA1F2?style=flat-square&logo=Twitter&logoColor=white)](https://twitter.com/muer_i) [![Gmail Badge](https://img.shields.io/badge/Gmail-d14836?style=flat-square&logo=Gmail&logoColor=white&link=mailto:kuuniin@gmail.com)](mailto:kuuniin@gmail.com)
</p>

<p>
![AReuma's GitHub stats](https://github-readme-stats.vercel.app/api?username=AReuma&show_icons=true&title_color=1b1a42&text_color=000000&icon_color=0b8ce5&bg_color=eff1f5&locale=en)&nbsp;&nbsp;&nbsp;[![Solved.ac Profile](http://mazassumnida.wtf/api/v2/generate_badge?boj=kuuniin)](https://solved.ac/kuuniin/) 
</p>
~~~
  
  

  
[깃허브🌱 링크](https://github.com/AReuma)