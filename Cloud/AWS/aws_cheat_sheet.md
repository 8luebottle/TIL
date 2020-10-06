# AWS CHEAT SHEET

### Table of Contents
* [Athena](#athena)
  * [Partition Projections](#partition-projections)
    * [DROP](#drop)
      * [Drop Table](#drop-table)
    * [SHOW](#show)
      * [Show Create Table](#show-create-table)
      * [Show Partitions](#show-partitions)
    * [REPAIR](#repair)
* [S3](#s3)
  * [LIST](#list)
    * [List Buckets](#list-buckets)
  * [GET](#get)
    * [Get Bucket Location](#get-bucket-location)
  * [REMOVE](#remove)
    * [Remove Multiple Files](#remove-multiple-files)


## Athena
<details>
  <summary>Partition Projections</summary>

### DROP
#### Drop Table
```sql
ALTER TABLE  <tableName>
DROP IF EXISTS PARTITION(year='yyyy', month='MM', day='dd')
```

### SHOW
#### Show Create Table
```sql
SHOW CREATE TABLE <tableName>
```
👉🏻 This shows table, and configuration info.

#### Show Partitions
```sql
SHOW PARTITIONS <tableName>
```
👉🏻 This shows whole partitioned data.

[↑ return to TOC](#table-of-contents)

#### REPAIR
##### Repair Manually
If your data looks like this,   
`s3://bucketName/path/distributionID/yyyy/MM/dd/hh`   
than
```sql
ALTER TABLE <db>.<bucketName>
ADD PARTITION (year='yyyy',month='MM', day='dd') 
LOCATION 's3://bucketName/path/distributionID/yyyy/MM/dd/hh'
```
```sql
# example code
ALTER TABLE default.cloudfront-test
ADD PARTITION (year='2020',month='10', day='05') 
LOCATION 's3://cloudfront-test/logs/abcdeabcded/2020/10/05/00'
```

##### Repair Automatically
If your data looks like this,
`s3://bucketName/path/distributionID/year=2020/month=10/day=05/hour=00`  
than
```sql
MSCK REPAIR TABLE <tableName>;
```

[↑ return to TOC](#table-of-contents)

</details>

## S3
<details>
  <summary>CLI Commands</summary>

### LIST
#### List Buckets
`aws s3 ls <bucketName>`

* w/ profile  
`aws --profile <profileName> s3 ls <bucketName>`


```
# output
2020-10-05 17:08:50 mybucketA
2020-10-06 14:55:44 mybucketB
```

`aws s3api list-obejcts`  
* w/ profile  
`aws --profile <profileName> s3 ls <bucketName>`  

```
# output
{
    "Buckets": [
        {
            "CreationDate": "2020-10-05T17:08:50.000Z",
            "Name": "mybucketA"
        },
        {
            "CreationDate": "2020-10-06T14:55:44.000Z",
            "Name": "mybucketB"
        },
        {
            "CreationDate": "2020-01-01T23:32:05+00:00",
            "Name": "mybucketC"
        }
    ],
    "Owner": {
        "DisplayName": "userName",
        "ID": "userID"
    },
}
```
👉🏻 Buckets are returned in alphabetical order.

### GET
#### Get Bucket Location
`aws s3api get-bucket-location --bucket <bucketName>`  
* w/ profile  
`aws --profile <profileName> s3api get-bucket-location --bucket <bucketName>`  


### REMOVE
#### Remove Multiple Files
Remove multiple files by `--exclude` and `--include` arguments   
`aws s3 rm s3://bucketName/path --recursive --exclude "*" --include "pattern*"`

```
# example code
aws s3 rm s3://cloudfront-test/logs --recursive --exclude "*" --include "abcdefghijklmnopqr/2020/10/04/*"
```

* **Results**      
![remove-multiple-objects](https://user-images.githubusercontent.com/48475824/95204315-e8a37680-081e-11eb-8361-873b5a800fa7.png)



[↑ return to TOC](#table-of-contents)

</detail>
