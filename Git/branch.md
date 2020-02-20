# Branch
여러명이 동일 프로젝트를 협업하기 위해서 각각의 브랜치를 만들어 작업한다.  
각각의 브랜치들은 서로의 작업영역에 영향을 주지 않는다.

![git-branch](https://user-images.githubusercontent.com/48475824/74917208-7fdfc900-540a-11ea-81b1-1b405a19a390.png)


### Table of Contents
* [Commands](#commands)
    * [Create](#create)
    * [Show](#show)
    * [Merge](#merge)
    * [Name](#name)
    * [Delete](#delete)



## Commands
1. ### Create
    #### Create New branch
    새 브랜치 만들기  
    <code>git branch \<newBranchName></code>

    #### Create New Branch & Checkout
    새 브랜치 만듬과 동시에 체크아웃 하기  
    <code>git checkout -b \<newBranchName></code>

    #### Create Tracking Branch
    원격 브랜치를 트래킹하는 새 브랜치 만들기  
    <code>git checkout --track \<remote/branchName></code>
    * branchName 을 가진 트래킹 브랜치가 생성된다.

    [Return to TOC](#table-of-contents)


1. ### Show
    #### Show All Branch (Remote + Local)
    원격저장소와 로컬 저장소의 브랜치 보기  
    <code>git branch -a</code>
    ```
    develop
    feature/channel
    * feature/user
    master
    remotes/origin/HEAD -> origin/master
    remotes/origin/develop
    remotes/origin/master
    ```

    #### Show Local Branches Only
    로컬 저장소의 브랜치 보기  
    <code>git branch </code>
    
    ```
    develop
    feature/channel
    * feature/user
    master
    ```

    #### Show Remote Branches Only
    원격 저장소의 브랜치 보기  
    <code>git branch -r</code>  
    ```
    origin/HEAD -> origin/master
    origin/develop
    origin/master
    ```

    #### Show Branch w/ Last Commit Info
    로컬 브랜치의 마지막 커밋 정보 보기  
    <code>git branch -v</code>
    ```
    develop         322bd34 Service
    feature/channel d7631d3 WIP : Channel
    * feature/user    15dcbce WIP : Restart
    master          8356e72 Initial commit
    ```

    [Return to TOC](#table-of-contents)

1. ### Merge
    > 둘 이상의 브랜치를 하나로 합치는 명령어

    #### Merge Branch
    > 머지 시키는 명령어는 <code>merge</code> 외에도 두 가지 방법이 더 존재한다.  

    1. Straight Merge   
        <code>git merge \<branchName></code>
        * 한 브랜치의 모든 변경 히스토리가 다른 브랜치에 머지 된다.

    2. Squashed Commit  
        <code>git merge --squash \<branchName></code>
        * 한 브랜치의 최종 커밋 히스토리만이 머지 된다.

    3. Cherry-picking :cherries:  
        <code>git cherry-pick \<commitName></code>
        * 다른 브랜치의 특정 커밋만이 현재의 브랜치에 머지 된다.

    #### Merge Branch w/o Commit
    커밋 없이 브랜치 머지 시키기  
    <code>git merge --no-commit \<branchName></code>

    [Return to TOC](#table-of-contents)


1. ### Name
    #### Move or Change Branch Name
    브랜치명을 변경하기 혹은 브랜치 옮기기  
    <code>git checkout -m \<selectedBranch> \<newBranch></code>

    
1. ### Delete
    #### Delete Branch
    브랜치 삭제  
    <code>git branch -d \<branchName></code>

    [Return to TOC](#table-of-contents)
