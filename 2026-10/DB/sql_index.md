# SQL INDEX
- 인덱스는 데이터베이스 검색속도를 높이기위해 사용

- 테이블의 특정 컬럼들을 복사해 정렬하는 별도의 데이터구조
- 테이블 전체를 읽지않고, 인텍스를 통해 select 속도향상
- Indexes 폴더에 저장됨
- PK는 인덱스로 자동등록됨
- 트리구조를 주로사용

## 주의사항
- 인덱스또한 데이터이므로 용량을 사용함
- 모든데이터를 인덱스화해서는 안됨(필요도없음)
- 인덱스를 사용하는 것이 조회속도에 차이가 발생하지 않는 쿼리에 대해서는 DB는 필터를사용하여 일반적인 방법으로 찾을것

## 사용법
생성 
`CREATE INDEX 인덱스명 ON (컬럼명)` : `CREATE INDEX views_title_id_idx ON views (title_id);`

삭제
`DROP INDEX 인덱스명`:`DROP INDEX views_title_id_idx`