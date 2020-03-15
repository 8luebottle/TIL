# Package jwt
**J**ason **W**eb **T**oken

### Table of Contents
* jwt Basic
    * Token의 필요성
    * [JWT 구조](#jwt-구조)  
      Header | Payload | Signature
    * JWT 발급 과정
    * JWT 사용 과정

* jwt 코드 열어보기
    * [MapClaims](#MapClaims)
    * [SigningMethodHMAC](#SigningMethodHMAC)
    * [Parser](#parser)
    * [jwt.New](#jwt.new)
    * [jwt.Parse](#jwt.parse)
    * [jwt.Valid](#jwt.valid)
    * [jwt.VerifyExpiresAt](#jwt.verifyexpiresat)
    * [jwt.VerifyIssuedAt](#jwt.verifyissuedat)
    * [jwt.VerifyNotBefore](#jwt.verifynotbefore)


## jwt Basic
### JWT 구조  
JWT 는 세 파트로 나뉜다.
1. Header
1. Payload
1. Signature

### Header

#### Payload  
Payload 는 Claim 을 담고있다.   
Claim 은 세 가지 타입으로 나뉜다.  
1. Reserved Claim
1. Public Claim
1. Private Claim

* **aud**  
  Audience  
  토큰을 사용할 대상
* **exp**  
  Expiration Time
  토큰의 만료 기간
* **iat**  
  Issued at  
  토큰의 발급 시간
* **iss**  
  Issuer  
  토큰의 발급자  
* **jti**  
  JWT ID  
  JWT 식별을 위한 ID
* **nbf**  
  Not Before  
  해당 값 이후부터 토큰 사용 가능  
  ```nbf``` < ```current time``` < ```exp```  
* **sub**  
  Subject  
  토큰의 주제

### Signature
Header + Payload + Signature Key

[↑ return to TOC](#table-of-contents)


## jwt 코드 열어보기
### MapClaims
```go
type MapClaims map[string]interface{}
```
[↑ return to TOC](#table-of-contents)


### SigningMethodHMAC
HMAC-SHA 알고리즘 구현
```go
type SigningMethodHMAC struct {
  Name string
  Hash crypto.Hash
}
```
지원하는 HMAC-SHA 종류는 아래와 같다.
* HS256  
  <!-- SHA-2 -->
* HS384
* HS512  

이 외의 알고리즘 종류는 에러(```signature is invalid```)를 리턴한다

[↑ return to TOC](#table-of-contents)


### Parser
```go
type Parse struct {
    ValidMethods           []string
    UseJSONNumber          bool
    SkipClaimsValidation   bool
}
```
[↑ return to TOC](#table-of-contents)


### jwt.New
새 토큰 생성시 사용.  
```method```인자에 암호화 할 알고리즘 종류를 전달해준다.
```go
func New(method SigningMethod) *Token {
  return NewWithClaims(method, MapClaims{})
}
```
* Raw : The raw token
    * Populated when you Parse a token.
* Method : 어떤 방법으로 암호화 시키는지.
* Header : 토큰의 첫번째 파트
* Claims : 토큰의 두번째 파트
* Signature : 토큰의 세번째 파트
* Valid : 유효한 토큰인지 판별 (T/F)
    * Populated when you Parse/verify a token.

[↑ return to TOC](#table-of-contents)


### jwt.Parse
```go
func Parse(tokenString string, keyFunc Keyfunc) (*Token, error) {
  return new(Parser).Parse(tokenString, keyFunc)
}
```

[↑ return to TOC](#table-of-contents)

### jwt.Valid
토큰의 유효성을 확인한다.  
클레임의 ```exp```, ```iat```, ```nbf```로 토큰의 유효기간을 판별.  
   * ```exp```, ```iat```, ```nbf``` 가 존재하지 않더라도 유효한 클레임으로 간주.
```go
func (m MapClaims) Valid() error {
  vErr := new(ValidationError)
  now := TimeFunc().Unix()

  if m.VerifyExpiresAt(now, false) == false {
     vErr.Inner = errors.New("Token is expired")
     vErr.Errors |= ValidationErrorExpired
  }

  if m.VerifyIssuedAt(now, false) == false {
     vErr.Inner = errors.New("Token used before issued")
     vErr.Errors |= ValidationErrorIssuedAt
  }

  if m.VerifyNotBefore(now, false) == false {
     vErr.Inner = errors.New("Token is not valid yet")
     vErr.Errors |= ValidationErrorNotValidYet
  }

  if vErr.valid() {
     return nil
  }

  return vErr
}
```
[↑ return to TOC](#table-of-contents)


### jwt.VerifyExpiresAt
```exp```과 ```cmp``` 의 비교를 통해 유효기간을 판별.  
```go
func (m MapClaims) VerifyExpiresAt(cmp int64, req bool) bool {
  switch exp := m["exp"].(type) {
  case float64:
     return verifyExp(int64(exp), cmp, req)
  case json.Number:
     v, _ := exp.Int64()
     return verifyExp(v, cmp, req)
  }
  return req == false
}
```
[↑ return to TOC](#table-of-contents)


### jwt.VerifyIssuedAt
```iat```와 ```cmp``` 의 비교를 통해 유효기간을 판별. 와
```go
func (m MapClaims) VerifyIssuedAt(cmp int64, req bool) bool {
  switch iat := m["iat"].(type) {
  case float64:
     return verifyIat(int64(iat), cmp, req)
  case json.Number:
     v, _ := iat.Int64()
     return verifyIat(v, cmp, req)
  }
  return req == false
}
```
[↑ return to TOC](#table-of-contents)


### jwt.VerifyNotBefore
```nbf```와 ```cmp``` 의 비교를 통해 유효기간을 판별. 
```go
func (m MapClaims) VerifyNotBefore(cmp int64, req bool) bool {
  switch nbf := m["nbf"].(type) {
  case float64:
     return verifyNbf(int64(nbf), cmp, req)
  case json.Number:
     v, _ := nbf.Int64()
     return verifyNbf(v, cmp, req)
  }
  return req == false
}
```

[↑ return to TOC](#table-of-contents)