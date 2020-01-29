# Docker Commands
도커의 명령어 모음


**Basic Commands Sytax**
```bash
docker <option> <command> <ARG...>
```
* option | 옵션
* command | 명령
* ARG... | 매개변수

> 링크를 클릭하여 이동  
| [attach](#attach) | [build](#build) | [commit](#commit) | [cp](#cp) | [create](#create) | [diff](#diff) |  [events](#events) | [exec](#exec) | [export](#export) | [history](#history) | [images](#images) | [import](#import) | [info](#info) | [inpect](#inspect) | [kill](#kill) | [load](#load) | [login](#login) | [logout](#logout) | [logs](#logs) | [pause](#pause) | [port](#port) | [ps](#ps) | [pull](#pull) | [push](#push) | [rename](#rename) | [restart](#restart) | [rm](#rm) | [rmi](#rmi) | [run](#run) | [save](#save) | [search](#search) | [start](#start) | [stats](#stats) | [stop](#stop) | [tag](#tag) | [top](#top) | [unpause](#unpause) | [update](#update) | [version](#version) | [wait](#wait) |


## [attach](https://docs.docker.com/engine/reference/commandline/attach/)
>Attach local standard input, output, and error streams to a running container.  
실행되고 있는 컨테이너에 입력(<code>stdin</code>)과 출력(<code>stdout</code>)을 연결하는 명령어.  

  * **Syntax**
  ```bash
  docker attach <option> <containerName, ID>
  ```

## [build](https://docs.docker.com/engine/reference/commandline/build/)
> Build an image from a Dockerfile  
Dockerfile로 image를 생성하는 명령어.

 * **syntax**
  ```bash
  docker build <option> <dockerfile Path>
  ```

* Local path 와 URL 사용 가능
* Dockerfile 이 있는 경로에서 build 명령을 실행

## [commit](https://docs.docker.com/engine/reference/commandline/commit/)
> Create a new image from a container's changes.  
컨테이너의 변경 사항을 이미지로 생성하는 명령어.

  * **Syntax**
  ```bash
  docker commit <option> <containerName, ID> <repositoryName>/<imageName>:<tag>
  ```


## [cp](https://docs.docker.com/engine/reference/commandline/cp/)
> Copy files/folders between a container and the local filesystem.  
컨테이너의 Directory/files을 host로 복사하는 명령어.

  * **Syntax**
  ```bash
  docekr cp <containerName>:<path> <hostPath>
  ```

## [create](https://docs.docker.com/engine/reference/commandline/create/)
> Create a new container.  
Image로 컨테이너를 생성하는 명령어.

  * **Syntax** 
  ```bash
  docker create <option> <imageName, ID> <command> <ARG...>
  ```

## [diff](https://docs.docker.com/engine/reference/commandline/diff/)
> Inspect changes to files or directories on a container's filesystem.  
컨테이너에서 변경된 file을 확인하는 명령어.  

  * **Syntax**  
  ```bash
  docker diff <containerName, ID>
  ```

  * 변경된 파일 비교 기준 --> 컨테이너를 생성한 이미지의 내용

## [events](https://docs.docker.com/engine/reference/commandline/events/)
> Get real time events from the server.  
Docker 서버에 일어난 event를 실시간으로 출력하는 명령어.

  * **Syntax**  
  ```bash
  docker events
  ```

  * 해당 명령어를 실행하게 되면 docker는 대기 상태가 된다.

## [exec](https://docs.docker.com/engine/reference/commandline/exec/)
> Run a command in a running container.  
외부에서 컨테이너 안의 명령을 실행하는 명령어.  

  * **Syntax**  
  ```bash
  docker export <option> <containerName, ID> <command> <ARG...>
  ```  

## [export](https://docs.docker.com/engine/reference/commandline/export/)
> Export a container's filesystem as a tar archive.  
컨태이너의 filesystem을 tar 파일로 저장하는 명령어.  

  * **Syntax**  
  ```bash
  docker export <containerName, ID>
  ```

  * 컨테이너의 내용이 표준 출력으로 출력된다.

## [history](https://docs.docker.com/engine/reference/commandline/history/)
> Show the history of an image.  
Image의 history를 출력하는 명령어.

  * **Syntax**
  ```bash
  docker history <option> <imageName, ID>
  ```

## [images](https://docs.docker.com/engine/reference/commandline/images/)
> List images.  
Image의 목록을 출력하는 명령어.

  * **Syntax**
  ```bash
  docker images <option> <imageName>
  ```

## [import](https://docs.docker.com/engine/reference/commandline/import/)
> Import the contents from a tarball to create a filesystem image.  
tar file로 압축된 filesystem으로부터 image를 생성하는 명령어.

  * **Syntax**  
  ```bash
  docker import <tar file's URL or-> <repositoryName>/<imageName>:<tag>
  ```

## [info](https://docs.docker.com/engine/reference/commandline/info/)
Display system-wide information

## [inspect](https://docs.docker.com/engine/reference/commandline/inspect/)
Return low-level information on Docker objects

## [kill](https://docs.docker.com/engine/reference/commandline/kill/)
Kill one or more running containers

## [load](https://docs.docker.com/engine/reference/commandline/load/)
Load an image from a tar archive or STDIN

## [login](https://docs.docker.com/engine/reference/commandline/login/)
Log in to a Docker registry

## [logout](https://docs.docker.com/engine/reference/commandline/logout/)
Log out from a Docker registry

## [logs](https://docs.docker.com/engine/reference/commandline/logs/)
Fetch the logs of a container

## [pause](https://docs.docker.com/engine/reference/commandline/pause/)
Pause all processes within one or more containers

## [port](https://docs.docker.com/engine/reference/commandline/port/)
List port mappings or a specific mapping for the container

## [ps](https://docs.docker.com/engine/reference/commandline/ps/)
List containers

## [pull](https://docs.docker.com/engine/reference/commandline/pull/)
Pull an image or a repository from a registry

## [push](https://docs.docker.com/engine/reference/commandline/push/)
Push an image or a repository to a registry

## [rename](https://docs.docker.com/engine/reference/commandline/rename/)
Rename a container

## [restart](https://docs.docker.com/engine/reference/commandline/restart/)
Restart one or more containers

## [rm](https://docs.docker.com/engine/reference/commandline/rm/)
Remove one or more containers

## [rmi](https://docs.docker.com/engine/reference/commandline/rmi/)
Remove one or more images

## [run](https://docs.docker.com/engine/reference/commandline/run/)
Run a command in a new container

## [save](https://docs.docker.com/engine/reference/commandline/save/)
Save one or more images to a tar archive (streamed to STDOUT by default)

## [search](https://docs.docker.com/engine/reference/commandline/search/)
Search the Docker Hub for images

 ## [start](https://docs.docker.com/engine/reference/commandline/start/)
Start one or more stopped containers

## [stats](https://docs.docker.com/engine/reference/commandline/stats/)
Display a live stream of container(s) resource usage statistics

## [stop](https://docs.docker.com/engine/reference/commandline/stop/)
Stop one or more running containers

## [tag](https://docs.docker.com/engine/reference/commandline/tag/)
Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE

## [top](https://docs.docker.com/engine/reference/commandline/top/)
Display the running processes of a container

## [unpause](https://docs.docker.com/engine/reference/commandline/unpause/)
Unpause all processes within one or more containers

## [update](https://docs.docker.com/engine/reference/commandline/update/)
Update configuration of one or more containers

## [version](https://docs.docker.com/engine/reference/commandline/version/)
Show the Docker version information

## [wait](https://docs.docker.com/engine/reference/commandline/wait/)
Block until one or more containers stop, then print their exit codes
