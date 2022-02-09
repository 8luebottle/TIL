# Buffer Pool 
캐시된 DB의 데이터가 저장되어 있는 공간인 버퍼풀에 대해 알아보자.

### Table of Contents

* [About Buffer Pool](#about-buffer-pool)  
* [Buffer Pool List](#buffer-pool-list)

## About Buffer Pool
DB에서도 데이터를 캐시해 놓는 공간이 존재한다. 이를 버퍼풀(buffer pool) 또는 [버퍼캐시(buffer cache)][buffer cache] 라고 일컫는다. 여타 캐시의 기능의 그러하듯 DB의 버퍼풀 또한 데이터에 접근하는 시간을 줄여 퍼포먼스를 높여준다.
- 데이터: 테이블 및 인덱스

### 퍼포먼스 향상  
대부분의 경우 SQL이 느린 원인은 디스크에서 진행되는 I/O 때문이다. [디스크에서 데이터를 읽거나 쓸 때 arm(actuator arm)][HDD actuator arm] 을 통해서 진행한다. 이러한 물리적 동작으로 적지않은 시간을 사용해야하기에 데이터풀에는 자주 사용되는 [데이터 블록][data block]을 저장해 놓는다. 찾고자 하는 블록을 디스크에 접근 전, 버퍼풀에서 읽는 덕분에 I/O 시간이 대폭 줄어든다.  

## Buffer Pool List
버퍼풀에 저장되어 있는 캐시를 효율적으로 관리하기 위해 MySQL은 블록들을 링크드 리스트로 관리한다. 버퍼풀 리스트의 구성은 아래의 그림과 같다.  

<img width="300" alt="buffer-pool-list" src="https://user-images.githubusercontent.com/48475824/153303357-fd10ca36-9dc2-4efd-b74b-9032b17bbe3a.png">  

An image from a [MySQL][image credit]  

리스트를 다루기 위해 MySQL 에서 사용하는 알고리즘은 LRU(Least Recently Used) 이다. 자주 사용하지 않는 데이터는 버퍼풀에서 제거된다.  
- add: 새로운 페이지(a.k.a block)는 리스트의 중간 지점에 추가 됨 ⇒ midpoint insertion
- remove: 꼬리쪽에 위치한 페이지는 점진적으로 삭제 됨 ⇒ evicted pages


<!-- link -->
[buffer cache]: https://docs.oracle.com/database/121/TGDBA/tune_buffer_cache.htm#TGDBA294
[data block]: ./logical_storage_structure.md#data-block
[HDD actuator arm]: https://babytiger.netlify.app/posts/hdd/
[image credit]: https://dev.mysql.com/doc/refman/8.0/en/innodb-buffer-pool.html
