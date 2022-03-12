# ElasticMQ
> In-memory message queue system

### Table of Contents

* [About](#about)
* [Configure file](#configure-file)
* [ElasticMQ via Docker](#elasticmq-via-docker)

## About
Scala 로 작성된 [ElasticMQ](https://github.com/softwaremill/elasticmq) 는 [Amazon SQS](https://github.com/8luebottle/AWS-SAA-Note/blob/master/Cheat-Sheets/sqs.md) 와 호환되는 메시지 대기열 시스템이다.


## Configure file
ElasticMQ 를 통해 손 쉽게 큐 생성/삭제, 전송 대기 시간, visibility timeout 등과 같은 설정을 다룰 수 있다.  

아래의 속성값은 모두 선택사항이다. 다만 `deadLetterQueue` 를 사용하고자 한다면 `name`과 `maxReceiveCount`는 반드시 작성해주어야 한다.  
  - defaultVisibilityTimeout
  - delay
  - receiveMessasgeWait
  - deadLetterQueue
    - name
    - maxReceiveCount
  - fifo
  - contentBasedDeduplication
  - copyTo
  - moveTo
  - tags

아래는 ElasticMQ 의 커스텀 config 파일 설정 파일(`customName.conf`). 

```
include classpath("application.conf")

node-address {
  protocol = http
  host = localhost
  port = 9324
  context-path = ""
}

queues {
  queue1 {
    defaultVisibilityTimeout = 10 seconds
    delay = 5 seconds
    receiveMessageWait = 0 seconds
    deadLettersQueue {
      name = "queue1-dead-letters"
      maxReceiveCount = 3 // from 1 to 1000
    }
    fifo = false
    contentBasedDeduplication = false
    copyTo = "audit-queue-name"
    moveTo = "redirect-queue-name"
    tags {
      tag1 = "tagged1"
      tag2 = "tagged2"
    }
  }
  queue1-dead-letters { }
  audit-queue-name { }
  redirect-queue-name { }
}
```

URL 은 `http://localhost:9324`로 설정되어 있다.  
해당 URL은 `node-address` 를 통해 커스터마이징 할 수 있다.  

```
include classpath("application.conf")

node-address {
  protocol = http
  host = hosName
  port = 9324
  context-path = ""
}
```

## ElasticMQ via Docker
ElastcticMQ 의 image: `softwaremill.elasticmq-native`

도커 컨테이너 띄울 때 직접 작성한 ElasticMQ 설정파일 사용하기.  

<img width="800" alt="run elasticMQ docker container" src="https://user-images.githubusercontent.com/48475824/158008168-aa213feb-7098-4d89-a326-25b3dc86b838.png">

```
docker run -p 9324:9324 -p 9325:9325 -v `pwd`/customName.conf:/opt/elasticmq.conf softwaremill/elasticmq-native
```

- `-p`  
  `-p 9324:9324 -p 9325:9325`  

  p flag 를 통해 9324 와 9325 의 Host의 포트와 컨테이너의 포트 바인딩.

  - **9324**: REST-SQS API Port

  - **9325**: UI Port  
    UI를 통해 queue의 실시간 정보를 얻을 수 있다.

- `-v`  
  `-v /customName.conf:/opt/elasticmq.conf`

  컨테이너의 데이터를 존속시키기 위해 위해 bind mount.
