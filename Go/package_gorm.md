# Pakcage gorm
gorm 은 Go의 ORM 라이브러리이다.

### Table of Contents
* gorm 코드 열어보기
    * [gorm DB 구조체](#gorm의-구조체)
    * [gorm.Debug](#gorm.Debug())
    * [gorm.clone](#gorm.clone())
    * [gorm.LogMode](#gorm.LogMode())
    * [gorm.AutoMigrate](#gorm.AutoMigrate())
    * [gorm.Open](#gorm.Open())


## Install gorm
gorm 패키지 받기  
```go
go get github.com/jinzhu/gorm 
```


## gorm 코드 열어보기
### gorm의 구조체
연결시킨 DB의 정보를 갖고있다.  
   ```go
    type DB struct {
        sync.RWMutex
        Value        interface{}
        Error        error
        RowsAffected int64

        // single db
        db                SQLCommon
        blockGlobalUpdate bool
        logMode           logModeValue
        logger            logger
        search            *search
        values            sync.Map

        // global db
        parent        *DB
        callbacks     *Callback
        dialect       Dialect
        singularTable bool

        // function to be used to override the creating of a new timestamp
        nowFuncOverride func() time.Time
    }
   ```

### gorm.Debug()
```go
func (s *DB) Debug() *DB { return s.clone().LogMode(true) }
```
* debug mode를 실행시킨다.
* Log 가 detail 하게 출력된다.

### gorm.clone()
```go
func (s *DB) clone() *DB
```
* clone()은 DB 구조체의 private method 이다.

### gorm.LogMode()
```go
func (s *DB) LogMode(enable bool) *DB {
  if enable {
     s.logMode = detailedLogMode
  } else {
     s.logMode = noLogMode
  }
  return s
}
```
* LogMode 는 DB의 메서드
* log mode 를 설정해준다.
    * true 값 일시  
    detailed log를 표시
    * false 값 일시  
    no log
    * default 값 일시  
    error logs만 프린트

### gorm.AutoMigrate()
```go
func (s *DB) AutoMigrate(values ...interface{}) *DB {
  db := s.Unscoped()
  for _, value := range values {
     db = db.NewScope(value).autoMigrate().db
  }
  return db
}
```
* given mode로 auto migration을 실행한다.
* Missing fields 만 add 시킨다.
* Current data 삭제하거나 변경하진 않는다.

### gorm.Open()
```go
func Open(dialect string, args ...interface{}) (db *DB, err error) {
  if len(args) == 0 {
     err = errors.New("invalid database source")
     return nil, err
  }
  var source string
  var dbSQL SQLCommon
  var ownDbSQL bool

  switch value := args[0].(type) {
  case string:
     var driver = dialect
     if len(args) == 1 {
        source = value
     } else if len(args) >= 2 {
        driver = value
        source = args[1].(string)
     }
     dbSQL, err = sql.Open(driver, source)
     ownDbSQL = true
  case SQLCommon:
     dbSQL = value
     ownDbSQL = false
  default:
     return nil, fmt.Errorf("invalid database source: %v is not a valid type", value)
  }

  db = &DB{
     db:        dbSQL,
     logger:    defaultLogger,
     callbacks: DefaultCallback,
     dialect:   newDialect(dialect, dbSQL),
  }
  db.parent = db
  if err != nil {
     return
  }
  // Send a ping to make sure the database connection is alive.
  if d, ok := dbSQL.(*sql.DB); ok {
     if err = d.Ping(); err != nil && ownDbSQL {
        d.Close()
     }
  }
  return
}

```
* 새로운 DB 연결 초기화
* driver가 첫번째로 임포트 되야 함.
    ```go
    // example
    s.DB, err = gorm.Open(DbDriver, DBURL)
    ```