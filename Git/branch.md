# Branch
여러명이 동일 프로젝트를 협업하기 위해서 각각의 브랜치를 만들어 작업한다.  
각각의 브랜치들은 서로의 작업영역에 영향을 주지 않는다.

![git-branch](https://user-images.githubusercontent.com/48475824/74917208-7fdfc900-540a-11ea-81b1-1b405a19a390.png)


### Table of Contents
* [Commands](#commands)
    * [Create](#create)
    * [Show](#show)
    * [Merge](#merge)
    * [Pull](#pull)
    * [Name](#name)
    * [Delete](#delete)



## Commands
1. ### Create
    #### Create New branch
    새 브랜치 만들기  
    `git branch <newBranchName>`

    #### Create New Branch & Checkout
    새 브랜치 만듬과 동시에 체크아웃 하기  
    `git checkout -b <newBranchName>`

    #### Create Tracking Branch
    원격 브랜치를 트래킹하는 새 브랜치 만들기  
    `git checkout --track <remote/branchName>`
    * branchName 을 가진 트래킹 브랜치가 생성된다.

    [Return to TOC](#table-of-contents)


1. ### Show
    #### Show All Branch (Remote + Local)
    원격저장소와 로컬 저장소의 브랜치 보기  
    `git branch -a`
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
    `git branch `
    
    ```
    develop
    feature/channel
    * feature/user
    master
    ```

    #### Show Remote Branches Only
    원격 저장소의 브랜치 보기  
    `git branch -r`  
    ```
    origin/HEAD -> origin/master
    origin/develop
    origin/master
    ```

    #### Show Branch w/ Last Commit Info
    로컬 브랜치의 마지막 커밋 정보 보기  
    `git branch -v`
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
    > 머지 시키는 명령어는 `merge` 외에도 두 가지 방법이 더 존재한다.  

    1. Straight Merge   
        `git merge <branchName>`
        * 한 브랜치의 모든 변경 히스토리가 다른 브랜치에 머지 된다.

    2. Squashed Commit  
        `git merge --squash <branchName>`
        * 한 브랜치의 최종 커밋 히스토리만이 머지 된다.

    3. Cherry-picking :cherries:  
        `git cherry-pick <commitName>`
        * 다른 브랜치의 특정 커밋만이 현재의 브랜치에 머지 된다.

    #### Merge Branch w/o Commit
    커밋 없이 브랜치 머지 시키기  
    `git merge --no-commit <branchName>`

    [Return to TOC](#table-of-contents)

1. ### Pull
    #### Pull origin branch to a local branch
    원격 브랜치를 새로 생성한 로컬 브랜치에 풀받기  
    `git checkout -b <localBranchName> origin/<remoteBranchName>`  
    \<remoteBranchName> 이름을 가진 원격 브랜치를 \<localBranchName> 을 가진 브랜치에 담는다.

1. ### Name
    #### Move or Change Branch Name
    브랜치명을 변경하기 혹은 브랜치 옮기기  
    `git checkout -m <selectedBranch> <newBranch>`

    
1. ### Delete
    #### Delete Local Branch
    브랜치 삭제  
    `git branch -d <branchName>`

    브랜치 강제 삭제  
    `git branch -D <branchName>`
    * 대문자 D를 사용  

    #### Delete All Local Branches Except Master and Develop
    Master와 Develop 브랜치를 제외한 모든 브랜치 삭제  
    `git branch | grep -v "master|develop" | xargs git branch -D`

    #### Delete Remote Branch
    원격 저장소의 브랜치 삭제  
    `git push <remoteName> --delete <branchName>`

    [Return to TOC](#table-of-contents)
