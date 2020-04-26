# SQS
> Reference : [Amazon SQS](https://aws.amazon.com/sqs/)

SQS : **S**imple **Q**ueue **S**ervice  
Amazon SQS 는 메시지 대기열 서비스를 제공한다.  

<img width="100" alt="SQS" src="https://user-images.githubusercontent.com/48475824/80058716-0036bd80-8565-11ea-8c3d-ace13e577e11.png"> 


### Table of Contents

- [Message Queues](#message-queues)
  - [메시지 전송 과정](#메시지-전송-과정)
  - [Retention period](#retention-period)
- [Types of Message Queues](#types-of-message-queues)  
  Standard Queues | FIFO Queues

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
사용자가 설정가능한 유지 기간은 최소 **60초** 최대 **1,209,600초**(14 일) 이다.  

## Types of Message Queues

SQS 가 제공하는 대기열은 두가지가 있다.

1. Standard Queues
1. FIFO Queues  
  FIFO : First-in-First-Out  


### Standard Queues 표준 대기열  
  기본으로 설정되어 있는 타입.  
  모든 리전에서 사용 가능.  
  처리량은 무제한이다.

### FIFO Queues  
  모든 리전에서 사용 가능한 표준 대기열과 다르게 FIFO 대기열은 일부분의 리전에서만 사용 가능하다.  
  초당 최대 3000개인 높은 메시지 처리량을 지원한다.

  2020년 4월 현재 FIFO Queue 를 사용할 수 있는 리전은 아래와 같다.  

  * **Asia Pacific**
    * Seoul
    * Singapore
    * Sydney
    * Tokyo
    * Mumbai  
    * Hong Kong  
    * China
      * Nigxia
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
