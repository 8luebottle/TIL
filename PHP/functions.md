# D

## define

Constant 를 정의해준다(runtime 시 정해짐).

`define ( string $name , mixed $value , bool $case_insensitive = false ) : bool`

```php
define('ICECREAM', $icecream)
```

- **Parameters**
  - `name` : 상수명

    예약어와 겹치는 이름 조차 define 으로 정의 가능.  
    - 해당 상수(예약어와 겹치는 이름을 지닌) 값을 가져오려 할 때에는 `constant()` 를 사용해야 한다. → 비록 가능하더라도 지양할 것

  - `value` : 상수 값

    값은 scalar value(a single value) 또는 array
    - int
    - float
    - string
    - bool
    - null
    - array
  - `case_insensitive`
    - default: false ⇒ case sensitive

- **Return values**
  - Success ⇒ `true`
  - Failure ⇒ `false`


# E

## end

Array 에 사용한다. 배열의 내부 포인터가 마지막 요소를 가리키도록 한다.

`end ( array|object &$array ) : mixed`
```php
$moods = array('confident', 'enlightened', 'hopeful', 'amused');
echo end($moods); // amused
```

- **Parameters**
  - array

- **Return values**
  - Success → `마지막 요소의 값`
  - Empty Array → `false`

## explode

문자열을 split 해준다.

`explode ( string $separator , string $string , int $limit = PHP_INT_MAX ) : array`

```php
$finance = "account bank credit debit EBT";
$result = explode(" ", $finance, -1);

echo $result[0]; // account
echo $result[3]; // debit
echo $result[4]; // Undefined array key
```

- **Parameters**
  - `separator`
    - `""` : seperator 를 빈 스트링으로 설정했다면 `false` 가 리턴된다.
  - `string`
    - split 할  문자열
  - `limit`
    - 양수 : maximum
    - 음수 : -limit 만큼 제외
    - `0` : 1 로 취급 (1번만 split 함)

- **Return Values**
  - string array
    나뉜 문자열들이 배열에 담겨 리턴된다.


# I

## isset

변수가 선언이 되었는지 확인해준다.

- different than `null`
- 만약 변수가 `unset()` 을 함수를 거쳤다면, 해당 변수는 set 되었다고 취급되지 X.

`isset ( mixed $var , mixed ...$vars ) : bool`

```php
$you = array ('💩' => 1, '🍠' => NULL);

var_dump(isset($you['💩']));  // TRUE
var_dump(isset($you['🍠']));  // FALSE
```

- **Parameters**
  - `var` : 체크할 변수
  - `vars` : 그외에 더 체크하고픈 변수들  
    왼쪽부터 차례대로 검증하며 `unset`된 변수를 맞딱들이는 순간 검증을 멈추고 `false`를 리턴.

- **Return Values**
  - `true` : value 가 존재 할 시
  - `false` : value 가 `null` 인 경우
    - null character 인 `\0` 는 `null`로 취급되지 않기에 `true` 가 리턴되니 주의!


# S

## strpos
String 에 담겨 있는 substring 의 position 을 찾아준다.

`strpos ( string $haystack , string $needle , int $offset = 0 ) : int|false`

```php
$tasty = 'vanilla-icecream'; 
$findme = 'cream';
$pos = strpos($tasty, $findme); // 11
```

- **Parameters**
  - `haystack` : whole 문자열
  - `needle` : 찾고자 하는 문자열
    - 문자열이 아니면 integer 로 형변환됨.
      - 8.0.0 부터 integer passing 은 더이상 지원 안됨.
  - `offset`
    - 문자열의 시작점 부터 카운트 됨.
    - `-` : 음수일 시 문자열 끝지점 부터 카운트 됨.

- **Return Value**
  - `integer`: 찾음  
    (whole 문자열에서) 찾은 문자열의 시작 위치

  - `boolean` : 못찾음  
    못찾은 경우 `false` 를 리턴.

  **`%주의%`**
  - return 된 결과를 boolean 으로 비교연산 하고자 한다면 반드시 `===` 를 사용해야 한다.
    → 그 이유는 needle 이 haystack 의 첫번째 위치에 와 있을 경우 `0` 이 리턴되는데 `==`로 비교할 경우 0 은 falsy 값으로서 비교되기 때문.

    - 부정형은 `!==`
