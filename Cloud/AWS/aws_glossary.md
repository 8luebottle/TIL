# AWS Glossary 
AWS 용어를 간략하게 알아보자.  
세부적인 내용은 각각의 개별적 Markdown file에서 참고 가능하다.  

> 링크를 클릭하여 이동 

| [A](#A) | [B](#B) | [C](#C) | [D](#D) | [E](#E) | [F](#F) | [G](#G) | [H](#H) | [I](#H) | [G](#G) | [K](#K) | [L](#L) | [M](#M) | [N](#N) | [O](#O) |
 [P](#P) | [Q](#Q) | [R](#R) | [S](#S) | [T](#T) | [U](#U) | [V](#V) | [W](#W) | [X, Y, Z](#XYZ) |[References](#References)|

 ---

## A
  * [**AMI**](https://docs.aws.amazon.com/general/latest/gr/glos-chap.html#AmazonMachineImage)  
  Amazon Machine Image  
  OS의 서버 이미지  
  Instance를 시작할 때 AMI를 지정해주어야 한다.

## B
## C
  * [**CDN**](https://docs.aws.amazon.com/general/latest/gr/glos-chap.html#content-delivery-network)  
  Content Delivery Network  
  CloudFront로써 data, video, application 및 API를 안전하고 빠르게 전송한다.


## D
  * [**Direct Connect**](https://aws.amazon.com/directconnect/)  
  전용선  
    * **Direct Connect 사용시의 장점**  
      1. 대역폭 비용 감소
      1. 일관된 네트워크 성능
      1. 모든 AWS Service와 호환 가능
      1. 간편성
      1. 탄력성
      1. Amazon VPC로 Private 연결
  
  * [**DNS**](https://docs.aws.amazon.com/general/latest/gr/glos-chap.html#domainnamesystem)  
  Domain Name System  
  문자로된 인터넷 주소를 Numeric IP Address<small>(숫자)</small>로 바꿔준다. 혹은 그 반대도 가능. 
    * 예)  
      <code>babytiger.netlify.com/</code> <--> <code>20X.189.105.112</code>  

  인간에겐 문자가 편리 | 컴퓨터에겐 숫자가 편리


## E
| [A](#A) | [B](#B) | [C](#C) | [D](#D) | [E](#E) | [F](#F) | [G](#G) | [H](#H) | [I](#H) | [G](#G) | [K](#K) | [L](#L) | [M](#M) | [N](#N) | [O](#O) |
 [P](#P) | [Q](#Q) | [R](#R) | [S](#S) | [T](#T) | [U](#U) | [V](#V) | [W](#W) | [X, Y, Z](#XYZ) |[References](#References)|
  * [**EBS**](https://aws.amazon.com/ebs/)  
  Amazon Elastic Block Store  
  하드디스크  
    * **Volume**  
    EBS로 생성한 디스크를 volume 이라고 일컫는다.
      * 4 Volume Types  
        1. Provisioned IOPS SSD (io1)
        1. General Purpose SSD (gp2)
        1. Throughput Optimized HDD (st1)
        1. Cold HDD (sc1)

  * **Elastic IP Address**  
  공인 IP 이지만 한번 할당되면 변하지 않는다.
  
  * [**EC2**](https://aws.amazon.com/ec2/)  
  Elastic Compute Cloud  
  서버

  * [**Elastic Load Balancing**](https://aws.amazon.com/elasticloadbalancing/)  
  들어오는 Traffic 분산시 사용 
      * **3 Types**
        1. **Application Load Balancer**  
          HTTP / HTTPS 트래픽에 적합
        1. **Network Load Balancer**  
          TCP / UDP / TLS 트래픽에 적합
        1. **Classic Load Balancer**  
          EC2 Instance에서 기본적인 로드 밸런싱을 제공


## F
  * **Firewall**  
  방화벽  
  인터넷에서 네트워크를 차단, 허용시 사용

## G
## H
## I
  * [**IGW**](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html)  
  Internet GateWay  
  IGW는 VPC의 Instance와 Internet 간에 통신할수 있도록 해준다.  
  IPv4, IPv6 를 지원.

## J 
## K
## L

## M
## N
## O
## P
  * **Public IP Address**  
  변경되는 공인 IP  
  AWS Instanc 시작할때 임의 IP로 할당된다.

## Q
## R
## S
  * [**S3**](https://aws.amazon.com/s3/)  
  Amazon Simple Sroage Service  
  Image, Video, Mp3등의 콘텐츠 저장 서비스. 

## T
## U
## V
  * [**VPC**](https://aws.amazon.com/vpc/)  
  Virtual Private Cloud  
  네트워크 할당시 사용  
    * IP 주소 범위 선택
    * Subnets 생성    
    * Route table 및 Network Gateways 구성

## W
## X, Y, Z
## References
  * [AWS Glossary](https://docs.aws.amazon.com/general/latest/gr/glos-chap.html)
  * [AWS 전문가 되기](https://brunch.co.kr/@topasvga/76)
