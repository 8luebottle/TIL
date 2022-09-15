# SES
> Reference: [Amazon SES](https://aws.amazon.com/ses/)

SES: **S**imple **E**mail **S**ervice  
Amaozon 의 Inbound & Outbound 이메일 서비스.

<img width="120" alt="SES" src="https://user-images.githubusercontent.com/48475824/190214158-8a49c8a5-109a-4b19-a365-4c5327a066c8.png"> 


### Table of Contents
- [About](#about)
  - [Use Cases](#use-cases)
  - [Relative Services](#relative-services)
  - [Region](#region)
  - [Send Box](#send-box)
- [Send](#send)
- [Receive](#receive)
- [SES w/ SNS](#ses-w-sns)

## About
Amazon 에서 제공하는 SES 를 통해 편리하고 빠르게 보안성 있는 이메일 솔루션을 구축할 수 있다.
- **편리성:**  
  이메일 솔루션을 구축하기 위해서는 여러가지 인프라구성이 필요하다. SES 를 사용한다면 여러 인프라를 단계별로 복잡하게 설정할 필요가 없다.
  - e.g. Network configuration, Email server management, IP address reputation, etc.

### Use Cases
- 이메일 자동화  
  개별, 대량의 이메일 전송 자동화
- 마케팅용 이메일  
  광고, 뉴스레터, 새 상품 입고알림 등
- 온라인 쇼핑  
  구매확정, 예약 주문 정보, 배송 정보 등

### Relative Services
AWS SES 와 함께 쓰이는 AWS 서비스는 아래와 같다.  
- **IAM**  
  이메일 전송과 관련하여 사용자 액세스를 제어하기 위한 용도
- **Lambda**  
  이메일 관련 이벤트 트리거 용도
- **SNS**  
  이메일 송수신 관련 알람 용도  
  - 이메일 전송 성공
  - 이메일 전송 실패
- **S3**  
  수신 이메일 저장 용도
- **KMS**  
  이메일 암호화 용도  
- **CloudTrail**  
  AWS SES API 호출 기록 용도
- **EC2**
- **Beanstalk**
- **Amazon CloudWatch**, **Amazon Kinesis Data Firehose**

### Region
현재(09.15.2022 기준) **이메일 수신**이 지원되는 AWS 리전은 총 세곳이다.

|Region| Endpoint |
|:---:|:---:|
|US East (N. Virginia)|inbound-smtp.us-east-1.amazonaws.com|
|US West (Oregon)|inbound-smtp.us-west-2.amazonaws.com|
|Europe (Ireland)|inbound-smtp.eu-west-1.amazonaws.com|

### Send Box
모든 새 계정은 샌드박스에 들어가게 된다. 새 SES 계정에 제한을 두는 이유는 도용 방지, 침해 방지, 그리고 발신자의 평판을 보호하기 위해서다.
- 발신 할당량:  
  하루(24h) 최대 200개.
- 전송 속도:  
  초(1s)당 1개.
- 전송 가능 주소:  
  확인된 주소에만 only.

샌드박스 상태는 region 마다 상이하다.
- 특정 계정이 한 리전의 샌드박스에서 제거되었지만 다른 리전에는 존재할 수 있음.

#### 샌드박스 삭제
AWS Management Console 또는 AWS CLI를 통해 샌드박스에 들어있는 계정 제거 요청을 할 수 있다.
- AWS Support 팀에서 해당 요청에 대해 검토 진행 후 24시간 이내에 응답.
  - 추가 정보 요청을 할 수 있음.
  - AWS 정책에 맞지 않는 경우 요청이 거절 될 수 있음.

[↑ return to TOC](#table-of-contents)

## Send
AWS SES 로 이메일 전송시 아래의 방법을 통해 이메일을 보낼 수 있다.
- SES console
  - 테스트 이메일 전송
- [SES SMTP Interface](https://docs.aws.amazon.com/ko_kr/ses/latest/dg/send-email-smtp.html)
  - 대용량 이메일 전송
- [SES API](https://docs.aws.amazon.com/ko_kr/ses/latest/dg/send-email-api.html)
  - 대용량 이메일 전송
  - curl, HTTPS Request, AWS SDK


[↑ return to TOC](#table-of-contents)

## Receive

[↑ return to TOC](#table-of-contents)

## SES w/ SNS
SES를 사용하면서 알림 기능을 위해 SNS 를 함께 사용하게 된다.  
- 예) 이메일이 반송되었거나 수신 거부된 경우의 알림.

### 알림 내용
SNS 알림 내용은 JSON 형태이다.

**Field Info:**  
- `notificaitonType`
  > 알림 유형
  
  `Bounce`, `Complaint`, 또는 `Delivery` 로 나뉜다.
  - `Bounce`  
    (실패) 이메일 전송이 실패된 경우.
    - Hard Bounce  
      수신자의 메일 서버가 이메일을 영구적으로 거부한 경우.
      - 이메일 수신자의 주소가 존재하지 않음.
    - Soft Bounce  
      SES 가 일정 시간 동안 이메일을 재 전송하였지만 실패한 경우.  
      - 수신자의 받은편지함이 꽉 차 있음.
  - `Complaint`  
    (실패) 수신자가 이메일을 받은 편지함에서 차단(수신 거부)시켜버린 경우.
  - `Delivery`  
    (성공) 이메일 전송이 성공적으로 완료 됨.

- `mail`  
  > 메일에 대한 정보
- `bounce`  
  > 반송 메일에 대한 정보
- `complaint`
  >  수신 거부에 대한 정보
- `delivery`  

[↑ return to TOC](#table-of-contents)
