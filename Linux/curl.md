# cURL Command in Linux
> cURL: client URL

## Send Multiple cURL Requests
cURL 요청을 병렬로 실행하고자 할 때 아래와 같은 방법을 사용할 수 있다.
1. URL List 가 담긴 txt 파일 작성
    - e.g. `url-list.txt`
2. xargs 명령어를 통한 curl 요청
    - e.g. `xargs -P 3 -n 1 curl -0 < url-list.txt`

    - About options
      - `P`: max-procs
      - `n`: max-args

예)  
- File: `url-list.txt`
  ```
  https://www.apple.com
  https://www.bestbuy.com
  https://www.craigslist.org
  ```

- Send Request:  
  `xargs -P 3 -n 1 curl -0 < url-list.txt`
