아래는 **Markdown (`.md`)** 파일 형식으로 작성된 **SQL 기본 명령어 정리 문서**입니다.  
이 파일을 그대로 **GitHub에 업로드**하거나 **Markdown 지원되는 문서 뷰어**에서 볼 수 있습니다.

# 📌 SQL 기초 명령어 정리

## 1. 데이터 조회 (SELECT)
### 📌 모든 데이터 조회 (`SELECT *`)
```sql
SELECT * FROM table_name;
```

### 📌 특정 컬럼 조회
```sql
SELECT column1, column2 FROM table_name;
```

### 📌 조건 조회 (`WHERE`)
```sql
SELECT * FROM table_name WHERE condition;
```
**예제:** 나이가 25 이상인 사용자 가져오기
```sql
SELECT * FROM Users WHERE age >= 25;
```

### 📌 중복 제거 (`DISTINCT`)
```sql
SELECT DISTINCT column_name FROM table_name;
```
**예제:** `Users` 테이블에서 중복된 `city` 값 제거하고 가져오기
```sql
SELECT DISTINCT city FROM Users;
```

### 📌 정렬 (`ORDER BY`)
```sql
SELECT * FROM table_name ORDER BY column_name ASC|DESC;
```
**예제:** 나이를 기준으로 오름차순 정렬
```sql
SELECT * FROM Users ORDER BY age ASC;
```

### 📌 상위 N개 데이터 가져오기 (`LIMIT`)
```sql
SELECT * FROM table_name LIMIT n;
```
**예제:** `Users` 테이블에서 상위 5개 데이터 가져오기
```sql
SELECT * FROM Users LIMIT 5;
```

---

## 2. 데이터 삽입 (INSERT)
```sql
INSERT INTO table_name (column1, column2) VALUES (value1, value2);
```
**예제:** `Users` 테이블에 새로운 사용자 추가
```sql
INSERT INTO Users (name, age, city) VALUES ('Alice', 25, 'Seoul');
```

---

## 3. 데이터 수정 (UPDATE)
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
**예제:** `Users` 테이블에서 Alice의 나이를 26으로 변경
```sql
UPDATE Users SET age = 26 WHERE name = 'Alice';
```

⚠️ **주의:** `WHERE` 조건을 추가하지 않으면 **모든 데이터가 변경될 수 있음!**

---

## 4. 데이터 삭제 (DELETE)
```sql
DELETE FROM table_name WHERE condition;
```
**예제:** `Users` 테이블에서 Alice 삭제
```sql
DELETE FROM Users WHERE name = 'Alice';
```

⚠️ **주의:** `WHERE`을 지정하지 않으면 **테이블의 모든 데이터가 삭제됩니다!**
```sql
DELETE FROM Users;  -- 모든 데이터 삭제됨 (주의!)
```

---

## 5. 테이블 생성 및 관리
### 📌 새로운 테이블 생성 (`CREATE TABLE`)
```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    ...
);
```
**예제:** `Users` 테이블 생성
```sql
CREATE TABLE Users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50),
    age INT,
    city VARCHAR(50)
);
```

### 📌 테이블 삭제 (`DROP TABLE`)
```sql
DROP TABLE table_name;
```
**예제:** `Users` 테이블 삭제
```sql
DROP TABLE Users;
```

⚠️ **주의:** `DROP TABLE`을 실행하면 테이블 자체가 삭제되며, 복구할 수 없음.

### 📌 테이블 구조 변경 (`ALTER TABLE`)
**컬럼 추가**
```sql
ALTER TABLE Users ADD email VARCHAR(100);
```

**컬럼 삭제**
```sql
ALTER TABLE Users DROP COLUMN email;
```

---

## 6. 데이터 검색 (LIKE, IN, BETWEEN)
### 📌 부분 검색 (`LIKE`)
```sql
SELECT * FROM table_name WHERE column_name LIKE pattern;
```
**예제:** `Users` 테이블에서 'A'로 시작하는 이름 찾기
```sql
SELECT * FROM Users WHERE name LIKE 'A%';
```

**예제:** 'li'가 포함된 이름 찾기
```sql
SELECT * FROM Users WHERE name LIKE '%li%';
```

### 📌 여러 개의 값 중 하나 검색 (`IN`)
```sql
SELECT * FROM table_name WHERE column_name IN (value1, value2, value3);
```
**예제:** 서울 또는 부산에 사는 사용자 찾기
```sql
SELECT * FROM Users WHERE city IN ('Seoul', 'Busan');
```

### 📌 범위 검색 (`BETWEEN`)
```sql
SELECT * FROM table_name WHERE column_name BETWEEN value1 AND value2;
```
**예제:** 나이가 20에서 30 사이인 사용자 찾기
```sql
SELECT * FROM Users WHERE age BETWEEN 20 AND 30;
```

---

## 7. 그룹화 및 집계 함수
### 📌 그룹화 (`GROUP BY`)
```sql
SELECT column_name, COUNT(*) FROM table_name GROUP BY column_name;
```
**예제:** `Users` 테이블에서 도시별 사용자 수 구하기
```sql
SELECT city, COUNT(*) FROM Users GROUP BY city;
```

### 📌 조건이 있는 그룹화 (`HAVING`)
```sql
SELECT column_name, COUNT(*) FROM table_name GROUP BY column_name HAVING condition;
```
**예제:** 사용자가 2명 이상 있는 도시만 가져오기
```sql
SELECT city, COUNT(*) FROM Users GROUP BY city HAVING COUNT(*) >= 2;
```

---

## 8. 조인 (JOIN)
### 📌 `INNER JOIN` (두 테이블의 공통 데이터 조회)
```sql
SELECT A.column, B.column
FROM table1 A
INNER JOIN table2 B
ON A.common_column = B.common_column;
```
**예제:** 고객과 주문 정보를 가져오기
```sql
SELECT Customers.name, Orders.order_date
FROM Customers
INNER JOIN Orders
ON Customers.customer_id = Orders.customer_id;
```

---

## 9. 뷰 (VIEW)
### 📌 뷰 생성 (`CREATE VIEW`)
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**예제:** 나이가 25 이상인 사용자만 포함하는 뷰 생성
```sql
CREATE VIEW AdultUsers AS
SELECT name, age FROM Users WHERE age >= 25;
```

### 📌 뷰 조회
```sql
SELECT * FROM view_name;
```
**예제:** `AdultUsers` 뷰 조회
```sql
SELECT * FROM AdultUsers;
```

