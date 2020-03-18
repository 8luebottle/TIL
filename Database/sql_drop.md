# SQL DROP
DROP 명령어를 통해 Database 와 Table 을 삭제할 수 있다.

## DROP TABLE
* Drop Single Table  
    ```
    DROP TABLE table_name;
    ```
    ```
    DROP TABLE users;
    ```

* Drop Multiple Tables
    ```
    DROP TABLE table1, table2;
    ```
    ```
    DROP TABLE users, admins;
    ```

* Drop Referenced by a Foreign Key Table
    ```
    DROP table table1;
    ```
    다른 테이블과 외래키를 통해 연결되어 있는 테이블인 경우 단순히 DROP 문으로 테이블을 삭제할 수 없다. 
    * 데이터의 안전성 보장을 위해 아래와 같은 오류를 발생시킨다.
        ```
        Cannot drop table 'table1' referenced by a foreign key constraint '......' on table 'table2'.
        ```
    table1 은 table2 와 관계가 형성되어 있다. FK 가 있는 table 을 삭제하기 위해서는 FK 를 끊어준후 다시 붙여주어야 한다.

    **해결법** (MySQL)
    ```
    SET FOREIGN_KEY_CHECKS = 0;
    DROP TABLE table1;
    SET FOREIGN_KEY_CHEKCS = 1;
    ```
    * ```FOREIGN_KEY_CHEKCS=0```  
      FK constraints 비활성화
    * ```FOREIGN_KEY_CHEKCS=1```  
      FK constraints 활성화
    
    **FK 제약조건 확인 법**  
    FOREIGN_KEY_CHECKS 의 값을 확인하기.  
    * 보여지는 값은 Local variable 의 값이다.
    ```
    SHOW VARIABLES WHERE variabe_name='foreign_key_checks';
    ```
    ```
    +--------------------+-------+
    | Variable_name      | Value |
    +--------------------+-------+
    | foreign_key_checks | ON    |
    +--------------------+-------+
    1 row in set (0.01 sec)
    ```

