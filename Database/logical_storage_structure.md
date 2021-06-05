# Logical Storage Structure  
데이터베이스에 담긴 데이터가 어떻게 담겨있는지 논리적 구조에 대해 알아보자.

### Table of Contents

* [About Logical Storage Structure](#about-logical-storage-structure)  


## About Logical Storage Structure
DB속 데이터는 data file 에 저장된다. 그리고 데이터 파일들은 Table Space 라는 논리적 저장공간에 담겨있다.  

Oracle DB에서의 논리적 단위는 아래와 같이 네가지로 나뉜다.  
> `Tablespace` > `Segment` > `Extent` > `Data Block`  

![logical-structure](https://user-images.githubusercontent.com/48475824/120893010-ef9fb480-c64b-11eb-8974-1919e7e25b80.png)
- `Tablespace` 는 `Segment`를 담는 컨테이너이다.  
- `Segment` 는 `Extent` 들로 구성되어 있으며 `Extent` 는 `Data block` 들의 모음이다.  

데이터는 실질적으로 data block(이하 블록)에 저장되어 있다. 즉, DBMS가 데이터를 읽고 쓰는 단위는 블록 단위이다.  
- Index 또한 블록단위로 데이터를 다룬다.  

Oracle DB에서 블록의 크기는 보통 8KB 크기를 가진다. 이는, 단순히 하나의 컬럼처럼 작은 양의 데이터를 불러오려해도 8KB 크기의 블록을 모두 읽어와야한다는 것을 의미한다.  

<br>

![Segment-Extent-Data_blocks](https://user-images.githubusercontent.com/48475824/120892671-66d44900-c64a-11eb-9955-e776f41394ed.png)

`Segment`에 데이터를 저장할 공간이 부족할 때에는 `Data Block` 단위가 아닌 `Extent` 단위로 공간을 확장한다.  
