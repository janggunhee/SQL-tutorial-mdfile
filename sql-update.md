# SQL - UPDATE

UPDATE 문은 테이블의 기존 레코드를 수정하는 데 사용됩니다.

### UPDATE Syntax

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```
> 참고 : 테이블의 레코드를 업데이트 할 때주의하십시오! 
> UPDATE 문에서 WHERE 절을 확인하십시오. 
> WHERE 절은 갱신해야하는 레코드를 지정핟나.WHERE 절을 생략하면 테이블의 모든 레코드가 업데이트됩니다!
> 

### Demo Database

![](///Users/janggunhee/projects/md-file/sql-md/images/demo-4.png)

### UPDATE Table

다음 SQL 문은 첫 번째 고객 (CustomerID = 1)을  new contact person 및 new city로 업데이트합니다.

```sql
UPDATE Customers
SET ContactName = 'Alfred Schmidt', City= 'Frankfurt'
WHERE CustomerID = 1;
```
![](///Users/janggunhee/projects/md-file/sql-md/images/update%20table.png)

### UPDATE Multiple Records

업데이트 될 레코드 수를 결정하는 것은 WHERE 절입니다. 

다음 SQL 문은 country가 'Mexico'인 모든 레코드에 대해 연락처 이름을 'Juan'으로 업데이트합니다.

```sql
UPDATE Customers
SET ContactName='Juan'
WHERE Country='Mexico';
```
![](///Users/janggunhee/projects/md-file/sql-md/images/update%20multie.png)

#### Update 할때 주의!! 

> 레코드를 업데이트 할 때는주의하십시오. WHERE 절을 생략하면 모든 레코드가 업데이트됩니다!

```sql
UPDATE Customers
SET ContactName='Juan';
Try it Yourself »
```
![](///Users/janggunhee/projects/md-file/sql-md/images/update%20careful.png)
