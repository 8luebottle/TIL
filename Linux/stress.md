# stress

Linux 에서 `stress` 도구를 통해 CPU, memory, I/O, disk 의 부하 테스트를 해 볼 수 있다.
- 또는 `stress` 의 updated 버전인 `stress-ng` 사용.
  - [source code](https://github.com/ColinIanKing/stress-ng) from GitHub

### Table of Contents
- [Installation](#installation)
- [stress Options](#stress-options)
  - [c](#-c) : cpu
  - [d](#-d) : disk
  - [i](#-i) : input/output
  - [m](#-m) : memory
  - [t](#-t) : timeout

## Installation
`stress` tool 설치

- Use `yum`:
    ```shell
    sudo yum install -y stress
    ```

- Use `apt-get`:
    ```shell
    sudo apt-get install stress
    ```

- On AWS EC2:  
    AWS EC2 에 설치하여 사용하고자 하는 경우
    ```shell
    sudo yum install -y amazon-linux-extras
    sudo amazon-linux-extras install epel
    sudo yum install -y stress
    ```
    - More info: 
      - [amazon-linux-extras](https://aws.amazon.com/ko/premiumsupport/knowledge-center/ec2-install-extras-library-software/)
      - [epel](https://docs.fedoraproject.org/en-US/epel/)

[↑ return to TOC](#table-of-contents)

## stress Options
> usage: `stress [OPTION [ARG]]`

**[suffix]**  
suffix 를 붙여줌으로써 상세 테스트 설정을 해 줄 수 있다.
- time 
  - s (second)
  - m (minute)
  - h (hour)
  - d (day)
  - y (year)

- size
  - B (Byte)
  - K (Kilobyte)
  - M (Megabyte)
  - G (Gigabyte)

stress 명령어와 함께 쓸수 있는 옵션값은 아래와 같다.

### -c
**c**pu  
> CPU 부하 테스트

- `stress -c <number of CPU core>`
  - e.g.) `stress -c 2 --timeout 300s`
- ```stress --cpu <number of CPU core>```
  - e.g.) `stress --cpu 1 --timeout 1m`

[↑ return to TOC](#table-of-contents)

### -d
**d**isk  
> Disk 부하 테스트

default: 1GB

- `stress -d <number of Hard Disk Drive> -hdd-bytes <size>`
  - e.g.) `stress -d 1 --hdd-bytes 2048M --timeout 2m`
- `stress --hdd <number of Hard Disk Drive> --hdd-bytes <size>`
  - e.g.) `stress --hdd 3 --hdd-bytes 77M`

[↑ return to TOC](#table-of-contents)

### -i
**i**nput output
> I/O 부하 테스트

- `stress -i`
  - e.g.) `stress -i 100`
- `stress --io`
  - e.g.) `stress --io 1 -t 30s`

[↑ return to TOC](#table-of-contents)

### -m
**m**emory  
> Memory 부하 테스트 

default: 256MB

- `stress -m <number of Process> --vm-bytes <size>`
  - e.g.) `stress -m 2 --vm-bytes 1024M` 
- `stress --vm <number of Process> --vm-bytes <size>`
  - e.g.) `stress --vm 1 --vm-bytes 128M --timeout 60s`

[↑ return to TOC](#table-of-contents)

### -t
**t**imeout
> 테스트의 Timeout 설정

- `stress -t`
  - e.g.) `stress -t 10s --cpu 8 --io 1`
- `stress --timeout`
  - e.g.) `stress --timeout 5m --vm 2 --vm-bytes 128M`

[↑ return to TOC](#table-of-contents)