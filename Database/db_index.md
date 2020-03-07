# Database Index
데이터베이스의 인덱스에 대해 알아보자.

### Table of Contetns
* [Index Basic](#index-basic)
* [속도](#속도)
* [종류](#종류)
* [생성](#생성)
* [스캔](#스캔)

## Index Basic
**INDEX 색인** : 원하는 데이터를 빠르고 쉽게 찾을수 있도록 특정 순서에 따라 배열해놓은 목록.

### Index의 특징
DB Index의 특징을 알아보기 위해 책의 Index와 비교해보도록 하겠다.
<img width="550" alt="book-index" src="https://user-images.githubusercontent.com/48475824/76143913-ab2b0f00-60be-11ea-8152-5ea57fee0dc5.png">  

> [Image Source](https://beehiveshoppe.com/cookbooks/digital-download-1935-southern-cookbook-of-old-dixie-recipes)

* **속도 향상**  
  책의 Index는 독자가 원하는 단어(데이터)가 위치한 페이지를 빠르게 찾아낼 수 있도록 돕는다.   
  DB의 Index도 책에서의 Index와 동일한 역할을 한다고 보면 된다.

  책 페이지가 많아질수록, DB의 데이터가 방대할수록 Index의 혜택을 톡톡히 누릴 수 있다. 그 혜택중 하나는 검색 속도이다.

* **용량 증가**  
  책의 Index 페이지가 별도로 존재하듯 DB에서도 Index의 테이블이 생성되야 한다. 이는 용량 증가를 야기한다.  
  ![index-table](https://user-images.githubusercontent.com/48475824/76144613-7e2e2a80-60c5-11ea-9f40-4aa5aee1f45e.png)

* **포인터**  
  인덱스는 Field 값과 Record의 포인터로 이루어진다.  
  포인터를 타고 원하는 데이터에 접근함으로써 데이터의 탐색 속도가 향상된다.  

## 속도
인덱스를 사용하는 이유 중 하나는 검색속도 향상에 있다.   
인덱스를 생성한다는 것은 테이블이 하나 더 생성된다는 것이고 이는 용량이 증가된다는 것을 의미한다. DB의 용량이 증가되었음에도 불구하고 속도가 빨라지는 이유는 무엇일까?  

**Index를 안 사용할 시 :**  원하는 데이터를 찾기 위해 특정 테이블의 첫번째 열부터 원하는 데이터를 찾을 때 까지 검색이 진행된다.  
**Index를 사용할 시 :**  인덱스를 이용해 특정 부분부터 검색을 시작한다.

![sorted-unsorted-books](https://user-images.githubusercontent.com/48475824/76145111-d535fe80-60c9-11ea-894d-79589ad76802.png)

* 인덱스를 사용하지 않는다면 데이터를 처음부터 찾아야 한다. DB에 담긴 데이터가 방대하면 방대할 수록 속도 차이가 발생하게 된다.   
* 인덱스는 저장될 때 컬럼을 기준으로 정렬이 되어 저장되게 된다. 이미 정렬되어 있기에 특정 조건의 데이터를 빠르게 찾아낼 수 있다.  
* 인덱스와 데이터 테이블은 서로 매핑 되어 있다. 원하는 데이터를 찾기 위해 먼저 인덱스에서 접근하여(포인터를 통해) 매핑된 테이블로 찾아가 데이터를 꺼내오게 된다.


## 종류
## 생성
## 스캔