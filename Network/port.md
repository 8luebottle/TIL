# PORT 
하드웨어에서 포트는 컴퓨터와 장치(혹은 컴퓨터)를 연결하는 물리적 인터페이스라면,  
소프트웨어서 포트는 네트워크상의 데이터가 입출력되는 논리적 인터페이스이다.

* **Hardware Port :** 물리적 입출력 단자
  * USB Port A
  * USB Port B
  * HDMI Port
  * VGA Port
* **Software Port :** 논리적 입출력 단자
  * 20 : FTP
  * 22 : SSH
  * 23 : Telnet
  * 25 : SMTP

네트워크의 포트에 대해 알아보도록 하자.

### Table of Contents
* [About Port](#about-port)
  * [Well-known port](#well-known-port)
    * [Table of Well-known port](#table-of-well-known-port)
    * [HTTP & HTTPS](#http-&-https)
      * 합정역 5번출구
  * [Registered port](#registered-port)
* [Check Port Info](#check-port-info)

## About Port
포트는 데이터를 주고 받을 때 통과하는 통로(또는 문)이다.

<img width="320" alt="door" src="https://user-images.githubusercontent.com/48475824/79042678-ad8c0600-7c34-11ea-9293-ec48c49b874b.jpg">

> Photo by Christian Stahl on Unsplash

0번 부터 시작되는 포트의 총 개수는 65535개가 존재한다. 이는 한 컴퓨터에 6만 5천개 이상의 문이 존재한다고 볼 수 있다.  

포트는 아래 세 가지 그룹으로 나뉜다.

* Well-known port : 0~1023  
* Registered port : 1024~49151  
* Dynamic Port : 49152~655535  

### Well-known port

0~1023 까지의 포트는 잘 알려진 포트(well-known port) 이다.  
이 범위의 포트들은 IANA에 의해 미리 지정된 것들이다. 각각의 포트마다 정해진 용도가 있다.  

* IANA : **I**nternet **A**ssigned **N**umbers **A**uthority  
  IANA는 인터넷 주소 자원(도메인, IP 주소 등)을 관리해주는 국제 기관이다.

#### Table of Well-known port

| Port | About                                  | TCP | UDP |
|:----:|----------------------------------------|:---:|:---:|
| 0    | Reserved                               |     | O   |
| 1    | TCPMUX                                 | O   | O   |
| 2    | CompressNET Management Utility         | O   | O   |
| 3    | CompressNET Compression Process        | O   | O   |
| 5    | Remote Job Entry                       | O   | O   |
| 7    | Echo Protocol                          | O   | O   |
| 9    | Discard Protocol                       | O   | O   |
| 11   | Active User                            | O   | O   |
| 13   | Daytime Protocol                       | O   | O   |
| 15   | netstat service                        | O   | O   |
| 17   | Quote of the Day                       | O   | O   |
| 18   | MSP                                    | O   | O   |
| 19   | CHARGEN                                | O   | O   |
| 20   | FTP - Data Transfer                    | O   |     |
| 21   | FTP - Control                          | O   |     |
| 22   | [SSH](https://github.com/8luebottle/TIL/blob/master/Network/ssh.md)                                 | O   | O   |
| 23   | Telnet Protocol                        | O   |     |
| 24   | Private mail                           | O   | O   |
| 25   | [SMTP](https://github.com/8luebottle/TIL/blob/master/Network/smtp.md)                                | O   |     |
| 27   | NSW User System FE                     | O   | O   |
| 34   | Remeote File                           | O   | O   |
| 35   | Private Printer Server Protocol        | O   | O   |
| 37   | TIME Protocol                          | O   | O   |
| 39   | RLP : Resource Location Protocol       | O   | O   |
| 41   | Graphics                               | O   | O   |
| 43   | WHOIS Protocol                         | O   |     |
| 50   | Remote Mail Checking Protocol          | O   | O   |
| 52   | XNS Time Protocol                      | O   | O   |
| 53   | DNS                                    | O   | O   |
| 56   | RAP : Route Access PRotocol            | O   | O   |
| 57   | MTP                                    | O   |     |
| 58   | XNS Mail                               | O   | O   |
| 69   | TFTP : Trivial File Transfer Protocol  |     | O   |
| 70   | Gopher Protocol                        | O   |     |
| 79   | Finger Protocol                        | O   |     |
| 80   | HTTP                                   | O   | O   |
| 81   | Torpark (Onion Routing)                | O   |     |
| 99   | WIP Message Protocol                   | O   |     |
| 107  | Remote TELNET Service Protocol         | O   |     |
| 109  | POP2                                   | O   |     |
| 110  | POP3                                   | O   |     |
| 113  | Identification Service                 |     | O   |
| 115  | SFTP                                   | O   |     |
| 118  | SQL Services                           | O   | O   |
| 119  | NNTP                                   | O   |     |
| 123  | NTP                                    |     | O   |
| 152  | BFTP                                   | O   | O   |
| 156  | SQL Service                            | O   | O   |
| 158  | DMSP                                   | O   | O   |
| 161  | SNMP                                   |     | O   |
| 162  | SNMPTRAP                               | O   | O   |
| 179  | BGP : Border Gateway Protocol          | O   |     |
| 194  | IRC : Internet Relay Chat              | O   | O   |
| 199  | SMUX, SNMP Unix Multiplexer            | O   | O   |
| 213  | IPX : Internetwork Packet Exchange     | O   | O   |
| 218  | MPP                                    | O   | O   |
| 220  | IMAP                                   | O   | O   |
| 311  | Mac OS X Server Admin                  | O   |     |
| 323  | IMMP                                   | O   | O   |
| 366  | ODMR : On-Demand Mail Relay            | O   | O   |
| 427  | SLP : Service Location Protocol        | O   | O   |
| 443  | HTTPS                                  | O   |     |
| 444  | SNPP : Simple Network Paging Protocol  | O   | O   |
| 500  | ISAKMP                                 |     | O   |
| 501  | STMF                                   | O   |     |
| 510  | Frist Class Protocol                   | O   |     |
| 513  | Who                                    |     | O   |
| 514  | Shell                                  | O   |     |
| 515  | Line Printer Daemon                    | O   |     |
| 518  | Talk                                   |     | O   |
| 520  | RIP : Routing Imformation Protocol     |     | O   |
| 525  | Timeserver                             |     | O   |
| 540  | UUCP                                   | O   |     |
| 561  | Monitor                                |     | O   |
| 587  | e-mail message submission              | O   |     |
| 631  | IPP : Internet Printing Protocol       | O   | O   |
| 651  | IEEE-MMS                               | O   | O   |
| 657  | IBM RMC Protocol                       | O   | O   |
| 660  | Mac OS X Server Administration         | O   |     |
| 675  | ACAP                                   | O   |     |
| 699  | Access Network                         | O   |     |
| 700  | EPP : Extensible Provisioning Protocol | O   |     |
| 701  | LMP : Link Management Protocol         | O   |     |
| 706  | SILC                                   | O   |     |
| 712  | Promise RAID Controller                |     | O   |
| 720  | SMQP : SImple Message Queue Protocol   | O   |     |
| 829  | CMP : Certificate Management Protocol  | O   |     |
| 901  | SWAT                                   | O   |     |
| 902  | VMware SErver Consol                   |     | O   |
| 903  | VMware Remote Console                  | O   |     |
| 911  | NCA : Network Console on Acid          | O   |     |
| 953  | DNS RNDC Service                       | O   | O   |
| 989  | FTPS Protocol (data)                   | O   | O   |
| 992  | TELNET Protocol over TLS/SSL           | O   | O   |
| 1023 | Reserved                               | O   | O   |

[↑ return to TOC](#table-of-contents)

#### HTTP & HTTPS

HTTP 의 포트는 80 HTTPS 의 포트는 443 이다.  

Goolge, Amazon 등과 같이 http/https 프로토콜을 이용하는 웹서버로 접속하기 위해서는 80번 이라는 문을 통해 통과하게 되는 것이다.  

아래의 예시를 보자.  
Port 번호를 바꾸면서 ```about.google``` 에 접속을 시도해 볼 것이다.  

1. about.google:```80```  
  이미 접속에 성공한 about.google에 80 포트를 붙여보기  
  성공적으로 작동.  
1. about.google:```123```  
  두번째로는 port 번호 123을 통한 접속 시도이다.  
  연결에 실패.
1. about.google:```443```  
  마지막으로는 HTTPS 포트번호인 443 을 통한 접속.  
  연결에 성공.

![Port Testing](https://user-images.githubusercontent.com/48475824/79060138-5762a580-7cbc-11ea-97f7-297de87eaaad.gif)  

웹서버에 접속 시도시 80, 443 이라는 두 문을 통해서만 접속 가능한 것을 볼 수 있다.  
이는 웹서버 자체가 두 문에서 클라이언트의 요청을 기다리고 있기 때문이다.  

좀 더 이해하기 쉽게 현실 세계를 비유한 예를 들어보겠다.

**합정역 5번 출구**  

미국과 독일에서 각각 한국으로 입국한 두 친구가 2주간 자가격리를 끝낸 후 서로 만나기로 약속했다.  
만남의 장소는 합정(Hapjeong)역.  

![meet-me-at-the](https://user-images.githubusercontent.com/48475824/79060477-68151a80-7cc0-11ea-99b7-0ff68b18f9f7.gif)

만약 그들이 ```"합정역에서 만나!"``` 라고 했다면 도착한 이후에 서로 재 연락하지 않는 이상 합정역에서 서로를 찾아 헤멜 것이다.  

단순히 어느 역에서 만나 라고 하는 대신 ```"합정역 5번출구에서 만나"``` 라고 한다면 서로를 찾는데 낭비하는 시간과 노력이 줄어들 것이다.  

<img width="300" alt="H" src="https://user-images.githubusercontent.com/48475824/79060634-6b110a80-7cc2-11ea-9fd8-d3c12f680e01.gif">  

이처럼 웹서버는 80번 포트(합정역 5번출구)를 통해 운영하기로 정해진 것이다.  
웹서버는 맞이할 클라이언트(맞이할 친구)의 요청을 80번 포트에서 기다리게 된다.  
80 포트(또는 443)가 아닌 다른 포트를 이용하여 접속 시도시 작동되지 않는 이유가 그 것이다.  
합정역 5번 출구가 아닌 엉뚱한 곳에서 친구를 만나려 했기 때문이다.

[↑ return to TOC](#table-of-contents)

### Registered Port

등록된 포트 | 범위는 (1024~49151)  
Super User의 권한이 없어도 사용 가능.

| Port  | About                                               | TCP | UDP |
|:-----:|-----------------------------------------------------|:---:|:---:|
| 1024  | Reserved                                            | O   | O   |
| 1080  | SOCKS Proxy                                         | O   |     |
| 1085  | WebObjects                                          | O   | O   |
| 1109  | KPOP : Kerberos Post Office Protocol                | O   |     |
| 1167  | Phone, conferemce calling                           |     | O   |
| 1194  | OpenVPN                                             | O   | O   |
| 1241  | Nessus Security Scanner                             | O   | O   |
| 1293  | IPSec                                               | O   | O   |
| 1311  | Dell OpenManage HTTPS                               | O   |     |
| 1137  | WASTE Encrypted File Sharing Program                | O   |     |
| 1431  | RGTP : Reserve Gossip Transport Protocol            | O   |     |
| 1433  | MSSQL Server                                        | O   |     |
| 1434  | MSSQL Monitor                                       | O   | O   |
| 1512  | WINS                                                | O   | O   |
| 1521  | Oracle database default listener                    | O   |     |
| 1524  | ingreslock, ingres                                  | O   | O   |
| 1526  | Oracle database common alternative for listener     | O   |     |
| 1547  | Laplink                                             | O   | O   |
| 1589  | Cisco VQP / VMPS                                    |     | O   |
| 1627  | iSketch                                             |     |     |
| 1701  | L2TP                                                |     | O   |
| 1716  | MMO                                                 | O   |     |
| 1755  | MMS : Microsoft Media Services                      | O   | O   |
| 1801  | Microsoft Message Queuing                           | O   | O   |
| 1812  | RADIUS authentication protocol                      | O   | O   |
| 1813  | RADIUS accounting protocol                          | O   | O   |
| 1920  | IBM Tivoli Monitoring Console                       | O   |     |
| 1972  | InterSystems Cache                                  | O   | O   |
| 1984  | Big Brother System and Network Monitor              | O   |     |
| 1985  | Cisco HSRP                                          |     | O   |
| 1997  | Chizmo Networks Transfer Tool                       | O   |     |
| 2002  | Secure Access Control Server for Windows            | O   |     |
| 2031  | mobrien-chat                                        | O   | O   |
| 2049  | Network File System                                 |     | O   |
| 2082  | Infowave Mobility Server                            | O   |     |
| 2086  | GNUnet                                              | O   |     |
| 2105  | IBM MiniPay                                         | O   | O   |
| 2144  | Iron Moutain LiveValut Agent                        | O   |     |
| 2211  | EMWIN                                               |     | O   |
| 2220  | NetIQ End2End                                       | O   | O   |
| 2261  | CoMotion Master                                     | O   | O   |
| 2303  | ArmA multiplayer                                    |     | O   |
| 2518  | willy                                               | O   | O   |
| 2525  | SMTP alternate                                      | O   |     |
| 2610  | Dark Ages                                           | O   |     |
| 2809  | IBM WAS                                             | O   |     |
| 2947  | gpsd GPS daemon                                     | O   |     |
| 2948  | WAP-push MMS                                        | O   | O   |
| 2967  | Symantec AntiVirus Corporate Edition                | O   |     |
| 3000  | Miralix License serve                               | O   |     |
| 3025  | netpd.org                                           | O   |     |
| 3051  | Galaxy Server                                       | O   | O   |
| 3101  | BlackBerry Enterprise Server communication to cloud | O   |     |
| 3235  | Galaxy Network Service                              | O   | O   |
| 3300  | Debate Gopher backend database system               | O   | O   |
| 3305  | OFTP                                                | O   | O   |
| 3306  | MySQL database System                               | O   | O   |
| 3313  | Verisys                                             | O   |     |
| 3423  | Xware Xtrm Communication Protocol                   | O   |     |
| 3516  | Smartcard Port                                      | O   | O   |
| 3527  | Microsoft Message Queuing                           |     | O   |
| 3535  | SMTP alternate                                      | O   |     |
| 3702  | Web Services Dynamic Discovery                      | O   | O   |
| 3723  | Blizzard Games(DIablo, Warcraft, StarCraft)         | O   | O   |
| 3724  | Club Penguin Disney online game for kids            | O   |     |
| 3880  | IGRS                                                | O   | O   |
| 3945  | EMCADS service                                      | O   | O   |
| 3979  | OpenTTD game                                        | O   | O   |
| 4111  | Xgrid                                               | O   |     |
| 4116  | Smartcard-TLS                                       | O   | O   |
| 4224  | Cisco Audio Session Tunneling                       | O   |     |
| 4664  | Google Desktop Search                               | O   |     |
| 4711  | MacAfee Web Gateway 7 - GUI Port HTTP               | O   |     |
| 4712  | MacAfee Web Gateway 7 - GUI Port HTTPS              | O   |     |
| 4750  | BladeLogic Agent                                    | O   |     |
| 5000  | VTun                                                |     | O   |
| 5003  | FileMaker                                           | O   | O   |
| 5050  | Yahoo! Messenger                                    | O   |     |
| 5060  | SIP : Session Initiation Protocol                   | O   | O   |
| 5070  | BFCP                                                | O   |     |
| 5093  | SafeNet, Client-to-Server                           |     | O   |
| 5099  | SafeNet, Server-to-Server                           | O   | O   |
| 5108  | VPOP3 Mail Server Webmail                           | O   |     |
| 5110  | ProRat Server                                       | O   |     |
| 5269  | XMPP                                                | O   |     |
| 5353  | Multicast DNS                                       |     | O   |
| 5432  | PostgreSQL database System                          | O   | O   |
| 5723  | Operations Manager                                  | O   |     |
| 5938  | TeamViewer remote desktop protocol                  | O   | O   |
| 6050  | Brighstor Arscerve Backup                           | O   |     |
| 6260  | planet M.U.L.E                                      | O   | O   |
| 6566  | SANE : Scanner Access Now Easy                      | O   |     |
| 6600  | MPD : Music Playing Daemon                          | O   |     |
| 6679  | OSAUT                                               | O   | O   |
| 6888  | MUSE                                                | O   | O   |
| 8080  | Apache Tomcat                                       | O   |     |
| 8089  | Splunk Daemon                                       | O   |     |
| 8200  | GoToMyPC                                            | O   |     |
| 8332  | Bitcoin JSON-RPC server                             | O   |     |
| 8333  | Bitcoin                                             | O   |     |
| 8484  | MapleStory                                          | O   | O   |
| 8887  | HyperVM HTTP                                        | O   |     |
| 8888  | HyperVM HTTPS                                       | O   |     |
| 9030  | Tor often used                                      | O   |     |
| 9050  | Tor                                                 | O   |     |
| 9110  | SSMP Message Protocol                               |     | O   |
| 9293  | Sony PlayStation RemotePlay                         | O   |     |
| 9418  | git, Git pack transfer service                      | O   | O   |
| 9561  | Network Time System Server                          | O   | O   |
| 10017 | AIX, NeXT, HPUX-rexd daemon control                 |     |     |
| 11211 | memcached                                           |     |     |
| 16080 | Mac OS X Server Web Service with performance cache  | O   |     |
| 19294 | Google Talk Voice and Video connections             | O   |     |
| 19295 | Google Talk Voice and Video connections             |     | O   |
| 19812 | 4D databse SQL Communication                        | O   |     |
| 30000 | Pokemon Netbattle                                   |     |     |
| 37777 | Digital Video Recorder hardware                     | O   |     |
| 49151 | Reserved                                            | O   | O   |

[↑ return to TOC](#table-of-contents)

### Dynamic Port

동적 포트 | 범위는 (49152~655535)  
개인적인 용도로 사용한다.

[↑ return to TOC](#table-of-contents)


## Check Port Info
사용중인 포트 정보 보기.  
```sudo lsof -i -P -n | grep LISTEN```

<img width=800 alt="port info" src="https://user-images.githubusercontent.com/48475824/84724260-b0073500-afc2-11ea-935d-83bcb6c6e3b2.png">

[↑ return to TOC](#table-of-contents)
