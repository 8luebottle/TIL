# SQS
> Reference : [Amazon SQS](https://aws.amazon.com/sqs/)

SQS : **S**imple **Q**ueue **S**ervice  
Amazon SQS 는 메시지 대기열 서비스를 제공한다.  

<img width="100" alt="SQS" src="https://user-images.githubusercontent.com/48475824/80058716-0036bd80-8565-11ea-8c3d-ace13e577e11.png"> 


### Table of Contents

- [Message Queues](#message-queues)
  - [메시지 전송 과정](#메시지-전송-과정)
  - [Retention period](#retention-period)
  - [이동 중인 메시지](#이동-중인-메시지)
- [Types of Message Queues](#types-of-message-queues)  
  Standard Queues | FIFO Queues
- [SQS Visibility Timeout](#sqs-visibility-timeout)

## Message Queues  

메시지 대기열 | 消息队列 | メッセージキュー  
서버리스 또는 마이크로 서비스 아키텍처에 사용되는 비동기식 서비스.  

메시지 대기열은 **버퍼** 와 **엔드포인트** 기능을 제공해준다.

메시지는 Producer 에서 생성되어 Queue 를 거쳐 Consumer 에 도착한다.  

<img width="500" alt="Amazon SQS" src="https://user-images.githubusercontent.com/48475824/80306627-66d70800-87ff-11ea-8687-887a46fca143.png">  

### 메시지 전송 과정
생산자(```producer```)가 메시지를 대기열(```queue```)에 추가해 놓는다.  
소비자(```consumer```)는 메시지를 검색하여 특정 작업을 수행하기 전까지 대기열(```queue```)에 저장해 놓는다.  

### Retention period

메시지는 처리되고 삭제되기 전까지 대기열에 저장된다.  
통상적인 메시지 유지 기간은 **4일** 이다.  
사용자가 설정 가능한 유지 기간은 최소 **60초** 최대 **1,209,600초**(14 일) 이다.  

### 이동 중인 메시지

저장된 메시지 수에는 할당량이 없지만, 이동중인 메시지 수에는 할당량이 있다.

SQS 메시지는 세 가지 상태로 분류할 수 있다.
1. **전송**  
  생산자가 대기열로 메시지를 전송한 상태
1. **수신**  
  소비자가 대기열에서 메시지를 수신한 상태
1. **삭제**  
  메시지가 대기열에서 삭제된 상태

위의 세 가지 상태 외에도 중간과정에 속하는 상태가 존재한다.
* **1-2 사이 | 전송과 수신 사이**  
  메시지는 생산자가 대기열로 전송했으나,  
  아직 소비자가 대기열에서 수신하지 못함이 된 후 저장된 상태  
* **2-3 사이 | 수신과 삭제 사이**  
  소비자가 대기열에서 수신했으나,  
  아직 대기열에서 삭제되지 않음이 된 후 이동 중인 상태

[↑ return to TOC](#table-of-contents)


## Types of Message Queues

SQS 가 제공하는 대기열은 두가지가 있다.

1. Standard Queues
1. FIFO Queues  
  FIFO : First-in-First-Out  


### Standard Queues 표준 대기열  
  기본으로 설정되어 있는 타입. 처리량은 무제한이다.  
  모든 리전에서 사용 가능.  

### FIFO Queues  
  모든 리전에서 사용 가능한 표준 대기열과 다르게 FIFO 대기열은 일부분의 리전에서만 사용 가능하다.  
  초당 최대 3000개라는 높은 메시지 처리량을 지원한다.

  2020년 4월 현재 FIFO Queue 를 사용할 수 있는 리전은 아래와 같다.  

  * **Asia Pacific**
    * Seoul
    * Singapore
    * Sydney
    * Tokyo
    * Mumbai  
    * Hong Kong  
    * China
      * Ningxia
      * Beijing

  * **Canada**
    * Central

  * **EU**
    * Frankfurt
    * Ireland  
    * London
    * Paris 
    * Stockholm

  * **South America**
    * Sao Paulo

  * **US** 
    * West
      * Oregon
      * N. California
    * East
      * Ohio
      * N. Virginia

  * **GovCloud**
    * US-East
    * US-West 

[↑ return to TOC](#table-of-contents)

## SQS Visibility Timeout  
SQS 제한 시간  

<img width="600" alt="Visibility Timeout" src="https://user-images.githubusercontent.com/48475824/88089008-4b915400-cbc6-11ea-92c3-844d2ca14a4d.png">


SQS는 메시지를 삭제해 주지 않는다. 그 이유는 SQS가 분산 시스템이기 때문에 소비자가 메시지를 실질적으로 언제 성공적으로 받았는지 확인할 길이 없기 때문이다. 그리하여 사용자는 수동으로 메시지 삭제 처리를 해 주어야 한다.

만약 삭제해 주지 않는다면 해당 메시지는 계속 대기열에 남아 있게 된다.  
대기열에 남아있는 메시지를 타 소비자가 접근할 수 없도록 해야한다. 이 때에 사용되는 것이 바로 '제한 시간(Visibility Timeout)'이다.
* 제한 시간을 걸어주게 되면 타 소비자는 메시지를 처리할 수 없게 된다.
  * Default Value : ```30s```
  * Min Value : ```0s```
  * Max Value : ```12h```

여기서 주의할 점은 Visibility Timeout 이 메시지의 '중복 수신 방지'를 보장하지는 않는다는 것이다.  

[↑ return to TOC](#table-of-contents)
