# EC2 
> Reference : [EC2](https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/concepts.html)

<img width="150" alt="EC2" src="https://user-images.githubusercontent.com/48475824/89402113-51a03c80-d751-11ea-9731-9848bc215adc.png">


### Table of Contents
- [About EC2](#about-ec2)
- [Instance](#instance)
  - [Instance Types](#instance-types)
- [Load Balancing](#load-balancing)
- [Auto Scaling](#auto-scaling)



## About EC2  
EC2 : **E**lastic **C**ompute **C**loud   
* Elastic : 여기서 탄력적이란 말은 컴퓨터, 서비스등을 생성 및 삭제하는 것이 매우 유연하다는 말이다. 
* 짧은 시간에 용량을 늘리고 줄일 수 있다.  

EC2란 AWS 에서 제공해주는 확장식 컴퓨팅이다.  
사용한 용량 만큼 비용을 지불하면 된다.  

[↑ return to TOC](#table-of-contents)


## Instance
하나의 EC2 인스턴스는 한대의 컴퓨터라고 볼 수 있다.  
AWS 로 부터 한대의 컴퓨터(EC2 Instance)를 빌려 원하는 OS 및 프로그램을 설치 할 수 있다.  

### Instance types
AWS 가 제공하는 인스턴스 유형은 상당히 많다.  
이 인스턴스들은 총 5가지로 그룹핑 된다.  
* General Purpose 범용 
* Compute Optimized 컴퓨팅 최적화 
* Storage Optimized 스토리지 최적화
* Memory Optimized 메모리 최적화
* Accelerated Computing 가속화된 컴퓨팅

#### General Purpose
* A1
* T3
* T3a
* T2
* M6g
* M5
* M5a
* M5n
* M4


#### Compute Optimized
* C6g
* C6
* C5a
* C5n
* C4

#### Storage Optimized
* I3
* I3en
* D2
* H1

#### Memory Optimized
* R6g
* R5
* R5a
* R5n
* R4
* X1e
* X1
* HighMemory
* z1d

#### Accelerated Computing
* P3  
  가장 최신형 GPU 인스턴스  
* P2
* Inf1
* G4
* G3
* F1


[↑ return to TOC](#table-of-contents)


## Load Balancing

[↑ return to TOC](#table-of-contents)


## Auto Scaling

[↑ return to TOC](#table-of-contents)
