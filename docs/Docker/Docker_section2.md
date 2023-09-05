---
layout: default
title: 도커 구조와 기본 명령어
parent: Docker
---

# 도커 구조와 기본 명령어
&nbsp;

## 1. 도커의 구조    
  
도커를 설치한 후 버전정보를 확인하면 클라이언트와 서버로 나눠져있다.  
도커는 클라이언트와 서버 역할을 각각 수행한다.  
  
도커 커맨드에 명령어를 입력하면 도커 클라이언트가 도커 서버로 명령을 전송한다.  
그 후 서버에서 멸령어를 수행 후 클라이언트로 전송해서 결과를 클라이언트 터미널에 출력이 된다.
&nbsp;
## 2. 도커 기본 명령어 
  
## run  
  
### -d
&nbsp;

![runOption-d-1.png](assets/images/Docker/DockerRunOptions/runOption-d-1.png)  
&nbsp;
![runOption-d-2.png](assets/images/Docker/DockerRunOptions/runOption-d-2.png)  
&nbsp;

>  detached mode(백그라운드 모드 )  
> 실행이 된 상태지만 로그가 뜨지 않는다.  

&nbsp;
&nbsp;

### -p [호스트에 연결할 포트]:[컨테이너 포트] -> [접속할 포트]:[컨테이너 내에서 서비스가 열고 있는 포트]  

&nbsp;

![runOption-p.png](assets/images/Docker/DockerRunOptions/runOption-p.png)  
&nbsp;
&nbsp;

> 호스트와 컨테이너의 포트를 연결

&nbsp;
&nbsp;

### -v [내 pc 저장소]:[서비스 저장 위치]
&nbsp;
&nbsp;

> 호스트와 컨테이너간의 디렉토리 공유  
> 컨테이너를 죽이면 저장된 데이터는 다 날아간다.  
> 지워지면 안되는 데이터를 내 pc 저장소에 저장되도록 설정하는 옵션.  

&nbsp;
&nbsp;

### -e

```shell
docker run -d -p 3306:3360 -e MYSQL_ALLOW_EMPTY_PASSWORD=true mariadb:10.9
```  
&nbsp;

> 컨테이너 내에서 사용할 환경변수 설정
> 위 처럼 설정하면 mysql에 접속할때 패스워드 없이 root를 만들 수 있다.    

&nbsp;
&nbsp;

### --name  
&nbsp;

![runOption-name.png](assets/images/Docker/DockerRunOptions/runOption-name.png)  
&nbsp;
&nbsp;

> 컨테이너 이름 설정  

&nbsp;
&nbsp;

### --rm  
&nbsp;

![runOption-rm-2.png](assets/images/Docker/DockerRunOptions/runOption-rm-2.png)  
&nbsp;
![runOption-rm-1.png](assets/images/Docker/DockerRunOptions/runOption-rm-1.png)  
&nbsp;
&nbsp;

> 프로세스 종료시 컨테이너 자동 제거  

&nbsp;
&nbsp;

### -it  
&nbsp;

![runOption-it.png](assets/images/Docker/DockerRunOptions/runOption-it.png)  
&nbsp;
&nbsp;
  
> -i와 -t를 동시에 사용한것으로 터미널 입력을 위한 옵션

&nbsp;
&nbsp;
### --network  

> 네트워크 연결  

&nbsp;
&nbsp;
<hr>
  
## ps  
> 실행중인 컨테이너 목록을 확인하는 명령어  
 
&nbsp;
## ps -a  


> 중지된 컨테이너도 확인할때 사용하는 명령어  

&nbsp;
&nbsp;

## stop

> 실행중인 컨테이너를 중지하는 명령어  

&nbsp;
&nbsp;

## rm

> 종료된 컨테이너를 완전히 제거하는 명령어 
> ps -a로 확인한 컨테이너 삭제할떄 사용된다  

&nbsp;
&nbsp;

## logs

> 로그를 확인하는 명령어  

&nbsp;
&nbsp;

## images

> 도커가 다운로드한 이미지 목록을 보는 명령어
> 이미지는 압축파일이라고 생각하면 된다

&nbsp;
&nbsp;

## pull

> 이미지를 다운로드하는 명령어  

&nbsp;
&nbsp;

# rmi

> 이미지를 삭제하는 명령어  

&nbsp;
&nbsp;

<hr> 

&nbsp;

[참고 블로그]  

[https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html](https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html)
[https://whitewing4139.tistory.com/204](https://whitewing4139.tistory.com/204)