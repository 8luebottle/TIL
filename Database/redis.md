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
 * In-Memory Solution
 * Key-Value
 * Single Thread
 
 ### Redis 장단점
 ### Redis 와 Cache
 
 
## Redis Data Structure
### Redis Collections
* Hash
* List
* Set
* Sorted Set
* Strings
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

## Redis Memeory
### 메모리 한계
#### maxmemory configuration  
Max Memory 최대 메모리 용량을 설정함으로써 그 이상을 사용하지 못하도록 함. 이 이상을 넘어갈 시에는 Option을 설정.  

**maxmemory policy**
1. noeviction
1. allkeys-lru
1. volatile-lru
1. allkeys-random
1. volatile-random
1. volatile-ttl
1. allkeys-lfu
1. volatile-lfu

**eviction**

 
### 메모리 관리  
하나의 큰 Instance 를 사용하는 것 보다는 여러개의 작은 Instances 를 사용하는 것이 안정성이 높다.

**ziplist**
