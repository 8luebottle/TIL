# Arrays
Go에서 Arrays는 길이가 고정되어 있다.
* 배열의 Index는 0부터 시작
* 배열은 연속된 메모리 공간을 순차적으로 사용하는 자료구조
* 배열의 요소는 자료형이 동일해야 한다.

## Declaration
**Syntax**
  * 배열 선언  
  <code>var \<arrayName> [length]\<dataType></code>
  ```go
  // Array Declaration Example
  var intArr [1]int
  var strArr [3]string
  var boolArr [2]bool

  fmt.Println(intArr)   // [0]
  fmt.Println(strArr)   // [  ]
  fmt.Println(boolArr)  // [false false]
  ```
  > 배열 선언 후에 값을 초기화 하지 않으면 Go 컴파일러는 zero value를 할당해 놓는다.


## Declaration & Initialization
**Syntax**
  * 배열 선언 및 초기화  
  <code>var \<arrayName> [length]\<dataType> = \[length]\<dataType>{...}</code>
  ```go
  var a [5]int = [5]int{10, 100, 1000, 200, 50}
  ```
  * 배열 선언 및 초기화 2 (간단하게)  
  <code>var \<arrayName> = [length]\<dataType>{...}</code>
  ```go
  var b = [5]int{20, 252, 7, 24, 29}
  ```

  * 배열 선언 및 초기화 3 (더 간단하게)  
  <code>\<arrayName> := [length]\<dataType>{...}</code>
  ```go
  c := [5]int{5, 4, 3, 2, 1}
  ```

  * 배열 선언 및 초기화 4 (여러 줄 사용)
  ```go
  <arrayName> := [length]<dataType>{
      <value1>,
      <value2>,
      ....
      <lastValue>, // 반드시 comma 로 마무리
  }
  ```
  > Comma로 마무리 하지 않는다면 <code>Syntax Error</code> 를 만나게 된다.  
  Last elment는 반드시 <code>, </code>로 마무리 해주어야 한다. <code>,</code> 를 끝에 붙여주지 않는다면 Go 컴파일러는 컴파일시 last element 뒤에 <code>;</code>을 붙여주게 되고 이는 <code>Syntax Error</code> 를 야기시킨다.

  ```go
  d := [5]int{
		32,
		29,
		79,
		25,
		0,
 }
  ```
  * 배열 선언 및 초기화 5 (배열 자동 길이 설정)
  > <code>...</code> operator 를 사용한다.  
  초기화할 값의 개수에 따라 자동으로 배열의 길이가 설정된다. (컴파일러가 설정해줌)  
  <code>\<arrayName> := [...]\<dataType>{...}</code>
  ```go
  e := [...]int{0, 1, 2}
  fmt.Println(len(e)) // 3
  e1 := [...]string{"U", "I", "O", "A"}
  fmt.Println(len(e1)) // 4
  ```
  * 다차원 배열 선언 및 초기화
  ```go
  <arrayName> := [length][length]<dataType>{
      {...},
      {...},
      {...},
  }
  ```
  ```go
  h := [3][3]int{
		{1, 2, 3},
		{4, 5, 6},
		{7, 8, 9},
  }
  fmt.Println(h) // [[1 2 3] [4 5 6] [7 8 9]]
  ```

## Insert elements into an array at the specific index
원하는 index 위치에 요소 삽입하기.  
**Syntax**  
  <code>\<arrayName> := [length]\<dataType>{\<specificIndex1> : \<value1>, \<specificIndex2> : \<value2>}</code>
  ```go
  x := [5]int{1 : 3000, 3: 20}
  fmt.Println(x) // [0 3000 0 20 0]
  ```
  > 초기화 하지 않는 값은 <code>0</code> 으로 할당됨 (int의 zero value는 0).

  ```go
  y := [5]string{1: "Pho", 4: "Dinner"}
  fmt.Println(y) // [ Pho   Dinner]
  ```
  > 빈자리는 empty string <code>""</code> 이 할당됨.

  ```go
  z := [5]bool{1: true, 3: false}
  fmt.Println("Array z : ", z) //[false true false false false]
  ```
  > 빈자리는 <code>false</code> 가 채워짐.

## 배열의 요소에 접근
 **Syntax**  
  * Square brackets<code>[]</code>을 통해 특정 요소에 접근
  * <code>[]</code> 안에는 요소가 위치한 index  
  <code>\<arrayName>[index]</code>
  ```go
  g := [3]string{"one", "two", "three"}
  fmt.Println(g[1]) // two
  ```

## 배열 복사
**Syntax**
 * 배열 복사하기  
 <code>\<originalArray> := \<copyArray></code>
 ```go
 k := [3]int{3, 2, 1}
 l := k
 fmt.Println(l) // [3 2 1]
 fmt.Println(reflect.ValueOf(k).Kind()) // array
 ```

## 배열 순회
**Syntax**  
  * 배열 순회 1 (for loop)
  ```go
  for i := 0; i < len(<arrayName>); i++ {
		fmt.Println(<arrayName>[i])
  }
  ```
  * 배열 순회 2 (for, range)  
  배열의 index와 value를 함께 얻을 수 있다.
  ```go
  for i, value := range <arrayName> {
		fmt.Println(i, value) // 배열의 index와 요소 함께 출력
  }
  ```
  * 배열 순회 3 (outside)  
  Loop Variable (<code>i</code>)를 for문 밖에 선언하여 사용 
  ```go
  i := 0
  for range <arrayName> {
		fmt.Println(<arrayName>[j])
		i++
  }
  ```
  * 배열 순회 4 (Skip Index)  
  배열 순회 2에서 index는 제외하고 Value만 얻고자 할 때 사용.  
  본래의 index 자리에 <code>_</code> 를 배치시킴
  > Go는 결과값을 여러개 return 할 수 있기에 변수 개수를 반드시 맞춰주어야 한다. 개수를 맞추기 위해 underscore 를 써준다.

  ```go
  for _, value := range <arrayName> { // 개수를 맞추어야 하기에 _ 를 생략할 수 없음
		fmt.Println(value) // 배열의 요소가 출력됨
  }
  ```
