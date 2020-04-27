# Blame
```git blame``` 을 통해 소스코드의 라인별 정보를 얻을 수 있다.


### Table of Contents
* [About](#about)
    * [Flags](#flags)
      * -L  
        원하는 라인만 보기
      * -l  
        long commit 으로 보기
      * -e  
        작성자의 이메일로 보기

## About
```git blame``` 은 코드 분석, 디버깅 또는 해당 라인의 작성자를 찾고자 할때 유용하게 사용된다.

```git blame``` 뒤에는 파일 이름과 확장자를 써준다.  

**Syntax**
```
git blame <fileName>
```

```git blame``` 을 통해 얻는 정보는 아래와 같다.
* Commit Hash  
* 작성자 이름(ID)  
* 마지막으로 수정한 날짜  
* 라인 번호  
* 코드  

e.g.  
예시로 Go 의 패키지 중 하나인 Gorilla Mux 에서 ```git blame``` 명령문을 사용해보겠다.  
```
git blame mux.go
```
  <img width="925" alt="git blame" src="https://user-images.githubusercontent.com/48475824/80333124-fe803900-8887-11ea-8952-598f3198f72c.png">

* Commit Hash  
  ```eac83ba2```
* 작성자 이름(ID)  
  ```moraes```
* 마지막으로 수정한 날짜  
  ```2012-10-03 01:48:17 -0300```
* 라인 번호  
  ```1```
* 코드  
  ```// Copyright 2012 The Gorilla Authors. All rights reserved.```

[↑ return to TOC](#table-of-contents)

### Flags
git blame 에서 사용 가능한 flag 는 다음과 같은 것들이 있다.  
* --incremental
* -b
* --root
* --show-stats
* --progress
* --score-debug
* -f, --show-name
* -n, --show-number
* -p, --porcelain
* --line-porcelain
* -c
* -t
* -l
* -s
* -e, --show-email
* -w
* --color-lines
* --color-by-age
* --indent-heuristic
* --minimal
* -S <file>
* --contents <file>
* -C[```<score>```]
* -M[```<score>```]
* -L <n,m>
* --abbrev[```=<n>```]

#### -L
> ```git blame <fileName> -L from, to```

원하는 라인(from~to)의 정보만 추출하여 확인할 수 있다.  
line 은 1 부터 시작.  
시작과 끝 라인은 콤마(```,```)로 구분

**e.g**
```
git blame mux.go -L 100, 110
```
```
758eb643 (Joe Wilner 2018-12-07 10:48:26 -0500 100)
758eb643 (Joe Wilner 2018-12-07 10:48:26 -0500 101)     if r.regexp.path != nil {
758eb643 (Joe Wilner 2018-12-07 10:48:26 -0500 102)             c.regexp.path = copyRouteRegexp(r.regexp.path)
758eb643 (Joe Wilner 2018-12-07 10:48:26 -0500 103)     }
758eb643 (Joe Wilner 2018-12-07 10:48:26 -0500 104)
758eb643 (Joe Wilner 2018-12-07 10:48:26 -0500 105)     if r.regexp.host != nil {
758eb643 (Joe Wilner 2018-12-07 10:48:26 -0500 106)             c.regexp.host = copyRouteRegexp(r.regexp.host)
758eb643 (Joe Wilner 2018-12-07 10:48:26 -0500 107)     }
758eb643 (Joe Wilner 2018-12-07 10:48:26 -0500 108)
758eb643 (Joe Wilner 2018-12-07 10:48:26 -0500 109)     c.regexp.queries = make([]*routeRegexp, 0, len(r.regexp.queries))
758eb643 (Joe Wilner 2018-12-07 10:48:26 -0500 110)     for _, q := range r.regexp.queries {
```


#### -l
l == long  

> ```git blame <fileName> -l```

짧은 Comming 정보 대신 긴(long) 커밋 정보를 확인할 수 있다.  

**e.g**
``` 
git blame mux.go -l
```
```
eac83ba2c004bb759a2875b1f1dbb032adf8bb4a (moraes  2012-10-03 01:48:17 -0300  5) package mux
```

#### -e
e == email

> ```git blame <fileName> -e```  
```git blame <fileName> --show-email```

작성자의 이름(ID) 대신 이메일을 확인할 수 있다.

**e.g**
```
git blame mux.go -e
```
```
eac83ba2 (<rodrigo.moraes@gmail.com>  2012-10-03 01:48:17 -0300   1) // Copyright 2012 The Gorilla Authors. All rights reserved.
```

[↑ return to TOC](#table-of-contents)