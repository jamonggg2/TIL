# Git

- init 초기화
    - `git init` 초기화 -> 숨김폴더로 `.git`이 생기고 앞으로 이걸 이후에 명령어로 조작
    - .git 사진첩같은거라 스냅샷이 여기에..

- status
    - `git status` 현재 폴더의 git 작업상태확인
    - 어느브랜치인지, 

## 명령어
- `add` : staging area에 올리기
```
git add <filename>

git add <filename>,<file2>,<file3>
git add . -> .은 현재폴더를 의미하기에, 지금 위치에있는 모든것을 의미
```

- `commit` : `.git` repository에 저장
    - `-m` : 옵션이지만 (거의)필수
    - 커밋내용에 대해 메세지 남겨야함 
    - config -> 첫 커밋의 경우 git아이디이름 설정필요함
```
git commit -m "message" ->커밋

git config --global user.email "email@email" ->이메일설정하기
git config --global user.email ->이메일설정 확인하기
git config --global user.name ->이름설정 확인하기 (설정하기도가능)
```

- `log` : 로그 확인하기
```
git log 
git log --oneline ->한줄로 간략보기
```

- `git branch -M main` -> main브랜치 이름이 master 이런거 인 경우에 main으로 이름 바꾼다는 그런뜻

- `remote` : 원격 저장소 주소를 별명(origin) 으로 추가
- `push` : 원격 저장소에 업로드


- 이럴땐
```
remote: Invalid username or token. Password authentication is not supported for Git operations.
-> 이런게 나오면 터미널 새거 열어서 brew install gh 입력 -> gh auth login 하여 로그인하기
```