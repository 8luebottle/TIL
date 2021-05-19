# Network Topology

다양한 통신망의 구성 형태에 대해 알아보도록 하자.

### Table of Contents
* [About Network Topology](#about-network-topology)
  * [Bus](#bus)
  * [Hybrid](#hybrid)
  * [Mesh](#mesh)
  * [Ring](#ring)
  * [Star](#star)

## About Network Topology

통신망의 구성형태(이하 '네트워크 토폴로지'라 한다) 는 물리적 구성형태와 논리적 구성형태로 나뉜다.  
- 물리적 토폴로지  
  구성 요소(노드, 링크)의 배치 형태에 따라 구분  
  - 노드 : 파일 서버, 워크 스테이션, 주변 장치
- 논리적 토폴로지  
  데이터의 흐름에 따라 구분

네트워크가 논리적으로 물리적으로 연결되는 방식에 따라 각기 다른 장단점을 지니게 된다. 대표적으로 사용되는 네트워크 토폴로지는 버스(bus)형, 하이브리드(hybrid)형, 망(mesh)형, 링(ring)형, 성(star)형이 있다.  

용도에 맞는 네트워크 토폴로지를 선택하기 위해서 고려해야 할 사항은 아래와 같다.  
- 비용  
- 내결함성
- 회선의 종류  
- 확장의 필요성


### Bus
> Backbone Topology 또는 Line Topology 라고도 불린다.  

한개의 통신 회선(cable)에 여러 노드들이 연결된 형태. 회선의 양쪽 끝부분에 Terminator 가 필요하다. 각각의 노드들은 Adapter 로 연결되어 있다.

보통 버스형은 LAN 과 같이 작은 규모의 네트워크에 사용된다.

<img src="https://user-images.githubusercontent.com/48475824/118780328-e4682d00-b8c6-11eb-8d1b-6240cffcbce3.png" alt="topology diagram info" title="topology diagram info" width="180" />

![bus topology](https://user-images.githubusercontent.com/48475824/118779638-35c3ec80-b8c6-11eb-9ff0-7e1f46e49e2f.gif)


#### 장점
- 간편한 설치  
  간단한 구조로 인해 설치가 어렵지 않음
- 저렴한 비용  
  다른 토폴로지에 비해서 적은 길이의 케이블이 사용됨
- 특정 노드가 실패 했을 시 다른 노드에 영향을 주지 않음
- 쉬운 노드의 추가 및 삭제

#### 단점
- 메인 회선이 고장났을시 네트워크 전체에 영향을 줌
- 병목 현상  
  한 회선에서 단일한 방향으로 데이터가 흐른다.  
  대용량의 트래픽에 적합하지 않으며 그로인해 버스형은 작은 규모의 네트워크에 사용된다.  
  - 예) LAN  

  각각의 노드들이 한가지 회선의 대역폭을 공유하기 때문에 연결된 노드의 수가 늘어나면 늘어날 수록 성능은 저하된다.
- 연결 가능한 노드수가 한정적임  
  버스의 길이가 한정적이기 때문에 연결 가능한 노드도 한정적
- 낮은 보안성  


### Hybrid  
두가지 이상의 통신망의 구성 형태가 함께 사용되는 토폴로지.  
- 예)  
  - Start + Bus Topology
  - Start + Ring Topology

### Mesh
각각의 노드는 다수의 노드들과 연결되어 그물망의 형태를 지니게 된다.  
망형은 두 가지 타입으로 구분된다.  
- Full Mesh
- Partial Mesh

### Ring
각각의 노드들은 두 개의 이웃(근접한) 노드들과 연결돼 있다. 연결된 노드들은 고리의 형태를 이룬다.  

#### 장점
- 간편한 설치  
- 저렴한 비용  
  버스형과 마찬가지로 적은 길이의 케이블이 사용됨


#### 단점
- 낮은 보안성  
- 어려운 노드 추가 및 삭제

