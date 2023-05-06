# Thread-safe data structure
> Thread-safe 한 자료구조 | 线程安全的数据结构

### Table of Contents
- [Types](#types)

## Types
여러개의 스레드가 동시에 접근해도 안전하게 사용할 수 있는 자료구조 종류.

1. Concurrent data structures
   > 동시성 자료구조 并发数据结构  

   여러개의 스레드에서 동시에 접근해도 안전하게 도착.
    - e.g.
      - ConcurrentHashMap
        - 동기화된 버킷 분할방식을 사용, 경합을 줄임.
      - ConcurrentLinkedQueue
        - 원자적 연산을 사용하여 Queue 에 아이템을 추가/삭제.
      - ConcurrentSkipListMap 
1. Synchroinized data structures
    > 동기화 자료구조 同步数据结构
    - e.g.
      - Synchronized lists
      - Synchronized stacks
      - Synchronized queues
1. Immutable data structures
    > 불변 자료구조 不可变数据结构
    - e.g.
      - ImmutableMap
        - 한번 생성되면 key-value 값 변경 X.
      - ImmutableList
        - 원소 추가, 제거, 변경 X.
        - read 작업이 많은 상황에 유용.
1. Lock-free data structures
    - e.g.
      - Lock-free stacks
      - Lock-free queue 
1. Wait-free data structures
    - e.g.
      - Wait-free stacks
        - lock 기다림 없이 stack 에 접근하여 push/pop 연산 수행.
        - 위험성:
          - 메모리 누수
          - 우선순위 역전
          - 처리량 감소
      - Wait-free queue
