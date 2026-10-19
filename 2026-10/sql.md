# SQL

## 생성
CREATE ROLE 이름 LOGIN PASSWORD '비번';

CREATE DATEBASE 데이터베이스이름 OWNER 이름

## 조회
SELECT 무엇을
FROM 어디서(테이블명 등)
WHERE 어떤조건으로

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