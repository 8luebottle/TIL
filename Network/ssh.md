# SSH 
> Reference : [SSH Academy](https://www.ssh.com/ssh/)

SSH : **S**ecure **SH**ell protocol

### Table of Contents

- [About SSH](#about-ssh)
  - [SSH-1, SSH-2](#ssh-1-ssh-2)
- [SSH and OS](#ssh-and-os)
  - [MacOS](#macos)
  - [Windows](#windows)
- [SSH Server, SSH Client](#ssh-server-ssh-client)
  - [원격 접속](#원격-접속)
- [SSH Configuration File](#ssh-configuration-file)
  - [User Specific Configuration Files](#user-specific-configuration-files)

## About SSH

SSH 는 데이터를 안전하게 송수신하기 위해 사용하는 프로토콜이다.

* SSH 는 안전한 데이터 전송 그리고 원격 접속을 위해 사용된다.

SSH 가 등장하기 이전에는 데이터 통신을 위해 Telnet, rlogin, rsh, rcp, rexec 등이 사용되었다. 현재 SSH 가 이들의 자리를 대체하게 된 이유는 보안성 때문이다.

Telnet 과 같은 경우 데이터를 주고 받을때 평문(plain text) 으로 주고 받는다. 데이터가 오가는 과정 중에 제 3자가 데이터를 탈취하여 해석할 수 있는 불상사가 발생할 수 있다. 비밀번호와 같은 중요한 데이터 또한 암호화가 되지 않기에 보안에 문제가 발생한다.  

이러한 문제를 해결하기 위해 나온 프로토콜이 SSH 이다.  
평문인 Telnet 과 달리 SSH 는 데이터를 암호화 시켜 전송한다. 제 3자가 데이터를 가로채더라도 쉽게 해석할 수 없게 된다.  
그렇지만 SSH 가 100%의 보안을 보장해 주는 것은 아니다. 바이러스나, 트로이목마(trojans) 같은 악성코드에서 보호될 수 없기 때문이다.  

### SSH-1, SSH-2

SSH 는 두 버전이 존재한다. SSH-1 과 SSH-2 이다.  
1995년 헬싱키 대학(Helsinki University of Technology)에서 컴퓨터 과학분야 연구원으로 있던 [Tatu Ylönen](https://ylonen.org/) 이 **SSH-1** 를 고안해 내었다. 그는 같은해 7월 SSH를 free software로 출시한다.  

이듬해인 1996년 **SSH-2** 가 개발되었다. SSH-2 는 보안이 더 강화된 SSH 이다. FTP 와 비슷하게 기능한다.

[↑ return to TOC](#table-of-contents)

## SSH and OS

SSH 를 사용하기 위해서는 SSH server 프로그램과 SSH client 프로그램이 필요하다.  

유닉스 기반인 리눅스와 맥은 별도의 SSH 설치가 필요하지 않다.  
윈도우 같은 경우에는 SSH가 내장되어 있지 않기에 별도의 설치를 필요로한다.  

### MacOS

<img width="300" alt="OpenSSH" src="https://user-images.githubusercontent.com/48475824/80451662-5c338480-895f-11ea-98bf-acd4b366bd71.gif">

**OpenSSH** 가 내장되어 있기에 바로 사용 가능하다.  
2020 4월 현재 최신 버전은 OpenSSH 8.2 (Feb 14, 2020) 이다.
- ssh, scp, sftp 를 통한 원격 조종
- 키 관리
  - ssh-add, ssh-keysign, ssh-keyscan, and ssh-keygen
- SSH 서버사이드 
  - sshd, sftp-server, ssh-agent

### Windows

아래의 소프트웨어중 하나를 선택하여 설치

- PuTTY
- TTSSH
- Cygwin
- MSSH
- WinSCP
- FileZilla

#### PuTTY

<img width="80" alt="PuTTY" src="https://user-images.githubusercontent.com/48475824/80448276-baa83500-8956-11ea-959e-3cb53b70f447.jpg">

Simon Tatham 이 개발한 무료 Telnet 및 SSH 클라이언트 소프트웨어.  
초기에는 Widows 용도로 만들어 졌지만 현재는 MacOS, Linux 에서도 사용 가능하다.
1998년 1월 8일 처음으로 출시되었으며 C 로 작성되었다.  

PuTTY 지원하는 프로토콜은 아래와 같다.

- SSH
- SCP
- Telnet
- rlogin

Download : [PuTTY](https://www.putty.org/)

#### TTSSH

TTSSH : Tera Term SSH

#### Cygwin

<img width="80" alt="Cygwin" src="https://user-images.githubusercontent.com/48475824/80449487-3bb4fb80-895a-11ea-8f93-3aee2586a359.png">

Cygwin 은 Cygnus Solutions 에서 개발하였다. 1995년에 출시. C 와 C++ 로 작성되었다.  
시그윈을 사용함으로써 Windows 상에서 Linux 를 쓰는 느낌을 낼 수 있다.  
* Linux 명령어
* Shell 사용

Cygwin 이 제공하는 원격 접속 기능
* ssh
* rsh
* telnet

Download : [Cygwin](https://cygwin.com/install.html)

#### WinSCP

<img width="80" alt="WinSCP" src="https://user-images.githubusercontent.com/48475824/80450259-1c1ed280-895c-11ea-9fa8-6ce170714c5d.png">

Martin Přikryl 가 C++ 로 작성한 윈도우용 오픈소스 소프트웨어.  
2000 년도에 첫 출시되었다.  

안전한 데이터 전송을 위해 SSH, SCP, SFTP 를 사용한다.

git repository : [winscp](https://github.com/winscp/winscp)

Download : [WinSCP](https://winscp.net/eng/download.php)

[↑ return to TOC](#table-of-contents)

#### FileZilla

<img width="80" alt="FileZilla" src="https://user-images.githubusercontent.com/48475824/80450686-0a89fa80-895d-11ea-81c2-08242d7c0b94.png">

2001 년 6월 22일 Tim Kosse 가 출시한 자유 소프트웨어  
Windows, Linux, 그리고 MacOS 에서 사용가능하다.  
C++, wxWidgets 로 작성되었다.  

Download : [FileZilla](https://filezilla-project.org/)

## SSH Server and SSH Client  

SSH 는 서버와 클라이언트의 구조를 갖는다.

### 원격 접속

SSH 는 대표적으로 원격접속을 위해 사용된다.

## SSH Configuration File

SSH 구성파일은 두 가지로 나뉜다.

- User specific configuration files
- System wide configuration files

### User Specific Configuration Files

**Use vim**
```
vim ~/.ssh
```

SSH 를 열어보면 아래와 같은 파일들을 볼 수 있다.
* config
* id_dsa
* id_dsa.pub
* id_rsa
* id_rsa.pub
* known_hosts

SSH-1 은 RSA 알고리즘만 제공  
SSH-2 는 RSA 와 DSA 알고리즘 모두 제공  
* **DSA** : **D**igital **S**ignature **A**lgorithm
* **RSA** : **R**ivest-**S**hamir-**A**dleman


#### config 
클라이언트 구성 파일

#### id_dsa
DSA 개인 키  

#### id_dsa.pub
DSA 공개 키

#### id_rsa
RSA 개인 키

#### id_rsa.pub
RSA 공개 키

#### known_hosts
```
vim ~/.ssh/known_hosts
```
Known hosts 에서 특정 호스트 관련 Finger Print를 미리 등록해 놓을 수 있다.

[↑ return to TOC](#table-of-contents)
