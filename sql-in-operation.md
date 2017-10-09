# SQL - IN 연산자

IN 연산자를 사용하여 WHERE 절에 여러 값을 지정할 수 있습니다. 

IN 연산자는 여러 OR 조건의 줄임말입니다.

### IN Syntax

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1, value2, ...);
```

or:

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name IN (SELECT STATEMENT);
```

### IN Operator Examples


다음 SQL 문은 'Germany', 'France'및 'UK'에있는 모든 고객을 선택합니다.

```sql
SELECT * FROM Customers
WHERE Country IN ('Germany', 'France', 'UK');
```
![](./images/gln%20in%20operation.png)

다음 SQL 문은 'Germany', 'France'또는 'UK'에 있지 않은 모든 고객을 선택합니다.

```sql
SELECT * FROM Customers
WHERE Country NOT IN ('Germany', 'France', 'UK');
```
다음 SQL.은 공급 업체와 동일한 국가의 모든 고객을 선택합니다.

```sql
SELECT * FROM Customers
WHERE Country IN (SELECT Country FROM Suppliers);
```

![](./images/in%20operation.png)