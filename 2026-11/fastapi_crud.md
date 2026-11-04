# CRUD

## Create
### POST method
- post는 내가 정보를 보내고, 이를 처리해달라는 목적을 가짐
- 데이터변경의경우 post로 처리
- html form에서 method="post" 속성지정
    지정하지않는경우 자동적으로 get임
- `from fastapi import Form`
- `@app.post('/주소')` , `def sample(name : str = Form()) :`
    fastapi에서는 form의 post로 보내진 값을 위과같이 접근함

### Redirect
- 다른페이지로 보내는 처리
- `from fastapi.responses import RedirectResponse`
- `RedirectResponse('보내질주소'', status_code=코드)`
    - 동적으로 리디렉션 주소를 작성하는경우 f스트링을 사용가능 (`RedirectResponse(f'/posts/post/{post_id}', status_code=303)`)

### HTTP 상태코드 (fastapi에만 해당하는거아님)
- 3으로 시작하는경우 리디렉션 메세지
- 303 : 다른 URI로 이동(리디렉션)하여 GET 요청을 수행해야 함을 나타내는 응답
    303 원래 보냈던 요청 메소드(예: POST, PUT 등)와 상관없이 무조건 GET 메소드로 변경되어 새로운 페이지를 요청
- 307 : Temporary Redirect 원래 보낸 메소드(POST, PUT 등)와 데이터(Body)를 그대로 유지한 채 리다이렉트 주소로 재요청
