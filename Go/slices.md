# Slices
Go 에서는 Array 보다는 Slice 더 자주 사용한다. 이유는 Slice의 유연함 때문이다.  
슬라이스는 배열과 비슷하지만 길이가 가변적이다.  

### Slice의 특징
  * 가변적인 **길이**<small>(length)</small>  
    * 길이 함수 : <code>len()</code>
    * *Index로 접근할 수 있는* 공간.
    * 길이가 고정적이지 않음. 그렇기에 <code>[]</code> 안에 길이를 지정하지 않음.
    * 슬라이스 길이는 용량보다 크게 설정할 수 없다.  
  * **용량**<small>(capacity)</small>을 지님
    * 용량 함수 : <code>cap()</code>    
    * 용량은 실제 *메모리에 할당된* 공간 을 말한다.  
    * 용량을 생략하면 슬라이스의 길이와 동일하게 설정된다.
    * 용량이 길이보다 크더라도 길이를 벗어난 Index에는 접근할 수 없다.  
      --> 접근 시도시 <code>runtime error</code> 발생
    * 용량이 가득차면 용량은 자동으로 늘어난다.
  * **Reference Type**
    * 슬라이스를 참조가 아니라 복사하고자 한다면 <code>copy()</code>함수를 사용해야 한다.
  * **nil**
    * 슬라이스를 선언만 하고 초기화 하지 않은 경우 값은 **nil**이 자동 할당 된다.

### Slice Internals
슬라이스 내부의 모습을 살펴보자.  
슬라이스를 구성하는 요소는 세가지가 있다.  
<img width="419" alt="slice internals" src="https://user-images.githubusercontent.com/48475824/73604669-c7c3bb00-45d7-11ea-88ea-51bbc0970c18.png"> 
  1. ptr | Pointer 포인터  
    슬라이스의 포인터는 배열의 첫 번재 요소를 가리킨다. 
  1. len | Length 길이
  1. cap | Capacity 용량 

**용량과 길이가 구분되어 있는 이유는?**  
  * 동적 배열을 구현하기 위해서 길이와 용량을 구분해 놓았다.  
  * 슬라이스는 길이를 동적으로 늘릴 수 있다.  
  * 만약 슬라이스의 요소가 늘어난다면 Go runtime은 정해진 알고리즘에 의해 슬라이스의 용량을 늘려놓는다.

## Slice expressions

**Syntax**
  * 슬라이스 선언  
    <code>var \<sliceName> []\<dataType></code>  
    ```go
    var a[]int
    var b[]string
    var c[]float32

    fmt.Println(a) // []
    fmt.Println(reflect.ValueOf(a).Kind()) // slice
    fmt.Println(b) // []
    fmt.Println(c) // []
    ```
    <code>[]</code> 로 생성된 슬라이스의 길이는 0이다.
    ```go
    var a []int
    fmt.Println(a[0]) 
    // panic: runtime error: index out of range [0] with length 0
    // 길이가 0인 슬라이스에 접근하려 했기에 오류가 발생한다.
    ```
  * 슬라이스에 길이와 용량 설정  
    make() 함수를 사용하여 값을 넣는다. 
    * make 함수의 **첫번째 매개변수** : <code>[]\<dataType></code>
    * make 함수의 **두번째 매개변수** : length (생략 불가)  
      생략시 오류 : <code>missing len argument</code>
    * make 함수의 **세번째 매개변수** : capacity (생략 가능)   
    <code>var \<sliceName> = make([]int, length, capacity)</code> 
    ```go
    var aa = make([]int, 3, 4)
    fmt.Println("len(aa) : ", len(aa)) // 3
    fmt.Println("cap(aa) : ", cap(aa)) // 4
    ``` 
    <code>\<sliceName> := make([]\<dataType>, length, capacity)</code> 
    ```go
    bb := make([]int, 5, 10)
    fmt.Println(len(bb)) // 5 
    fmt.Println(cap(bb)) // 10
    // bb슬라이스의 길이는 5 용량은 10
    ``` 
    capacity는 생략 가능 
      * 용량을 생략하면 슬라이스의 길이와 동일하게 설정된다.    
      ```go
      // 용량 생략
      bbb := make([]int, 3)
      fmt.Println("len(bbb)", len(bbb)) // 3
      fmt.Println("cap(bbb)", cap(bbb)) // 3
      ```
      * 이렇게 생성된 슬라이스의 요소는 Zero Values를 갖는다.
      ```go
      b1 := make([]int, 3)
      fmt.Println("b1[0]", b1[0]) // 0
      b2 := make([]string, 3)
      fmt.Println("b2[0]", b2[0]) // ""
      b3 := make([]bool, 3)
      fmt.Println("b3[0]", b3[0]) // false
      ```
  * 슬라이스 선언 및 초기화  
    <code>{}</code> 중괄호를 사용하여 값을 할당한다.
    * 한줄로 선언 및 초기화  
      <code>\<sliceName> :=[]\<dataType>{\<value1>,\<value2>}</code>
      ```go
      cc := []int{1, 2, 3}
      ```
    * 여러줄로 선언 및 초기화  
      반드시 Comma(<code>,</code>)로 마무리
      ```go
      <sliceName> := []{
          <value1>,
          <value2>,
          ...
          <lastValue>,
      }
      ```
      ```go
      cc := []int{
        1, 
        2, 
        3,
      }
      ```

## Slice에 값 추가
append() 함수를 통해 슬라이스의 끝에 값을 추가할 수 있다.
  * 추가할 수 있는 개수에는 제한이 없다.

```go
cc := []int{1, 2, 3}
cc = append(cc, 7, 0, 88)
fmt.Println(cc) // [1 2 3 7 0 88]
```

### Slice + Slice
slice 에 다른 slice를 append 시킬 때는 <code>...</code>를 사용한다.

**Syntax**   
  <code>slice1 = append(slice1, slice2...)</code>  
  * slice1에 slice2를 붙임.
  * ellipsis notation(<code>...</code>)을 두 번째 매개변수, 추가되는 슬라이스 뒤에 적어준다.

```go
d := []int{10, 100, 1000}
e := []int{11, 111, 1111}
d = append(d, e...) // 슬라이스 d에 e를 추가
fmt.Println(d) // Slice d :  [10 100 1000 11 111 1111]
```

### Reference Type
슬라이스는 레퍼런스 타입이다.  
슬라이스는 내장된 배열에 대한 Pointer이다.   
sliceA에 또 다른 슬라이스인 sliceB를 대입한다면 값이 복사되는 것이 아니라 참조가 된다.  
  * 슬라이스를 복사하고 싶다면 copy() 함수를 사용할 것. 
  * sliceB의 요소의 값을 바꾸게 되면 sliceA도 함께 영향을 받는다.  

```go
// Reference Type
sliceA := []int{1, 2, 3}
var sliceB []int
sliceB = sliceA // sliceB 에 sliceA 대입
sliceB[0] = 100000 // sliceB의 첫 번째 요소 변경
fmt.Println(sliceA) // [100000 2 3]
fmt.Println(sliceB) // [100000 2 3]
```

### Slice and copy function
슬라이스의 요소를 모두 복사하고자 한다면 <code>copy()</code> 함수를 사용한다.  

**Syntax**  
<code>copy(\<copySlice>, \<originalSlice>)</code>  
  * 복사된 slice에는 make함수로 공간을 항당해주어야 한다.
    * 공간이 할당되지 않은 빈 슬라이스에는 요소를 복사할 수 없기 때문이다.

  ```go
  // Copy one slice into another slice
  s1 := []int{1, 2, 3, 4, 5}
  s2 := make([]int, 5) // make 함수로 공간을 할당
  copy(s2, s1)

  fmt.Println(s1) // [1 2 3 4 5]
  fmt.Println(s2) // [1 2 3 4 5]
  ```
  > 복사를 완료하였으니 복사된 슬라이스(<code>s2</code>)의 요소를 변경한 후 원본 슬라이스(<code>s1</code>)에 영향을 미치는지 살펴보도록 하자.

  ```go
  // Slice modification
  s2[0] = 1001010
  fmt.Println("Original s1 : ", s1) //  [1 2 3 4 5]
  fmt.Println("Coppeid s2 : ", s2)  // [1001010 2 3]
  ```
  > 복사한 s2의 첫 번째 요소만 변경되었고, 원본 슬라이스는 영향을 받지 않았다.

    
  * 만약 공간을 길이보다 적게 설정한다면 설정한 공간만큼의 요소까지만 복사된다.
  ```go
  // if cap < len
  s1 := []int{1, 2, 3, 4, 5}
  s2 := make([]int, 3) // make 함수로 공간을 할당
  copy(s2, s1)

  fmt.Println(s1) // [1 2 3 4 5]
  fmt.Println(s2) // [1 2 3]
  ```


### Sub-slice  
슬라이스의 일부를 떼어 부분 슬라이스를 만들 수 있다.  
**Syntax**  
<code>\<subSlice> := \<originalSlice>[start_index:end_index]</code>

end index는 인덱스보다 1 많다.
  * end index == Total index + 1
    * 만약 길이가 7인 index의 슬라이스의 끝까지 참조하고자 한다면 <code>[0:7]</code> 이 아닌 <code>[0:8]</code> 이 되어야 한다.
  * 참조이기 때문에 부분 슬라이스의 요소를 바꾸면 배열의 요소도 바뀐다.

  ```go
  s := []int{1, 2, 3, 4, 5, 6, 7, 8}
	subS := s[2:5]
	fmt.Println(subS) // [3 4 5]
  ```
  ```go
  subAll := s[0:8]
	fmt.Println(subAll) // [1 2 3 4 5 6 7 8]
  subEnd := s[0:len(s)]
  fmt.Println(subEnd) // [1 2 3 4 5 6 7 8]
  ```
  ```go
  ss := []string{"Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"}
	fmt.Println(ss[1:2]) // [Tue]
	fmt.Println(ss[1:1]) // []
	fmt.Println(ss[3:5]) // [Thu Fri]
  fmt.Println(ss[:])   // [Mon Tue Wed Thu Fri Sat Sun]
	fmt.Println(ss[:2]) // [Mon Tue]
	fmt.Println(ss[1:]) // [Tue Wed Thu Fri Sat Sun]
  ```
  * 용량을 설정할 때 기존 슬라이스의 용량을 넘길 수는 없다.
  ```go
  // Sub-slice  + Capacity
	ss1 := []int{1, 2, 3, 2, 1, 2, 3, 1, 2}
	ss2 := ss1[0:6:8] // Capacity : 8
	fmt.Println("len(ss2) : ", len(ss2), "cap(ss2) : ", cap(ss2))
	// len(ss2) :  6 cap(ss2) :  8
	fmt.Println("ss2 : ", ss2) // [1 2 3 2 1 2]
  ```
