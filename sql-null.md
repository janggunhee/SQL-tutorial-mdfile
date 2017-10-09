# SQL NULL Values

NULL는 값이 없는 필드입니다. 

테이블의 필드가 선택적이면이 필드에 값을 추가하지 않고 새 레코드를 삽입하거나 레코드를 업데이트 할 수 있습니다. 그런 다음 필드는 NULL 값으로 저장됩니다.

>참고 : NULL 값이 0 값 또는 공백이있는 필드와 다른 것을 이해하는 것이 매우 중요합니다. NULL 값이있는 필드는 레코드를 생성하는 동안 비어있는 필드입니다.


### NULL 값을 테스트하는 방법? 

`=`, `<`또는 `<>`와 같은 비교 연산자로 NULL 값을 테스트 할 수 없습니다. 

`IS NULL` 연산자와 `IS NOT NULL` 연산자를 사용해야 합니다.

### IS NULL Syntax

```sql
SELECT column_names
FROM table_name
WHERE column_name IS NULL;
```

### IS NOT NULL Syntax

```sql
SELECT column_names
FROM table_name
WHERE column_name IS NOT NULL;
```
![](///Users/janggunhee/projects/md-file/sql-md/images/demo4.png)

'Persons'테이블의 'Address'열이 선택 사항이라고 가정합니다. 'Address'에 값이 없는 레코드가 삽입되면 'Address'열은 NULL 값으로 저장됩니다.

### The IS NULL Operator

다음 SQL 문은 IS NOT NULL 연산자를 사용하여 주소가있는 모든 사람을 나열합니다.

```sql
SELECT LastName, FirstName, Address FROM Persons
WHERE Address IS NOT NULL;
```
![](///Users/janggunhee/projects/md-file/sql-md/images/isnotnull.png)