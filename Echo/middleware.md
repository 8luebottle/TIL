# Echo-Middleware
> Reference : [Echo Doc](https://echo.labstack.com/)

### Table of Contents

* [3 Levels](#3-levels)
  * [Group Level](#group-level)
    * [Before Router](#before-router)
    * [After Router](#after-router)
  * [Root Level](#root-level)
  * [Route Level](#route-level)
* [Skipping Middleware](#skipping-middleware)


## 3 Levels

에코에서 제공하는 미들웨어를 세 가지 레벨로 나눌 수 있다.

1. Group Level
1. Root Level
1. Route Level

### Group Level
새 그룹을 생성하여 특정 그룹에게만 middleware 가 적용되게 설정.
```go
e := echo.New()
admin = e.Group("/admin", middleware.BasicAuth())
```

[↑ return to TOC](#table-of-contents)

### Root Level
Root 레벨은 Router 가 '실행되기 이전'과 '실행된 후' 라는 두 그룹으로 나뉜다.

* Before Router
* After Router

#### Before Router
이 레벨에서 미들웨어를 등록할 시에는 ```Pre()``` 함수를 사용한다.  

* HTTPSRedirect
* HTTPSWWWRedirect
* WWWRedirect
* NonWWWRedirect
* AddTrailingRedirect
* AddTrailingSlash
* RemoveTrailingSlash
* MethodOverride
* Rewrite

[↑ return to TOC](#table-of-contents)

#### After Router
이 레벨에서 미들웨어를 등록할 시에는 대부분의 경우 ```Use()``` 함수를 사용한다.  
이곳에서 등록된 미들웨어는 라우터 이후(after)에 실행되게 된다.

```go
// E.g.
import (
    "github.com/labstack/echo/middleware"
)

e := echo.New()
e.Use(middleware.Logger())
e.Use(middleware.Recover())
```

이 레벨단의 내장되어 있는 미들웨어는 아래와 같다.

* BodyLimit
* Logger
* GZip
* Recover
* BasicAuth
* JWTAuth
* Secure
* CORS
* Static

[↑ return to TOC](#table-of-contents)

### Route Level
새 Route 를 정의함을 통해 미들웨어를 특정 핸들러에게만 적용시킬 수 있다.

```go
e := echo.New()
e.GET("/", <HandlerA>, <MiddlewareB>)
```
* ```HandlerA``` 에게만 ```MiddlewareB``` 적용시키기

[↑ return to TOC](#table-of-contents)


## Skipping Middleware
특정 조건에 해당될 때 미들웨어를 사용하지 않고 스킵하도록 설정 할 수 있다.

* 스킵시에는 ```Skipper``` 함수를 사용.
  ```go	
  Skipper func(echo.Context) bool
  ```

```go
// E.g.
e := echo.New()
e.User(middleware.LoggerWithConfig(middleware.LoggerConfig{
    Skipper: func(c echo.Context) bool {
        if strings.HasPrefix(c.Request().Host, “localhost”){
            return true
        }
        return false
    },
}))
```