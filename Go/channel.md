# Channel
Go 에서 기본 자료형으로 제공되는 채널은 goroutine끼리 통신하기 위해 사용된다.

### Table of Contents
- [About Channel](#about-channel)
  - [Types of Channel](#types-of-channel)
    - Unidirectional Channel | Bidirectioanl Channel
    - Buffered Channel | Unbuffered Channel
- [hchan struct](#hchan-struct)
- [Close Channel](#close-channel)
- [Deadlock](#deadlock)
- [Livelock](#livelock)
- [Starvation](#starvation)
- [Select](#select)
- [Shape of data flow](#shape-of-data-flow)


## About Channel
### Types of Channel
#### Unidirectional Channel
**단방향 채널**은 송신(Send only) 혹은 수신(Receive only) 한쪽의 역할만 담당하는 채널을 말한다.  
```<-``` 연산자의 위치를 통해 send only 인지 receive only 인지가 결정된다.  
* sender  
  ```go
  var sendCh chan <- string
  ```
* receiver
  ```go
  var recCh <- chan
  ```

  ```chan``` 을 기준으로 화살표가 어디에 위치해 있는지 생각한다면 송신인지 수신인지 구별하기가 수월해진다.  
  * **data comes out**  
    ``` <- chan``` 화살표가 채널로 부터 나오니 수(受)신.
  * **data goes in**  
    ```chan <-``` 화살표가 채널로 보내지니 송(送)신.

#### Bidirectional Channel
**양방향 채널**은 읽고(read) 쓰기(write)가 모두 가능한 채널을 일컫는다.
```go
var bidCh chan
```

#### Buffered Channel
#### Unbuffered channel


[↑ return to TOC](#table-of-contents)


## hchan struct
hchan은 채널의 중요한 자료구조이다.   
이를 통해 링크드 리스트와 closed flags를 주고 받는다.  

hchan 는 아래의 field 로 이루어져 있다.  

```go
type hchan struct {
  qcount   uint          
  dataqsiz uint           
  buf      unsafe.Pointer 
  elemsize uint16
  closed   uint32
  elemtype *_type 
  sendx    uint   
  recvx    uint   
  recvq    waitq 
  sendq    waitq 
  lock     mutex
}
```
* qcount : queue 안의 총 데이터
* dataqsiz : 순환 queue의 크기
* buf : dataqsiz 요소로 이루어진 배열의 포인터
* elemsize : 요소 크기
* elemtype : 요소 타입  
  요소의 타입은 아래와 같이 11 종류가 있다.
  * size
  * ptrdata
  * uintptr
  *	hash 
  * tflag
  *	align
  *	fieldAlign
  *	kind
  * equal
  * gcdata 
  * str	
  * ptrToThis 
* sendx : 보낸 인덱스
* recvx : 받은 인덱스
* recvq : recv waiters 의 리스트
* sendq : send waiters의 리스트
* lock : mutex  
  lock은 hcan의 모든 필드를 보호하는 역할을 한다.

[↑ return to TOC](#table-of-contents)


## Close Channel
Go 에는 close 라는 내장형 함수가 존재한다.  
이 함수는 **채널을 닫을**때 사용된다.  
* close()
  ``` go
  func close(c chan<- Type)
  ```
  * close 함수에 전할 parameter 는 bidirectional 채널이거나 send-only 채널이어야 한다.  
  * close 는 마지막 value 를 받은 후 채널을 닫아준다.
  * 닫은 채널에는 data 를 전송할 수 없다. (Panic)
  * 닫힌 채널을 다시 닫을 수 없다. (Panic)

채널의 상태(status)를 변경하지 않고서 채널이 닫혔는지 아닌지의 여부를 확인하는 쉬운 방법은 존재하지 않는다.  


[↑ return to TOC](#table-of-contents)


## Deadlock
데드락이 발생하기 위해서는 4개의 필요충분 조건(Coffman condition)이 필요하다.
1. Mutual Exclusion
1. Ciruclar Wait
1. Hold and Wait
1. No Pre-emption

[↑ return to TOC](#table-of-contents)

## Livelock
[↑ return to TOC](#table-of-contents)


## Starvation
[↑ return to TOC](#table-of-contents)


## Select
하나 이상의 채널이 존재한다면 select를 사용해보자.

[↑ return to TOC](#table-of-contents)



## Shape of Data Flow
채널로 부터 보내지는 데이터의 흐름에 따라 종류가 나뉜다.  
* Fan-out
* Fan-In
* Funnel
* Turnout
