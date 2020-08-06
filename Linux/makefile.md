# Makefile
> Reference : [Makefile的写法](https://www.youtube.com/watch?v=E1_uuFWibuM)

<img width="150" alt="Makefile" src="https://user-images.githubusercontent.com/48475824/89472365-39650780-d7bb-11ea-8d40-cddad54e5498.png">


### Table of Contents
- About
  - [make](#make)
  - [Makefile](#makefile)
    - [Makefile 내부구조](#makefile-내부구조)
<!-- 
<img width="637" alt="Original" src="https://user-images.githubusercontent.com/48475824/89475658-92d13480-d7c3-11ea-9b74-a092a3558dc6.png"> -->


## About
make 는 Makefile 을 토대로 프로그램을 컴파일 한다.  
make 는 Makefile 속에 명시되어 있는 의존관계(dependencies)와 명령(commands)을 참고하여 프로그램을 빌드시켜준다.  

### make  
make 는 Linux의 파일 관리 유틸리티이다.  
이는 Makefile 을 기준으로 프로그램을 빌드해준다.  

```make```  
make 명령어를 실행 :  make 는 Makefile 이 존재할 시 Makefile 을 실행시킨다.  
* 반드시 Makefile 명이 아니여도 된다.  
  make 가 찾을 수 있는 또 다른 이름은 ```GNUmakefile``` 과 ```makefile``` 이 있다.  
  make 가 찾는 순서는 ```GNUmakefile``` → ```makefile``` → ```Makefile```  
  하지만, ```GNUmakefile``` 이름의 경우 make 가 인식을 못하는 경우도 있으니 안전하게 ```Makefile```을 사용하도록 하자. 

[↑ return to TOC](#table-of-contents)


### Makefile  
make 로 컴파일(```编译```)할 파일들을 일일이 지정해줄 수 있지만 Makefile 을 통해 간편히 컴파일 가능하다.  

개발을 진행시 라인수가 늘어나게 되면서 여러 모듈로 쪼개지게 되고 그로인해 컴파일 해야할것들이 늘어나게 된다. 단순히 make 를 통해 컴파일 시킬 수 있지만 너무 번거로운 작업(길어지는 명령어)이 되어버린다. 게다가 컴파일해야 할 것을 빼먹는 경우도 발생하게 된다.  

Makefile 은 이러한 문제점들을 해결해주며 컴파일을 편리하게 만들어준다.  


#### Makefile 내부구조 
Makefile 은 내부적으로 세 가지로 구조로되어 있다.  
* 목표 target
* 의존관계 dependency
* 명령 command

    ```bash
    target: dependencies  
            command
    ```
    * command 앞은 tab 으로 들여쓰기  

Makefile 은 한 라인을 명령어로 인식하기 때문에 한 라인에 한 명령어를 작성해 주어야 한다.  

[↑ return to TOC](#table-of-contents)
