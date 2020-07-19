# AWS Lambda
AWS Lambda 는 AWS 플랫폼에서 함수를 실행하여 데이터를 간편하게 처리할 수 있게 해주는 서비스이다.

<img alt="Lambda Logo" src="https://user-images.githubusercontent.com/48475824/87877903-f580ad00-ca1b-11ea-81c7-117a6b7e7214.png" width="100">

### Table of Contents
* [About](#about)
  * [FaaS](#faas)
* [Lambda + Other Services](#lambda-+-other-services)
  * [4 Groups](#4-groups)
* [References](#refrences)

## About
Lambda 를 사용한다면 시스템 자원을 프로비저닝할 필요 없이 Serveless로 코드를 실행시킬 수 있다.  

AWS Lambda 를 통해 필요할 때만 코드를 실행시킬 수 있다. 코드가 실행될 때에만 비용이 부과됨으로 인해 코드 실행되지 않는 상황에서의 비용을 감소시킬 수 있다.

만약 동시다발적으로 여러 이벤트가 발생할 경우, 람다는 함수를 복사하여 병행적으로 실행시킨다.  
람다 함수의 크기는 workload의 사이즈와 일치한다.

### FaaS
FaaS : **F**unction **a**s **a** **S**ervice  
Lambda는 서버리스 FaaS 에 해당하는 타입이다.

[↑ return to TOC](#table-of-contents)


## Lambda + Other Services
보통 Lambda 는 함수를 호출하기 위해 다른 AWS 서비스와 통합되어 사용된다.  
람다와 통합되는 서비스는 함수(JSON 형식)에 Data 를 Event로 전송시킨다.  
람다는 전달해야 하는 이벤트를 객체로 변환시킨 후 함수로 전달한다.
<br><br>

람다와 함께 사용되는 아마존의 서비스는 아래와 같다.
- **A**
    - Alexa
    - API Gateway
- **C**
    - CloudTrail
    - CloudWatch
    - CloudFormation
    - CloudFront
    - CodeCommit
    - CodePipeline
    - Cognito
- **D**
    - DynamoDB
- **E**
    - EC2
    - ElastiCache
    - Elastic Load Balancing
    - EFS
- **I**
    - IoT
- **K**
    - Kinesis
- **L**
    - Lex
- **R**
    - RDS
- **S**
    - S3
    - SES
    - SNS
    - SQS
    - Step Functions
- **X**
    - X-Ray


### 4 Groups
위의 서비스들을 네 가지 타입으로 grouping 할 수 있다.
1. **이벤트를 읽는 서비스**  
    Lambda 함수를 동기적으로 호출하는 서비스
    - Amazon Kinesis
    - Amazon DynamoDB 
    - Amazon Simple Queue Service

1. **동기 호출**  
    Lambda 함수를 동기적으로 호출하는 서비스
    - Elastic Load Balancing 
    - Amazon Cognito
    - Amazon Lex
    - Amazon Alexa
    - Amazon API Gateway
    - Amazon CloudFront
    - Amazon Kinesis Data Firehose
    - AWS Step Functions
    - Amazon Simple Storage Service 배치

1. **비동기 호출**  
    Lambda 함수를 비동기적으로 호출하는 서비스
    - Amazon Simple Storage Service
    - Amazon Simple Notification Service
    - Amazon Simple Email Service
    - AWS CloudFormation
    - Amazon CloudWatch Logs
    - Amazon CloudWatch Events
    - AWS CodeCommit
    - AWS Config
    - AWS IoT
    - AWS IoT Events
    - AWS CodePipeline

1. **통합 서비스**  
    다른 방식으로 Lambda와 통합되는 서비스
    - Amazon Elastic File System
    - AWS X-Ray



## References
[AWS Lambda](https://docs.aws.amazon.com/ko_kr/lambda/latest/dg/welcome.html)

[↑ return to TOC](#table-of-contents)