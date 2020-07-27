# CLI
**CLI :**  **C**ommand Line **I**nterface

### Table of Contents
- [About CLI](#about-cli)
  - [aws configure](aws-configure)
    - [4 Prompts](4-prompts)
    - [aws configure w/o profile option](aws-configure-w/o-profile-option)
    - [aws configure w/ profile option](aws-configure-w/-profile-option)

## About CLI
AWS와 관련된 작업을 수행하기 위한 한 방편으로 CLI를 사용할 수 있다.  

AWS CLI는 현재 두 버전이 존재한다.
* Version 1.x
* Version 2.x


### aws configure
AWS CLI를 통해 설정 정보를 저장 한다.  
```aws configure``` 설정 시 ```-- profile``` 옵션을 지정해 줄 수 있는데 만약 ```--profile``` 을 명시하지 않는다면 ```default``` 로 간주된다.  

설정한 config 는 파일로 저장된다.
* MacOS  
  ```~/.aws/credential```
* Windows  
  ```C:₩Users₩userName₩.aws₩credentials```

#### 4 Prompts
설정 정보를 ```aws configure``` 명령어를 통해 입력할 시 아래의 네가지를 입력하도록 요구받는다.  
1. **Access Key ID**  
  액세스 키 ID
1. **Secrete Access Key**  
  보안 액세스 키
1. **AWS Region**  
  AWS 리전
1. **Output Format**  
  출력 형식은 4가지 타입이 제공된다.  
    1. **json**  
      출력 형식을 지정해 주지 않을시 default 로 json이 설정된다.  
    1. **yaml**  
      AWS CLI version 2 Only.  
      CLI version 1 에서는 yaml 출력타입를 사용할 수 없다.  
    1. **text**  
      여러개의 탭으로 구분된 문자열의 값의 형태.  
    1. **table**  
      +|- 문자로 셀 테투리 만들어진 표.  

```aw
AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
Default region name [None]: us-west-2
Default output format [None]: json
```

#### aws configure w/o profile option  
default 설정.
```
aws configure
```

```
[default]
region=us-west-2
output=json
```

#### aws configure w/ profile option 
AWS 사용시 보통 여러 계정을 갖고 있는 경우가 많다. 계정별 설정 정보를 저장하기 위해 ```--profile``` 옵션을 사용한다.  
```
aws configure --profile userName
```

```
[profile userName]
region=us-east-1
output=yaml
```

[↑ return to TOC](#table-of-contents)