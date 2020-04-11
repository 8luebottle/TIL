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
| 22   | SSH                                    | O   | O   |
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