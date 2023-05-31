# RDS

### Table of Contents
- [RDS CLI Commands](#rds-cli-commands)

## RDS CLI Commands
### `describe-db-log-files`
> 특정 DB 인스턴스에 대한 DB 로그 파일 목록 보기

`aws rds describe-db-log-files --db-instance-identifier <dbInstanceID>`

- The Result:
```shell
{
    "DescribeDBLogFiles": [
        {
            "LogFileName": "error/mysql-error-running.log",
            "LastWritten": 1659279600,
            "Size": 0
        },
        {
            "LogFileName": "error/mysql-error-running.log.2022-08-01.01",
            "LastWritten": 1659322800,
            "Size": 12345
        },
    ]
}
```
- `DescribeDBLogFiles`: 로그 파일 관련 정보가 담긴 배열.
  - `LogFileName`: 로그 파일 명
  - `LastWritten`: 로그가 마지막으로 기록된 시간.
  - `Size`: 로그 파일 크기 (Byte).


### `download-db-log-file-portion`
> 특정 로그파일 다운로드 하기

`aws rds download-db-log-file-portion --db-instance-identifier <dbInstanceID> --log-file-name <logFileName> --output text`
- `--log-file-name` (`-lfn`): 다운로드 할 로그 파일 명칭
  - `describe-db-log-files` 로 부터 얻은 리스트의 특정 `LogFileName` 을 입력.

- `--output` (`-o`): 결과 출력 형식
  > 결과 출력 형식의 종류
  - `json`
  - `text`
  - `table`
  - `yaml`

