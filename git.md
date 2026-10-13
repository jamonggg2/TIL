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