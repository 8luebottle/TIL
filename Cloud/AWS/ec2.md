# EC2 
> Reference : [EC2](https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/concepts.html)

<img width="150" alt="EC2" src="https://user-images.githubusercontent.com/48475824/89402113-51a03c80-d751-11ea-9731-9848bc215adc.png">


### Table of Contents
- [About EC2](#about-ec2)
- [Instance](#instance)
  - [Instance Types](#instance-types)
  - [Instance Lifecycle](#instance-lifecycle)
- [AMI](#ami)
- [Load Balancing](#load-balancing)
- [Auto Scaling](#auto-scaling)
- [EC2 CLI Commands](#ec2-cli-commands)
  - [modify-instance-attribute](#modify-instance-attribute)


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
인스턴스를 고를 때는 보통 메모리 용량과 연산력을 기준으로 결정하게 된다.  
AWS 가 제공하는 인스턴스 유형은 상당히 많다. 이 인스턴스들은 총 5가지로 그룹핑 된다.  

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

### Instance Lifecycle
인스턴스의 시작부터 종료되기까지의 과정에는 여러 상태가 존재한다.  

![instance_lifecycle](https://user-images.githubusercontent.com/48475824/117335422-198f7b00-aed6-11eb-88bf-743df00df0f9.png)

|  상태  |비용 청구|
|:-----:|:-----:|
|pending|X|
|running|O|
|stopping|△|
|stopped|X|
|shutting-down|X|
|terminated|X|
- stopping
  - `중지` 상태로 전환되는 경우 비용 X  
  - `최대 절전 모드`로 전환되는 경우 비용 O

**시작**  
- Instance를 시작(AMI를 Launch)하게 되면 `pending` 상태로 접어든다.  
  사용자가 지정한 AMI를 통해 부팅되는 과정이다.

**준비**  
- Instance가 준비되면 `running` 상태로 바뀐다.  
  - 비용 발생  
    사용 비용은 이 시점부터 청구되기 시작한다.  
    최소 1분의 비용이 청구되며 초를 기점으로 비용이 계산된다.  
    (`running` 상태에 있는 경우 Instance가 유휴상태 또는 연결되지 않은 경우일지라도 비용은 청구됨)

**중지**  
- Instance를 중지시킬 시 `running` → `stopping` → `stopped` 상태로 바뀌게 된다.  
- 비용  
  부과 X  
  - 중지된 이후(`stopped` 상태) 에는 `사용 요금`, `데이터 전송요금` 이 부과되지 않는다.  
  부과 O
  - Amazon EBS Volume 에 대한 Storage
- 중지된 Instance를 실행시킬 시 `stopped` → `running` 상태로 전환된다.  
  상태의 전환과정 중에 대한 비용은 초 단위로 청구된다. 이 역시 최소 1분의 요금이 부과됨.
- 중지 방지(`stop protection`) 사용.  
  중지 방지 사용을 통해 실수로 인스턴스를 중지(stop) 또는 종료(terminate) 시키는 것을 미연에 방지할 수 있다.  
  - spot instance 는 해당 기능 사용 불가.
  

**최대 절전 모드 (suspend-to-disk)**
- 최대 절전 모드는 Amazon EBS 지원 Instance만 해당.
- `running` → `stopping` → `stopped`
- 해당 모드에 있더라도 EBS 볼륨 비용이 청구된다.  
  (RAM data 에 대한 Storage 비용이다.)

**재부팅**  
- 운영체제의 재부팅과 같이 동작하며 Instance는 동일한 호스트 컴퓨터에 남아있게 된다.
  - Public DNS Name, Private IP Address 등 모든 데이터가 유지됨.
- 비용은 초 단위로 청구된다.  
  비용이 청구되는 이유는 재부팅 시 `running` 상태로 남아 있기 때문
- 몇 분 정도 소요  

**만료**  
- 재시작 가능  
  Amazon EBS Volume
- 재시작 불가  
  Root Device Volume

**종료**
- 상태가 `shutting-down` 또는 `terminated`로 변경되는 순간 요금이 발생하지 않는다.  


[↑ return to TOC](#table-of-contents)


## AMI  
AMI : Amazon Machine Image  

EC2 인스턴스를 띄우기 위해서는 AMI 가 필요하다.  
AMI에는 인스턴스의 구성요소인 OS, 애플리케이션 서버, 아키텍쳐와 같은 정보가 담겨 있다.  

한번 생성해 놓은 AMI는 지속적으로 재사용 가능하다.  
- 기존에 만들어 놓은 AMI를 통해 동일한 환경을 지닌 새 인스턴스를 빠르게 띄울 수 있다.  

AMI의 컨텐츠는 암호화 되어 있다.  

### AMI 선택 시 고려할 요소  
- Architecture
- Launch Permissions  
  - public
  - explicit
  - implicit
- OS
- Region
- Storage for the root device  
  - Boot time
  - Device volume
  - Data persistence
  - Size limit
  - Stopped state


[↑ return to TOC](#table-of-contents)


## Load Balancing

[↑ return to TOC](#table-of-contents)


## Auto Scaling

[↑ return to TOC](#table-of-contents)

## EC2 CLI Commands
### `modify-instance-attribute`
> EC2 인스턴스의 속성 변경하기

#### `--disable-api-stop`
> 실행 중이거나 중단된 instance 의 중지 방지를 **활성화** 시키기.

`aws ec2 modify-instance-attribute --instance-id <instanceID> --disable-api-stop`

#### `--no-disable-api-stop`
> 실행 중이거나 중단된 instance 의 중지 방지를 **비활성화** 시키기.

`aws ec2 modify-instance-attribute --instance-id <instanceID> --no-disable-api-stop`

- The Result:  
  ```shell
  {
      "StoppingInstances": [
          {
              "CurrentState": {
                  "Code": 64,
                  "Name": "stopping"
              },
              "InstanceId": “<instanceID>”,
              "PreviousState": {
                  "Code": 16,
                  "Name": "running"
              }
          }
      ]
  }
  ```

[↑ return to TOC](#table-of-contents)
