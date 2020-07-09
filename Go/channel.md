# Channel
Go 에서 기본 자료형으로 제공되는 채널은 goroutine끼리 통신하기 위해 사용된다.

### Table of Contents
- [About Channel](#about-channel)
- [hchan struct](#hchan-struct)


## About Channel
채널의 종류
  * 양방향 채널
  * 단방향 채널


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
