# SQL

## 생성
CREATE ROLE 이름 LOGIN PASSWORD '비번';

CREATE DATEBASE 데이터베이스이름 OWNER 이름

## CRUD
- INSERT : 열삽입
    `INSERT INTO tb1 (col1, col2, col3) VALUES ('a', 'b', 1234);`
    -  컬럼에 매칭되는 위치의 값으로 생성된다
- UPDATE : 존재하는 열 내의 값 변경
    `UPDATE tb1 SET col1 = 'a' WHERE col1 = 'b';`
    - 조건에 해당하는 열의 지정컬럼 값을 변경
- DELETE : 열삭제
    `DELETE FROM tb1 WHERE col1 = 'a';`

## 조회
SELECT 무엇을
FROM 어디서(테이블명 등)
WHERE 어떤조건으로

### 출력 변경
- CAST : 타입변경
    `CAST(col1 AS sometype)`
    - 컬럼의 데이터를 지정한 타입형태로 변경
- SPLIT_PART : 기준에 따른 분할
    `SPLIT_PART(col1, splitPoint, whatsec)`
    - 컬럼의 데이터를 지정엔기준점을 기준으로 분할하여 몇번째 부분인지 선택 출력
-  사용예시
```
SELECT date_added, CAST(date_added AS date)
FROM titles 
WHERE show_id IN ('s1','s2','s8800');
-- text타입이었던 date_added컬럼의 값을 date타입으로 변경출력

SELECT duration, SPLIT_PART(duration,' ',1) 
FROM titles WHERE show_id IN ('s1', 's2'); 
-- ' '를 기준으로하여 분할한 첫번째부분 
```

## 조건들
- LIMIT : 지정된 갯수만큼만
- 등호부등호 = ,!= , <,>, <=,>=
- AND, OR
- IN (여러값, 중에, 해당하면, 다), NOT IN
- BETWEEN 이값이랑 AND 이값사이에, NOT BETWEEN
- IS NULL, IS NOT NULL
- COALESCE(NULL대신, 기본값, 설정하기)
    `SELECT COALESCE(col1, 'non' ) FROM tb1;`
        ->col1의 값이 NULL인 경우에는 'non'을 조회한다  
    `SELECT COALESCE(co1, co2, 'non') FROM tb1;`
        ->col의 값이 NULL인 경우에는 col2값을, 그값도 NULL인 경우에는 'non'을 조회한다
- DISTINCT 중복제거된
    `SELECT DISTINCT col1 FROM tb1;`
        ->col1의 값이 중복제외하고 조회된다
- ORDER BY, ORDER BY DESC 오름내림차순으로
- LIKE 패턴검색
    `SELECT col1 FROM tb1 WHERE col1 LIKE '%test%';`
        ->col1의값에서 어느위치든 'test'가 포함되어있는 경우 조회한다
    `SELECT col1 FROM tb1 WHERE col1 LIKE '_test';`
        ->col1의값에서 '문자하나와test' 인 경우 조회한다
    `SELECT col1 FROM tb1 WHERE col1 ILIKE 'test';`
        ->col1의 값에서 대소문자 구분없이 'test'인 경우 조회한다
- GROUP BY 값이 같은것을 묶는다
    `SELECT col1, COUNT(*) FROM tb1 GROUP BY col1;`
        ->col1값이 같은 경우끼리 묶이고, 각 묶음마다 몇개씩 묶였는지 출력한다


## 테이블 조작

### 테이블 제거
- DROP TABLE
    `DROP TABLE tb1;`
        -> tb1 테이블 자체를 삭제
    `DROP TABLE IF EXISTS tb1;`
        -> 테이블이 존재하는 경우에만 제거 (오류방지)

### 컬럼 변경
- ALTER
    - 컬럼 타입 변경
        `ALTER TABLE tb1 ALTER COLUMN col1 TYPE sometype USING col1::sometype;`
    - 컬럼 추가
        `ALTER TABLE tb1 ADD COLUMN newcol sometype;`
    - 사용예시
        ```
        ALTER TABLE titles ALTER COLUMN date_added 
        TYPE date USING date_added::date;

        ALTER TABLE titles ADD COLUMN minutes integer;
        ```
    - 새로 추가하는 컬럼에 값 업데이트하기 (사용예시)
        ```
        UPDATE titles
        SET minutes = SPLIT_PART(duration, ' ', 1)::integer
        WHERE duration LIKE '%min';
        ```

### 제약조건 설정
- NOT NULL : 해당 컬럼 값으로 NULL 금지
    - `ALTER TABLE tb1 ALTER COLUMN col1 SET NOT NULL;`
- 컬럼규칙 : 해당 컬럼 값에 조건제한설정(패턴, 불가능패턴 등)
    - `ALTER TABLE tb1 ADD CONSTRAINT 규칙이름1 CHECK 조건;`
- 유니크키 : 겹치는값불가
    - `ALTER TABLE tb1 ADD CONSTRAINT 규칙이름1 UNIQUE col1;`
- 기본키 : 테이블 기본키생성
    - `ALTER TABLE tb1 ADD COLUMN col1 bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY;`
- 사용예시
    
    ```
    ALTER TABLE titles ALTER COLUMN show_id SET NOT NULL;
    ALTER TABLE titles ADD CONSTRAINT titles_type_check CHECK (type IN('Movie', 'TV Show'));
    -- ->type에는 Move 나  TV Show 문자만 들어갈수있음
    ALTER TABLE titles ADD CONSTRAINT titles_rating_check CHECK (rating NOT LIKE '%min');
    ALTER TABLE titles ADD CONSTRAINT titles_release_year_check CHECK (release_year BETWEEN 1900 AND 2026);
    ALTER TABLE titles ADD CONSTRAINT titles_show_id_key UNIQUE (show_id);
    ALTER TABLE titles ADD COLUMN id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY;
    ```