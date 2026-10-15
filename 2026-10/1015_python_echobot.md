# python으로 텔레그램 챗봇 만들기 실습

## 챗봇 구성
유저 - 텔레그램서버 - 내서버
1. 유저가 메세지를 텔레그램으로 전송하면, 텔레그램을통해 내서버까지 요청도달
2. 내서버에서 응답이 텔레그램서버를 통해 유저에게 도달

## setting
1. 터미널에서 UV 설치 : python 설치를 위함
2. 프로젝트폴더 생성후 python init 
    - 이때 프로젝트 폴더 내에서 uv init 하면서 git도 자동적으로 init됨
3. uv add fastapi, uvicorn, requests, python-dotenv 
    - fastapi : 서버를위한 웹프레임워크
    - uvicorn : 웹서버엔진
    - requests : HTTP 통신라이브러리
    - python-dotenv : 보안이 필요한 설정을 .env로 관리하게 하는 도구
4. 텔레그램 BotFather를 추가하여 token발급
5. 외부연결을 위해 ngrok 사용 
    - ngrok : 로컬 실행중인 웹서버를 외부인터넷 접속할수있게 임시보안도배인을 만들어 연결해주는 터널링 프로그램