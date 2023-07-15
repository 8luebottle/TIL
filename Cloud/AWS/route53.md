# Route53

> Reference : [Route53](https://aws.amazon.com/route53/)

### Table of Contents

- [About](#about)
- [The Origin of Name](#the-origin-of-name)
- [Record Types](#record-types)
- [Routing Policies](#routing-policies)

# About

> AWS 의 DNS 서비스  
> Amazon Route 53 is a `highly available` and `scalable` Domain Name System (DNS) web service.

- `highly available`
  - Route53 이 지속적으로 이용 가능한 상태를 유지하는 능력
- `scalable`
  - Rout53 이 변화하는 요구 사항에 따라 자원을 효율적으로 확장할 수 있는 능력
    - 트래픽 증가/감소 시 유연하게 대응 가능
  - e.g. 많은 양의 DNS 쿼리 트래픽 처리를 위해 자동으로 리소스를 확장
    - DNS query == request
      - Query: 사용자가 domain name 에 대한 IP 주소를 질문하기 때문

- DNS 는 인터넷에서 도메인 이름(www.example.com)을 IP 주소(192.0.2.1)로 변환하는 역할을 한다.
- 도메인 이름과 IP 주소간의 매핑 관리
- 사용자 도메인 이름 요청을 처리하여 internet application 으로 트래픽을 라우팅.
  - Internet application:
    - Website
    - Web Application
    - API service
    - Etc

# The Origin of Name

- `Route`
  - 경로 설정, 라우팅과 관련
- `53`  
  DNS의 기본 포트 번호인 53번 에서 비롯.
  - DNS는 도메인 이름과 IP 주소 간의 매핑을 관리하는 프로토콜.
  - 보통 TCP/UDP port 53 을 사용하여 통신을 지원.

[↑ return to TOC](#table-of-contents)

# Record Types

각 레코드는 타입을 지니며 아래는 Route 53 에서 지원하는 레코드 타입이다. 각각의 레코드 타입은 특정한 목적과 역할을 지니고 있다.

### A (Address Record):

- 도메인 이름을 IPv4 주소로 매핑.
- e.g. `192.0.2.1`

### AAAA (IPv6 Address Record):

- 도메인 이름을 IPv6 주소로 매핑.
- e.g. `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

### CNAME (Canonical Name Record):

- 도메인 이름을 다른 도메인 이름으로 별칭(alias)화.
  - 다른 도메인 이름에 매핑 가능.
- e.g. `example.com`

### CAA (Certification Authority Authorization):

- 인증서 발급을 허용하는 인증 기관(Certificate Authority)을 지정.
- 도메인에 대한 인증서 발급 권한을 제한.
- e.g. `0 issue "letsencrypt.org"`

### MX (Mail Exchange Record):

- 도메인 이름과 연관된 이메일 서버를 지정.
  - 이메일 트래픽을 처리할 이메일 서버를 설정.
- e.g. `10 mail.example.com`

### NAPTR (Name Authority Pointer Record):

- ENUM(전화번호와 인터넷 도메인 이름 간의 매핑) 서비스를 위해 사용.
  - 전화번호와 도메인 이름 간의 연결 정보를 제공.
- e.g. `100 10 "U" "E2U+sip" "!^.*$!sip:info@example.com!" .`

### NS (Name Server Record):

- 도메인에 대한 네임 서버를 지정합니다.
- e.g. `ns1.example.com`

### PTR (Pointer Record):

- IP 주소를 도메인 이름으로 매핑.
- IP 주소의 역방향(DNS reverse lookup) 조회 지원.

### SOA (Start of Authority Record):

- 도메인의 권한 부여 시작 지점을 지정.
- 도메인 이름, 메일 주소, 시리얼 번호, 갱신 주기, 재시도 주기 etc.

### SPF (Sender Policy Framework):

- 이메일 송신자가 허용되는 서버를 지정.
  - 도메인에 대한 이메일 발송을 승인하는 서버를 지정.
- e.g. `"v=spf1 include:_spf.google.com ~all"`

### SRV (Service Locator):

- 도메인 이름과 연관된 서비스 및 해당 서비스의 위치를 지정.
- e.g. `10 60 5060 sipserver.example.com`

### TXT (Text Record):

- 도메인에 대한 텍스트 정보를 저장.
  - e.g. SPF 설정, DKIM 레코드 etc.

[↑ return to TOC](#table-of-contents)

# Routing Policies

> 路由策略

Route53 에서 제공하는 라우팅 정책은 아래와 같다. 트래픽을 어떻게 처리하고 분배할지를 결정한다.

### 단순 라우팅 정책

> Simple routing policy 简单路由策略

- 하나의 리소스만 있는 경우. 도메인에 대한 모든 트래픽을 단일 리소스로 전달.
  - e.g. 단일의 웹 서버
- 특별한 조건이나 가중치에 따라 트래픽 분산 X

### 장애 조치 라우팅 정책

> Failover routing policy 故障转移策略

- 액티브-패시브 장애 조치(Active-Passive Failover)를 구성하려는 경우에 사용.
  - 기본 리소스(Active 主动)
    - 활성 상태로 운영되는 리소스
  - 백업리소스(Passive 被动)
    - 비활성 성태로 대기하고 있는 리소스
- 기본 리소스가 정상적으로 작동하지 않을 경우 해당 정책은 자동으로 트래픽을 백업 리소스로 전환.

### 지리 위치 라우팅 정책

> Geolocation routing policy 地理位置路由策略

- 사용자 위치에 따른 라우팅 정책. CDN, DB Server 등 지리위치 기반으로 서비스를 최적화 하기 용이.
- 지리적 위치에 따라 트래픽을 분배.
- 사용자의 IP주소를 기반으로 위치를 결정한다.

### 지리 근접 라우팅 정책

> Geoproximity routing policy 地理位置临近度路由

- 리소스 위치 정보를 토대로 최적의 트래픽 경로를 결정.
- 글로벌한 앱의 트래픽을 분산하고 성능 향상용.

### 지연 시간 라우팅 정책

> Latency routing policy 延迟路由策略

- 리소스 중 최상의 지연 시간을 제공하는 리전으로 트래픽을 라우팅해줌.
- 다수의 리전에 리소스가 분산되어 있을 경우 유리.
  - 사용자들에게 가장 가까운 리전으로부터 제공하기에 응답 시간 최소화.

### IP 기반 라우팅 정책 

> IP-based routing 基于 IP 的路由

- 사용자의 IP 주소를 분석하여 트래픽을 적절한 리소스로 전달.
- 보통 사용자의 위치에 따라 트래픽을 라우팅하기 위해 사용.
  - 전세계적으로 분산된 사용자들에게 최상의 성능 제공.

### 다중 응답 라우팅 정책

> Multivalue answer routing policy 多值应答路由

- 무작위로 선택된 최대 8개(다중)의 정상 레코드로 응답.
- 다중 리소스를 동시에 사용하여 트래픽을 분산하기 위해 사용.
  - 로드 밸런싱 효과.
  - 가용성 및 성능 향상.

### 가중치 기반 라우팅 정책

> Weighted routing policy 加权路由策略

- 사용자가 지정해 놓은 트래픽 비율에 따라 여러 리소스로 라우팅.
- 다수의 리소스/엔드포인트가 존재할 경우 원하는 비율에 맞추어 분배 가능.

[↑ return to TOC](#table-of-contents)
