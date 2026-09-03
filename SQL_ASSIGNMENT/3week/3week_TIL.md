# SQL_ADVANCED 3주차 정규 과제 

📌SQL_ADVANCED 정규과제는 매주 정해진 분량의 『*혼자 공부하는 SQL*』 을 읽고 학습하는 것입니다. 이번주는 아래의 **SQL_ADVANCED_3rd_TIL**에 나열된 분량을 읽고 공부하시면 됩니다.

아래의 문제를 풀어보며 학습 내용을 점검하세요. 문제를 해결하는 과정에서 개념을 스스로 정리하고, 필요한 경우 제시된 강의를 참고하여 보완하는 것이 좋습니다.

<!-- 강의 링크는 아래와 같습니다.
https://www.youtube.com/watch?v=1YmWy-7-OhQ&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=10
https://www.youtube.com/watch?v=tuQFkzjqEGw&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=11
https://www.youtube.com/watch?v=IOCsreDYqFE&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=12
-->

**교재 실습 예제 파일은 07_SQL_ADVANCED_Template 레포지토리의 src 폴더에 업로드되어 있습니다. market_db 파일도 해당 폴더에 함께 포함되어 있으니 참고하시기 바랍니다.**

**👀(수행 인증샷은 필수입니다.)** 

## SQL_ADVANCED_3rd_TIL

### 4장 SQL 고급 문법
#### 01. MySQL의 데이터 형식
#### 02. 두 테이블을 묶는 조인
#### 03. SQL 프로그래밍 


## Study Schedule

| 주차  | 공부 범위     | 완료 여부 |
| ----- | ------------- | --------- |
| 1주차 | p.24~99    | ✅         |
| 2주차 | p.102~155   | ✅         |
| 3주차 | p.158~213  | ✅         |
| 4주차 | p.216~271 | 🍽️         |
| 5주차 | p.274~327 | 🍽️         |
| 6주차 | p.330~369 | 🍽️         |
| 7주차 | p.372~407 | 🍽️         |


<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 학습 내용 정리

## 1. MySQL의 데이터 형식

- 정수형 타입에는 TINUINT, SMALLINT, INT, BIGINT가 있다.
- 같은 범위에서 음수는 안 쓰고 양수만 쓰고 싶을 때에는 뒹 UNSIGNED를 붙이면 된다.

- 문자형 타입에는 CHAR와 VARCHAR가 있다. CHAR 고정적으로 글자 크기를 잡기 때문에 정한 크기보다 작은 수의 문자를 입력할 경우 메모리를 낭비하게 될 수 있다. VARCHAR는 내부적으로 필요한 공간만 확보하기 때문에 조금 더 효율적이다. 하지만 CHAR에 비해 속도가 조금 더 느리다는 단점이 있다.

- 긴 글을 입력할 때는 LONGTEXT를  쓴다.

- 실수형 타입에는 FLOAT와 DOUBLE이 있다. FLOAT는 4바이트, DOUBLE은 8바이트를 차지한다.

- 날짜형에는 DATE, TIME, DATETIME이 있다. 

- SQL에서도 변수를 지정할 수 있는데, @뒤에 원하는 변수명을 적어서 값을 대입하면 된다. (EX. SET @count = 3;)
- 지정된 변수는 워크벤치를 닫았다 열면 유지가 되지 않다. 임시적으로만 쓸 수 있다.

- 데이터의 형 변환에는 명시적 변환과 암시적 변환이 있다.
- 명시적 형 변환: CAST과 CONVERT는 거의 비슷하지만 쓰이는 방식이 약간 다르다.



> **확인문제: 다음 보기에서 데이터 형식의 변환에 사용되는 함수를 2개 고르세요.**

보기는 아래와 같습니다.
```
CONVERT() / DATA() / CAST() / MOVE() / TYPE() / SUM() / AVG() / CURRENT_DATE()
```

```
CONVERT(), CAST()
```

dsf

## 2. 두 테이블을 묶는 조인

- 기본키는 테이블의 컬럼 중 중복되는 값이 없어야 하고 빈 값도 허용하지 않는 컬럼을 말한다. 

- 내부 조인은 조인 중 가장 많이 사용되는 문법으로, 대부분 2개 테이블을 조합해서 사용한다. 
- WHERE 조건이 있다면 해당 조건에 맞는 행만 출력이 된다.

- 외부 조인은 두 테이블을 조인할 때 필요한 내용이 한쪽 테이블에만 있어도 결과를 추출할 수 있는 기능이다.


> **확인문제: 다음 SQL은 회원으로 가입만 하고, 한 번도 구매한 적이 없는 회원의 목록을 조회하는 쿼리입니다. 빈칸에 들어갈 가장 적절한 구문을 고르세요..**

```sql
SELECT DISTINCT M.mem_id, B.prod_name, M.mem_name, M.addr
  FROM member M
    LEFT OUTER JOIN buy B
    ON M.mem_id = B.mem_id
  __________
  ORDER BY M.mem_id;
```
보기는 아래와 같습니다.
```
1. JOIN B.prod_name IS NULL
2. LIMIT B.prod_name IS NULL
3. HAVING B.prod_name IS NULL
4. WHERE B.prod_name IS NULL
```
```
정답은 4번이다. buy 테이블에서 한 번도 구매한 적이 없는 사람을 찾기 위해서는 buy 테이블에서 가져오는 prod_name이라는 정보가 빈칸, 즉 NULL이어야 한다. HAVING은 그룹화 후 그룹 단위로 필터링하는 문법이므로 여기서는 사용되지 않는다.
```

## 3. SQL 프로그래밍 

- 이번 장의 내용은 대부분 컴퓨터 언어를 다루는 것과 비슷하다.

조건문
- IF문은 파이썬이나 C언어와 비슷하게 조건문이 맞을 때 출력되는 결과를 정해주는 함수이다.
- IF ~ ELSE 문은 참일 때와 거짓일 때에 실행해야 될 결과들이 각각 있을 때 사용한다. 
- CASE는 참과 거짓뿐만이 아니라 여러 가지 조건 중에서 선택해야 하는 경우에 사용한다.

반복문
- WHILE

동적 SQL
- PREPARE / EXECUTE
-  실시간으로 쿼리문을 변형시키면서 결과물을 출력할 수 있다.
- PREPARE에서 ?에 들어갈 값을 EXECUTE에서 지정해 줄 수 있다.


> **확인문제: 다음은 CASE 문의 형식입니다. 빈칸에 들어갈 가장 적절한 명령어를 보기에서 고르세요..**

```sql
CASE
    (1) 조건 THEN
        SQL문장들1
    ELSE
        SQL문장들4
END (2);
```

보기는 아래와 같습니다.
```
WHEN / THEN / CURRENT / DATE / TIME / IF / END IF / CASE
```

```
여기에 답을 적어주세요!
(1) WHEN
(2) CASE
```


---

# 2️⃣ 실습과제

## 1. 데이터베이스 구축

아래 코드를 MySQL Workbench에 붙여넣은 후,  
**전체 드래그 → 실행 (Ctrl + shift + Enter)** 하여 데이터베이스를 구축하세요.

```sql
-- 1. 데이터베이스 생성
CREATE DATABASE IF NOT EXISTS week3_db;

-- 2. 사용할 데이터베이스 선택
USE week3_db;

-- 3. 기존 테이블 삭제 (초기화용)
DROP TABLE IF EXISTS orders;
DROP TABLE IF EXISTS customers;

-- 4. 테이블 생성 (조인 실습용)
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(20),
    signup_date_str VARCHAR(8) 
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,           
    order_date_str VARCHAR(8), 
    amount_str VARCHAR(10)     
);

-- 5. 데이터 삽입
INSERT INTO customers VALUES
(1, '진아', '20240218'),
(2, '혜인', '20230302'),
(3, '규서', '20220315'),
(4, '규영', '20210401'),
(5, '철원', '20230909'),
(6, '예운', '20240201'),
(7, '민서', '20220320'),
(8, '광윤', '20240105'); -- 주문 없는 고객(외부 조인용)

INSERT INTO orders VALUES
(101, 1, '20240220', '12000'),
(102, 1, '20240303', '30000'),
(103, 2, '20240111', '15000'),
(104, 3, '20221201', '9000'),
(105, 5, '20231111', '20000'),
(106, 7, '20220707', '5000'),
(107, 99, '20240210', '7000'); -- 고객 테이블에 없는 customer_id (외부 조인용)
```

## 2. 실습 문제

다음 SQL 문을 작성하고 실행 결과를 확인 후 인증 사진을 아래에 업로드하세요.

1. **데이터 형식 변환**
   - orders 테이블의 `order_date_str`을 DATE 형식으로 변환하여 조회하시오.
   (힌트: STR_TO_DATE 사용)

   ![alt text](images_3/image.png)


2. **데이터 형식 변환**
   - orders 테이블의 `amount_str`을 숫자형으로 변환하여 조회하시오.

   ![alt text](images_3/image-1.png)


3. **내부 조인 (INNER JOIN)**
   - customers와 orders를 customer_id 기준으로 내부 조인하여
     고객 이름(name)과 주문 번호(order_id)를 함께 조회하시오.

     ![alt text](images_3/image-2.png)

4. **외부 조인 (LEFT JOIN)**
   - customers를 기준으로 LEFT JOIN을 수행하여,
     주문이 없는 고객도 함께 조회하시오.

     ![alt text](images_3/image-3.png)

5. **스토어드 프로시저 (IF문 사용)**
   - 입력받은 금액이 10000 이상이면 '고액 주문',
     그렇지 않으면 '일반 주문'을 출력하는
     프로시저를 생성하시오.
   - 생성 후 CALL로 실행 결과를 확인하시오.

   ![alt text](images_3/image-4.png)


### 🎉 수고하셨습니다.






