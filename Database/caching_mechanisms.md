# Caching Mechanisms

DB에서 쿼리결과를 캐시 메모리에 저장하여 빠르게 실행할 수 있도록 하는 기술

### Table of Contents

- [About Caching Mechanisms](#about-caching-mechanisms)
- [Caching Mechanisms Based on Database Types](#caching-mechanisms-on-database-types)
- [Oracle's Library Cache Vs. MySQL's Query Cache](#oracles-library-cache-vs-mysqls-query-cache)
  - Commonalitites
  - Differences

## About Caching Mechanisms

자주 사용되는 SQL문과 관련된 `실행 계획(Execution Plan)`이나 메타데이터 정보를 캐시에 보관한다. 이는 DB 성능을 향상시키고 리소스를 효율적으로 활용할 수 있도록 해준다.SQL문을 처리시 처음부터 실행 계획을 짜고 메타데이터를 조회하는 것은 많은 비용을 필요로 한다. 이러한 비용 절감을 위해 캐시에 저장해놓고 필요시 캐시에서 빠르게 가져와 실행한다.

- `실행계획`: DB System이 SQL문을 어떻게 처리(실행)할 것인지에 관한 계획

Caching Machanism의 목적:

- 빠른 응답 시간
  - 미리 계산한 결과 재사용
- 리소스 절약
  - 반복적 연산 최소화
- 최적화된 성능
- 데이터 일관성 유지
- 부하 분산

## Caching Mechanisms on Database Types

데이터베이스 종류에 따른 캐시 메커니즘

| Database Type        | Caching Mechanism        |
| :------------------- | :----------------------- |
| Oracle               | Library Cache            |
| MySQL                | Query Cache              |
| Microsoft SQL Server | Procedure Cache          |
| PostgreSQL           | Shared Buffer Cache      |
| MongoDB              | Query Cache, Index Cache |
| Redis                | In-memory Data Store     |
| Memcached            | Distributed Memory Cache |

## Oracle's Library Cache Vs. MySQL's Query Cache

Oracle은 더 세분화된 캐시 종류를 사용한다.

- Library Cache: SQL 문의 파싱 결과와 실행 계획을 저장
- Dictionary Cache: 데이터베이스 객체 정보를 저장

### Commonalitites

- 기능:
  - Oracle: 쿼리 결과와 실행 계획을 저장하여 성능 향상
  - MySQL: 쿼리 결과를 저장하여 성능 향상
- 캐시 공유: 여러 세션 간에 캐시 정보 공유 가능

- `Oracle` SQL 파싱시 캐시에
  - 존재 O → Soft Parsing: 캐시에서 찾아 바로 실행
  - 존재 X → Hard Parsing: 최적화, 로우 소스 생성 단계 총 과정을 거쳐 실행

### Differences

| Types     | Oracle                                | MySQL              |
| :-------- | :------------------------------------ | :----------------- |
| 캐시 종류 | 라이브러리 캐시, 데이터 딕셔너리 캐시 | 단일 쿼리 캐시     |
| 저장      | SQL문의 파싱 결과와 실행 계획 저장    | SELECT문 결과 저장 |

- `MySql`의 8.0에서 Query Cache는 더이상 사용되지 않는다.
  - [`The query cache is deprecated as of MySQL 5.7.20, and is removed in MySQL 8.0.`](https://dev.mysql.com/doc/refman/5.7/en/query-cache.html)
  - [Deprecated 된 이유](https://dev.mysql.com/blog-archive/mysql-8-0-retiring-support-for-the-query-cache/): 확장성 문제, 병목현상 유발
