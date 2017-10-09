# SQL - LIKE 연산자

LIKE 연산자는 WHERE 절에서 열의 지정된 패턴을 검색하는 데 사용됩니다. 

LIKE 연산자와 함께 사용되는 두 개의 와일드 카드가 있습니다. 

 - % - 백분율 기호는 0, 하나 또는 여러 문자를 나타냅니다. 
 - _ - 밑줄은 단일 문자를 나타냅니다

**`%` 와 `_`은 조합하여 사용할 수도 있습니다!**

### LIKE Syntax

```sql
SELECT column1, column2, ...
FROM table_name
WHERE columnN LIKE pattern;
```
**AND 또는 OR 연산자를 사용하여 여러 조건을 결합 할 수도 있습니다.**

|LIKE Operator	|Description|
----------------|-------------
|WHERE CustomerName LIKE `'a%'`|	`'a'`로 시작하는 값을 찾습니다."|
|WHERE CustomerName LIKE `'%a'`|	`'a'`로 끝나는 값을 찾습니다."|
|WHERE CustomerName LIKE `'%or%'`|`'or'`값이 있는 어떤 위치의 어떤 값도 찾습니다.|
|WHERE CustomerName LIKE `'_r%'`|	두 번째 위치에 `'r'`이 있는 값을 찾습니다.|
|WHERE CustomerName LIKE `'a_%_%'`|`'a'`로 시작하고 길이가 3 자 이상인 값을 찾습니다.|
|WHERE ContactName LIKE `'a%o'`|	`'a'`로 시작하고 `'o'`로 끝나는 값을 찾습니다.|


#### Demo Database

![](./images/demo%205.png)


### SQL LIKE Examples

다음 SQL 문은 CustomerName이 'a'로 시작하는 모든 고객을 선택합니다.

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE 'a%';
```
![](./images/a%20customer.png)

다음 SQL 문은 CustomerName이 'a'로 끝나는 모든 고객을 선택합니다.

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '%a';
```
다음 SQL 문은 CustomerName이 'or'인 모든 고객을 선택합니다.

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '%or%';
```
![](./images/or%20customer.png)

다음 SQL 문은 두 번째 위치에 'r'이 있는 CustomerName을 가진 모든 고객을 선택합니다.

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '_r%';
```

다음 SQL 문은 CustomerName이 'a'로 시작하고 길이가 3 자 이상인 모든 고객을 선택합니다.
```sql
SELECT * FROM Customers
WHERE CustomerName LIKE 'a_%_%';
```

다음 SQL 문은 ContactName이 'a'로 시작하고 'o'로 끝나는 모든 고객을 선택합니다.

```sql
SELECT * FROM Customers
WHERE ContactName LIKE 'a%o';
```
다음 SQL 문은 CustomerName이 'a'로 시작하지 않는 모든 고객을 선택합니다.

```sql
SELECT * FROM Customers
WHERE CustomerName NOT LIKE 'a%';
```
![](./images/not%20a.png)

