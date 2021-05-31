# Hub

### Table of Contents
* [About Hub](#about-hub)

## About Hub
![Hub](https://user-images.githubusercontent.com/48475824/120174748-669a0f00-c240-11eb-94e5-086ad11b2a38.png)  
Image credit : [Amazon.com](https://www.amazon.com/NETGEAR-5-Port-Gigabit-Ethernet-Unmanaged/dp/B07S98YLHM/ref=sr_1_3?dchild=1&keywords=ethernet+hub&qid=1622455876&sr=8-3)

네트워크 허브(통상 Ethernet Hub)는 여러개의 장치들을 연결시켜준다.  
허브로 들어오는 데이터는 가야할 곳(정해진 Port)을 모른채 모든 Port 마다 전송된다.  
- **(X) Routing Table** : 허브는 스위치나 라우터처럼 routing table 을 갖고 있지 않다.
- **(X) 보안성** : 모든 노드(장비)마다 데이터가 전송되기에 보안에 취약하다.

허브는 Collision Domain 을 공유하기 때문에 `데이터 충돌`이라는 문제가 발생한다.  
- **Switch** : 장치들을 연결해주는 스위치는 허브가 개선된 버전이라 볼 수 있다.  
  - 향상된 속도 : 허브보다 처리할 수 있는 패킷의 숫자가 더 크다.
  - 충돌 X : 스위치에서는 데이터 충돌이 발생하지 않는데 그 이유는 데이터가 자신의 경로를 알기 때문 이다. 패킷(데이터 전송 단위)의 맨 앞에 붙은 MAC address 를 기반하여 데이터가 전송된다.  
  > [네트워크 토폴로지](https://github.com/8luebottle/TIL/blob/master/Network/network_topology.md) : 성형(Start Topology)의 중앙에 위치한 허브는 이더넷 허브가 아닌 스위치를 지칭한다.
