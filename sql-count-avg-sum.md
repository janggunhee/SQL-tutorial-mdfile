# SQL - COUNT(), AVG(), SUM() 함수

 - COUNT () 함수는 지정된 기준과 일치하는 행 수를 반환합니다. 
 - AVG () 함수는 숫자 열의 평균값을 반환합니다. 
 - SUM () 함수는 숫자 열의 총 합계를 반환합니다.

### COUNT() Syntax

```sql
SELECT COUNT(column_name)
FROM table_name
WHERE condition;
```

### AVG() Syntax
```sql
SELECT AVG(column_name)
FROM table_name
WHERE condition;
```

### SUM() Syntax

```sql
SELECT SUM(column_name)
FROM table_name
WHERE condition;
```

#### Demo Database

![](///Users/janggunhee/projects/md-file/sql-md/images/demo-8.png)

### COUNT() Example

다음 SQL 문은 제품 수를 찾습니다.

```sql
SELECT COUNT(ProductID)
FROM Products;
```
![](///Users/janggunhee/projects/md-file/sql-md/images/count-.png)

### AVG() Example

다음 SQL 문은 모든 제품의 평균 가격을 찾습니다.

```sql
SELECT AVG(Price)
FROM Products;
```
![](///Users/janggunhee/projects/md-file/sql-md/images/avg.png)


#### Demo Database
아래는 Northwind 샘플 데이터베이스의 'OrderDetails'표에서 선택한 항목입니다.

![](///Users/janggunhee/projects/md-file/sql-md/images/demo-9.png)

### SUM() Example

```sql
SELECT SUM(Quantity)
FROM OrderDetails;
```
![](///Users/janggunhee/projects/md-file/sql-md/images/sum.png)
