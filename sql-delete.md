# SQL - DELETE Statement

DELETE 문은 테이블의 기존 레코드를 삭제하는 데 사용됩니다.

### DELETE Syntax

```sql
DELETE FROM table_name
WHERE condition;
```

>참고 : 테이블에서 레코드를 삭제할 때주의하십시오! DELETE 문의 WHERE 절을 확인하십시오. 
>WHERE 절은 삭제될 레코드를 지정합니다. WHERE 절을 생략하면 테이블의 모든 레코드가 삭제됩니다!


### Demo Database

![](./images/demo%205.png)

### SQL DELETE Example

다음 SQL.은 : Customers; 테이블에서 고객 'Alfreds Futterkiste'를 삭제합니다.

```sql
DELETE FROM Customers
WHERE CustomerName='Alfreds Futterkiste';
```
![](./images/delets%20customer.png)

### Delete All Records

테이블을 삭제하지 않고 테이블의 모든 행을 삭제할 수 있습니다. 이것은 테이블 구조, 속성 및 인덱스가 손상되지 않는다는 것을 의미합니다.

```sql
DELETE FROM table_name;
```
or:
```sql
DELETE * FROM table_name;
```