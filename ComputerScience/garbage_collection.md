# Garbage Collection
> 가비지 컬렉션 | 垃圾收集 | ガーベジコレクション

Garbage Collection에 대해 알아보자.   
이는 자동 메모리 관리의 핵심으로 간주되며, 현대 소프트웨어 개발에서 중요한 개념 중 하나이다.

### Table of Contents
- [The Origin of Garbage Collection](#the-origin-of-garbage-collection)
- [Garbage Collected Languages](#garbage-collected-languages)
- [The Need for Garbage Collection](#the-need-for-garbage-collection)
- [Dynamic Memory Allocation](#dynamic-memory-allocation)

## The Origin of Garbage Collection
> 가비지 컬렉션의 기원

1959년에 미국의 컴퓨터 과학자인 존 맥카시(John McCarthy)가 Lisp에서 수동 메모리 관리를 간소화하기 위해 이 개념을 만들었다.   
이 혁신은 프로그래머들이 메모리 관리로부터 오는 부담을 덜어주었고, 그 결과로 프로그래머들은 코드 개발에 보다 많은 시간과 노력을 집중할 수 있게 되었다.

## Garbage Collected Languages
다양한 프로그래밍 언어가 가비지 컬렉션을 지원하고 있다. 이러한 언어들은 동적 메모리 할당을 사용하고 메모리 관리를 자동화한다.
- Go, Python, Java, JavaScript, C#, Kotlin, PHP, Rust, Swift etc.

### Non-Garbage Collected Languages
가비지 컬렉션을 지원하지 않는 언어들은 수동으로 메모리를 관리해야한다.
- C, C++, Ada, COBOL, Assembly Language etc.

## The Need for Garbage Collection
> 가비지 컬렉션의 필요성

Garbage Collection 이 없을 때 발생하는 문제들은 다음과 같다.

1. **메모리 누수(Memory Leaks)**  
  프로그램이 메모리를 제대로 해제하지 않아 메모리가 계속해서 낭비되는 현상.  
    - 이러한 오류는 예기치 않은 동작을 일으킬 수 있으며, 심각한 버그와 보안 취약점을 초래할 수 있다. 따라서 포인터를 주의 깊게 관리하고 항상 유효한 메모리 위치를 가리키도록 하는 것이 중요하다.
2. **Dangling Pointer**  
  포인터가 더 이상 유효한 메모리 위치를 가리키지 않고 무효한 메모리 위치를 가리킬 때 발생한다.  
  Dangling pointer 는 심각한 버그와 보안 취약점의 원인이 될 수 있다.
    - **댕글링 포인터가 발생하는 시나리오:** 
      - 할당 해제된 메모리  
        포인터가 해제되거나 해제된 메모리를 계속 참조하는 경우  
        - 이 경우 프로그램은 예기치 않은 동작 또는 충돌 현상이 발생할 수 있다.
      - 유효하지 않은 객체  
        포인터가 더 이상 존재하지 않는 객체를 가리키거나 어떤 이유로 유효하지 않은 경우
      - Wild Pointers  
        NULL도 포함하여 아무 것도 초기화되지 않은 포인터
3. **수동 메모리 관리 부담**  
   가비지 컬렉션이 없는 경우, 개발자가 메모리 할당과 해제를 직접 처리해야 한다. 이로 인해 코드가 복잡해지고 버그가 발생하기 쉬워진다.

## Dynamic Memory Allocation
> GC 와 관련된 중요한 개념 중 하나인 `동적 메모리 할당`

- 프로그램 실행 중에 필요한 만큼의 메모리를 동적으로 할당한다:  
  - **동적:** 프로그램이 실행 중에 메모리를 할당하고 해제하면서 메모리 사용을 동적으로 조절할 수 있다. 
  - 데이터 구조의 크기와 모양을 조정할 수 있다.
  - 동적 배열을 만들거나 연결 리스트를 조작할 때 유용.
- 필요하지 않은 메모리는 해제된다:  
  - 동적으로 할당된 메모리는 더 이상 필요하지 않을 때 해제된다. → 메모리 누수 문제 방지.
- 효율적인 메모리 사용을 가능하게 한다:  
  - 메모리를 효율적으로 사용하도록 도와준다. 필요한 메모리만 할당하고 필요하지 않은 메모리를 해제함으로써 메모리 낭비를 최소화하기 때문.

---
### Cited Information:

- [The Garbage Collection Handbook: The Art of Automatic Memory Management](https://www.google.co.kr/books/edition/The_Garbage_Collection_Handbook/wsbJEAAAQBAJ?hl=en&gbpv=1&dq=The+Garbage+Collection+Handbook:+The+Art+of+Automatic+Memory+Management&printsec=frontcover)    
  By Richard Jones, Antony Hosking, Eliot Moss

- [Origins of Garbage Collection](https://groups.seas.harvard.edu/courses/cs252/2016fa/16.pdf)  
  Harvard University  