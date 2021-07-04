# Scheduling
Scheduling 을 통해 CPU를 효율적으로 사용할 수 있다.  

### Table of Contents
* [About Scheduling](#about-scheduling)
  * [Processs state](#process-state)
  * [PCB](#pcb)
* [Scheduling Algorithms](#scheduling-algoritms)
  * [Criteria](#criteria)

## About Scheduling  
스케쥴링은 preemtive와 non-preemtive 방식이 존재한다.

- Preemtive Scheduling 선점 스케쥴링
- Non-Preemtive Scheduling 비선점 스케쥴링  

### Process state
프로세스의 상태는 아래의 다섯가지로 나눌수 있다.

1. **New**  
  생성: process가 생성되어진 상태  
1. **Ready**  
  준비: process가 CPU에서 실행 될 때 필요한 모든 리소스가 준비 완료 되어 있는 상태  
1. **Running**  
  실행: process가 CPU에서 실행되고 있는 상태  
1. **Waiting**  
  대기: process가 특정 이벤트를 기다리고 있는(실행되고 있지 않은) 상태  
1. **Terminated**  
  완료: process의 실행이 완료 또는 중단된 상태  

![process state](https://user-images.githubusercontent.com/48475824/124386488-aa87a480-dd15-11eb-824b-5809e797822e.png)

CPU 는 `ready` 상태에 놓여있는 여러 프로세스중 하나의 프로세스를 선택한다.  

### PCB 
> PCB: Process Control Block  
OS가 프로세스를 제어하기 위해 필요한 정보들은 `프로세스 제어 블록`(PCB) 에 저장되어 있다.  

![pcb](https://user-images.githubusercontent.com/48475824/124385633-8aee7d00-dd11-11eb-9f90-654179aab208.png)  
- Process state  
  프로세스 상태 관련 데이터가 담겨 있다.  
  (New, Ready, Waiting, Running, Terminated)
- Process number  
- Process counter  
  프로세스 카운터  
- Registers
- Memory Limits
- List of open files


## Scheduling Algorithms  
스케쥴링 알고리즘은 아래와 같은 것들이 있다.  
- **FCFS**  
  First Come, First Served
- **RR**  
  Round Robin
- **SJF**  
  Shortest Job First
- **Multilevel Feedback Queues**  
- **Lottery Scheduling**  

### Criteria
좋은 스케쥴링 알고리즘을 판별하기 위한 기준  
- CPU Utilization
- Throughput
- Turnaround time
- Waiting time
- Response time
