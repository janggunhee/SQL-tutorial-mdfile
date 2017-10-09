# SQL - AND, OR and NOT 연산자

## AND, OR , NOT 연산자

WHERE 절은 AND, OR 및 NOT 연산자와 결합 할 수 있습니다. 

`AND` 및 `OR` 연산자는 둘 이상의 조건에 따라 레코드를 필터링하는 데 사용됩니다.
 - `AND`로 구분 된 모든 조건이 `TRUE`이면 `AND` 연산자가 레코드를 표시합니다. 
 - `OR` 연산자는 `OR`로 구분 된 조건 중 하나가 `TRUE`인 경우 레코드를 표시합니다. 
 
`NOT` 연산자는 조건이 `NOT TRUE` 경우 레코드를 표시합니다.

### AND Syntax

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 AND condition2 AND condition3 ...;
```

### OR Syntax

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 OR condition2 OR condition3 ...;
```

### NOT Syntax

```sql
SELECT column1, column2, ...
FROM table_name
WHERE NOT condition;
```

### Demo Database

![](///Users/janggunhee/projects/md-file/sql-md/images/demo-1.png)

### AND Example

다음 SQL 문은 country가 'Germany'이고 도시가 'Berlin'인 'Customers'의 모든 필드를 선택합니다.

```
SELECT * FROM Customers
WHERE Country='Germany' AND City='Berlin';
```
![](///Users/janggunhee/projects/md-file/sql-md/images/german.png)

### OR Example

다음 SQL 문은 도시가 'Berlin'또는 'München'인 'Customers'의 모든 필드를 선택합니다.

```
SELECT * FROM Customers
WHERE City='Berlin' OR City='München';
```

![](///Users/janggunhee/projects/md-file/sql-md/images/german-mun.png)

### NOT Example

다음 SQL.은 country가 'Germany'가 아닌 'Customers'의 모든 필드를 선택합니다.

```
SELECT * FROM Customers
WHERE NOT Country='Germany';
```
![](///Users/janggunhee/projects/md-file/sql-md/images/not%20german.png)

### AND, OR 및 NOT 연산자 결합

> AND, OR 및 NOT 연산자를 결합 할 수도 있습니다. 

다음 SQL 문은 국가가 'Germany'이고 도시가 'Berlin'또는 'München'(복잡한 표현식을 형성하기 위해 괄호를 사용해야 함) 인 'Customers'의 모든 필드를 선택합니다.

```
SELECT * FROM Customers
WHERE Country='Germany' AND (City='Berlin' OR City='München');
```
![](///Users/janggunhee/projects/md-file/sql-md/images/combine.png)

다음 SQL 문은 country가 'Germany'가 아니며 'USA'가 아닌 'Customers'의 모든 필드를 선택합니다.

```
SELECT * FROM Customers
WHERE NOT Country='Germany' AND NOT Country='USA';
```
![](///Users/janggunhee/projects/md-file/sql-md/images/not%20german%20usa.png)
