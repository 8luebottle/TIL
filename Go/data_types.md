# Data Types
Go의 자료형에 대하여.

## Numbers
Go에서 숫자는 정수, 실수, 복소수로 표현할 수 있다.
> <small>int, uint, float의 뒤에 붙은 숫자는 bits를 말한다. </small>

### Integers
* **int**  
부호 있는 정수 (integer)  
  * **int8**  
  값의 범위 : -128~127
  * **int16**  
  값의 범위 : -32768~32767
  * **int32**  
  값의 범위 : -2147483648~2147483647
  * **int64**  
  값의 범위 : -9223372036854775808~9223372036854775807.

* **rune**  
rune == int32  
  - 보통 유니코드 문자 코드를 저장할때 사용.  
  - 반드시 single quotation marks<code>('')</code>를 사용. Double quotation marks<code>("")</code>를 사용시 컴파일 오류 발생.
  - 문자는 저장 가능하지만 문자열은 저장할 수 없다.

* **uint**  
부호 없는 정수 (unsigned interger)  
Zero 와 Positive 숫자만 표현 가능
  * **uint8**  
  값의 범위 : 0~255
  * **uint16**  
  값의 범위 : 0~65535
  * **uint32**  
  값의 범위 : 0~4294967295
  * **uint64**  
  값의 범위 : 0~18446744073709551615

* **byte**  
byte == uint8

* **uintptr**  
Pointer 저장시 사용 (unsigned integer pointer)


### Floating-point numbers
Go에서 실수를 표현할때는 '고정소수점 방식'과 '부동소수점 방식'을 사용할 수 있다.  
주의할 것은 컴퓨터는 2진수 기반이면서 한정적인 메모리로 인해 실수를 정확하게 표현하지 못한다.
* **float**
  * **float32**
  * **float64**


### Complex numbers
실수와 허수로 이루어진 복소수.  
복소수 또한 실수이기에 계산시 정확히 표현이 불가하다.
* **complex**
  * **complex64**
  * **complex128**
  
## Booleans
Go 의 불리언 값은 true 와 false 로 나뉜다.
Boolean은 논리값을 나타내는 자료형이다.
  * true와 false의 크기는 1 byte.
  ```
  var b2 bool = false
	fmt.Println(unsafe.Sizeof(b2)) // 1
  ```

Boolean은 논리연산자와 함께 쓰인다.
  * 논리합 AND  
    <code>&&</code>
  * 논리곱 OR  
    <code>||</code>
  * 논리 부정 NOT  
    <code>!</code>   
    ```
    // AND, OR, NOT
    fmt.Println(true && true)   // true
    fmt.Println(true && false)  // false
    fmt.Println(false && true)  // false
    fmt.Println(false && false) // false

    fmt.Println(true || true)   // true
    fmt.Println(true || false)  // true
    fmt.Println(false || true)  // true
    fmt.Println(false || false) // false

    fmt.Println(!false) // true
    fmt.Println(!true)  // false

    fmt.Println(!!false) // false
    fmt.Println(!!true)  // true
  ```
