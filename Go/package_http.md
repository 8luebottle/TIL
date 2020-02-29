# Package http
```net/http``` 패키지를 통해 HTTP 서버를 구현할 수 있다.

### Table of Contents
* HTTP Basic

* http 코드 열어보기
  * Interface
    * [ResponseWriter](#responsewriter)
    * [Handler](#handler)
    * [Flusher](#flusher)
    * [Hijacker](#Hijacker)

## HTTP Basic
HTTP는 Stateless 이다.


## http 코드 열어보기

### Interface
#### ResponseWriter
HTTP 응답을 위한 인터페이스, response 를 구성해준다.
```go
type ResponseWriter interface {
  Header() Header
  Write([]byte) (int, error)
  WriteHeader(statusCode int)
}
```
* ```Header``` 는 ```WriteHeader```로 부터 받은 header map을 리턴한다.  
    ```go
    w.Header().Set("Content-Type", "application/json")
    ```
    * Contenty 타입을 application/json 으로 지정

* ```Write``` 는 데이터를 쓴다.
    * ```Header``` 에 Content-Type이 담겨져 있지 않다면, ```Write``` 는 Content-Type 셋을 추가시킨다.을
    * ```WriteHeader```가 호출되기 전이라면, ```Write``` 는 데이터를 쓰기 전에 ```WriteHeader(http.StatusOK)``` 를 호출한다.
    * ```Writer``` 가 쓰게 될 데이터의 총 사이즈가 몇 kb밖에 안된다면 ```Flush``` 는 호출되지 않는다. Content-Length 헤더는 자동으로 추가된다.

* ```WriteHeader``` 는 HTTP 응답 헤더를 제공된 상태코드와 함께 보낸다.
    * status code 는 유효한 코드여야 한다. (1xx-5xx의 범주)


#### Handler
Handler 인터페이스는 응답 처리를 위해 사용된다.  
```Handler``` 는 서버가 클라이언트로 부터 요청을 받았을 때 그 요청을 핸들링 해준다.
```go
type Handler interface {
  ServeHTTP(ResponseWriter, *Request)
}
```
* ```ServeHTTP``` 는 두 매개변수를 받는다.
    * ```ResponseWriter``` 인터 페이스 
    * ```Request``` 를 가리키는 포인터


#### Flusher
```go
type Flusher interface {
  Flush()
}
```


#### Hijacker
```go
type Hijacker interface {
  Hijack() (net.Conn, *bufio.ReadWriter, error)
}
```