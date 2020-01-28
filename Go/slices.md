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
  * Reference Type 

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
```go
cc := []int{1, 2, 3}
cc = append(cc, 7, 0, 88)
fmt.Println(cc) // [1 2 3 7 0 88]
```

### Slice + Slice
slice 에 다른 slice를 append 시킬 때는 <code>...</code>를 사용한다
```go
d := []int{10, 100, 1000}
e := []int{11, 111, 1111}
d = append(d, e...) // 슬라이스 d에 e를 추가
fmt.Println(d) // Slice d :  [10 100 1000 11 111 1111]
```

### Reference Type
