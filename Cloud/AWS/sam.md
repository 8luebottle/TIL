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
    - [Required](#required)  
      Transform, Resources
    - [Optional](#optional)  
      Globals, Description, Metadata, Parameters, Mappings, Conditions, Outputs
  - [Resource Types](#resource-types)  
      Api, Application, Function, HttpApi, SimpleTable, LayerVersion
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

### Template Section

템플릿은 반드시 포함시켜야 하는 부분과 선택적인 부분으로 나뉜다.

1. Required
    * Transform
    * Resources

1. Optional
    * Globals
    * Description
    * Metadata
    * Parameters
    * Mappings
    * Conditions
    * Outputs


#### Required  
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
    - **Resource types**  
      
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

      

#### Optional
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

### Resource Types
리소스 종류에 대해 알아보자.
다양한 리소스 타입은 [여기](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html) 에서 확인 가능하다.  

* AWS::Serverless::Api
* AWS::Serverless::Application
* AWS::Serverless::Function
* AWS::Serverless::HttpApi
* AWS::Serverless::SimpleTable
* AWS::Serverless::LayerVersion

#### Function
```AWS::Serverless::Function``` 은 람다 함수, IAM 실행역할(IAM execution role)과 이벤트 소스 매핑(event source mapping)을 생성한다.
* IAM : Identity and Access Management

**Function 속성**  
함수의 속성중에서 반드시 적어주어야 하는 속성은 ```Handler```와 ```Runtime``` 이다.

* AssumeRolePolicyDocument  
  자료형 : IAM policy document 객체

* AutoPublishAlias  
  자료형 : string  
  Alias 의 이름.  
  ```AutoPublishAlias : <alias-name>```

  Lambda에 alias 를 설정 후, 추가적으로 api gateway 설정을 해주어야 한다.

* CodeUri  
  자료형 : string 또는 S3 Location 객체  
  S3 Location 객체는 ```Bucket```, ```Key```, ```Version``` 을 담고 있다.  
  S3 Location Objects 의 예)  
  ```yaml
  CodeUri:
    Bucket: mybucket-name
    Key: code.zip
    Version: 121212
  ```

* DeadLetterQueue  
  자료형 : map 또는 DeadLetterQueue 객체  

  예) 
  ```yaml
    DeadLetterQueue:
      Type: `SQS` or `SNS`
      TargetArn: ARN of the SQS queue or SNS topic to use as DLQ.
  ```

* DeploymentPreference  
  자료형 : DeploymentPreference 객체  
  안전한 Lambda 배포를 위해서 설정.  

  설정의 예)  
  Globals 에다 설정해 놓는다.
  ```yaml
  AutoPublishAlias: live
  DeploymentPreference:
  Type: Linear10PercentEvery10Minutes
  ```

* Description  
  자료형 : string
  해당 람다 함수에 관한 설명

* Envrionment  
  자료형 : Function Environment 객체  

  예)  
  ```yaml
  Variables:
    TABLE_NAME: my-table
    STAGE: prod
  ```

* EventInvokeConfig  
  자료형 : EventInvokeConfig 객체  

  예)  
  ```yaml
  MyFunction:
   Type: 'AWS::Serverless::Function'
   Properties:
      EventInvokeConfig:
      MaximumEventAgeInSeconds: Integer (Min: 60, Max: 21600)
      MaximumRetryAttempts: Integer (Min: 0, Max: 2)
      DestinationConfig:
          OnSuccess:
          Type: [SQS | SNS | EventBridge | Function]
          Destination: ARN of [SQS | SNS | EventBridge | Function]
          OnFailure:
          Type: [SQS | SNS | EventBridge | Function]
          Destination: ARN of [SQS | SNS | EventBridge | Function]
  ```

* Events  
  자료형 : Map of string  
  Key 값은 알파벳과 숫자로만 이루어져 있다.  

* FunctionName  
  자료형 : string  
  람다 함수명.  
  최대 64 Characters 까지  
  직접 함수명을 지정해 주지 않는다면 AWS CloudFormation 이 유니크한 이름을 생성시켜준다.  

  * 이름 형식의 예)  
    * Function name : ```my-function```
    * Function ARN : ```arn:aws:lambda:us-west-2:123456789012:function:my-function```
    * Partial ARN : ```123456789012:function:my-function```

* **Handler** (Required)  
  자료형 : string  
  코드의 담긴 함수가 실행된다.

* Inlinecode  
  자료형 : string  
  람다의 인라인 코드.  

* KmsKeyArn  
  자료형 : string  

* Layers  
  자료형 : list of string

* MemorySize  
  자료형 : integer  
  Default 값은 128MB

* PermissionsBoundary  
  자료형 : string  
  ARN 의 허락된 범위  

* Policies  
  자료형 : string 또는 list of string  

* ProvisionedConcurrencyConfig  
  자료형 : ProvisionedConcurrencyConfig 객체  

* ReservedConcurrentExecutions  
  자료형 : integer  

* Role  
  자료형 : string  
  해당 함수를 실행하는데 필요한 ARN 또는 IAM 역할.  
  * ARN (Amazon Resource Names)  

  역할을 기입해주지 않으면 해당 함수는 default role 로 설정된다.

* **Runtime** (Required)  
  자료형 : string  
  실행시간 환경.

* Tags  
  자료형 : Map of string  

* Timeout  
  자료형 : integer  
  함수가 실행될 시간 제한(최대 시간)기입.  
  이 시간이 지나면 함수는 죽게된다.  
  단위는 초(second).  
  Default : 3 초.  

* Tracing  
  자료형 : string  
  * Active
  * PassThrough

* VersionDescription  
  자료형 : string

* VpsConfig  
  자료형 : VPC config 객체  


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