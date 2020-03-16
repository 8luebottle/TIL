# SMTP 

### Table of Contents
* [SMTP Basic](#smtp-basic)
* [SMTP Reply Code](#smtp-reply-code)
* [Mail System Components](#mail-system-components)

## SMTP Basic
SMTP : **S**imple **M**ail **T**ransfer **P**rotocol   
간이 전자우편 전송 프로토콜  

SMTP 는 1982년 인터넷 문서 [RFC 821](https://tools.ietf.org/html/rfc821) 에서 처음 정의되었다.   
* 해당 문서를 통해 SMTP 의 동작원리에 대해 알아볼 수 있다.

<img width="750" alt="smtp-pop" src="https://user-images.githubusercontent.com/48475824/76755086-9a695000-67c6-11ea-86f8-437296be665b.png">

* SMTP : Simple Mail Transfer Protocol
  * 메일 송신용 프로토콜 
* POP : Post Office Protocol 
  * 메일 수신용 프로토콜

SMTP 는 인터넷 상에서 전자우편(Electronic Mail)을 보낼 때 사용되는 프로토콜이다. 사실상의 표준으로써 e-mail 을 한 서버에서 다른 서버로 전송한다.  
* 신뢰성 있는 TCP 연결을 통해 메일을 간단하고 효율적이게 전송시킨다.
* 스트림 방식을 통해 전송.
* Default TCP Port : 25

SMTP 는 ASCII  데이터만 처리 가능하다.
* 텍스트를 7비트 ASCII 코드로 인코딩한다.  
* 다양한 종류의 데이터를 처리하고자 한다면 MIME을 프로토콜을 사용하면 된다.
  * MIME : Multi-purpose Internet Mail Extensions  
    * SMTP 확장형
    * Image , Audio, Video 등의 데이터 처리 가능

[↑ return to TOC](#table-of-contents)


## SMTP Reply Code  
응답은 Carrage return + Line feed 로 끝난다.

* 220  
  Service Ready

* 221  
  Service closing transmission channel

* 250  
  Requested mail action completed

* 354  
  Start mail input

* 500  
  Command unrecognised

* 530  
  Access denied

* 554  
  Transaction faild

[↑ return to TOC](#table-of-contents)


## Mail System Components  
<img width="733" alt="mail-system-components" src="https://user-images.githubusercontent.com/48475824/76760191-8a566e00-67d0-11ea-9f2d-6c0d53db5e53.png">

> Image Credit : David Byers

* **MAA**  
  Mail Access Agent  
  * 메일박스에 있는 email을 읽음
  * 예) Courier IMAPD

* **MDA**  
  Mail Delivery Agent  
  * MTA 로 부터 메일을 받음  
  * 로컬 메일박스에 메일을 전송  
  * 메일을 다른 MTA 로 전송
  * 예) Profix local, smtp 

* **MRA**  
  Mail Retreival Agent  
  * MAA 로 부터 메일 검색
  * 예) Fetchmail

* **MSA**  
  Mail Submission Agent  
  * MUA 로 부터 메일을 받음

* **MTA**  
  Mail Transfer Agent  
  * 메일을 중계 및 전달  
  * 메일 전송 서버  
  * 예) Sendmail

* **MUA**  
  Mail User Agent  
  * 메일을 읽고 씀  
  * 클라이언트 프로그램
  * 예) Mozilla Thunderbird, Outlook Express

[↑ return to TOC](#table-of-contents)