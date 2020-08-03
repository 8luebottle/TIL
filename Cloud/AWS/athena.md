# Athena
> Reference : [Athena](https://docs.aws.amazon.com/ko_kr/athena/)

<img width="150" alt="AWS Athena" src="https://user-images.githubusercontent.com/48475824/89182480-c26c1b00-d5d0-11ea-833d-cc80ac37ad26.png">


### Table of Contents
- [About Athena](#about-athena)
  - [Why Athena](#why-athena)
  - [Pricing](#pricing)
- [Accesing Athena](#accessing-athena)
- [Athena with other services](#athena-with-other-services)


## About Athena 
Athena 는 SQL 을 통해 S3에 저장된 데이터(비정형, 반정형, 정형)를 다룰수 있게 해준다.  
쿼리문을 통해 데이터를 간편하게 분석할 수 있다. 비용은 실행한 쿼리 기준으로 산정된다. 

### Why Athena  
* 비용 절감  
  실행에 성공한 쿼리문에 대한 비용만 청구된다.  

    
* 편리성  
  서버리스 서비스이기 때문에 관리할 요소(인프라)들이 줄어든다.  
  작성한 SQL로 편리하게 데이터를 다룰 수 있다.  
  
  <img width="600" alt="SQL Athena" src="https://user-images.githubusercontent.com/48475824/89180504-dd3c9080-d5cc-11ea-854d-b1c3b65664d5.png">


### Pricing  
  Athena 는 쿼리로 부터 스캔된 데이터의 양에 따라 요금을 측정한다.  
  비용은 지역마다 차이가 있다. 보통 테라바이트 당 5불 선이다.  

  **[1 TB 당 비용]**  
  이는 08.03.2020 기준이다.  
  * $5.00
    * 서울
    * 도쿄
    * 미국 동부 버지니아 북부
    * 미국 동부 오하이오
    * 미국 서부 오레곤 
    * 유럽 프랑크푸르트
    * 유럽 런던
  * $5.50
    * 홍콩
  * $6.50
    * 중동 바레인
  * $6.75
    * 캘리포니아 북부
  * $7.00  
    * 유럽 파리

  **[비용절감]**  
  파티셔닝 사용과 데이터를 압축한다면 30%~90% 의 비용 절감효과를 볼 수 있다.  
  데이터 압축시 비용이 절감되는 이유는 압축한 만큼 Athena가 스캔할 데이터가 줄어들기 때문이다.  

  **[추가 비용]**  
  **AWS Glue** 의 데이터 카탈로그를 사용한다면 추가 비용이 발생하게 된다.   
  * AWS Glue는 최소 2개의 DPU가 필요하다. 초 단위로 DPU 시간당 서울기준 $0.44가 청구된다.  
    * 요금은 올림 처리 됨.

  **AWS Lambda** 와 함께 사용하는 경우, 함수 요청 수, 기간, 코드 실행시 소요된 시간에 따라 요금이 추가된다.  

[↑ return to TOC](#table-of-contents)


## Accessing Athena  
아테나를 사용하기 위해서는 아래의 네가지 방법중 하나를 사용하면 된다.  
* AWS Management Console 
* Athena API
* Athena CLI
* JDBC  
  **J**ava **D**ata**b**ase **C**onnectivity  
* ODBC  
  **O**pen **D**ata**b**ase **C**onnectivity

[↑ return to TOC](#table-of-contents)


## Athena with other services  
아테나와 함께 사용할 수 있는 아마존의 서비스 종류는 아래와 같다.  
* AWS CloudFront  
  Amazon의 CDN 서비스 

* AWS CloudFormation

* AWS Glue

* AWS QuickSight

* Amazon VPC

* Elastic Load Balancing

* IAM  
  아래에서 하나 선택
  * AmazonAthenaFullAccess  
  * AWSQuickSightAthenaAccess  

[↑ return to TOC](#table-of-contents)


## Athena Data Source Connectors  
아테나 데이터 원본 커넥터는 아래와 같은 것들이 있다.  

* AWS CMDB Connector
* CloudWatch Connector
* CloudWatch Metrics Connector
* DocumentDB Connector
* DynamoDB Connector
* Elasticsearch Connector
* HBase Connector
* Connector for JDBC-Compliant Data Sources
* Redis Connector
* TPC Benchmark DS (TPC-DS) Connector

[↑ return to TOC](#table-of-contents)
