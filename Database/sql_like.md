# SQL LIKE
SQL의 LIKE 연산자  
 
### Table of Contents
 * [LIKE Operator](#like-operator)
   * 연산자 %
   * 연산자 _


## LIKE Opeartor  
LIKE 연산자를 통해 특정 값을 조회 할 수 있다.

LIKE 와 조합하여 사용하는 기호연산자로는 ```%```와 ```_```가 있다.


### 연산자 %
SQL 문에서 ```%``` 는 와일드카드(*)와 동일한 역할을 한다.  

#### Syntax
* ```<character>%```
* ```%<character>```
* ```%<character>%```

#### 예)
상황 : ```at&t``` 라는 회사가 사용한 저장소 총 용량을 확인하고자 함.

SQL Syntax 
  ```sql
  SELECT SUM(capacity)
  FROM `company_report`
  WHERE `company_code` LIKE 'at&t%'
  ```
위의 SQL 문의 의미는 다음과 같다.

  `company_report` 테이블에 해당하는   
  `company_code` 컬럼에서   ```at&t```라는 값을 포함한 모든(```%```) 데이터를 조회하여  
  ```capacity```(사용한 용량)를 합계낸 값을 추출  

결과  
  <img width="86" alt="total capacity" src="https://user-images.githubusercontent.com/48475824/89561545-9c09e200-d853-11ea-9fdd-d732202466c2.png">

 ```%``` 로 인해 ```at&t``` 회사의 지점1(```at&t1```)과 지점2(```at&t2```) 값이 합산해서 나온다.  
 

[↑ return to TOC](#table-of-contents)


### 연산자 _
SQL 문에서 ```_``` 는 한 글자(Characters) 를 의미한다.  
* character : 문자뿐만아니라 숫자와 대부분의 punctuation 도 포함.  

#### 예)
```t-mobi__``` → t-mobi 로 시작하여 두가지 아무 문자(```_```)로 이루어진 값  

[↑ return to TOC](#table-of-contents)
