# Start Point of SQL

## SQL  문법

### SELECT문
`SELECT`문은 데이터베이스에서 선택적으로 데이터를 가져올 때 사용한다. 선택된 데이터는 테이블 형태로 반환되며 이를 보통 result-set이라고 한다. 아래는 `SELECT`문의 기본 형태이다.

```SQL
SELECT <field_name> FROM <table_name> 
```

`*`를 이용하여 전체 Field의 데이터를 가져올 수 있다. 혹은 Field_name을 입력하여 원하는 FIeld의 데이터만을 불러온다. 

```SQL
SELECT * FROM Customers
SELECT CustomerID, Country FROM Customers
```

많은 경우에 데이터 필드는 중복된 값을 포함한다. `SELECT DISTINCT`문으로 이런 중복을 제거한 행을 얻을 수 있다.

```SQL
SELECT DISTINCT Country FROM Customers
```

<br>

### WHERE 구문

`SELECT`문이 데이터 테이블에서 행을 선택했다면, `WHERE`구문은 열을 선택합니다. `WHERE` 조건에 맞는 기록만을 추출하여 반환해 주는 것입니다. 

```
SELECT <field_name> FROM <table_name> WHERE <condition>
```

예를 들어, 소속 나라가 멕시코인 고객 혹은 CustomerID가 1인 고객의 모든 정보를 가져오려면 다음과 같이 작성하면 됩니다.

```SQL
SELECT * FROM WHERE Country = 'Mexico'
SELECT * FROM WHERE CustomerID = 1
```

`WHERE`문의 조건에는 equal을 뜻하는 = 말고도 다른 연산자를 사용 할 수 있다.

	- = : Equal
	- <> : Not equal
	- > : Greater than
	- < : Less than 
	- >= : Greater than equal
	- <= : Less than equal
	- BETWEEN : Between an inclusive range
	- LIKE : Search for a pattern
	- IN : To specify multiple values for a column

<br>

### AND, OR and NOT 연산자
`WHERE`구문은 하나 이상의 조건이  AND, OR 그리고 NOT 연산자와 결합하여 다양한 페턴의  데이터를 필터링이 가능하다.  각각의 연산자 뜻은 알고 있으니 바로 예로 넘어가자.

```SQL
SELECT <field_name> FROM <table_name> WHERE <condition1> AND <condition2> AND <condition3>
SELECT <field_name> FROM <table_name> WHERE <condition1> OR <condition2> OR <condition3>
SELECT <field_name> FROM <table_name> WHERE NOT <condition>
```

국적이 독일이고 거주도시가 베를린인 고객의 정보를 가져오고 싶으면?
```SQL
SELECT * FROM Customers WHERE Country='Germany' and City='Berlin'
```

독일 국적이 아닌 고객의 정보를 가져오고 싶으면?
```SQL
SELECT * FROM Customers WHERE NOT Country='Germany'
```

독일 국적도 아니고 한국 국적도 아닌 고객의 정보를 가져오고 싶으면?
```SQL
SELECT * FROM Customers WHERE NOT Country='Germany' AND NOT Country='Korea'
```

<br>

### ORDER BY로 정렬하기

`SELECT` 문을 통해 선택된 데이터를 오름차순 혹은 내림차순으로 정렬 할 때, `ORDER BY`를 사용한다. `ORDER BY`에 정렬 기준이 될 행을 입력하고 그 뒤에 오름차순(ASC) 내림차순(DESC)을 결정해준다. 디폴트 시 자동으로 오름차순으로 정렬한다. 

```
SELECT <field_name> FROM <table_name> ORDER BY <field_name> ASC|DESC
```

국적을 기준으로 고객정보를 오름차순으로 정렬하고 고객이름을 기준으로 내림차순으로 정렬하고 싶다면 어떻게 해야할까?

```
SELECT * FROM Customers ORDER BY Country ASC CustomerName DESC
```

<br>

### INSERT INTO문
데이터베이스에서 데이터를 빼내올 수 있다면, 데이터를 집어 넣을 수도 있겠다. `INSERT INTO`문은 새로운 record를 해당 테이블에 삽입한다. 필드 이름을 입력하여 원하는 필드에만 값을 넣을 수 있고, 테이블 이름을 입력하여 전체 필드에 대해 값을 넣어 줄 수 있다. 이때, 필드의 순서와 입력하려는 값의 순서를 일치 시켜 주어야 한다.

```
INSERT INTO <table_name> (field_name) VALUES <values>
INSERT INTO <table_name> VALUES <values>
```

`INSERT INTO VALUES `로 고객이름, 연락 받을 이름, 주소, 도시, 우편번호, 국적을 삽입해보자.

```
INSERT INTO Customers (CustomerName, ContactNamse, Address, City, PostalCode, Country) VALUES ('Namwoo Seo', 'namwoo', 'Bundang-gu', 'Seoul', '13433', 'South Korea')
```

<br>

### Null Values

NUll Value는 value 값이 없음을 의미한다. NULL에 대한 판단에는 `IS NULL` `IS NOT NULL`연산자가 사용된다.

```
SELECT <field_names>FROM <table_name> WHERE <field_name> IS NULL
SELECT <field_names>FROM <table_name> WHERE <field_name> IS NOT NULL
```

주소가 없는 고객 정보를 가져오는 SQL문을 적어보자.
```
SELECT * FROM Customers WHERE Address IS NULL
```

<br>

### Update문

`UPDATE`문은 이미 존재하는 데이터를 수정활 때 사용한다. 
>조심해야할 점은 `WHERE`의 조건문을 생략하면 전체 데이터 해당 셋으로 업데이트 된다.

```
UPDATE <table_name> SET <ield1 = value1, field2= value2> WHERE <condition>
```

고객아이디 = 1 인 고객 정보에서 연락 할 이름과  도시 정보를 수정하자. 여기서 고객아이디는 고유하기 때문에 단 하나의 record에 대해서 변경된다. 

```
UPDATE Customers SET ContactName='Youngchan', City='Seville' WHERE CustomerID = 1
```

이번엔 국가가 한국인 고객정보에서 연락 할 이름과 주소를 변경해보자. 상식적으로 국가가 한국인 고객은 많이 존재한다. 그러므로 조건문에 맞는 모든 record에 대해 모두 업데이트가 일어난다.

```
UPDATE Customers SET ContactName='Namwoo', Address='Sinsa' WHERE Country='Korea'
```

<br>

### delete문

`DELETE`문에서 조심해야 할 점은 `WHERE` 조건문을 생략할 경우 테이블의 모든 데이터가 지워진다.

```
DELETE FROM <table_name> WHERE <condition>
```

고객 이름이 Alfreds Futterkiste인 고객 정보를 지워 보자.
```
DELETE FROM Customers WHERE CustomerName = 'Alfreds Futterkiste'
```

<br>

### TOP, LIMIT 그리고 ROWNUM 구문

`TOP, LIMIT, ROWNUM` 구문은 반환 할 record의 갯수를 지정해준다. 데이터 테이 위에서 부터 지정된 숫자만큼의 record가 반환된다. 이 구문들이 필요한 이유는 한번에 수 천개의 record가 반환 될 경우 메모리 문제와 같이 프로그램 자체에 문제를 발생 시키기 때문이다.

참고로 데이터베이스 종류에 따라 문법이 조금씩 다르다.

```
'''SQL Server '''
SELECT TOP <number> | PERCENT <field_names> FROM <table_name> WHERE <condition>
```

```
'''MySQL'''
SELECT <field_names> FROM <<table_name> WHERE <condition> LIMIT <number>
```

```
'''Oracle'''
SELECT <field_names> FROM <table_name> WHERE ROWNUM <= <number>
```

주어진 테이블에서 위로 부터 세개의 record를 반환하는 SQL문을 작성해보자.
```
SELECT TOP 3 * FROM Customers
```

국적이 독일인 고객 정보 테이블에서 위로 부터 50%에 해당되는 열들을 가져와보자.

```
SELECT TOP 50 | PERCENT FROM Customers WHERE Country='Germany'
```

위 예제를 MySQL 데이터베이스 문법으로 고쳐 보자. MySQL과 Oracle 데이터베이스에는 퍼센트 기능이 없는건가?
```
SELECT * FROM Customers WHERE Country = 'Germany' LIMIT  3 
```

<br>

### MIN(), MAX() 함수

`MIN()`함수는 입력된 Field에서 최소값을 반환하고 `MAX()`는 최대값을 반환한다.

```
SELECT MIN(<field_name> FROM <table_name> WHERE <condition>
SELECT MAX(<field_name> FROM <table_name> WHERE <condition>
```

가장 크고, 작은  고객아이디를 각각 반환해보자.

```
SELECT MIN(CustomerID) AS smallestID FROM Customers
SELECT MAX(CustomerID) AS biggestID FROM Customers
```

<br>

### COUNT() AVG() SUM() 함수
`COUNT()`는 해당 행과 조건문에 만족하는 열의 개수를 반환한다.
`AVG()`는 숫자로 이루어진 행의 평균 값을 반환한다.
`SUM()`은 숫자로 이루어진 행의 총 합을 반환한다.

```
SELECT COUNT(<field_name>) FROM <table_name> WHERE <condition>
SELECT AVG(<field_name>) FROM <table_name> WHERE <condition>
SELECT SUM(<field_name>) FROM <table_name> WHERE <condition>
```

#### 상품 테이블 Products

| ProductID | ProductName | SupplierID | CategoryID | Unit               | Price |
| --------- | ----------- | ---------- | ---------- | ------------------ | ----- |
| 1         | Chais       | 1          | 1          | 10 boxes x 20 bags | 18    |
| 2         | Chang       | 1          | 1          | 8 bottles          | 20    |
| 3         | Syrup       | 1          | 2          | 550 ml bottle      | 10    |
| 4         | Seasoing    | 2          | 2          | 20 boxes           | 25    |
| 5         | Mixed salt  | 2          | 1          | 1 L bottle         | 15    |

위 상품 테이블에서 상품 개수를 반환하는 쿼리문을 짜보자.
```
SELECT COUNT(ProductID) FROM Products
```

평균 상품 가격을 쿼리문으로 구해보자.
```
SELECT AVG(Price) FROM Products
```
 <br>

### LIKE 연산자
`WHERE`구문으로 지정 해준 행에서 `LIKE`연산자를 이용하여 입력한 패텬에 일치하는 열만을 가져온다.

```
SELECT <field_names> FROM <table_name> WHERE <field_name> LIKE <pattern>
```

패턴을 작성 할 때 두 가지 와일드카드가 사용된다. `%`는 0, 1 혹은 많은 문자 올 수 있음을 의미한다. `_`은 단 하나의 문자를 말한다.  또한 [charlist]를 통해 매칭하려는 문자의 집합을 정의하고 [!charlist] 혹은 [^charlist]로 매칭 하지않으려는 문자 집합을 정의한다. 아래는 여러가지 가능한 패턴의 예들이다. 

```
WHERE CustomerName LIKE 'a%'	a로 시작하는 모든 값
WHERE CustomerName LIKE '%a'	a로 끝나는 모든 값
WHERE CustomerName LIKE '%or%'	값에 or이 들어가는 값
WHERE CustomerName LIKE '_r%'	두 번째 자리에 r이 들어가는 값
WHERE CustomerName LIKE 'a_%_%'	a로 시작해서 최소한 3자리인 값
WHERE CustomerName LIKE 'a%o'	a로 시작해서 o로 끝나는 값
```

Customers 테이블에서 "ber"으로 시작하는 도시 이름을 가진 고객정보를 가져와보자.
```
SELECT * FROM Customers WHERE City LIKE 'ber%'
```
bsp로 시작하지 않는 도시이름을 가진 고객정보를 불러오자.
```
SELECT * FROM Customers WHERE City LIKE '[!bsp]%'
```

<br>

### IN 연산자
`IN`연산자는 `OR`연산자의 조합으로 이루어져있어,` WHERE`조건문으로 가져온 행에서 입력한 값 해당하는 열만을 가져온다. 아래 두 번쨰 기본형태는 하나의 쿼리문 안에 또 다른 쿼리문이 들어 갈 수 있음을 시사한다.

```
SELECT <field_names> FROM <table_name> WHERE <fiield_name> IN <values>
SELECT <field_names> FROM <table_name>  WHERE <field_name> IN <SELECT statement>
```

독일, 프랑스 혹은 영국 국적을 가진 고객 정보를 `IN` 연산자를 이용해 얻어오자.
```
SELECT * FROM Customers WHERE Country IN ('Germany', 'France', 'UK')
```

공급자와 같은 국적을 가진 고객정보 리스트르 가져오자. 여기서 공급자는 다른 데이터 테이블에 존재한다.
```
SELECT * FROM Customers WHERE Country IN (SELECT Country FROM Supplier)
```

<br>

###  BETWEEN 연산자
`BETWEEN`연산자는 입력한 범위내에 해당하는 열만을 추출한다. 범위에는 숫자, 문자 혹은 날짜가 올 수 있으며, 범위의 시작과 끝을 지정해주어야 한다. 여기서는 시작과 끝이 포함된 범위이다.

```
SELECT <field_names> FROM <table_name> WHERE <field_name> BETWEEN <value1> AND <value2>
```

가격이 10에서 20 사이인 제품의 정보을 가져와보라.
```
SELECT * FROM Prodcuts WHERE Price BETWEEN 10 AND 20
```
가격이 10에서 20사이가 아닌 제품의 정보는? 
```
SELECT * FROM Prodcuts WHERE Price NOT BETWEEN 10 AND 20
```

가격이 10에서 20이면서, 카테고리 아이디가 1,2,3이 아닌 제품의 정보를 꺼내오라.
```
SELECT * FROM Products WHERE (Price BETWEEN 10 AND 20) AND NOT CategoryID IN (1,2,3)
```

Carnarvon Tigers와 Mozzarella di Giovanni 사이에 있는 모든 제품 정보를 선택해보자.
```
SELECT * FROM Products WHERE ProductName BETWEEN 'Carnarvon Tiger' AND 'Mozzarella di Giovanni' ORDER BY ProductName ASC
```

Orders 테이블에서 2017년 1월 1일 부터 2017년 10월 6일 까지 주문 정보를 가져오자.
```
SELECT * FROM Orders WHERE OrderDate BETWEEN #01/01/2017# AND #06/10/2017#
```

<br>

### Aliases
Aliases는 테이블과 행에 임시의 이름을 부여한다. 종종 행의 이름을 그대로 쿼리문에 쓰면 가독서이 떨어지는데 Aliases로 좀더 쉽고 단순한 이름을 지어줄 수 있다.
```
SELECT <field_name> AS <alias_name> FROM <table_name>
```

고객 아이디와 고객 이름을 alias로 대체해보라.
```
SELECT CustomerID AS ID, CustomerName AS Customer FROM Customers
```

고객 이름과 연락 받을 이름을 alias로 바꾸어보라. 
>alias 이름에 공백이 있을 경우 " "나 [ ]꺽쇠괄호가 필요하다.
```
SELECT CustomerName AS Customer, ContactName AS [Contact Persion] FROM Customers
```

주소, 우편번호, 도시 그리고 국적을 연결해서 하나의 alias를 만들어 보자.
```
SELECT CustomerName, Address+', ' + PostalCode + ' ' + City + ', '+Country AS Address FROM Customers
```
MySQL 데이터베이스에서는 다음과 같이 쓴다.
```
SELECT CustomerName, CONCAT(Address+', ' + PostalCode + ' ' + City + ', '+Country) AS Address FROM Customers
```

이번것은 좀 재밌있는 예제이다. Customers 테이블과 Orders 테이블이 있다. Customers 테이블에서는 고객이름을 가져오고, Orders테이블에서는 주문 아이디와 주문 날짜를 가져오자. 가져온 행들에서 고객 이름이 Around the Horn이고 고객 아이디가 4인 고객의 기록을 꺼내오자.

```
SELECT Orders.OrderID, Orders.OrderDate, Customers.CustomerName FROM Customers, Orders WHERE Customers.CustomerName="Around the Horn" AND Customers.CustomerID=Orders.CustomerID
```
Alias를 써서 테이블 이름을 바꾸어 보자.
```sql
SELECT o.OrderID, o.OrderDate, c.CustomerName FROM Customers AS c, Orders AS o WHERE c.CustomerName = 'Around the Horn' AND c.CustomerID = o.CustomerID
```



### INNER JOIN
두 테이블에서 값이 서로 매칭되는 열만을 선택 반환할 떄 사용한다. 두 테이블의 교집합을 선별한다.

```sql
SELECT <field_names> FROM <table1> INNER JOIN <table2> ON <table1.field_name> = <table2.field_name>
```

Order 테이블의 고객 아이디와 Customers 테이블의 고객 아이디가 매칭 되는 열만을 
선택하고 OrderID와 CustomerName 행 정보만을 가져오자.

```sql
SELECT Orders.OrderID, Customers.CustomerName FROM Orders INNNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID
```

이번엔 세개의 테이블을 조인해보자. 위 예제에서 Order 테이블의 선박업체 아이디와 Shipper 테이블의 선박업체 아이디가 매칭 되는 열을 추가로 조인하자.

``` sql
SELECT FROM Orders INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID INNER JOIN Shippers ON Orders.ShipperID = Customers.CustomerID
```

<br>

### LEFT JOIN

`LEFT JOIN` 은 왼쪽 테이블을 기준으로 모든 record를 리턴 해주고, 매칭되는 오른쪽 테이블의 record를 붙여준다. 매칭되는 record가 없을 경우 NULL 값을 리턴한다.

```sql
SELECT <field_names> FROM <table1> LEFT JOIN <table2> ON <table1.field_name> = <table2.field_name>
```

Customers 테이블에서 모든 고객 이름과 Orders테이블에서 고객 아이디와 일치하는 주문 아이디 정보를 조인하고, 고객 이름순으로 조인된 테이블을 정렬해보자.

```sql
SELECT Customers.CustomerName, Orders.OrderID FROM Customers LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID ORDER BY Customers.CustomerName | ASC
```



<br>

### RIGHT JOIN

`RIGHT JOIN` 은 오른쪽 테이블을 기준으로 모든 record를 리턴 해주고, 매칭되는 왼쪽 테이블의 record를 붙여준다. 매칭되는 record가 없을 경우 NULL 값을 리턴한다.

```sql
SELECT <field_names> FROM <table1> RIGHT JOIN <table2> ON <table1.field_name> = <table2.field_name>
```

Employees 테이블에서 모든 직원들의 성과 이름을 리턴하고, EmployeeID에 매칭되는 OrderID 데이터를 오른쪽 조인하자. 그리고 OrderID로 오름차순 정렬을 해보자.

```SQL
SELECT Orders.OrderID, Employees.LastName, Employees.FirtstName FROM Orders RIGHT JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID ORDER BY Orders.OrderID
```

<br>

### FULL OUTER JOIN

`FULL OUTER JOIN`은 왼쪽 테이블에 매칭되는 모든 열과 오른쪽 테이블에 매칭되는 모든 열을 리턴한다.

```sql
SELECT <field_names> FROM <table1> FULL OUTER JOIN <table2> ON <table1.field_name> = <table2.field_name> 
```

`FULL OUTER JOIN`을 사용하여 Custmers의 고객 아이디에 매칭 되는 모든 고객 이름과 주문 아이디를 리턴하고, Orders의 고객 아이디에 매칭 되는 모든 주문 아이디와 고객 이름을 리턴하자.

```SQL
SELECT Cusotmers.CustomerName, Orders.OrderID FROM Customers FULL OUTER JOIN Orders ON Customers.CustomersID = Orders.CustomersID ORDER BY Orders.OrderID
```

<br>

### SELF JOIN

자기 자신의 테이블을 사용하여 조인 명령을 수행한다. 한 테이블내에서 일정한 관계에 있는 정보들을 테이블로 나타낼 수 있다.

```sql
SELECT <field_names> FROM <table1 T1> <table1 T2> WHERE <condition>
```

 Customers 테이블내에서 고객 아이디가 다르고 도시가 같은 고객의 짝을 모두 찾아보자.  `JOIN` 명령이 A, B 두 테이블 모두에게 적용되기 때문에 내용은 같고 순서만 다른 짝이 나온다.

```sql
SELECT A.CustomerName AS CustomerName1, B.CustomerName AS CustomerName2, A.City FROM Customers A, Customers B WHERE A.CustomerID <> B.CustomerID AND A.City = B.City ORDER BY A.City
```

<br>

### UNION

`UNION` 연산자를 이용하여 두 개 이상의 `SELECT`문의 result-set을 하나로 합해 줄 수 있다. 각각의 `SELECT`문은 같은 개수의 선택된 행을 가지고 있어야하고, 포함하는 데이터 타입이 비슷해야한다. 그리고 각각의 result-set에는 같은 정렬 방식이 적용되야 한다.

```sql
SELECT <field_names> FROM <table1> UNION SELECT <field_names> FROM <table2> 
```

#### UNION ALL

`UNION`하는 과정에서 중복된 값을 허용하고 싶을 때는 `UNION ALL`을 사용한다.

```sql
SELECT <field_names> FROM <table1> UNION ALL SELECT <field_names> FROM <table2>
```

Customers 테이블과 Suppliers 테이블에서 UNION 연산자를 써서 모든 도시 정보를 가져와 합해보자.

```sql
SELECT City FROM Customers UNION SELECT City FROM Suppliers ORDER BY City
```

위 예제에서 `WHERE`조건문을 써서 독일 국적을 가진 고객의 모든 도시 정보를 가져오자. (중복된 값을 허용하라)  

```sql
SELECT City FROM Customers WHERE Country ='Germany' UNION ALL SELECT City FROM Suppliers WHERE Country ='Germany' ORDER BY City
```



<br>

### GROUP BY 문

`GROUP BY`문은 보통 `COUNT, MAX, MIN, SUM, AVG` 함수들과 같이 쓰인다. "나라 별로 고객의 수가 얼마나 되는지 알고 싶으면 어떻게 할까?" 먼저 가져온 나라 데이터  행에서 나라별로 그룹화 시킨 뒤, 그 숫자를 세면 될 것 이다.

```SQL
SELECT Country, COUNT(CustomerID) FROM Customers GROUP BY Country ORDER BY COUNT(CustomerID) ASC
```

`GROUP BY`와 `JOIN`문을 같이 써보자. Orders와 Shippers 두 테이블을 조인하여 각 선박업체가 얼만큼의 주문량을 가지고 있는지 알아보자.

```sql
SELECT Shippers.ShipperName, COUNT(Order.OrderID) FROM Orders LEFT JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID GROUP BY ShipperName
```

<br>

### HAVING 구문

`HAVING` 구문은 `COUNT, MAX, MIN, SUM, AVG` 함수와 같이 쓸 수 있는 조건문을 제공한다. `WHERE`가 위 함수와 같이 쓰이지 않기 때문에 탄생했다.

Customers 테이블에서 나라별 고객 수가 5명을 초과하는 데이터 테이블을 만들어 보라.

```SQL
SELECT Country, COUNT(CustomerID) FROM Customers GROUP BY Country HAVING COUNT(CustomerID) > 5
```

위 예제를 고객 수에 대해 내림차순을 정렬 해보라.

```SQL
SELECT Country, COUNT(CustomerID) FROM Customers GROUP BY Country HAVING COUNT(CustomerID) > 5 ORDER BY COUNT(CustomerID) DESC
```

접수한 주문량이 10개를 초과한 직원의 성명과 주문량을 표시하는 테이블을 작성하라.

```SQL
SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberofOrders FROM Orders INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID GROUP BY LastName HAVING COUNT(Orders.OrderID) > 10
```

'Davolio'와 'Fuller' 직원의 주문량이 25개 초과했는지 확인하고, 초과 했을 시 해당 직원의 주문량을 보여주는 테이블을 작성하라. 

```SQL
SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberofOrders FROM Orders INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID WHERE LastName = 'Davolio' or LastName='Fuller' Last GROUP BY LastName HAVING COUNT(Orders.OrderID)
```

<br>

### EXISTS 연산자

`EXISTS` 연산자는 서브쿼리문을 테스트하는 사용된다. 서브쿼리문이 하나 이상의 레코드를 리턴하는 경우  `EXISTS`는  True을 리턴한다. 그러나 단순히 True만을 리턴해주는 것이 아니라, 메인 쿼리에 서브 쿼리의 조건문을  적용 시킬 수 있다.

가격이 20 미만인 제품을 가지는 공급업체의 리스트를 리턴해보자.

```sql
SELECT SupplierName FROM Suppliers WHERE EXISTS (SELECT ProductName FROM Products WHERE SupplierID = Suppliers.SupplierID AND Price < 20)
```

가격이 20 인 제품을 가고 있는 공급업체의 리스트를 리턴해보자.

```sql
SELECT SupplierName FROM Suppliers WHERE EXISTS (SELECT ProductName FROM Products WHERE SupplierID = Suppliers.SupplierID AND Price = 20)
```

<br>

### ANY 그리고 ALL 연산자

`ANY`와 `ALL` 연산자는 `WHERE`과 `HAVING`구문과 같이 사용된다.  `ANY`는 서브쿼리의 하나 이상의 값이 조건문과 일치하면 True를 리턴한다. `ALL`은 서브쿼리의 모든 값이 조건문과 일치하면 True를 리턴한다.

OrderDetails 테이블에서  주문 수량이 10개인 제품만을 확인하고 Products 테이블에서  해당 제품 이름을 리턴하라.

```sql
SELECT ProductName FROM Products WHERE ProductID = ANY (SELECT ProductID FROM OrderDetails WHERE Quantity = 10) 
```

OrderDetails 에 있는 모든 주문의 주문 수량이 10개 을 때만,  Produects에서 제품 이름을 리턴하라.

```sql
SELECT ProductName FROM Products WHERE ProductID = ALL (SELECT ProductID FROM OrderDetails WHERE Quantity = 10)
```

<br>

### SELECT INTO 문

`SELECT INTO`는 한 테이블에서 데이터를 복사해서 다른 테이블로 붙여 넣을 때 사용한다.

```sql
SELECT <field_names> INTO <newtable> IN <externaldb> FROM <oldtable> WHERE <conditions>
```

Customers 테이블의 모든 데이터를 복사하여  Customerbackup 테이블에 저장하자.

```sql
SELECT * INTO Customerbackup FROM Customers
```

Customers 테이블에서 독일 국적을 가진 고객의 정보를 CustomerGermany 테이블로 복사해보자.

```sql
SELECT * INTO CustomerGermnay FROM Customers WHERE Country = 'Germany'
```

 Customers와 Orders 두 테이블에서 CustomerID가 같은 정보를 LEFT JOIN한 뒤, 고객 이름과 주문 아이디 행만을  Customerbackup 테이블에 복사해오자.

```sql
SELECT Customers.CustomerName, Orders.OrderID INTO Customerbackup FROM Customers LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID
```

SELECT INTO 문을 이용해서 기존의 테이블과 구조가 같지만 빈 테이블을 만들 수 있다.

```SQL
SELECT * INTO <newtable> FROM <oldtable> WHERE 1 = 0
```

<br> 

### INSERT INTO SELECT 문

`SELECT INTO` 문과 다르게 새로운 테이블을 생성하지 않고, 기존의 테이블에 데이터를 복사 붙여넣기 한다. 소스 테이블(복사)과 타겟 테이블(붙여넣기)안의 데이터 타입이 일치해야한다. 타겟 테이블에 이미 들어가 있는 데이터에 대해서는 영향을 주지 못한다.

```sql
INSERT INTO <table2> SELECT * FROM <table1> WHERE <conditions>
```

```sql
INSERT INTO <table2> (files_names) SELECT <file_names> FROM <table1> WHERE <conditions>
```

Suppliers에서 공급업체 이름, 도시, 나라 정보를 복사해서  Customers테이블에 붙여넣자.

```sql
INSERT INTO Customers (CustomerName, City, Country) SELECT SuppliersName, City, County FROM Suppliers
```

Suppliers에서 국적이 독일인 공급업체 이름, 도시, 나라 정보를 복사해서 Customers테이블에 붙여넣자.

```sql
INSERT INTO Customers (CustomerName, City, Country) SELECT SupplierName, City, Country FROM Suppliers WHERE Country = 'Germany'
```

<br>

###  IFNULL(), ISNULL(), COALESCE(),  NVL() 함수

`IFNULL(expression, value)`: 만약 expression이 NULL인 경우 value를 리턴한다.

`COALESCE(value1, value2, ...)`: value list에서 첫 번째 NON NULL 값을 리턴한다.

`ISNULL(expression, value)`: SQL server에서 사용되며,  IFNULL()과 기능이 같다.

`NVL(expression, value)`  : Oracle에서 사용되며, IFNULL()과 기능이 같다.

아래 테이블에서 UnitsOnOrder와 같이 선택사항인 경우 해당 값으로 NULL이 들어가 있다.

| ID   | ProductName | UnitsPrice | UnitsInStock | UnitsOnOrder |
| ---- | ----------- | ---------- | ------------ | ------------ |
| 1    | Jarlsberg   | 10.45      | 16           | 15           |
| 2    | Mascarpone  | 32.56      | 23           |              |
| 3    | Gorgonzola  | 15.67      | 9            | 20           |

아래 같이 NULL 값으로 연산을 하면 결과로 NULL 값이 나온다. 상식적으로 우리는 0 값을 얻고 싶다.

```sql
SELECT ProductName, UnitPrice * (UnitsInStock + UnitsOnOrder)
FROM Products;
```

<br>

### Comments

당신이 아는 그 주석 기능이다.

한 줄 주석의 시작은  `--`로 시작하며 끝은 줄 바꿈을 해주어야 한다. 긴 주석을 달고 싶으면 `/* */`을 사용하자. 
