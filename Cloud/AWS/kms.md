# KMS
> Reference : [Amazon KMS](https://aws.amazon.com/sqs/)

**KMS :** **K**ey **M**anagement **S**ervice


### Table of Contents
- [About KMS](#about-kms)
- [CMK](#cmk)
  - [Symmetric and Asymmetric](#symmetirc-and-asymmetric)
  - [Meta Data of CMK](#meta-data-of-cmk)
  - [3 Types CMK](#3-types-cmk)
- [Data Keys](#data-keys)
  - [Create Data Key](#create-data-key)


## About KMS 
KMS를 통해 데이터를 암호화 할 수 있다.  
암호화가 필요한 중요한 정보나 디지털 서명에 AWS KMS를 사용한다.  

KMS 는 미국 연방정보처리 규격인 [FIPS 140-2](https://csrc.nist.gov/projects/cryptographic-module-validation-program/Certificate/3139) 를 사용한다.
* FIPS 140-2  
  FIPS : **F**ederal **I**nformation **P**rocessing **S**tandars

[↑ return to TOC](#table-of-contents)



## CMK  
CMK : **Customer Master Key**  
고객 마스터 키  
이는 중앙 집중식으로 키를 관리할 수 있게 해준다.  

CMK 를 통해 데이터를 암호화 및 복호화 한다.  
AWS 계정을 통해 CMK를 생성하고 관리할 수 있다. KMS 내부적으로는 CMK를 관리하지 못한다.  


### Symmetric and Asymmetric
대칭과 비대칭 CMK 모두 생성 가능하다.

1. Symmetric CMKs | 대칭 CMKs  
  단일 256 비트 보안 암호화 키  
1. Asummetric CMKs | 비대칭 CMKs


### Meta Data of CMK
CMK의 메타데이터  
* Key ID  
  키 ID  
  Account 와 Region 내의 키를 식별하는 역할을 한다.
* Key State  
  키 상태
* Creation Date  
  생성 날짜
* Description  
  설명


### 3 Types of CMK
1. **고객 관리형 CMK**  
  Customer managed CMK  
  고객이(사용자) 모든 제어 권한(생성, 소유 및 관리)을 가진 CMK  
  고객 관리형 CMK는 매달 요금을 지불해야 한다. 비용은 프리티어를 초과해서 사용한 만큼 부과된다.
1. **AWS 관리형 CMK**  
  AWS managed CMK  
  고객 대신 AWS가 CMK를 생성, 관리 해준다.  
  사용자는 AWS CloudTrail Log를 통해 CMK 사용여부를 살펴 볼 수 는 있지만, CMK 자체를 관리하거나 교체 할 수 있는 권한은 없다.
1. **AWS 소유 CMK**  
  AWS Owned CMK  


[↑ return to TOC](#table-of-contents)



## Data Keys
Data Encryption Keys  
암호화 하고자 하는 데이터가 방대할 때는 데이터키를 사용하게 된다.  
KMS 내부적으로는 Data Key를 사용하고 관리할 수 없기 때문에 KMS 밖에서 Datakey를 다루어야 한다.  

### Create Data Key  
AWS KMS는 지정된 CMK 를 통해서 Data Key를 생성한다.  
```GenerateDataKey``` 를 통해 데이터 키를 만들 수 있다.  

<img src="https://user-images.githubusercontent.com/48475824/88276246-a9828080-cd19-11ea-9c3f-9afdf1df5ab8.png" width=300>


[↑ return to TOC](#table-of-contents)