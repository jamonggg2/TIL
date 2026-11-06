# CRUD

## POST method
- post는 내가 정보를 보내고, 이를 처리해달라는 목적을 가짐
- 데이터변경의경우 post로 처리
- html form에서 method="post" 속성지정
    지정하지않는경우 자동적으로 get임
- `from fastapi import Form`
- `@app.post('/주소')` , `def sample(name : str = Form()) :`
    fastapi에서는 form의 post로 보내진 값을 위과같이 접근함

## Redirect
- 다른페이지로 보내는 처리
- `from fastapi.responses import RedirectResponse`
- `RedirectResponse('보내질주소'', status_code=코드)`
    - 동적으로 리디렉션 주소를 작성하는경우 f스트링을 사용가능 (`RedirectResponse(f'/posts/post/{post_id}', status_code=303)`)

## HTTP 상태코드 (fastapi에만 해당하는거아님)
- 3으로 시작하는경우 리디렉션 메세지
- 303 : 다른 URI로 이동(리디렉션)하여 GET 요청을 수행해야 함을 나타내는 응답
    303 원래 보냈던 요청 메소드(예: POST, PUT 등)와 상관없이 무조건 GET 메소드로 변경되어 새로운 페이지를 요청
- 307 : Temporary Redirect 원래 보낸 메소드(POST, PUT 등)와 데이터(Body)를 그대로 유지한 채 리다이렉트 주소로 재요청

## ORM : Object Relational Mapping
- SQL이아닌 서버개발언어 그대로 DB조작
- 한가지 언어로 개발을 진행할 수 있어서 생산성 향상가능
- SQL로 컨버팅하는것이라 처리속도는 SQL로 작성하는것보다는 더 느릴 수 있음

### sqlArchemy
- 파이썬과 db를 연결
- 설치 `uv add sqlalchemy`
- 사용법은 공식문서의 step을 보면서 따라할것
    1. 연결할 DB와 테이블에 대한 객체, 클래스 생성
    ```
    from sqlalchemy.orm import DeclarativeBase ,Mapped, apped_column

    # 필수클래스 
    class Base(DeclarativeBase):
        pass

    class 테이블클래스명 (Base): # 위에서 만든 클래스를 상속받음
        __tablename__ = "실제테이블명"

    컬럼명1: Mapped[int] = mapped_column(primary_key=True)
    컬럼명2: Mapped[데이터타입을 파이썬기준작성]
    ```

    2. DB연결을 위한 엔진 생성
    ```
    from sqlalchemy import create_engine

    DB_URL = "postgresql(사용db)+psycopg(매칭된라이브러리)://디비아이디:비번@localhost:5432(접속정보)/dbname데이터베이스명"

    engine = create_engine(DB_URL, echo=True)   #echo는 로그확인을 위한 옵션으로 미작성시F
    ```

    3. DB에 접속하는 세션을 열어서 조작
    ```
    from sqlalchemy.orm import Session

    with Session(engine) as db: #세션은 with절에서 연다
    ```

        - select
        ```
        from sqlalchemy import select
        
        전체데이터 = db.scalars(select(테이블클래스명)).all()
        조건데이터 = select(테이블클래스명).where(테이블클래스명.컬럼명1.in_(["엥이거", "sql아니야?"]))
        조건데이터2 = select(테이블클래스명).where(테이블클래스명.컬럼명1 == "찾는거")
        하나의데이터 = db.get(테이블클래스명, pk값)
        ```

        - insert
        ```
        새데이터 = 테이블클래스(컬럼1=컬럼1값, 컬럼2=컬럼2값)
        db.add(새데이터)
        db.commit()

        여러개데이터1 = 테이블클래스(컬럼1=컬럼1값, 컬럼2=컬럼2값)
        여러개데이터2 = 테이블클래스(컬럼1=컬럼1값, 컬럼2=컬럼2값)
        db.add_all([여러개데이터1, 여러개데이터2])
        db.commit()
        ```

        - udate
        ```
        변경할데이터 = db.get(테이블클래스, pk값)
        변경할데이터.컬럼명 = 신규값1
        변경할데이터.컬럼명2 = 신규값2
        db.commit()
        ```

        - delete
        ```
        지울데이터 = db.get(테이블클래스, pk값)
        db.delete(지울데이터)
        db.commit()
        ```
#### sqlArchemy로 fk있는 테이블 조작
- 추가 import 필요
```
from sqlalchemy import ForeignKey
from sqlalchemy.orm import relationship
from typing import List
```

- 테이블간의 종속관계를 코드로 명시필요
```
# 부모테이블
class 부모(Base):
    __tablename__ = '실제부모테이블명'
    pk컬럼 : Mapped[int] = mapped_column(primary_key=True)
    컬럼1 : Mapped[데이터타입]

    자식통로이름 : Mapped[List["자식테이블명"]] = relationship(
        back_populates='부모통로이름',
        cascade='all, delete-orphan' #실제 테이블설정에따라작성
    )

# 자식테이블
class 자식(Base):
    __tablename__ = '실제자식테이블명'
    pk컬럼 : Mapped[int] = mapped_column(primary_key=True)
    컬럼1 : Mapped[str]
    fk컬럼 : Mapped[int] = mapped_column(ForeignKey('실제부모테이블명.pk컬럼', ondelete='CASCADE')) #실제 테이블설정에따름

    #파이썬 객체관점의 부모참조통로
    부모통로이름 : Mapped['부모테이블명'] = relationship(back_populates='자식통로이름')
```

- 부모조회후 이에 연결된 자식값은 부모객체를 이용하여 가져올 수있다
```
        부모데이터 = db.get(부모테이블, pk값)
        자식데이터들 = 부모데이터.자식통로이름

        #자식데이터들은 객체이므로 .컬럼 으로 내부값을 접근한다
```
