# FastAPI

##  신규세팅
`uv init . --bare --python 3.14`
- `.` : 현재폴더에. 만약 하위폴더를 지정하고싶으면 이 대신에 폴더명작성
- `--bare`: 소스 코드 예시 파일(`hello.py` 또는 `main.py`)을 만들지 않고 `pyproject.toml`과 최소한의 설정 파일만 깔끔하게 생성
- `--python 3.14`: 프로젝트의 기본 파이썬 버전을 3.14로 지정

`uv add "fastapi[standard]"`
- FastAPI 세팅
- uv init된 폴더의 터미널에서 실행

- main.py 생성
    - `from fastapi import FastAPI`
    - `app = FastAPI()`

- 개발서버실행 
    `uv run fastapi dev`

## 라우팅처리
- def위에 데코레이터로 @app.get('/주소') 를 단다
- 데코레이터에 있는 주소의 요청이 오는경우, 그걸 달고있는 def가 처리하게하는 분기처리
- 라우팅은 위에서부터 아래로 내려오면서 값을 확인하므로 차례에있어 주의가 필요할 수 있다

## 동적주소처리
 - 예시 : `@app.get('/profile/{username}')` 
 - input name으로 접근


## html 연결
### py
'''
from fastapi.templating import Jinja2Templates
from fastapi import Request

templates = Jinja2Templates(directory='templates')
'''
- Jinja2Templates 사용
- def 인자로 `(request : Request)`
- return
    ```
    return templates.TemplateResponse(
            request=request, 
            name='보낼html파일.html'
            context={'키':보낼값}
    )
    ```
    - request : 필수요소
    - name : 어느페이지로???
    - context : 보낼값, 생략하면 값을 전달하지 않습니다
- `directory=루트에만들폴더명` : 헤당폴더를만들어 그안에  html파일을 넣습니다 

### html
`<p>{{keyname}}</p>` 
- Jinja2Templates
    - context의 키를 사용하여 html에서 값을 사용할 수있음 
    - `{% for i in num %}` 와같은 형태로 for문을 돌릴수있음
    - `{{ loop.index }}` 로 for문에서 인덱스값을 사용할수있음
- `<form action="이동할주소">`안의 input을 통해 사용자입력 값을 전달받아 처리하게 할 수있다
- 전달을 받은 def는 인자로 `<input name="이것"> `input에서 들어오는 값을 인자로 설정해놓아야 받을 수 있다