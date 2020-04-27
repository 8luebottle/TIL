# SSH 
SSH : **S**ecure **SH**ell protocol

### Table of Contents

- [About SSH](#about-ssh)
  - [SSH-1, SSH-2](#ssh-1,-ssh-2)
- [SSH and OS](#ssh-and-os)
- [SSH Server, SSH Client](#ssh-server,-ssh-client)

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
1995년 헬싱키 대학(Helsinki University of Technology)에서 연구원으로 있던 Tatu Ylönen 이 **SSH-1** 를 고안해 내었다. 그는 같은해 7월 SSH를 free software로 출시한다.  

이듬해인 1996년 **SSH-2** 가 개발되었다. SSH-2 는 보안이 더 강화된 SSH 이다. FTP 와 비슷하게 기능한다.

[↑ return to TOC](#table-of-contents)

## SSH and OS

[↑ return to TOC](#table-of-contents)


## SSH Server and SSH Client

[↑ return to TOC](#table-of-contents)