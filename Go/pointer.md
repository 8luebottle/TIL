# Pointer
<img width="545" alt="pointer" src="https://user-images.githubusercontent.com/48475824/73606961-79241a00-45f3-11ea-8b93-23d70838860a.png">  

Go언어에는 C, C++ 처럼 포인터가 있다. 포인터는 변수이다. 하지만 특별한 변수이다. 
 * 포인터는 메모리 주소만을 저장하기 위해 만들어진 특별한 변수이다.  
  * 포인터 변수에는 메모리 주소만 저장된다.
  ```go
  // 포인터 변수는 메모리 주소만 저장 가능
	var pp *int
	pp = 1          // 포인터 변수에 정수 할당 시도
	fmt.Println(pp) // cannot use 1 (type int) as type *int in assignment
  ```
  pp는 포인터변수 이기에 메모리 주소만 할당 가능하다. <code>pp = 1</code> 을 통해 정수를 할당하려고 하였으나 오류를 만나게 된다.

 * 자신이 사용하고자 한는 메모리의 '주소값'을 포인터 변수를 통해 저장할 수 있다.

포인터는 메모리의 주소<small>(위치)</small>를 담고 있다.
 * 포인터 값  == 변수의 주소
 ```go
 // 주소의 예
 0xc000096040
 ```

 * 포인터를 잘 이해하기 위해서는 메모리가 구성되고 관리되는 방법을 알아야 한다.  
    * Static, Global
    * Automatic, Local
    * Dynamic
    * Scope
    * Lifetime  
    메모리의 종류를 이해하는 것이 포인터의 동작을 이해하는데 도움이 된다.

 * 모든 값이 주소를 갖고있지는 않더라도 모든 변수에는 주소가 있다.
    * Struct의 field, Array의 element도 변수이기 때문에 주소를 갖고 있다. 


### Pointer의 특징
  * 참조 Reference  
  <code>&\<pointerName></code>  
    * &연산자는 단항 연산자이며 변수만을 피연산자(operand)로 사용한다.

  * 역참조 Dereference  
  <code>*\<pointerName></code>  
    * 포인터변수에 값을 대입할 때 사용
    * 포인터변수의 값을 가져올 때 사용

  * Pointer의 제로값은 어느 Type이던지 <code>nil</code> 이다. 
    * 포인터 변수를 선언하면 nil로 초기화 된다.
    * nil pointer은 아무 주소도 참조하고 있지 않은 포인터를 말한다.  
      * 포인터 변수 <code>p</code> 가 있고 <code>p != nil</code> 이 <code>true</code> 라는 것은 p가 이미 특정 변수를 가리키고 있다는 것을 의미.

  * 포인터 연산 불가
    * Go언어에서는 메모리 주소를 연산하여 직접 다룰 수 없다.

  * Pointer 끼리는 비교할 수 있다.
    * 비교연산자(<code>==</code>) 를 사용한다.
    * 참인 경우  
    <small>그 외에는 모두 false</small>
      * 두 포인터가 동일한 변수를 가리킴.
      * 두 포인터가 제로값인 nil을 가짐.  

  * <code>*</code> <small>(Asterisk)</small>를 자료형 앞에 붙인다.
    * C, C++ 인 경우 <code>*</code> 는 자료형 뒤에 온다.

  * <code>new()</code> 함수를 통해 메모리를 할당한다.  
    * <code>new()</code> 함수는 지정한 자료형의 크게에 맞는 메모리 공간을 할당해준다.

  * Garbage Collection 지원.  
    * Go언어는 가비지 컬렉션을 지원해준다. 그로인해 메모리 해제는 신경쓰지 않고 메모리 할당에만 신경쓰면 된다.  
        * C/C++ 같은 경우 프로그래머가 직접 <code>free()</code>/ <code>delete()</code> 함수를 통해 메모리 해제를 해주어야 한다.


## Pointer expressions

**Syntax**
  * 포인터 변수 선언  
  <code>var \<pointerName> *Type</code>  
  ```go
  var p *int                        
	fmt.Println("p", p)                            // <nil>
	fmt.Println("Type of p : ", reflect.TypeOf(p)) // *int
  ```  
  p라는 포인터변수를 선언만 해 주었기 때문에 Go 컴파일러가 해당 값을 <code>nil</code> 로 설정해 주었다.  
   * C언어의 NULL 값이 Go언어에서는 <code>nil</code> 이다.  
      * C에서 NULL은 정수 0이지만 Go에서의 <code>nil</code> 은 숫자 0이 아니다.  
      즉, <code>fmt.Println(nil == 0)</code>은 compiler error를 낸다.


  * new() 함수  
  <code>var \<pointerName> *Type = new(Type)</code>  
  <code>var \<pointerName> = new(Type)</code>
  ```go
  var p1 *int
	var p2 *int = new(int)
  var p3 = new(int)

	fmt.Println(p1) // <nil>
	fmt.Println(p2) // 0xc000096038
  fmt.Println(p3) // 0xc000096040
  ```
  p1은 선언만 한 포인터변수 이기에 초기값으로 <code>nil</code> 이 할당됬다.  
  p2는 <code>new()</code> 함수를 통해 선언과 동시에 메모리를 할당. 메모리 값으로 <code>0xc000096038</code> 이 할당되었다.  
  메모리 주소는 시스템마다 다며 컴파일 할 때 마다 달라진다.


  * dereference | 역참조  
  역참조를 사용하여 메모리 주소의 값을 대입하거나 가져올 수 있다.  
  <code>\*\<pointerName></code>  
  <code>\*\<pointerName> = values</code>  
    ```go
    var numPtr *int = new(int)
    fmt.Println(numPtr) // 0xc00009690
    //dereference
    *numPtr = 2020
    fmt.Println(*numPtr) // 2020
    ```
    * **변수를 선언**할 때 <code>*</code> 를 붙이면 포인터형 변수가 되지만,  
     **변수를 사용**할 때 <code>*</code> 를 붙이면 역참조가 된다.


  * reference | 참조  
  일반 변수에 참조(<code>&</code>)를 사용하면 포인터형 변수에 대입할 수 있다.  
    ```go
    // reference &
    var n int = 2020   // 일반 변수 n
    var nPtr *int = &n // 참조로 n 변수의 메모리 주소를 구한 후, 포인터 변수 nPtr에 대입
    fmt.Println(n)     // 2020
    fmt.Println(&n)    // 0xc000096048
    fmt.Println(nPtr)  // 0xc000096048
    ```
    변수 앞에 <code>&</code> 를 붙이면 해당 변수의 메모리 주소를 뜻한다.  
    즉, <code>var nPtr *int = &n</code> 는 일반변수 <code>n</code> 의 주소 자체를 포인터변수 <code>nPtr</code> 의 값으로 할당해 준 것. 

  
  * 포인터 직접 다루기 불가  
  Go언어의 포인터는 직접 다룰 수 없다.  
    * 메모리 주소를 직접 대입할 수 없음.
    * 포인터 연산을 할 수 없음
      ```go
      // Go 언어에서는 Pointer연산을 지원하지 않는다.
      var numPtr4 *int = new(int)
      numPtr4++              // 연산시도 --> invalid operation: numPtr4++ (non-numeric type *int)
      numPtr4 = 0xc0820062d0 // cannot use 826814784208 (type int) as type *int in assignment
      ```
