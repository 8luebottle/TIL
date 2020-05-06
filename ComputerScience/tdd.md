# TDD
> Reference : [Clean Code By. Robert C. Martin](https://www.goodreads.com/book/show/3735293-clean-code)

**TDD** : **T**est **D**riven **D**evelopment

### Table of Contents

- [About TDD](#about-tdd)
- [F.I.R.S.T](#first)
  - [Fast](#fast)
  - [Independent](#independent)
  - [Repeatable](#repeatable)
  - [Self-validating](#self-validating)
  - [Timely](#timely)
- [Red Green Refactor](#red-green-refactor)
  - [Red](#red)
  - [Green](#green)
  - [Refactor](#refactor)

## About TDD

TDD란 Test Code를 먼저 작성하고 그 이후에 해당 테스트를 만족시키는 실제 코드를 작성해나가는 개발 방법중 하나다.  

## F.I.R.S.T

깨끗한 코드는 테스트 코드 조차 깨끗해야 한다.  
이를 달성하기 위해 F.I.R.S.T 룰이 적용된다.  

### Fast

**속도는 빠르게**  
테스트 코드는 한번 작성한 후 한번 돌려봄으로써 끝나지 않는다.  
유지보수를 하며 코드를 개선해 나갈때 지속적으로 테스트 코드를 돌려봐야 한다. 

> 빠르게 돌아갈 수 있는 테스트 코드를 짜야 한다.

### Independent

**독립성을 지닌**  
여러개의 테스트가 서로 의존성을 지니면 안된다.  
한 테스트는 한 개념만 담당하여 테스트 하도록 코드를 짜야 한다. 테스트 코드가 독립적이지 못하고 서로 의존성을 지닌다면 특정 부분에서 테스트가 실패했을 시 결함을 찾아내기가 어려워진다.  

> 독립성을 지닌 테스트 코드를 짜야 한다.

### Repeatable

**반복 가능한**  
환경에 영향 받지 않는 테스트 코드를 만들어야 한다.  
테스터가(테스트 코드를 돌려보는) 인터넷이 연결가능한 상황에 있던 아니던, QA 환경이던 실제 환경이던 간에 테스트 가능하도록 만들어야 한다.

> 환경에 구애받지 않고 반복 가능한 코드를 짜야 한다.

### Self-validating

**자체 검증 가능한**  
테스트의 결과값은 성공(Pass) 혹은 실패(Fail) 두 가지 상황만 존재해야 한다.  
Pass/Fail 이라는 boolean 결과 값을 리턴하도록 테스트 코드를 작성해야 한다. 한눈에 실패인지 성공인지 알 수 있도록 해야하며 통과 여부를 가려내기 위해 로그 파일을 읽게 해서는 안 된다.  

> 테스트 코드의 결과값은 성공 아니면 실패가 되도록 짜야 한다.

### Timely

**적시에**  
TDD 에서의 테스트 코드는 실제 코드를 구현하기 전에 먼저 짜게 된다.  
실제 코드 구현된 후에 테스트 코드를 짜게 될 시 어려움을 느끼는 경우가 많다. 먼저 테스트 코드를 작성하고 이를 만족시키는 실제 코드를 구현해 나간다.

> 테스트 코드는 적시에 짜야 한다.

[↑ return to TOC](#table-of-contents)

## Red Green Refactor
<img width="200" alt="RGR" src="https://user-images.githubusercontent.com/48475824/81224680-0e83df80-9023-11ea-9601-73d57f6d05f9.png">

Red, Green, Refactor 이라는 세 단계 싸이클로 TDD가 진행된다.

### Red
### Green
### Refactor

[↑ return to TOC](#table-of-contents)