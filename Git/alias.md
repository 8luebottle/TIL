# Alias
git 에서 사용하는 명령어에게 별명을 부여할 수 있다.  
그로 인해 자주 쓰는 긴 명령어들을 축약하여 편리하게 사용 가능하다.

### Table of Contents
* [Setup](#setup)

## Setup 
alias 를 ```gitconfig``` 파일에 등록하는 과정은 아래와 같다.

1. **Open gitconfig file**  
    ```vim ~/.gitconfig```

1. **Add your alias**  
    자신이 자주 쓰는 명령어들을 등록하도록 하자. 
    ```
    [alias]
        br = branch
        ch = checkout
        cm = commit
        ps = push
        pl = pull
        st = status
        us = upstream
    ```

    log 를 graph 형태로 예쁘게 보여주기 위해 커스터마이징 한 log alias 를 아래와 같이 등록해 주었다.
    ```
     l = log --decorate --stat --graph --pretty=format:'%d %C(bold green)%h%Creset (%ar - %C(bold blue)%an%Creset), %n%n %s%n'
    ```

1. **Check alias**  
    등록한 alias 가 잘 반영되었는지 확인해보자.  
    <code>git l</code>

    ![git alias](https://user-images.githubusercontent.com/48475824/87239690-01350800-c44d-11ea-8d76-dd380d913093.png)