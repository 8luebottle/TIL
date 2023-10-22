# Context
> 컨텍스트 | 上下文 | コンテキスト |

### Table of Contents
- [About](#about)
- [Key Roles](#key-roles)
- [Do](#do)
- [Don't](#dont)
- [Key Methods](#key-methods)

## About
Go 서버에서 각 요청은 goroutine 을 통해 병렬적으로 처리된다. 고루틴은 동시에 실행되며 서로 간섭하지 않아야 한다. Context 는 이러한 고루틴간의 안전한 데이터 및 정보 공유를 지원한다.

- **목적**: Google 은 Context Package 를 특정한 목적을 가지고 개발하였는데, 이는 복잡한 서버 환경에서 안전하고 효율적인 동시성 처리를 지원하기 위해서였다.

- **명칭**: Context 라는 명칭은 해당 패키지가 주로 요청과 작업의 문맥(context)을 관리하고 전달하기 위해 명명된 것으로, 안전하고 효율적인 동시성 처리를 위한 핵심 구성 요소임을 명확하게 나타내고 있다.

## Key Roles 
Context는 요청을 처리시 보안 자격 증명, 추적 정보, 데드라인, 취소 신호와 같은 정보를 함께 전달한다. 이를 통해 Go 서버는 여러 요청을 동시에 처리하면서도 안전하게 요청 범위의 정보를 공유하고, 각 고루틴이 작업을 중지하거나 시간 초과 등의 조건을 감지할 수 있다.

- `보안 자격 증명`, `추적 정보`, `데드라인` 및 `취소 신호`를 API 및 프로세스 경계를 횡단하여 전달.
  - **보안 자격 증명(security credentials)**:
    - 보안과 관련된 정보 (e.g., 인증 토큰 etc)
  - **추적 정보(tracing information)**:
    - 시스템에서 요청이 어떻게 처리되는가에 대한 정보 (e.g., 추적 ID, 로깅 정보 etc)
  - **데드라인(deadline)**: 
    - 특정 작업을 수행하는데 허용된 시간.
  - **취소 신호(cancellation signals)**:
    - 요청이 취소되었음을 나타내는 신호 (e.g., 사용자 요청 취소, 시간 초과 etc)
      - 사용자 요청 취소: 요청한 페이지의 로딩시간이 길어 요청을 취소한 경우
      - 시간 초과: 특정 작업이 지정된 시간 내에 완료되지 못햇을 경우
      - 에러: 예상치 못한 에러가 발생한 경우
    - Context 가 취소될 경우 파생된 context 들도 함께 취소된다.
      - 즉, 연결되어있는 상위 작업이 취소되면 하위 작업도 안전하게 종료되어 리소스가 회수되도록 한다.
- Go 프로그램에서 들어오는 RPC 및 HTTP 요청부터 나가는 요청까지 함수 호출 체인을 통해 Context를 전달.
  - 함수 호출 체인(function call chain): 요청이 처리되는 과정
  - 요청에 관련된 정보 및 설정을 Context를 통해 전달하고 공유: 클라이언트가 서버로 요청 → 서버에서 다양한 중간 단계 및 서비스를 거침
- 동일한 Context를 여러 함수 호출 사이에서 안전하게 공유할 수 있다.
  - Context는 한 번 생성되면 내부의 정보가 변경되지 않기 때문.

## DO
- 함수의 첫 번째 매개변수로 Context를 사용 할 것.
- Request와 관련이 없어 보이더라도 Context를 사용 할 것.

## DONT
- 구조체에 Context 멤버 추가하기.
  - 대안: 메서드에 매개변수로 넘기기.
  - 예외: 표준 라이브러리나 서드파티 라이브러리의 인터페이스와 일치해야 하는 메서드인 경우.
- 사용자 정의 Context 유형 만들기.

## Key Methods
- Deadline
  ```go
  Deadline() (deadline time.Time, ok bool)
  ```
  - 작업을 시작해야 하는 시간 (데드라인) 및 데드라인이 설정되었는지 여부를 반환.
  - 작업이 시작해야 하는지 여부를 결정.
  - 작업에 시간 제한을 부여.
- Done
  ```go
  Done() <-chan struct{}
  ```
  - 작업에 대한 취소 신호 역할을 하는 채널을 반환.
    - 채널이 닫히면 해당 함수는 작업을 중단하고 반환.
- Err
  ```go
  Err() error
  ```
  - Context가 취소된 이유를 나타냄.
  - nil:
    - Done 채널이 아직 닫히지 않은 경우.
- Value
  ```go
  Value(key any) any
  ```
  - Context와 관련된 값을 가져올 때 사용. 주로 사용자 지정 데이터를 Context에 저장하고 추출하는데 사용.
  - nil:
    - 특정 키에 대한 값이 없는 경우
- [WithValue](https://pkg.go.dev/context#WithValue)
  - Context에 관련된 값을 추가할 때 사용.
- [WithTimeout](https://pkg.go.dev/context#WithTimeout)
  - 해당 Context 에 시간 제한을 설정하고자 할 때 사용.
- [Background](https://pkg.go.dev/context#Background)
  ```go
  Background() Context
  ```
  - 모든 Context 트리의 루트.
    - 다른 모든 context 는 이를 기반으로 파생된다.
  - 취소되지 않음.
  - 기한 및 값이 없음.
    - 무한 기한을 지니고 있음.
  - 전역적으로 사용.
    - 주로 main 함수나 초기화 작업에 사용.
    - 앱의 최상위 레벨에서 시작할 때 주로 활용됨.

---
### Cited Information:

- [Go Concurrency Patterns: Context](https://go.dev/blog/context) by. Sameer Ajmani  
  Published: 29 July 2014
- [Documentation](https://pkg.go.dev/context)  
  Published: Oct 10, 2023 