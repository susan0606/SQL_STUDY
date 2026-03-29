# SQL_ADVANCED 4주차 정규 과제 

📌SQL_ADVANCED 정규과제는 매주 정해진 분량의 『*혼자 공부하는 SQL*』 을 읽고 학습하는 것입니다. 이번주는 아래의 **SQL_ADVANCED_4th_TIL**에 나열된 분량을 읽고 공부하시면 됩니다.

아래의 문제를 풀어보며 학습 내용을 점검하세요. 문제를 해결하는 과정에서 개념을 스스로 정리하고, 필요한 경우 제시된 강의를 참고하여 보완하는 것이 좋습니다.

<!-- 강의 링크는 아래와 같습니다.
https://www.youtube.com/watch?v=DMNpkj_bZIs&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=13
https://www.youtube.com/watch?v=BUHj-behLyc&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=14
https://www.youtube.com/watch?v=JrXWxku7ZIM&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=15
-->

**교재 실습 예제 파일은 07_SQL_ADVANCED_Template 레포지토리의 src 폴더에 업로드되어 있습니다. market_db 파일도 해당 폴더에 함께 포함되어 있으니 참고하시기 바랍니다.**

**👀(수행 인증샷은 필수입니다.)** 

## SQL_ADVANCED_4th_TIL

### 5장 테이블과 뷰
#### 01. 테이블 만들기
#### 02. 제약조건으로 테이블을 견고하게
#### 03. SQL 가상의 테이블: 뷰 


## Study Schedule

| 주차  | 공부 범위     | 완료 여부 |
| ----- | ------------- | --------- |
| 1주차 | p.24~99    | ✅         |
| 2주차 | p.102~155   | ✅         |
| 3주차 | p.158~213  | ✅         |
| 4주차 | p.216~271 | ✅         |
| 5주차 | p.274~327 | 🍽️         |
| 6주차 | p.330~369 | 🍽️         |
| 7주차 | p.372~407 | 🍽️         |


<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 학습 내용 정리

## 1. 테이블 만들기 

<!-- 이번 챕터에서 제시된 실습을 흐름에 맞게 진행한 후, 실습 과정이 보일 수 있도록 인증 사진을 2장 이상 제출해 주세요. -->

![alt text](images_4/image-5.png)

![alt text](images_4/image-6.png)

![alt text](images_4/image-7.png)


## 2. 제약조건으로 테이블을 견고하게 

<!-- 제약조건에 관해 배우게 된 점을 적어주세요. -->

- 기본 키 (primary key): 데이터를 식별하는 고유 번호 (예: 학번, 아이디). 중복 불가, null 불가. (테이블당 1개만 설정 가능하며, 설정 시 클러스터형 인덱스가 자동 생성됨)

- 외래 키 (foreign key): 두 테이블의 관계를 연결하는 다리 역할. 부모(기준) 테이블의 기본 키나 고유 키를 참조해야 함.

- 고유 키 (unique): 중복을 허용하지 않는 유일한 값. (기본 키와 비슷하지만 null 값을 허용한다는 점이 다름)

- 체크 (check): 입력되는 데이터가 조건에 맞는지 점검 (예: 키는 0보다 커야 함).

- 기본값 (default): 값을 따로 입력하지 않았을 때 자동으로 채워질 값 지정.

- not null: 비어있는 값(null)을 절대 허용하지 않음.

- 테이블 삭제 순서: 기본 키-외래 키로 연결된 부모-자식 테이블이 있다면, 삭제할 때는 반드시 자식 테이블(외래 키가 있는 곳)을 먼저 삭제하고, 부모 테이블(기본 키가 있는 곳)을 나중에 삭제해야 함.


> **확인문제: 다음 보기 중에서 각 문항이 설명하는 것을 고르세요.**

보기는 아래와 같습니다.
```
CHECK / DEFAULT / PRIMAY KEY / UNIQUE / NOT NULL / FOREIGN KEY
```

```
여기에 답과 그 이유를 적어주세요!
1. 입력되는 데이터가 조건에 맞는지 검사하는 기능: CHECK
2. 값을 입력하지 않으면 자동으로 들어갈 값: DEFAULT
3. 빈 값을 입력하는 것을 허용하지 않음: NOT NULL
```


## 3. 가상의 테이블: 뷰 

<!-- 뷰에 관해 배우게 된 점을 적어주세요. -->

1. 뷰(View)의 기본 개념
- 한마디로 가상의 테이블임.
- 실제 데이터를 저장하지 않고 select 문 자체만 저장함.
- 참조하는 테이블 수에 따라 단순 뷰(1개)와 복합 뷰(2개 이상)로 나뉨.

2. 뷰를 사용하는 2가지 이유
- 보안 유지: 사용자에게 보여줘도 되는 열(아이디, 이름 등)만 뷰로 제공하여 민감한 개인정보 유출을 막음.
- 복잡한 쿼리 단순화: 복잡한 조인 쿼리를 매번 칠 필요 없이, 뷰를 만들어두면 select * from 뷰이름;으로 간단히 조회 가능함.

3. 핵심 SQL 문법
- 생성: create view 뷰이름 as select...
- 수정: alter view 뷰이름 as select...
- 삭제: drop view 뷰이름;
- 생성/덮어쓰기: create or replace view 뷰이름... (기존에 뷰가 있으면 덮어쓰고, 없으면 새로 만들어줘서 실무에서 가장 자주 쓰임)

> **확인문제: 다음은 뷰의 특징입니다. 거리가 먼 것을 하나 고르세요.**

보기는 아래와 같습니다.
```
1️⃣ 뷰에는 테이블의 모든 열을 포함시켜야 합니다.
2️⃣ 뷰는 복잡한 SQL을 단순하게 만드는 효과가 있습니다.
3️⃣ 뷰는 보안에 도움이 됩니다.
4️⃣ 일부 사용자가 테이블에는 접근하지 못하게 하고, 뷰에만 접근하도록 설정할 수 있습니다.
```

```
1번. 뷰는 사용자의 편의에 따라 필요한 열만 골라서 생성할 수 있음.
```


---

# 2️⃣ 실습과제

## 1. 데이터베이스 구축

아래 코드를 MySQL Workbench에 붙여넣은 후,  
**전체 드래그 → 실행 (Ctrl + Shift + Enter)** 하여 데이터베이스를 생성하세요.

```sql
CREATE DATABASE IF NOT EXISTS week4_db;
USE week4_db;
```

## 2. 실습문제

1. 다음 조건을 만족하는 `users` 테이블을 생성하시오.
```
- user_id는 INT이며 **기본키(Primary Key)**로 설정합니다.
- name은 VARCHAR(20)이며 NULL을 허용하지 않습니다.
- email은 VARCHAR(50)이며 중복을 허용하지 않습니다.
- signup_date는 DATE 타입으로 설정합니다.
- grade는 INT이며 기본값(Default)을 1로 설정합니다.
```

2. 다음 조건을 만족하는 orders 테이블을 생성하시오.
```
- order_id는 INT이며 기본키(Primary Key)로 설정합니다.
- user_id는 INT이며 NULL을 허용하지 않습니다.
- amount는 INT이며 0보다 커야 합니다.
- order_date는 DATE 타입으로 설정합니다.
```

3. 다음 조건을 만족하여 데이터를 삽입하시오.
```
- users 테이블에 3명 이상의 데이터를 직접 INSERT 하시오.
- orders 테이블에 3건 이상의 데이터를 직접 INSERT 하시오.
```

4. users와 orders 테이블을 활용하여 다음 컬럼을 보여주는 뷰 user_order_view를 생성하시오.
```
- user_id
- name
- amount
```

5. 생성한 user_order_view를 조회하시오.

## 3. 제출 방법

1. 각 문제의 실행 결과가 보이도록 화면을 캡처합니다.
2. 테이블 생성 결과, 데이터 삽입 결과, 뷰 생성 및 조회 결과가 모두 보이도록 제출합니다.

![alt text](images_4/image.png)

![alt text](images_4/image-1.png)

![alt text](images_4/image-2.png)

![alt text](images_4/image-3.png)

![alt text](images_4/image-4.png)
### 🎉 수고하셨습니다.



