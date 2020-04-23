# AWS SAM
> Resources : [AWS CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide)

**SAM** : **S**erverless **A**pplication **M**odel  
SAM 은 AWS 상에서 Serveless 어플리케이션을 구축할 때 사용하는 프레임워크 이다.

<img width="250" alt="SAM" src="https://user-images.githubusercontent.com/48475824/80070812-90353100-857e-11ea-80f3-48d417d2c6f7.png">

AWS SAM 을 사용하여 서버리스 어플리케이션을 정의할 수 있다.
* Serverless 
  개발자가(사용자가) 서버를 고려하지 않고 앱과 서비스를 구축할 수 있다.  
  인프라 관리에 관한 개발자의 업무를 줄여준다.  
  줄어드는 업무의 예) 
  * 패치 적용 
  * 클러스터 프로비저닝
  * 용량 프로비저닝
  * OS 유지 관리

거의 모든 앱이나 백엔드 서비스는 서버리스를 통해 구축 가능하다.

### Table of Contents

- [AWS SAM Components](#aws-sam-components)
  - [Template Sepcifiction](#template-spefication)
    - [Template Section](#template-section)
  - [CLI](#cli)
    - [Install SAM CLI](#install-sam-cli)
    - [Upgrade SAM CLI](#upgrade-sam-cli)
  - [Deploy](#deploy)

## AWS SAM Components

AWS SAM 은 아래의 구성요소로 이루어져 있다.

- Template Specification
- CLI

### Template Specification

SAM Template Specification 은 YAML 또는 JSON 형식을 지니고 있다.  

Template 의 예)
```yaml
AWSTemplateFormatVersion: 2020-04-23 
 Transform: [LalaMacro, AWS::Serverless]
 Resources:
    WaitCondition:
      Type: AWS::CloudFormation::WaitCondition
    LalaBucket:
      Type: 'AWS::S3::Bucket'  
      Properties:
        BucketName: MyBucket 
        Tags: [{"key":"value"}] 
        CorsConfiguration:[]   
    LalaEc2Instance:
      Type: 'AWS::EC2::Instance' 
      Properties:
        ImageID: "lala-2020"
```

[↑ return to TOC](#table-of-contents)

#### Template Section

템플릿은 아래의 부분으로 나뉜다.

**Required**  
반드시 포함시켜야 하는 부분

1. **Transform**  
  e.g) ```AWS::Serverless-2020-04-23```

1. **Resources**  
  스택의 리소스(Resrouces)와 속성(Properties)을 지정해준다.  
  리소스의 키 명은 ```Resources``` 이다.  
  **e.g) JSON**
    ```json
    "Resources" : {
    "LalaEC2Instance" : {
        "Type" : "AWS::EC2::Instance",
        "Properties" : {
        "ImageId" : "lala-0ff8a4950f237f972"
        }
      }
    }
    ```
    **e.g) YAML**
    ```yaml
    Resources:
    Logical ID:
        Type: Resource type
        Properties:
        Set of properties
    ```

    **리소스가 지닌 필드**
    - **Logical ID**  
      알파벳과 숫자로만 이루어져 있다.  
      템플릿 안에서는 유일한 값이어야 한다.  
      리소스는 EC2 Instance ID 또는 S3 버킷명 과 같은 ```Physical ID``` 도 갖고 있다.  
    - **Resource type**  
      다양한 리소스 타입은 [여기](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html) 에서 확인 가능하다.  
      e.g)  
      ```service-provider::service-name::data-type-name```

      ```AWS::EC2::Instance```
    - **Resource properties**  
      e.g) JSON
      ```json
      "Resources" : {
        "LalaEC2Instance" : {
            "Type" : "AWS::EC2::Instance",
            "Properties" : {
            "ImageId" : "lala-0ff8a4950f237f972"
            }
        }
      }
      ```
      e.g) YAML  
      ```yaml
      Resources:
        LalaEC2Instance:
            Type: "AWS::EC2::Instance"
            Properties:
            ImageId: "lala-0ff8a4950f237f972"
      ```

**Optional**  
선택 사항  

1. Globals  
  공통적인 요소들을 설정한다.

1. Description  
  템플릿에 관한 설명 (Text String)

1. Metadata  
  템플릿에 관해 추가적으로 전달해줄 정보

1. Parameters  

1. Mappings  

1. Conditions  

1. Outputs

[↑ return to TOC](#table-of-contents)

### CLI

SAM Command Line Interface

#### Install SAM CLI
Brew 를 통한 설치법은 아래와 같다.
```
brew tap aws/tap
brew install aws-sam-cli
```

[↑ return to TOC](#table-of-contents)

#### Upgrade SAM CLI
Brew 를 통한 SAM CLI 최신버전 업그레이드
```
brew upgrade aws-sam-cli
```

[↑ return to TOC](#table-of-contents)


### Deploy
배포 과정은 다음과 같다. (대소문자는 구분 안함)
* SAM build
* SAM package
* SAM deploy

#### SAM Build


#### SAM Package


#### SAM Deploy

[↑ return to TOC](#table-of-contents)