# Stash 
`stash` 는 로컬에서 수정한 내역을 임시로 저장할 수 있게 해주는 명령어다.  

### Table of Contents
* [About](#about)
  * [LIFO](#lifo)
  * [Apply & Pop](#apply-&-pop)
  * [When to use git stash](#when-to-use-git-stash)

* [Commands](#commands)  
  * [Stash](#stash)
  * [Apply](#apply)
  * [Clear](#clear)
  * [Drop](#drop)
  * [List](#list)
  * [Pop](#pop)
  * [Show](#show)

## About
보통 로컬 리포지토리에서 변경을 가한 내역을 바로 `commit` 하고 싶지 않은 경우 사용한다.  
`stash` 라는 명칭이 지닌 "넣어두다, 치워두다"의 의미 처럼 해당 명령어를 사용한다면, 진행중이던 작업내역을 일시적으로 다른 곳에 치워놓고 나중에 꺼내서 작업할수 있다.  

`stash` 로 저장된 내역들은 특정 Branch 에 종속적이지 않으므로 어느 Branch 에서든 꺼내(`pop` or `apply`) 사용할 수 있다.

![stash-pop](https://user-images.githubusercontent.com/48475824/121684289-772c6e00-caf9-11eb-97c6-3e59d7d33239.gif)

### LIFO  
Stash 에는 LIFO stack 이 사용된다.  
LIFO stack 에 존재하는 stash 기록들은 ID 가 존재한다. 
- ID 는 `stash@{#}` 형태로 구분된다.  
  - `stash@{0}`
  - `stash@{1}`
  - `stash@{2}`
  - `stash@{3}`

**apply w/o ID**  
`git stash apply`  
stash 적용시 ID 를 명시하지 않는다면, 제일 마지막으로 stack에 쌓인 기록이 제일 먼저 `pop` 된다.  
- 즉, 아래의 이미지에서 제일 상단에 위치한 `stash@{0}` 이 브랜치에 적용된다.  

  <img width="436" alt="stash stack" src="https://user-images.githubusercontent.com/48475824/121688583-9679ca00-cafe-11eb-9028-04145f2aec93.png">

**apply w/ ID**  
`git stash apply <stashID>`  
특정 stash 내역을 적용하고자 한다면 ID 를 이용해서 가능하다.  
- 예) 쌓여있는 stack 에서 세번째 stash 를 적용하고자 한다면 → `git apply stash@{2}`

[↑ return to TOC](#table-of-contents)


### Apply & Pop
임시방편으로 `stash` 명령어로 저장한 내역들을 꺼내 사용하고자 할때는 `apply` 또는 `pop` 을 사용한다.  
- `apply` : 임시 저장한 내용을 현재 브랜치에 적용하기.  
  - `apply`로 가져온 변경내역은 stash 의 stack에 그대로 존재한다.  
  - 적용한 내역들을 stack 에서 삭제하기 위해서는 `drop` 명령어를 이용한다.  
- `pop` : 임시 저장한 내용을 현재 브랜치에 적용시킨후 스택에서 지우기.  
  - `pop` 은 `apply` + `drop` 을 합친 명령어라 보면 된다.  

[↑ return to TOC](#table-of-contents)


### When to use git stash
1. **feature_A 라는 브랜치에서 작업을 하던 도중 feature_B 의 기능을 먼저 추가해야하는 상황 일 때.**  

    - 작업자는 feature_A 에서 feature_B 브랜치로 전환해야 한다.
    - 하지만 변경된 내역을 git 이 알도록 기록(저장) 하지 않는다면 아래와 같은 에러 메시지를 만나게 된다.  
      ```
      error: Your local changes to the following files would be overwritten by checkout:

      fileName.ext
      fileName2.ext

      Please commit your changes or stash them before you switch branches.
      Aborting
      ```

    - 작업한 내역들을 휘발시키지 않기위해 기록해 두는 방법은 두 가지가 존재한다. 바로 `commit` 과 `stash` 이다.  
      - `commit` : 작업한 내역을 영구적인 기록으로 남겨놓고자 할 때.  
      - `stash` : 작업하던 내용들을 임시적인 기록으로 남겨놓고자 할 때.  
      작업물들이 아직 commit 하기에는 부적합(여러가지 사유로)하다고 느껴지는 경우 `stash` 를 이용하게 된다.  

1. feature_D 에서 필요한 작업들을 feature_C 에서 잘못 작업해버린 상황일 때  
   - `git stash`  
    변경된 내역들을 현재 작업중인 feature_C 브랜치에 commit 하는 대신 stash 처리한다.  
   - `git checkout feature_D`  
     feature_C 에서 feature_D 브랜치로 전환.  
   - `git stash pop`  
     가장 최근에 저장한 `stash` 내역을 feature_D 로 가져와 적용시키기.

[↑ return to TOC](#table-of-contents)


## Commands

### Stash
- **`git stash`**  
  git stash 로 임시 저장된 내용은 `WIP on <branchName>: <commitHash>` 형태로 기록된다.
  - `WIP on feature_device_control: 123456d`

### Apply
- **`git stash apply`**  
  가장 최근에 임시저장해 놓은 stash 를 해당 브랜치(현재 checkout 되어 있는)에 적용 시키기.  

  - `git stash apply <stashID>`  
    특정 stash ID 를 명시함으로써 해당 ID를 지닌 stash 를 현재 브랜치에 적용시켜준다.  
    - `git stash apply stash@{13}`

### Clear
- **`git stash clear`**  
  stash stack 에 있는 모든 stash를 삭제해주는 명령어.  

### Drop
- **`git stash drop`**  
  가장 최신 stash 를 제거 하는 명령어.  

  - `git stash drop <stashID>`
    ID 를 통해 특정 stash 를 제거하는 명령어.  
    - `git stash drop stash@{22}`  

### List
- **`git stash list`**   
  stash stack 에 쌓인 전체 stash 리스트를 나열한다.  
  만약 stash를 apply만 하고(`git stash apply`) 지우지 않았다면 리스트에 그대로 남아있게 된다.  

  ```
  stash@{0}: WIP on develop: 12b3456 enhance: net drive API (#100)
  stash@{1}: WIP on add_smart_search: 54321zy feat: keword search (#98)
  stash@{2}: WIP on doc_mail_sender: 77377eb doc: mail sender (#77)
  ```

### Pop
- **`git stash pop`**  
  가장 최신의 stash 를 적용(`apply`)과 동시에 제거(`drop`)를 수행해주는 명령어.  
  - 만약 stash 가 진행되던 중 충돌이 발생했다면 제거되지 않은 채로 stash stack에 남아있게 된다. 충돌을 해결 한 후 stash stack 에서 제거해주면 된다.  

### Show
- **`git stash show`**   
  해당 명령어를 통해 가장 최신 stash의 파일 리스트를 살펴볼 수 있다.  
  - 수정이 이루어진 파일명
  - 추가/삭제된 코드 정보  
  
  ```
  prefix/file_name1.ext   |  16 +++++++++
  prefix/file_name2.ext   | 411 +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++-----------------------------------------------------------------------------------------------------------
  prefix/file_name3.ext   |  41 ++++++++++++-----------
  prefix/file_name4.ext   |  60 +++++++++++++++++++++++++++++++++
  4 files changed, 313 insertions(+), 215 deletions(-)
  ```

  - `git stash show -p`  
    제일 최신 stash(`stash@{0}`)를 변경 이전(Original Parent)의 상태와 비교해 볼 수 있다.  

  - `git stash show -p <stashID>`  
    제일 최신 stash 가 아닌, 특정한 stash의 변경 사항을 살펴보고자 할 때 stash ID를 명시해준다.  
    - `git stash show -P stash@{5}`

  - `git stash show -p <stashID> --name-only`  
    특정 stash의 변경된 파일명만 나열하고자 할 때 사용한다.  
    - `git stash show -p stash@{7} --name-only`

  - `git stash show -p | git apply --reverse`  
    Apply 한 stash 내역들을 되돌리고자 할 때 사용한다.  

  - `git stash show -p | git apply -R`  
    위의 명령과 동일한 기능을 한다. 좀 더 짧게 쓴 버전이라고 생각하면 된다.  


[↑ return to TOC](#table-of-contents)