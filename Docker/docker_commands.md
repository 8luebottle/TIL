# Docker Commands
도커의 명령어 모음


**Basic Commands Sytax**
```bash
docker <option> <command> <ARG...>
```
* option | 옵션
* command | 명령
* ARG... | 매개변수

### Table of Contents
> 링크를 클릭하여 이동  
| [attach](#attach) | [build](#build) | [commit](#commit) | [cp](#cp) | [create](#create) | [diff](#diff) |  [events](#events) | [exec](#exec) | [export](#export) | [history](#history) | [images](#images) | [import](#import) | [info](#info) | [inpect](#inspect) | [kill](#kill) | [load](#load) | [login](#login) | [logout](#logout) | [logs](#logs) | [pause](#pause) | [port](#port) | [ps](#ps) | [pull](#pull) | [push](#push) | [rename](#rename) | [restart](#restart) | [rm](#rm) | [rmi](#rmi) | [run](#run) | [save](#save) | [search](#search) | [start](#start) | [stats](#stats) | [stop](#stop) | [tag](#tag) | [top](#top) | [unpause](#unpause) | [update](#update) | [version](#version) | [wait](#wait) |

# A
## attach
>Attach local standard input, output, and error streams to a running container.  
실행되고 있는 컨테이너에 입력(<code>stdin</code>)과 출력(<code>stdout</code>)을 연결하는 명령어.  

* **Syntax**
  ```bash
  docker attach <option> <containerName, ID>
  ```

[↑ return to TOC](#table-of-contents)


# B
## build
> Build an image from a Dockerfile  
Dockerfile로 image를 생성하는 명령어.

* **syntax**
  ```bash
  docker build <option> <dockerfile Path>
  ```

* Local path 와 URL 사용 가능
* Dockerfile 이 있는 경로에서 build 명령을 실행

[↑ return to TOC](#table-of-contents)


# C
## commit
> Create a new image from a container's changes.  
컨테이너의 변경 사항을 이미지로 생성하는 명령어.

* **Syntax**
  ```bash
  docker commit <option> <containerName, ID> <repositoryName>/<imageName>:<tag>
  ```

[↑ return to TOC](#table-of-contents)
## cp
> Copy files/folders between a container and the local filesystem.  
컨테이너의 Directory/files을 host로 복사하는 명령어.

* **Syntax**
  ```bash
  docekr cp <containerName>:<path> <hostPath>
  ```

[↑ return to TOC](#table-of-contents)

## create
> Create a new container.  
Image로 컨테이너를 생성하는 명령어.

* **Syntax** 
  ```bash
  docker create <option> <imageName, ID> <command> <ARG...>
  ```

[↑ return to TOC](#table-of-contents)


# D
## diff
> Inspect changes to files or directories on a container's filesystem.  
컨테이너에서 변경된 file을 확인하는 명령어.  

* **Syntax**  
  ```bash
  docker diff <containerName, ID>
  ```

  * 변경된 파일 비교 기준 --> 컨테이너를 생성한 이미지의 내용

[↑ return to TOC](#table-of-contents)


# E
## events
> Get real time events from the server.  
Docker 서버에 일어난 event를 실시간으로 출력하는 명령어.

* **Syntax**  
  ```bash
  docker events
  ```

  * 해당 명령어를 실행하게 되면 docker는 대기 상태가 된다.

[↑ return to TOC](#table-of-contents)

## exec
> Run a command in a running container.  
외부에서 컨테이너 안의 명령을 실행하는 명령어.  

* **Syntax**  
  ```bash
  docker export <option> <containerName, ID> <command> <ARG...>
  ```  

[↑ return to TOC](#table-of-contents)

## export
> Export a container's filesystem as a tar archive.  
컨태이너의 filesystem을 tar 파일로 저장하는 명령어.  

* **Syntax**  
  ```bash
  docker export <containerName, ID>
  ```

  * 컨테이너의 내용이 표준 출력으로 출력된다.

[↑ return to TOC](#table-of-contents)


# H
## history
> Show the history of an image.  
Image의 history를 출력하는 명령어.

* **Syntax**
  ```bash
  docker history <option> <imageName, ID>
  ```

  - `CREATED BY`: 각각의 Image Layer 가 어떤 명령어를 통해 생성됬는지 표시.
  - `SIZE`: Image 디스크 크기.

    ```
    IMAGE          CREATED         CREATED BY                                      SIZE      COMMENT
    a617c1c92774   18 months ago   /bin/sh -c #(nop)  CMD ["redis-server"]         0B
    <missing>      18 months ago   /bin/sh -c #(nop)  EXPOSE 6379                  0B
    <missing>      18 months ago   /bin/sh -c #(nop)  ENTRYPOINT ["docker-entry…   0B
    <missing>      18 months ago   /bin/sh -c #(nop) COPY file:df205a0ef6e6df89…   374B
    <missing>      18 months ago   /bin/sh -c #(nop) WORKDIR /data                 0B
    <missing>      18 months ago   /bin/sh -c #(nop)  VOLUME [/data]               0B
    <missing>      18 months ago   /bin/sh -c mkdir /data && chown redis:redis …   0B
    <missing>      18 months ago   /bin/sh -c set -eux;   savedAptMark="$(apt-m…   31.6MB
    <missing>      18 months ago   /bin/sh -c #(nop)  ENV REDIS_DOWNLOAD_SHA=cd…   0B
    <missing>      18 months ago   /bin/sh -c #(nop)  ENV REDIS_DOWNLOAD_URL=ht…   0B
    <missing>      18 months ago   /bin/sh -c #(nop)  ENV REDIS_VERSION=6.2.1      0B
    <missing>      18 months ago   /bin/sh -c set -eux;  savedAptMark="$(apt-ma…   4.15MB
    <missing>      18 months ago   /bin/sh -c #(nop)  ENV GOSU_VERSION=1.12        0B
    <missing>      18 months ago   /bin/sh -c groupadd -r -g 999 redis && usera…   329kB
    <missing>      18 months ago   /bin/sh -c #(nop)  CMD ["bash"]                 0B
    <missing>      18 months ago   /bin/sh -c #(nop) ADD file:3c32f1cd03198e141…   69.2MB
    ```

[↑ return to TOC](#table-of-contents)


# I
## images
> List images.  
Image의 목록을 출력하는 명령어.

* **Syntax**
  ```bash
  docker images <option> <imageName>
  ```

[↑ return to TOC](#table-of-contents)

## import
> Import the contents from a tarball to create a filesystem image.  
tar file로 압축된 filesystem으로부터 image를 생성하는 명령어.

* **Syntax**  
  ```bash
  docker import <tar file's URL or-> <repositoryName>/<imageName>:<tag>
  ```

[↑ return to TOC](#table-of-contents)

## info
> Display system-wide information.  
시스템, Docker Container, Image rotn, setting 등의 info를 출력하는 명령어.

* **Syntax**
  ```bash
  docker info
  ```

[↑ return to TOC](#table-of-contents)

## inspect
> Return low-level information on Docker objects.  
container, image의 세부 정보를 JSON 형태로 출력하는 명령어.  

* **Syntax**
  ```bash
  docker inspect <option> <containerName of imageName, ID>
  ```

### Inspect Volume
  - **Syntax**  
  ```docker volume inspect <volumeName>```  
    ```
    [
      {
          "CreatedAt": "2020-05-05T19:48:06Z",
          "Driver": "local",
          "Labels": null,
          "Mountpoint": "/var/lib/docker/volumes/f3c60a00000a6b207a0000aaa000f00000000af0fed1e4c5a184d9aaaa0cb5e0/_data",
          "Name": "f3c60a00000a6b207a0000aaa000f00000000af0fed1e4c5a184d9aaaa0cb5e0",
          "Options": null,
          "Scope": "local"
      }
    ]
    ```

[↑ return to TOC](#table-of-contents)


# K 
## kill
> Kill one or more running containers.  
컨테이너를 중지하는 명령어.  

* **Syntax**
  ```bash
  docker kill <option> <containerName, ID>
  ```

[↑ return to TOC](#table-of-contents)


# L
## load
> Load an image from a tar archive or STDIN.  
tar file로 image를 생성하는 명령어.  

* **Syntax**
  ```bash
  docker load <option>
  ```

  * tar file은 image 이름과 태그가 포함되어 있다.

[↑ return to TOC](#table-of-contents)

## login
> Log in to a Docker registry.  
Docker 레지스트리에 로그인 하는 명령어.  

* **Syntax**
  ```bash
  docker login <option> <dockerRegistryURL>
  ```

  ```shell
  $ docker login https://index.docker.io/v1 
  ```

* **Options**
  - `-u`, `--username`  
    사용자명
  - `-p`, `--password`  
    비밀번호
  - `--password-stdin`
    파일을 통한 비밀번호 input.
    Shell 히스토리에 password 입력한 기록을 남기지 않기 위해 파일에 미리 입력되 있는 비밀번호를 사용할 수 있다.

    ```shell
    $ cat ~/docker_pw.txt | docker login --username 8luebottle --password-stdin
    ```

[↑ return to TOC](#table-of-contents)

## logout
> Log out from a Docker registry.  
Docker 레지스트리에서 로그아웃 하는 명령어.  

* **Syntax**
  ```bash
  docker logout <dockerRegistryServerURL>
  ```

[↑ return to TOC](#table-of-contents)

## logs
> Fetch the logs of a container.  
컨테이너의 log를 출력하는 명령어.  

* **Syntax**
  ```bash
  docker logs <containerName, ID>
  ```

[↑ return to TOC](#table-of-contents)


# P
## pause
> Pause all processes within one or more containers.  
컨테이너에서 실행되고 있는 모든 processes를 일시 정지하는 명령어.  

* **Syntax**
  ```bash
  docker pause <containerName, ID>
  ```

[↑ return to TOC](#table-of-contents)

## port
> List port mappings or a specific mapping for the container.  
컨테이너에서 port가 열려 있는지 확인하는 명령어.  

* **Syntax**
  ```bash
  docker port <containerName, ID> <port>
  ```

[↑ return to TOC](#table-of-contents)
## ps
**PS** : **P**rocess **S**tatus
> List containers.  
현재 실행중인 컨테이너의 목록을 출력하는 명령어.  

* **Syntax**
  ```bash
  docker ps <option>
  ```

* **Options**
  - `-a`, `--all`  
    모든 컨테이너를 출력  
    default 값은 false로 되어있다. 그로인해 모든 컨테이너가 출력되는 것이 아닌 시작된 컨테이너만 출력된다. 모든 컨테이너를 보고자 할 때 해당 option 을 사용하자.  
  - `-l`, `--latest`  
    제일 최신에 생성된 컨테이너 출력  
    실행중이지 않은 컨테이너도 해당된다.  
  - `-q`, `--quite`  
    실행중인 컨테이너 ID 만 출력  
  - `--no-trunc`  
    컨테이너 목록 출력시 truncate 를 적용시키지 않음. 
  - `s`, `--size`  
    총 파일 사이즈 출력  
    - size: 쓰기 가능 사이즈 only
    - virtual size: 읽기 전용(read-only) 사이즈와 쓰기 가능(writable) 사이즈의 총 합

    ```shell
    $ docker ps -s

    CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS       PORTS                      NAMES               SIZE
    123a45bcd68   alpine    "/bin/sh"                n days ago      Up n days                               cheetah              3.95MB (virtual 9.49MB)
    ```

[↑ return to TOC](#table-of-contents)

## pull
> Pull an image or a repository from a registry.  
Docker 레지스트리에서 image를 pull받는 명령어.  

* **Syntax**
  ```bash
  docker pull <option> <repositoryName>/<imageName>:<tag>
  ```

  * \<repositoryName>
    * Docker Hub User Name
    * Repository Address
  * tag를 지정해주지 않으면 tag가 붙은 image가 모두 pull 되버린다.

[↑ return to TOC](#table-of-contents)

## push
> Push an image or a repository to a registry.  
Docker 레지스트리에 image를 올리는 명령어.  

* **Syntax**
  ```bash
  docker push <repositoryName>/<imageName>:<tag>
  ```

  * \<repositoryName>
    * Docker Hub User Name
    * Repository Address
  * tag를 지정해주지 않으면 tag가 붙은 image가 모두 push 되버린다.

[↑ return to TOC](#table-of-contents)


# R
## rename
> Rename a container.
컨테이너의 명칭을 변경하는 명령어.

* **Syntax** 
  ```shell
  docker rename <oldName> <newName>
  ``` 

[↑ return to TOC](#table-of-contents)

## restart
> Restart one or more containers.
컨테이너를 재시작 시키는 명령어.

* **Syntax**  
  ```shell
  docker restart <option> <container>
  ```

* **Option**  
  - `-t`, `--time`  
    n초 이후 재시작 시킴.  
    - default: 10s

    ```shell
      docker restart -t 5 blueberry-tree
      ```

[↑ return to TOC](#table-of-contents)

## rm
> Remove one or more containers.  
가동중이지 않은 컨테이너를 삭제하는 명령어.

* **Syntax**  
  ```shell
  docker rm <option> <container>
  ```

* **Options**  
  - `-f`, `--force`  
    실행중인 컨테이너를 강제로 삭제 시킴.
    - 실행중인 컨테이너는 해당 옵션(`-f`) 없이 삭제 시킬 수 없다. 오류 발생.
      ```shell
      $ docker rm sushi-lover

      Error response from daemon: You cannot remove a running container 123a45bcd6789e0fghi12jk3456l7m8nopq901234567c59ec9b483a4adb7bc41. Stop the container before attempting removal or force remove
      ```

  - `-v`, `--volumes`  
    컨테이너에 할당되어 있는 볼륨을 삭제 시킴.


[↑ return to TOC](#table-of-contents)

## rmi
Remove one or more images

## run
> Run a command in a new container.  
컨테이너를 생성(`create`)하고 시작(`start`)시키는 명령어.

* **Syntax**  
  ```shell
  docker run <options> <image>
  ```

* **Options**  
  - `-d`, `--detach`  
    컨테이너를 백그라운드에서 실행 시킴.
    - 명령어 실행 후 Container ID 가 출력된다.
  - `-e`, `--env`  
    환경 변수를 설정함.
  - `-i`, `--interactive`
    표준 입력(STDIN)을 지속적으로 열어두도록 함.
  - `-m`, `--memory`
    메모리를 제한 시킴.
    - unit: b, k, m, g
  - `--rm`
    컨테이너가 종료 될 시 자동 삭제됨.
    - Test 용도로 잠시 만들어서 사용하는 컨테이너에 사용하기 적합한 옵션.
  - `-t`, `--tty`  
    **T**ele**ty**pewriter: pseudo-TTY 를 할당 시킴. 
    - 실행중인 컨테이너에 Input 을 단말 디바이스(termianl device)로 진행할 것임을 명시.



[↑ return to TOC](#table-of-contents)


# S
## save
Save one or more images to a tar archive (streamed to STDOUT by default)

## search
> Search the Docker Hub for images.
Docker Hub 의 Public 이미지를 검색하는 명령어.

* **Syntax**
  ```bash
  docker search <option> <searchKeyword>
  ```

  - STARS: 즐겨찾기로 등록된 수
  - OFFICIAL: 공식 이미지
  - AUTOMATED: Dockerfile을 통해 자동 생성된 이미지
    ```shell
    $ docker search rabbitmq

    NAME                                                   DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
    rabbitmq                                               RabbitMQ is an open source multi-protocol me…   4470      [OK]
    bitnami/rabbitmq                                       Bitnami Docker Image for RabbitMQ               89                   [OK]
    nasqueron/rabbitmqadmin                                RabbitMQ management plugin CLI tool Lightwei…   1                    [OK]
    bitnami/rabbitmq-exporter                                                                              1
    circleci/rabbitmq-delayed                              https://github.com/circleci/rabbitmq-delayed…   1
    rabbitmqoperator/cluster-operator                      The RabbitMQ Cluster Operator Docker Image      1
    nasqueron/rabbitmq                                     RabbitMQ wth management, MQTT and STOMP plug…   0                    [OK]
    itisfoundation/rabbitmq                                                                                0
    rapidfort/rabbitmq                                     RapidFort optimized, hardened image for Rabb…   0
    clearlinux/rabbitmq                                    RabbitMQ multi-protocol messaging broker wit…   0
    corpusops/rabbitmq                                     https://github.com/corpusops/docker-images/     0
    drud/rabbitmq                                          rabbitmq                                        0                    [OK]
    bitnami/rabbitmq-cluster-operator                                                                      0
    ibmcom/rabbitmq-exporter-ppc64le                                                                       0
    newrelic/k8s-nri-rabbitmq                              New Relic Infrastructure RabbitMQ Integratio…   0
    ibmcom/rabbitmq-server-ppc64le                                                                         0
    ibmcom/rabbitmq-java-client-ppc64le                                                                    0
    ibmcom/rabbitmq-java-client                                                                            0
    circleci/rabbitmq                                      This image is for internal use                  0
    ```

* **Options**  
  - `--limit`  
     n 개의 리스트만 출력.  

     ```shell
     $ docker search nginx --limit 2

     NAME            DESCRIPTION                  STARS     OFFICIAL   AUTOMATED
     nginx           Official build of Nginx.     17401     [OK]
     bitnami/nginx   Bitnami nginx Docker Image   140                  [OK]
     ```

  - `--filter=stars=n`  
    n 개 이상 starring 된 이미지 검색.

    ```shell
    $ docker search postgres --filter=stars=150

    NAME                 DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
    postgres             The PostgreSQL object-relational database sy…   11447     [OK]
    bitnami/postgresql   Bitnami PostgreSQL Docker Image                 154                  [OK]
    ```

[↑ return to TOC](#table-of-contents)

## start
> Start one or more stopped containers.
정지상태에 있는 컨테이너를 가동시키는 명령어.

* **Syntax**  
  ```shell
  docker start <options> <container>
  ```

  ```shell
  $ docker start ada_lovelace
  ```

[↑ return to TOC](#table-of-contents)

## stats
> Display a live stream of container(s) resource usage statistics.
컨테이너의 상태를 확인하는 명령어.

* **Syntax**  
  ```shell
  docker stats <options> <container>
  ```

  - CPU %: CPU 사용률
  - MEM %: Memrory 사용률
  - PIDS: 컨테이너에 이해 생성된 프로세스와 커널의 스레드 개수
    ```shell
    $ docker stats ada_lovelace

    CONTAINER ID   NAME           CPU %     MEM USAGE / LIMIT   MEM %     NET I/O           BLOCK I/O         PIDS
    12a345b67890   ada_lovelace   0.01%     231MiB / 3.844GiB   5.87%     1.95kB / 1.57kB   12.3MB / 20.5kB   109
    ```

* **Options**  
  - `-a`, `--all`  
    모든 컨테이너 출력. (중지상태에 있는 컨테이너도 포함)
  - `--no-stream`  
    Live stream 을 적용하지 않고 첫 번째 상태 결과만 출력.

[↑ return to TOC](#table-of-contents)

## stop
> Stop one or more running containers.  
실행중인 컨테이너를 정지시키는 명령어.

* **Syntax**  
  ```shell
  docker stop <options> <container>
  ```

  ```shell
  $ docker stop big_brother
  ```

* **Option**  
  - `-t`, `--time`  
    컨테이너를 n 초 이후에 정지시킴.
    - default: 10s

    ```shell
    $ docker stop -t 3 big_brother
    ```


[↑ return to TOC](#table-of-contents)


# T
## tag
Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE

## top
Display the running processes of a container

[↑ return to TOC](#table-of-contents)


# U
## unpause
Unpause all processes within one or more containers

## update
Update configuration of one or more containers

[↑ return to TOC](#table-of-contents)


# V
## version
> Show the Docker version information.  
도커의 버전 정보를 출력하는 명령어.  

### Check docker-compose Version
- **Syntax**  
  ```docker-compose --version```  

  result : ```docker-compose version 1.25.4, build 8d51620b```

### Update docker-compose Version
pip 를 사용하여 최신 버전으로 업데이트 하는 법은 아래와 같다.
- **Syntax**  
  ```sudo pip install --upgrade docker-compose```

[↑ return to TOC](#table-of-contents)


# W
## wait
Block until one or more containers stop, then print their exit codes

[↑ return to TOC](#table-of-contents)
