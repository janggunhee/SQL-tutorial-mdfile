# SQL - BETWEEN 연산자

**BETWEEN** 연산자는 주어진 범위 내의 값을 선택합니다. 값은 숫자, 텍스트 또는 날짜 일 수 있습니다. 

**BETWEEN** 연산자는 시작과 끝 값이 포함됩니다.

### BETWEEN Syntax

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

#### Demo Database

![](///Users/janggunhee/projects/md-file/sql-md/images/demo10.png)



### BETWEEN Example

다음 SQL 문은 가격이 10과 20 사이 인 모든 제품을 선택합니다.

```sql
SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20;
```
![](///Users/janggunhee/projects/md-file/sql-md/images/between.png)

### NOT BETWEEN Example

앞의 예제 범위를 벗어난 제품을 표시하려면 NOT BETWEEN :

```sql
SELECT * FROM Products
WHERE Price NOT BETWEEN 10 AND 20;
```

### BETWEEN with IN Example

다음 SQL 문은 가격이 10과 20 사이 인 모든 제품을 선택합니다. CategoryID가 1,2 또는 3 인 제품을 표시하지 않습니다.

```sql
SELECT * FROM Products
WHERE (Price BETWEEN 10 AND 20)
AND NOT CategoryID IN (1,2,3);
```
![](///Users/janggunhee/projects/md-file/sql-md/images/between%20in.png)


### BETWEEN Text Values Example

다음 SQL.은 'Carnarvon Tigers'와 'Mozzarella di Giovanni'사이에 ProductName이있는 모든 제품을 선택합니다.

```sql
SELECT * FROM Products
WHERE ProductName BETWEEN 'Carnarvon Tigers' AND 'Mozzarella di Giovanni'
ORDER BY ProductName;
```
![](///Users/janggunhee/projects/md-file/sql-md/images/between%20in2.png)
![](///Users/janggunhee/projects/md-file/sql-md/images/btween%20in%203.png)




### BETWEEN Dates Example

다음 SQL 문은 OrderDate BETWEEN '04 -July-1996 '및 '09-Junly-1996'이있는 모든 주문을 선택합니다.

#### Sample Table

![](///Users/janggunhee/projects/md-file/sql-md/images/demo%2011.png)

```sql
SELECT * FROM Orders
WHERE OrderDate BETWEEN #07/04/1996# AND #07/09/1996#;
```
![](///Users/janggunhee/projects/md-file/sql-md/images/sample%20table.png)
