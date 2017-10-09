# SQL SELECT INTO 

SELECT INTO 문은 한 테이블의 데이터를 새 테이블로 복사합니다.

## SELECT INTO Syntax

모든 열을 새 테이블로 복사 :

```sql
SELECT *
INTO newtable [IN externaldb]
FROM oldtable
WHERE condition;
```
일부 열만 새 테이블로 복사 :

```sql
SELECT column1, column2, column3, ...
INTO newtable [IN externaldb]
FROM oldtable
WHERE condition;
```

> 새 테이블은 이전 테이블에 정의 된대로 컬럼 이름 및 유형으로 작성됩니다. 
> AS 절을 사용하여 새 열 이름을 만들 수 있습니다.
> 

### SQL SELECT INTO Examples

다음 SQL 문은 Customers 백업 복사본을 만듭니다.

```sql
SELECT * INTO CustomersBackup2017
FROM Customers;
```

다음 SQL 문은 IN 절을 사용하여 테이블을 다른 데이터베이스의 새 테이블로 복사합니다.

```sql
SELECT * INTO CustomersBackup2017 IN 'Backup.mdb'
FROM Customers;
```

다음 SQL 문은 몇 개의 열만 새 테이블에 복사합니다.

```sql
SELECT CustomerName, ContactName INTO CustomersBackup2017
FROM Customers;
```

다음 SQL 문은 독일 고객 만 새 테이블로 복사합니다.

```sql
SELECT * INTO CustomersGermany
FROM Customers
WHERE Country = 'Germany';
```

다음 SQL 문은 하나 이상의 테이블의 데이터를 새 테이블로 복사합니다.

```sql
SELECT Customers.CustomerName, Orders.OrderID
INTO CustomersOrderBackup2017
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

>Tip: SELECT INTO를 사용하여 다른 테이블의 스키마를 사용하여 새 테이블을 만들 수도 있습니다. 
>쿼리가 데이터를 반환하지 않게하는 WHERE 절을 추가하기 만하면됩니다.
>

```sql
SELECT * INTO newtable
FROM oldtable
WHERE 1 = 0;
```
