# Redis
**Re**mote **Di**ctionary **S**erver 의 약자  
<img width="200" alt="Redis" src="https://user-images.githubusercontent.com/48475824/76482720-57bb1700-6458-11ea-8e1e-f666ad03f5c2.png">  
 Redis는 Salvatore Sanfilippo 가 만든 오픈소스 저장소이다.  
 2009년 5월 10일 처음 릴리즈 되었다. 안정성이 검증되어 수많은 회사들이 사용하고 있다.
 * Well Known Companies using redis
    * Instagram
    * Uber
    * Twitter
    * Pinterest
    * Snapchat
    * Github
    * Flickr
    * Slack
    * Medium
    * Samsung
    * Naver
    * etc...
 
 ### Table of Contents
 * [Redis Basic](#redis-basic)  
   Redis 특징 | Redis 장단점 | Redis 와 Cache
   
 * [Redis Data Structre](#redis-data-structure)  
   Redis Collection
   * Hash
   * List
   * Set
   * Sorted Set
   * Strings

 * [Redis Use Cases](#redis-use-cases)  
   Authorization | Chat | Cache | Leaderboards | Queue

 * [Redis Memory](#redis-memory)  
   메모리 한계 | 메모리 관리

   
 ## Redis Basic
 ### Redis 특징
 * NoSQL
 * In-memory Solution
 * Key-Value
 * Single Thread

#### NoSQL
다양한 종류의 NoSQL 데이터베이스가 존재한다.  
Key-value 방식은 NoSQL의 가장 기본적인 구조인데 Redis 는 Key-Value 기반이다.  
 * NoSQL 의 다른 구조 : Graph, Document, Column Store

가변적인 구조로 데이터를 저장 할 수 있다.  
<img width="985" alt="no-sql" src="https://user-images.githubusercontent.com/48475824/76520652-a7c0ca80-64a6-11ea-8f4a-87a0fba4822e.png">

[Image Source](https://www.scylladb.com/resources/nosql-vs-sql/)

#### In-memory Solution
Redis 는 In-memory 기술을 사용한다.  
하드디스크에서 데이터를 처리하는게 아닌 메모리 안(In-memory)에서 데이터를 관리한다.  

CPU(Processor)와 물리적으로 가깝게 위치해 있을수록 속도가 빠르다.  
메모리(SDRAM)는 디스크보다 CPU에 근접해 있기에 처리 속도가 몇 백배 빠르다. 

<img width="350" alt="Memory Diagram" src="https://user-images.githubusercontent.com/48475824/76518656-d9d02d80-64a2-11ea-8cf2-2f7fd977540d.png">

[Image Source](https://hazelcast.com/glossary/memory-caching/)

<!-- 메모리 기반으로 데이터를 관리하기 때문에 디스크 접근 으로 걸리던 시간을 줄임. -->

#### Key-Value
키-값 기반으로 데이터를 저장한다.  
값에 올 수 있는 자료형은 총 다섯가지 유형으로써 아래와 같다.  
 * Hash
 * List
 * Set
 * Sorted Set
 * String

속성은 키와 값 두 가지만 존재한다. 

#### Single-Thread
한번에 하나의 명령만 실행할 수 있다. 

 
### Redis 장단점
#### 장점
* 빠른 속도
* 영속적 데이터 보존
* 편의성 향상
* 낮은 개발 난이도

#### 단점
* 메모리 파편화
<!-- * 응답 속도 -->

### Redis 와 Cache
 

[↑ return to TOC](#table-of-contents)

## Redis Data Structure
### Redis Collections  
Redis는 5가지의 데이터 구조를 제공한다.  
* Hash
* List
* Set
* Sorted Set
* Strings

#### Hash
Key 와 Value 로 이루어진 Object 와 같은 형태의 데이터를 저장하기 좋다.  
Key 와 Key 의 Sub Key 가 존재한다.  
```hmset <set> <subkey1> <value1> <subkey2> <value2>```  
```hmget <key> <subkey>```  
```hget <key>```  
```hgetall <key>```  

#### List  
배열 형태의 데이터 구조  
* Push  
  ```lpush <key> <value>```  
  ```rpush <key> <value>```
* Pop  
  ```lpop <key>```  
  ```rpop <key>```

#### Set
파이썬의 Set 처럼 순서가 없고 중복된 값이 없는 구조  
보통 Redis에서 Set은 데이터의 유무 확인을 위해 사용한다.  
```sadd <key> <value>```  
```smembers <key>```  
```sismember <key> <value>```

#### Sorted Set
Redis 에서 자주 사용되는 자료구조  
Set의 특징을 갖고 있지만 Score 를 통해 순서를 정할 수 있다.  
  * 주의할 점 : Score 는 Double 타입으로서 값이 정확하지 않다. 실수가 표현 할 수 없는 값들이 있다는 것을 염두에 두어야 한다.
    * 해결법 → String 형태로 데이터 전달하기.

```zadd <key> <score> <value>```  
```zrange <key> <startindex> <endindex>```  

#### Strings
Key-Value 매핑 구조  
* Single Key  
  ```set <key> <value>```  
  ```get <key>```
* Multi Key  
  ```mset <key1> <value1> <key2> <value2> <key3> <value3>```  
  ```mget <key1> <key2> <key3>```

#### 주의 사항
**Collection**

## Redis Use Cases
* Authorization
* Chat
* Cache
    * Full Page Cache
    * Session Cache
* Leaderboards
* Queue  

[↑ return to TOC](#table-of-contents)


## Redis Memory

### 메모리 한계
#### maxmemory configuration  
Max Memory 최대 메모리 용량을 설정함으로써 그 이상을 사용하지 못하도록 함.   
이 이상을 넘어갈 시에는 Option을 설정.  

**maxmemory policy**
1. noeviction  
  기존 데이터를 보존.  
  OOM 오류를 반환하고 새로운 데이터는 버림.
    * OOM : Out Of Memory
1. allkeys-lru  
  LRU 알고리즘을 통해 데이터를 삭제.  
    * LRU : Least Recently Used
1. volatile-lru  
  기본 값  
1. allkeys-random  
  렌덤하게 데이터를 삭제시켜 저장 공간 확보.  
1. volatile-random
  expire set 중 렌덤으로 데이터를 삭제.  
1. volatile-ttl 
  expire set 중 TTL 값이 짧은 것 부터 삭제.  
    * TTL : Time To Live
1. allkeys-lfu  
  가장 적게 엑세스된 키를 제거하여 저장 공간 확보.  
1. volatile-lfu
  expire set 중 가장 적게 엑세스 된 키 순으로 삭제.  

**eviction**  
Eviction 이란 Maxmemory 초과로 데이터가 지워지는 것을 뜻한다.  
 
### 메모리 관리  
하나의 큰 Instance 를 사용하는 것 보다는 여러개의 작은 Instances 를 사용하는 것이 안정성이 높다.

**ziplist**  
메모리를 적게 쓰기 위해서 ziplist를 사용할 수 있다.  
List, Hash, Sorted Set 과 같은 구조를 ziplist 로 바꿀 수 있다.

[↑ return to TOC](#table-of-contents)