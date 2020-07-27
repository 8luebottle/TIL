# CLI
**CLI :**  **C**ommand Line **I**nterface

### Table of Contents
- [About CLI](#about-cli)
  - [aws configure](aws-configure)
    - [4 Prompts](4-prompts)
    - [aws configure w/o profile option](aws-configure-wo-profile-option)
    - [aws configure w/ profile option](aws-configure-w-profile-option)

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
        ```
        aws iam list-users --output json
        ```
        ```json
        {
            "Users": [
                {
                    "Path": "/",
                    "UserName": "Admin",
                    "UserId": "AIDA1111111111EXAMPLE",
                    "Arn": "arn:aws:iam::123456789012:user/Admin",
                    "CreateDate": "2014-10-16T16:03:09+00:00",
                    "PasswordLastUsed": "2016-06-03T18:37:29+00:00"
                },
                {
                    "Path": "/backup/",
                    "UserName": "backup-user",
                    "UserId": "AIDA2222222222EXAMPLE",
                    "Arn": "arn:aws:iam::123456789012:user/backup/backup-user",
                    "CreateDate": "2019-09-17T19:30:40+00:00"
                },
                {
                    "Path": "/",
                    "UserName": "cli-user",
                    "UserId": "AIDA3333333333EXAMPLE",
                    "Arn": "arn:aws:iam::123456789012:user/cli-user",
                    "CreateDate": "2019-09-17T19:11:39+00:00"
                }
            ]
        }
        ```
    1. **yaml**  
      AWS CLI version 2 Only.  
      CLI version 1 에서는 yaml 출력타입를 사용할 수 없다.  
        ```
        aws iam list-users --output yaml
        ```
        ```yaml
        Users:
        - Arn: arn:aws:iam::123456789012:user/Admin
          CreateDate: '2014-10-16T16:03:09+00:00'
          PasswordLastUsed: '2016-06-03T18:37:29+00:00'
          Path: /
          UserId: AIDA1111111111EXAMPLE
          UserName: Admin
        - Arn: arn:aws:iam::123456789012:user/backup/backup-user
          CreateDate: '2019-09-17T19:30:40+00:00'
          Path: /backup/
          UserId: AIDA2222222222EXAMPLE
          UserName: arq-45EFD6D1-CE56-459B-B39F-F9C1F78FBE19
        - Arn: arn:aws:iam::123456789012:user/cli-user
          CreateDate: '2019-09-17T19:30:40+00:00'
          Path: /
          UserId: AIDA3333333333EXAMPLE
          UserName: cli-user
        ```
    1. **text**  
      여러개의 탭으로 구분된 문자열의 값의 형태.  
        ```
        aws iam list-users --output text --query 'Users[*].[UserName,Arn,CreateDate,PasswordLastUsed,UserId]'
        ```
        ```aw
        USERS   arn:aws:iam::123456789012:user/Admin                2014-10-16T16:03:09+00:00   2016-06-03T18:37:29+00:00   /          AIDA1111111111EXAMPLE   Admin 
        USERS   arn:aws:iam::123456789012:user/backup/backup-user   2019-09-17T19:30:40+00:00                               /backup/   AIDA2222222222EXAMPLE   backup-user 
        USERS   arn:aws:iam::123456789012:user/cli-user             2019-09-17T19:11:39+00:00                               /          AIDA3333333333EXAMPLE   cli-user
        ```
    1. **table**  
      +|- 문자로 셀 테투리 만들어진 표.  
        ```
        aws iam list-users --output table
        ```
        ```sql
        -----------------------------------------------------------------------------------------------------------------------------------------------------------------
        |                                                                                 ListUsers                                                                     |
        +---------------------------------------------------------------------------------------------------------------------------------------------------------------+
        ||                                                                                  Users                                                                      ||
        |+----------------------------------------------------+---------------------------+---------------------------+----------+-----------------------+-------------+|
        ||                         Arn                        |       CreateDate          |    PasswordLastUsed       |   Path   |        UserId         |   UserName  ||
        |+----------------------------------------------------+---------------------------+---------------------------+----------+-----------------------+-------------+|
        ||  arn:aws:iam::123456789012:user/Admin              | 2014-10-16T16:03:09+00:00 | 2016-06-03T18:37:29+00:00 | /        | AIDA1111111111EXAMPLE | Admin       ||
        ||  arn:aws:iam::123456789012:user/backup/backup-user | 2019-09-17T19:30:40+00:00 |                           | /backup/ | AIDA2222222222EXAMPLE | backup-user ||
        ||  arn:aws:iam::123456789012:user/cli-user           | 2019-09-17T19:11:39+00:00 |                           | /        | AIDA3333333333EXAMPLE | cli-user    ||
        +---------------------------------------------------------------------------------------------------------------------------------------------------------------+
        ```

```aw
AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
Default region name [None]: us-west-2
Default output format [None]: json
```

[↑ return to TOC](#table-of-contents)

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

[↑ return to TOC](#table-of-contents)

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
