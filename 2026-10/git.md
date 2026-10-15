# Git

- init 초기화
    - `git init` 초기화 -> 숨김폴더로 `.git`이 생기고 앞으로 이걸 이후에 명령어로 조작
    - .git 사진첩같은거라 스냅샷이 여기에..

- status
    - `git status` 현재 폴더의 git 작업상태확인
    - 어느브랜치인지, 
- .gitignore 
    - 해당이름의 파일을 생성하여, 그안에 파일명을 작성해놓으면 해당파일들은 git추적에서 제외된다
    - *.확장자, 폴더명/ 와같은 형태로 해당확장자전부 해당폴더이하를 제외할수있다
    - .gitignore.io 사이트를 활용하여 git사용시 제외가 필요한 리스트를 자동확인생성가능하다
    - git rm —cached 파일명 -> 이미 추적되던 파일을 깃에서 뺄때 해당 명령어를 추가적으로 사용해주어야 한다

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

git reflog ->지워진 로그까지 확인
```

- `git branch -M main` -> main브랜치 이름이 master 이런거 인 경우에 main으로 이름 바꾼다는 그런뜻

- `remote` : 원격 저장소 주소를 별명(origin) 으로 추가
- `push` : 원격 저장소에 업로드
```
git push origin main(브랜치명)
```


- 이럴땐
```
remote: Invalid username or token. Password authentication is not supported for Git operations.
-> 이런게 나오면 터미널 새거 열어서 brew install gh 입력 -> gh auth login 하여 로그인하기
```

- `reset` : 커밋취소삭제
```
git reset --soft HEAD~1 -> soft옵션 , 직전 커밋의 파일 수정본은 남기고, 커밋자체는 삭제함 (add되어있는상태)

git reset --mixed HEAD~1 -> mixed옵션, 파일수정본은 남기고, 커밋은 삭제되며 unstaged된 상태

git reset --hard HEAD~1 -> hard옵션, 커밋과 수정된 내용전부 삭제

git reset --hard HEAD@{1} ->reflog로 지워진 지난 커밋을 보고 삭제된 커밋상태로 돌리기(1은 예시이며 1커밋삭제전을 의미한다)
```

- `revert` : 커밋취소
```
git revert HEAD -> 직전 커밋을 취소하지만 삭제되하지않고 취소기록을 남김
```
HEAD대신에 돌리고싶은 커밋해시값입력가능


- `restore` : 수정취소
```
git restore --staged -> 수정사항은 남기고 커밋전 add만 취소

commit --amend -m "수정메세지" -> 마지막 커밋의 메세지만 수정
```

- `switch` : 브랜치전환
```
git switch -c 신규브랜치명 ->신규브랜치를 현재브랜치내용을 복사하며 생성
git switch 브랜치명 -> 존재하는 브랜치로 이동

git branch -> 브랜치목록보기
git branch -d 브랜치명 -> 브랜치삭제
```

- `merge` : 브랜치병합
```
git merge 브랜치명 ->현재브랜치에 입력브랜치를 합친다
```

- `stash` : 임시저장
```
git stash -> 수정중이던 브랜치를 임시저장하고 이후 다른브랜치로 이동
git stash pop -> 임시저장한 브랜치로 돌아와 임시저장내용 꺼내기
```
