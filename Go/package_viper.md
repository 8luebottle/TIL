# Package Viper  
<img width="200" alt="viper" src="https://user-images.githubusercontent.com/48475824/77227394-683f6000-6bc3-11ea-814e-d425c6429fe0.png">

환경 설정 파일들을 다루기 위해 Viper Package 를 사용한다.

### Table of Contents
* [viper Basic](#viper-basic)
* [viper 코드 열어보기](#viper-코드-열어보기)
    * [viper.Readconfig](#viperreadconfig)
    * [viper.ReadInConfig](#viperreadinconfig)
    * [viper.WriteConfig](#viperwriteconfig)
    * [viper.Set](#viperset)
    * [viper.MergeInConfig](#vipermergeinconfig)

## viper Basic
viper 은 유명한 configuration 패키지로써 많은 Go 프로젝트들 내에서 사용되었다. 

* **Hugo** : 정적 사이트 생성기
* **Notary** : Docker 이미지 위변조 방지 툴
* **RexRay** : Docker 와 Mesos 의 Container 스토리지 오케스트레이션 엔진 

  <img width="150" alt="viper-project" src="https://user-images.githubusercontent.com/48475824/77227225-016d7700-6bc2-11ea-8cfe-31c9724cd2c5.png">

### env variable
환경 변수는 실행 환경 정보의 값을 지니고 있다.  
Go 에서 env variable 을 관리하기 위해 자주 사용되는 패키지들은 세가지가 있다.
1. os package
1. godotenv package
1. viper package

이 중 viper package 에 대해 알아보자.

### Install
```go get github.com/spf13/viper```

### 기본 사용법
**Instance**  
viper 인스턴스 생성하기  
```viper.New()```

**Set File & Path**  
config 파일과 경로를 설정하기 위해서 ```SetConfigFile``` 이라는 메서드를 사용한다.  
```viper.SetConfigFile(".env")```  
* Viper 는 env 파일 외에 다양한 파일들을 지원한다.
    * HCL
    * TOML
    * JSON
    * YAML
    * etc..

**Read Config File**   
viper 에서 config 파일을 읽어들이는 메서드는 두 가지가 있다. 
1. ```ReadConfig()```  
    * yaml
    * json

1. ```ReadInConfig()```  
    * byte buffer

[↑ return to TOC](#table-of-contents)


## viper 코드 열어보기
### viper.ReadConfig
Configuration 파일을 읽어들인다.  
```go
func (v *Viper) ReadConfig(in io.Reader) error {
    v.config = make(map[string]interface{})
    return v.unmarshalReader(in, v.config)
}
```
* key 가 파일내에 존재하지 않을 때 해당 key 는 nil 값으로 설정된다.

[↑ return to TOC](#table-of-contents)


### viper.ReadInConfig
미리 설정해둔 경로로 가서 디스크나 키-값 스토리지에 있는 config 파일을 찾아 읽어들인다.
* 설정된 경로의 예)  
```viper.AddConfigPath(currentdir())```
```go
func (v *Viper) ReadInConfig() error {
	jww.INFO.Println("Attempting to read in config file")
	filename, err := v.getConfigFile()
	if err != nil {
		return err
	}

	if !stringInSlice(v.getConfigType(), SupportedExts) {
		return UnsupportedConfigError(v.getConfigType())
	}

	jww.DEBUG.Println("Reading file: ", filename)
	file, err := afero.ReadFile(v.fs, filename)
	if err != nil {
		return err
	}

	config := make(map[string]interface{})

	err = v.unmarshalReader(bytes.NewReader(file), config)
	if err != nil {
		return err
	}

	v.config = config
	return nil
}
```

[↑ return to TOC](#table-of-contents)


### viper.WriteConfig
현재의 viper configuration 을 파일에 쓴다. 파일이 작성되는 위치는 미리 지정해둔 경로이다.  
만약 경로가 설정되 있지 않다면 err 를 리턴한다.
```go
func (v *Viper) WriteConfig() error {
	filename, err := v.getConfigFile()
	if err != nil {
		return err
	}
	return v.writeConfig(filename, true)
}
```

[↑ return to TOC](#table-of-contents)


### viper.Set
Set을 통해 직접 config 의 key 와 value 를 설정
```go
func (v *Viper) Set(key string, value interface{}) {
	key = v.realKey(strings.ToLower(key))
	value = toCaseInsensitiveValue(value)

	path := strings.Split(key, v.keyDelim)
	lastKey := strings.ToLower(path[len(path)-1])
	deepestMap := deepSearch(v.override, path[0:len(path)-1])

	deepestMap[lastKey] = value
}
```

* Key 는 case-insensitive 

[↑ return to TOC](#table-of-contents)


### viper.MergeInConfig
새 config 파일과 기존에 존재하는 config 파일을 합병시킨다.
```go
func (v *Viper) MergeInConfig() error {
	jww.INFO.Println("Attempting to merge in config file")
	filename, err := v.getConfigFile()
	if err != nil {
		return err
	}

	if !stringInSlice(v.getConfigType(), SupportedExts) {
		return UnsupportedConfigError(v.getConfigType())
	}

	file, err := afero.ReadFile(v.fs, filename)
	if err != nil {
		return err
	}

	return v.MergeConfig(bytes.NewReader(file))
}
```

[↑ return to TOC](#table-of-contents)
