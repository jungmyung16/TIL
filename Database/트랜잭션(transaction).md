## 트랜잭션(Transaction) 개요

- 트랜잭션은 **데이터베이스에서 하나 이상의 작업을 논리적으로 묶어서 하나의 단위로 처리**하는 개념
- 여러 작업 중 하나라도 실패하면 전체 작업이 실패한 것으로 간주하고, 모두 성공하면 최종 반영하여 데이터의 신뢰성을 유지
- COMMIT
  - 트랜잭션의 모든 변경사항을 데이터베이스에 영구적으로 저장
- ROLLBACK
  - 트랜잭션의 변경사항을 모두 취소, 데이터베이스를 트랜잭션 시작 이전의 상태로 되돌리는 것
- START TRANSACTION
  - 트랜잭션의 경계를 명확히 하고, 트랜잭션이 시작되는 시점을 명시
  - COMMIT 명령이 실행될 때까지 작업 반영x

> 예시) **은행 시스템에서의 이체**  
> 사용자가 계좌 A에서 계좌 B로 돈을 이체할 때:  
> ① A 계좌에서 금액 차감  
> ② B 계좌에 금액 추가  
> 두 작업 모두 성공해야만 트랜잭션이 완료되며, 하나라도 실패하면 처음 상태로 되돌아가야 함.

## ![Image](https://github.com/user-attachments/assets/9d809f29-4aca-4590-b123-a55550225614)

## 트랜잭션의 4가지 핵심 특성(ACID)

### ① 원자성(Atomicity)

- 트랜잭션의 모든 작업이 완벽히 수행되거나 전혀 수행되지 않아야 하는 성질
- 중간 단계가 존재하지 않음
- **은행 예시:** 이체 시 돈이 빠져나갔는데 상대방 계좌에 들어가지 않은 상황이 발생하면 안 됨.

### ② 일관성(Consistency)

- 트랜잭션이 완료된 후 데이터베이스가 항상 유효하고 일관된 상태를 유지해야 하는 성질
- 데이터베이스의 제약 조건을 항상 만족해야 함.
- **은행 예시:** 이체 후 계좌의 잔액이 음수로 표시되는 상황이 발생하면 안 됨.

### ③ 격리성(Isolation)

- 다수의 트랜잭션이 동시에 실행되더라도 서로 영향을 미치지 않고 독립적으로 수행되는 성질
- 동시 처리되는 트랜잭션은 서로 중간 결과를 볼 수 없어야 함.
- **은행 예시:** 두 고객이 동시에 동일한 계좌에서 출금할 때 서로 간섭하지 않아야 함.

### ④ 지속성(Durability)

- 트랜잭션이 정상적으로 완료(COMMIT)된 후 그 결과가 영구적으로 보장되어야 하는 성질
- 완료된 작업은 시스템이 종료되거나 장애가 발생해도 반드시 유지되어야 함.
- **은행 예시:** 고객이 송금 완료 후 은행 시스템이 갑자기 종료되더라도 이미 송금된 금액은 정상적으로 유지되어야 함.
  ![Image](https://github.com/user-attachments/assets/99c246b7-13fb-4ca8-8062-20a1f61a3c71)

---

## 💻 MariaDB에서의 트랜잭션 실습 예제

### (1) 실습 테이블 생성 및 데이터 입력

```sql
-- 계좌 정보를 저장할 accounts 테이블 생성
CREATE TABLE accounts (
    id INT PRIMARY KEY AUTO_INCREMENT,   -- 고유 ID (자동 증가)
    name VARCHAR(50),                    -- 계좌 소유자 이름
    balance INT                          -- 계좌 잔액
);

-- 계좌 정보 예시 데이터 입력
INSERT INTO accounts (name, balance)
VALUES ('Alice', 1000),  -- Alice 계좌, 잔액 1000원
       ('Bob', 500);     -- Bob 계좌, 잔액 500원
```

---

### (2) 트랜잭션을 이용한 이체 실습 SQL 예제

```sql
-- 트랜잭션 시작
START TRANSACTION;

-- Alice의 계좌에서 Bob의 계좌로 200원을 이체하는 작업 수행
-- [1단계] Alice 계좌에서 잔액을 200원 차감
UPDATE accounts
SET balance = balance - 200
WHERE name = 'Alice';

-- [2단계] Bob 계좌로 잔액 200원 입금
UPDATE accounts
SET balance = balance + 200
WHERE name = 'Bob';

-- [3단계] 변경된 잔액 확인 (임시 상태, 아직 확정 전)
SELECT * FROM accounts;

-- 위 작업이 모두 성공했을 경우 트랜잭션을 완료하고 변경사항 확정
COMMIT;

-- 만약 작업 중 오류가 발생하거나 결과가 원치 않으면 작업 취소
-- ROLLBACK; (오류 발생 시 사용)
```

---

## **요약**

- **원자성(Atomicity)**: 전부 성공 or 전부 실패
- **일관성(Consistency)**: 트랜잭션 전후 데이터 무결성 유지
- **격리성(Isolation)**: 다수의 트랜잭션 동시 수행 시 독립적 실행 보장
- **지속성(Durability)**: 완료된 트랜잭션 결과 영구 유지

→ MariaDB에서는 다음 명령어를 이용하여 트랜잭션을 제어함:

- **시작:** `START TRANSACTION`
- **완료(성공 시):** `COMMIT`
- **취소(실패 시):** `ROLLBACK`
  ![Image](https://github.com/user-attachments/assets/442ab008-fcf8-46c1-903e-0f76ba0e473d)
