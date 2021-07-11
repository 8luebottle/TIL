# MMU
메모리 관리 장치(MMU)에 대해 알아보자.

### Table of Contents
- [About MMU](#about-mmu)
  - [Role of MMU](#role-of-mmu)
  - [2 Registers](#2-registers)
- [Address Translation](#address-translation)  
  Logical Address Vs. Physical Address
  - [Why Logical Address is Required](#why-logical-address-is-required)


## About MMU
> MMU : Memory Management Unit  

MMU는 메모리를 관리해주는 하드웨어 부품이며 보통 CPU의 일부분으로 구성되어 있다 (별도의 칩으로 사용되기도 함).  

* **현재 사용하는 노트북의 예)**  
  2019년 형 MacBook Pro 16-inch 모델에서 사용되는 프로세서(CPU) 는 Intel의 i7 9th Generation 이다. 이 프로세서에 MMU가 존재한다.

  ![macbook-intel-i7-processor](https://user-images.githubusercontent.com/48475824/121796210-59bee780-cc52-11eb-81a2-f3741f0bfe0a.gif)
  ![intel-i7-MMU](https://user-images.githubusercontent.com/48475824/121797255-21230c00-cc5a-11eb-95ee-81c4aad07f4f.png)  

### Role of MMU
MMU가 담당하는 역할은 몇가지가 존재하는데 그 중 주된 역할은 `주소변환` 역할이다. `논리적 주소`를 `물리적 주소`로 변환시켜 준다.  
이 외에도 `캐시 통제`, `권한 통제`, `메모리 보호`, `읽기/쓰기 보호`, `버스 중재` 등의 역할을 담당한다. 이 모든것은 메모리 관리와 관련이 있다.  

### 2 Registers
MMU 에는 두개의 레지스터가 존재한다.  
- **MDR : Memory Data Register**  
  메모리(메인 메모리)에 보내지게 될 데이터가 저장된다.  
- **MAR : Memory Address Register**  
  논리적 주소는 MAR 에 저장된다.  

[↑ return to TOC](#table-of-contents)

### Address Translation
MMU는 `논리적 메모리 주소`를 `물리적 메모리 주소`로 변환해준다.  
- **Physical Address 물리적 주소**  
  물리적 주소는 실제 하드웨어 부품인 RAM 칩에서 사용하는 실질적 주소를 의미한다.  
- **Logical Address 논리적 주소**  
  가상 주소(Virtual Address)라고도 불리우는 논리적 주소는 진짜 주소인 물리적 주소와 대조된다. 물리적으로 존재하는 주소는 아니지만 메모리를 안전하게 관리하기 위해서 사용된다.  
  - 우리가 사용하는 프로그램은 논리적 주소를 사용한다. 즉, 프로그램은 물리적 주소를 알지 못한다.  
  - 논리적 주소는 CPU로 부터 생성된다.  

논리적 주소는 CPU가 생성하며 MMU는 이를 물리적 주소로 변환하여 준다.  

![logical-to-physical](https://user-images.githubusercontent.com/48475824/121799816-2b98d200-cc69-11eb-96dc-321a1aa4464a.png)


#### Why Logical Address is Required
물리적 주소와 논리적 주소를 구분짓게 된 이유가 있다.

논리적 주소의 탄생 이전, 프로그램은 실제 물리적 주소를 사용했었다.  
유저는 컴퓨터 사용시 보통 둘 이상의 프로그램들을 함께 돌린다. 각각의 프로그램이 유효한(사용 가능한) 주소만 사용하면 평화롭고 지속적으로 컴퓨터를 사용 가능하지만 문제는 서로 다른 프로그램이 동일한 주소를 사용하려 할 때 발생한다.  
- 문제 상황의 예)  
  IDE 로 코딩을 진행중이던 사용자는 Podcast를 듣고 있다.  
  코딩을 하다 막히는 부분으로 인해 browser 를 킨후 의문점을 검색하려는 순간, browser 는 Podcast 가 사용하고 있던 동일한 물리 주소를 참고하였다. !!문제 발생!! 
  - 메모리 보호의 필요성 : 프로그램의 프로세스들이 안전하게 격리되어 운용되도록 해야함.
  - 읽기/쓰기 보호의 필요성 : 읽기와 쓰기 가능/불가능 영역의 구분이 필요함.

[↑ return to TOC](#table-of-contents)