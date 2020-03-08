# Database Index
데이터베이스의 인덱스에 대해 알아보자.  
DB에서 데이터를 가져올때 적지않은 시간이 걸린다.   
DB 튜닝을 잘 하기 위해서는 INDEX에 대한 이해가 필수적이다.

### Table of Contents
* [Index Basic](#index-basic)  
  Index의 특징
* [속도](#속도)  
  Index의 손익 분기점
* [선정](#선정)  
  Do | Don't  
* [종류](#종류)  
  B-Tree Index | B+Tree Index | Bitmap Index | Composite Index
* [분류](#분류)  
  Key | 파일 조직 | Data 범윈
* [생성](#생성)
* [스캔](#스캔)  
  INDEX FAST FULL SCAN | INDEX FULL SCAN  
  INDEX RANGE SCAN | INDEX RANGE SCAN DESCENDING  
  INDEX SKIP SCAN | INDEX UNIQUE SCAN

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
  각각의 포인터는 하나의 Full Table Record 를 가리키고 있다.  
  포인터를 타고 원하는 데이터에 접근함으로써 데이터의 탐색 속도가 향상된다.  

[↑ return to TOC](#table-of-contents)


## 속도
인덱스를 사용하는 이유 중 하나는 검색속도 향상에 있다.   
인덱스를 생성한다는 것은 테이블이 하나 더 생성된다는 것이고 이는 용량이 증가된다는 것을 의미한다. DB의 용량이 증가되었음에도 불구하고 속도가 빨라지는 이유는 무엇일까?  

**Index를 안 사용할 시 :**  원하는 데이터를 찾기 위해 특정 테이블의 첫번째 열부터 원하는 데이터를 찾을 때 까지 검색이 진행된다.  
**Index를 사용할 시 :**  인덱스를 이용해 특정 부분부터 검색을 시작한다.

![sorted-unsorted-books](https://user-images.githubusercontent.com/48475824/76145111-d535fe80-60c9-11ea-894d-79589ad76802.png)

* 인덱스를 사용하지 않는다면 데이터를 처음부터 찾아야 한다. DB에 담긴 데이터가 방대하면 방대할 수록 속도 차이가 발생하게 된다.   
* 인덱스는 저장될 때 컬럼을 기준으로 정렬이 되어 저장되게 된다. 이미 정렬되어 있기에 특정 조건의 데이터를 빠르게 찾아낼 수 있다.  
* 인덱스와 데이터 테이블은 서로 매핑 되어 있다. 원하는 데이터를 찾기 위해 먼저 인덱스에서 접근하여(포인터를 통해) 매핑된 테이블로 찾아가 데이터를 꺼내오게 된다.

### Index의 손익 분기점
인덱스 사용이 반드시 속도 향상으로 결부되지 않는다. 인덱스에도 손익분기점이 존재한다.  
* INDEX RANGE SCAN 을 사용하는 것이 TABLE FULL SCAN 보다 느려졌을 때 손익분기점을 넘어섰다고 본다.
  * 보통 테이블의 전체 데이터중 10~15% 이내의 데이터를 출력하고자 할때 인덱스의 효과를 볼 수 있다.
    > 예) 손익 분기점 15%  
    1000개의 레코드에서 150개 이상을 읽을 때, FULL SCAN 을 사용하는 것아 더 효율적임을 의미.
* 손익 분기점을 넘어서게 되면 인덱스를 사용하는 것 보다 못하다.
  * 이때는 FULL SCAN 을 사용할 것

[↑ return to TOC](#table-of-contents)


## 선정
인덱스를 최대한 효율적으로 사용하기 위해 __적합한 컬럼__ 을 선정해 주어야 한다.

### Do 
Index는 ```SELECT``` 문의 ```WHERE```, ```JOIN``` 에서 높은 성능을 발휘한다.  
* **SELECT**  
```SELECT``` 에 자주 등장하는 컬럼을 잘 조합하여 인덱스로 설정  
이는 별도로 테이블로 가서 데이터를 출력할 필요가 없게 해준다.

* **WHERE**  
  ```WHERE``` 에 자주 등장하는 컬럼을 인덱스로 설정

* **ORDER BY**  
  ```ORDER BY```에 자주 등장하는 컬럼을 인덱스로 설정  
  인덱스는 정렬되어 있기에 별도로 ```ORDER BY```를 실행할 필요가 없기 때문.  
  

### Don't
```INSERT```, ```UPDATE```, ```DELETE``` 가 빈번하게 발생할 때는 INDEX를 사용하지 않는것이 좋다.  
* Record 삽입, 수정, 삭제가 자주 발생한다면 인덱스의 수를 최소화 해야한다.
    * Index 자체가 정렬이 된 채로 저장되어야 하기 때문에 ```INSERT``` 시 속도가 느리다.   
    테이블에 ```INSERT``` 하려는 데이터의 적합한 위치를 찾아서 저장을 해야하기 때문.  
    또한 Index 에도 데이터를 추가해줘야 한다. 

[↑ return to TOC](#table-of-contents)


## 종류
다양한 인덱스 종류가 있다.  

* B-Tree Index
* B+Tree Index
* Bitmap Index
* Cluster Index
* Composite Index
* Function Based Index
* etc ....


### B-Tree Index
Balanced Tree Index  
가장 많이 사용되는 인덱스 구조.  
대부분의 관계형 데이터베이스의 Default Index 타입이다.

트리의 형태를 가진다.
  * Root
  * Branch (non-leaf)
  * Leaf

<img width="600" alt="B-Tree" src="https://user-images.githubusercontent.com/48475824/76155139-625d6f80-612b-11ea-92ad-8310f9e64ca3.png">
  
[Image Source](https://www.qwertee.io/blog/postgresql-b-tree-index-explained-part-1/)



### B+Tree Index
### Bitmap Index
데이터 값의 종류가 적고 동일한 데이터가 많을 때 사용.  

<img width="550" alt="bitmap" src="https://user-images.githubusercontent.com/48475824/76155193-f596a500-612b-11ea-9477-3eb7b0aa3f90.gif">   

[Image Source](https://www.computer.org/csdl/journal/tk/2012/09/ttk2012091570/13rRUIIVlkJ)


### Composite Index
여러 컬럼을 조합(결합)하여 인덱스를 구성하는 방법.  
결합하려는 컬럼들의 순서가 중요하다.  

```WHERE``` 의 조건 컬럼 2개 이상이 ```AND``` 로 연결되어 사용되는 경우 → 결합 인덱스 사용.

![composite-index](https://user-images.githubusercontent.com/48475824/76155317-fd574900-612d-11ea-8516-8fce19420937.png)

[Image Source](https://mapr.com/docs/60/MapR-DB/Indexes/design-composite-index.html)

[↑ return to TOC](#table-of-contents)


## 분류
다양한 인덱스 종류를 분류하는 법도 여러가지이다.  
![Index-Methods](https://user-images.githubusercontent.com/48475824/76146961-32867b80-60db-11ea-95ce-2a3b1f38c3f9.png)

### Key
* Primary Index 기본 인덱스
* Secondary Index 보조 인덱스

### 파일 조직
* Clustered Index 집중 인덱스
* Nonclustred Index 비집중 인덱스

### DATA 범위
* Dense Index 밀집 인덱스
* Sparse Index 희소 인덱스

[↑ return to TOC](#table-of-contents)


## 생성
인덱스는 열 단위로 생성된다.

[↑ return to TOC](#table-of-contents)


## 스캔
INDEX SCAN 방식은 아래와 같다.

* **INDEX FAST FULL SCAN**  
  Multi Block I/O

* **INDEX FULL SCAN**  
  모두 스캔  
  Single Block I/O

* **INDEX RANGE SCAN**  
  특정 범위 스캔

* **INDEX RANGE SCAN DESCENDING**  
  특정 범위를 역순으로 스캔

* **INDEX SKIP SCAN**  
  중간 중간 스킵하며 스캔

* **INDEX UNIQUE SCAN**  
  Unique Index를 사용하여 스캔

[↑ return to TOC](#table-of-contents)
