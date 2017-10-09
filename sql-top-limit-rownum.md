# SQL - TOP, LIMIT, ROWNUM 

#  SQL - SELECT TOP Clause

SELECT TOP 절은 리턴 할 레코드 수를 지정하는 데 사용됩니다.

SELECT TOP 절은 수천 개의 레코드가있는 큰 테이블에서 유용합니다. 
많은 수의 레코드를 반환하면 성능에 영향을 줄 수 있습니다.

>Note: 모든 데이터베이스 시스템이 SELECT TOP 절을 지원하는 것은 아닙니다. 
>MySQL은 제한된 수의 레코드를 선택하기 위해 LIMIT 절을 지원하고 Oracle은 ROWNUM을 사용합니다.

![](///Users/janggunhee/projects/md-file/sql-md/images/select%20top.png)

### Demo Database

![](///Users/janggunhee/projects/md-file/sql-md/images/demo%20-6.png)

## SQL TOP, LIMIT and ROWNUM Examples

다음 SQL 문은 'Customers'테이블에서 처음 세 개의 레코드를 선택합니다.

```sql
SELECT TOP 3 * FROM Customers;
```
![](///Users/janggunhee/projects/md-file/sql-md/images/select%20top3.png)

다음 SQL 문은 LIMIT 절을 사용하는 동일한 예제를 보여줍니다.

```sql
SELECT * FROM Customers
LIMIT 3;
```
![](///Users/janggunhee/projects/md-file/sql-md/images/select-limit.png)

다음 SQL 문은 ROWNUM을 사용하는 동일한 예제를 보여줍니다.

```sql
SELECT * FROM Customers
WHERE ROWNUM <= 3;
```

### SQL TOP PERCENT Example

다음 SQL 문은 'Customers'테이블에서 레코드의 처음 50 %를 선택합니다.

```sql
SELECT TOP 50 PERCENT * FROM Customers;
```

### ADD a WHERE CLAUSE

다음 SQL 문은 국가가 'Germany'인 'Customers'테이블에서 처음 세 개의 레코드를 선택합니다.

```sql
SELECT TOP 3 * FROM Customers
WHERE Country='Germany';
```
다음 SQL 문은 LIMIT 절을 사용하는 동일한 예제를 보여줍니다.

```sql
SELECT * FROM Customers
WHERE Country='Germany'
LIMIT 3;
```

다음 SQL 문은 ROWNUM을 사용하는 동일한 예제를 보여줍니다.

```sql
SELECT * FROM Customers
WHERE Country='Germany' AND ROWNUM <= 3;
```