# For Loop

Go언어의 문법은 심플 그 자체이다. 반복문에서도 그 특징이 확연히 나타나는데 for loop이 전부이기 때문이다.

### for loop 의 특징
  * 소괄호 <code>()</code> 를 사용하지 않음
  * 하지만 중괄호(<code>{}</code>)는 필수
    * for 문 내부에 코드가 단 한줄일지라도 중괄호는 꼭 써주어야 한다.
  * for 을 while 처럼 사용 가능
    * while 문이 존재하지 않는다. 하지만 for 을 while 처럼 사용할 수 있다는 사실.
  * 여는 중괄호(<code>{</code>)를 for이 존재하는 동일 라인에 써주어야 함
    * 이를 어길 시 컴파일시 오류가 난다.

### for loop expressions
**Syntax**  
  * 초기식은 루프가 시작되기 전에 실행된다.
  * 조건문은 루프가 반복될 때마다 실행된다.
  * 증감식은 루프의 본문 이후에 실행된다.
```bast
for 초기식; 조건식; 증감식{
    ...
}
```
```go
sum := 0
for i := len(i)-1; i <= 0; i-- {
    sum += i
}
```

**for-each in Go**
  * <code>range</code> 를 통해 키와 값 쌍을 추출할 수 있다.
```bash
for key, value := range collection{
    ...
}
```
```go
years := [5]int{2019, 2020, 2021, 2022, 2023}
for idx, year := range years{
    fmt.Println(idx, year)
}
```

**for-each in Go (w/ blank indentifier)**
* 빈 식별자 사용하기
```bash
for _, val := range collection {
    ...
}
```
```go
towns := [5]string{"Seoul", "NY", "SF", "LA", "Peking"}
for _, town := range towns {
    fmt.Println(town)
}
```

**Nested for loop**
* 중첩 for loop
```go
for i:= 0; i < 5; i++{
  for j :=1; j < 6; j++{
    fmt.Println(i, j)
  }
}
```

**Infinite loop**
* Go의 무한 루프는 조건을 생략하면 된다.  
* 무한루프를 종료하기 위해서는 <code>continue</code>, <code>break</code> 또는 <code>return</code> 을 사용한다.
```bash
for {
  ...
}
```
```go
for {
    fmt.Println("Keep calm and do coding")
}
```

**While loop in Go**
* for loop 을 while loop 처럼 사용하기
```bash
for bool조건식{
    ...
}
```
```go
for y < 100 {
    fmt.Println(y)
    y++
}
```
