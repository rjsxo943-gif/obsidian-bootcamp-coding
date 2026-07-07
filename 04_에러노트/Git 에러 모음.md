
> Git과 GitHub를 쓰다가 명령어를 잘못 치거나, 이상한 화면에 들어갔을 때 빠져나오는 방법을 정리한 노트.

---

## 🚨 제일 먼저 외울 탈출 명령어

Git 쓰다가 이상한 화면에 들어가면 아래부터 시도한다.

|상황|탈출 방법|
|---|---|
|명령어 실행 중 멈춘 것 같음|`Ctrl + C`|
|`git log`, `git diff` 화면에서 못 나감|`q`|
|`vim` 화면에 들어감|`Esc` → `:q` → Enter|
|`vim`에서 저장 안 하고 나가기|`Esc` → `:q!` → Enter|
|`vim`에서 저장하고 나가기|`Esc` → `:wq` → Enter|
|`nano` 화면에 들어감|`Ctrl + X`|
|터미널 글자가 이상하게 먹통 같음|`Ctrl + C` 먼저|

---

## 🧭 Git 작업 전에 항상 확인할 것

Git 명령어 치기 전에 먼저 현재 상태를 확인한다.

```bash
git status
```

현재 폴더 위치 확인:

```bash
pwd
```

현재 폴더 안 파일 확인:

```bash
ls
```

Windows PowerShell에서는 이것도 가능하다.

```powershell
dir
```

---

## ✅ Git 기본 흐름

GitHub에 코드를 올리는 기본 순서는 항상 이거다.

```bash
git status
git add .
git commit -m "메시지"
git push
```

예시:

```bash
git status
git add .
git commit -m "0629 반복문 함수 sys.argv 실습"
git push
```

---

## 1. `nothing to commit, working tree clean`

## 상황

```text
nothing to commit, working tree clean
```

## 의미

변경된 파일이 없다는 뜻이다.

즉, Git이 볼 때 새로 저장할 내용이 없다.

## 해결

먼저 파일을 실제로 수정했는지 확인한다.

```bash
git status
```

수정한 게 없으면 정상이다.  
수정했는데도 안 뜨면 파일을 저장하지 않았을 가능성이 있다.

VS Code나 메모장에서 저장 후 다시 확인한다.

```bash
git status
```

---

## 2. `Changes not staged for commit`

## 상황

```text
Changes not staged for commit:
  modified: README.md
```

## 의미

파일은 수정됐는데 아직 `git add`를 안 했다는 뜻이다.

## 해결

```bash
git add .
git commit -m "README 수정"
git push
```

특정 파일만 추가하려면:

```bash
git add README.md
```

---

## 3. `no changes added to commit`

## 상황

```text
no changes added to commit
```

## 의미

`commit`하려고 했는데 `git add`를 안 했다는 뜻이다.

## 해결

```bash
git add .
git commit -m "수정 내용 저장"
```

## 내 식으로 이해

```text
git add = 커밋할 파일을 장바구니에 담기
git commit = 장바구니에 담긴 걸 저장하기
git push = GitHub로 올리기
```

---

## 4. `fatal: not a git repository`

## 상황

```text
fatal: not a git repository
```

## 의미

현재 폴더가 Git 저장소가 아니라는 뜻이다.

즉, `.git` 폴더가 없는 곳에서 Git 명령어를 친 것이다.

## 해결

현재 위치 확인:

```bash
pwd
```

폴더 목록 확인:

```bash
ls
```

프로젝트 폴더로 이동:

```bash
cd 폴더이름
```

예시:

```bash
cd C:\Users\rjsxo\bootcamp\mycodehouse
```

그다음 다시 확인:

```bash
git status
```

---

## 5. 폴더 잘못 들어갔을 때

## 현재 폴더 확인

```bash
pwd
```

## 한 단계 위로 나가기

```bash
cd ..
```

## 특정 폴더로 들어가기

```bash
cd 폴더이름
```

## 폴더 안 파일 보기

```bash
ls
```

PowerShell에서는:

```powershell
dir
```

## 예시

```bash
cd ..
cd mycodehouse
git status
```

---

## 6. `git log`에서 못 나올 때

## 상황

`git log`를 쳤더니 화면이 바뀌고 아무 명령어도 안 먹는 것처럼 보임.

```bash
git log
```

## 해결

그냥 키보드에서:

```text
q
```

를 누르면 나온다.

## 같은 상황

아래 명령어들도 화면이 길면 `less` 화면으로 들어갈 수 있다.

```bash
git log
git diff
git show
```

나가는 법은 전부:

```text
q
```

---

## 7. `vim`에 들어갔을 때

## 상황

`git commit`을 메시지 없이 쳤거나, Git이 기본 에디터를 열었을 때 이상한 화면에 들어감.

```bash
git commit
```

## 해결 1: 저장 안 하고 나가기

```text
Esc
:q!
Enter
```

## 해결 2: 저장하고 나가기

```text
Esc
:wq
Enter
```

## 해결 3: 그냥 commit 메시지를 명령어에 넣기

앞으로는 이렇게 쓰면 vim에 안 들어간다.

```bash
git commit -m "커밋 메시지"
```

---

## 8. `nano`에 들어갔을 때

## 상황

터미널 아래에 이상한 메뉴가 보임.

```text
^G Help  ^O Write Out  ^X Exit
```

## 해결

저장 안 하고 나가기:

```text
Ctrl + X
N
Enter
```

저장하고 나가기:

```text
Ctrl + X
Y
Enter
```

---

## 9. `Your branch is up to date with 'origin/main'`

## 상황

```text
Your branch is up to date with 'origin/main'
```

## 의미

내 로컬 브랜치와 GitHub 원격 브랜치가 같은 상태라는 뜻이다.

## 해결

에러가 아니다. 정상 메시지다.

변경한 파일이 있다면 `git status`에서 따로 표시된다.

```bash
git status
```

---

## 10. `rejected` / `fetch first` / `non-fast-forward`

## 상황

```text
! [rejected] main -> main
error: failed to push some refs
hint: Updates were rejected because the remote contains work that you do not have locally.
```

## 의미

GitHub에 있는 내용이 내 로컬보다 앞서 있어서 바로 push가 안 된다는 뜻이다.

## 해결

먼저 GitHub 내용을 받아온다.

```bash
git pull
```

그다음 다시 push한다.

```bash
git push
```

## 충돌이 나면

충돌 파일을 열어서 직접 정리해야 한다.

충돌 표시 예시:

```text
<<<<<<< HEAD
내 로컬 내용
=======
GitHub에 있던 내용
>>>>>>> origin/main
```

필요한 내용만 남기고 위 표시들을 삭제한 뒤:

```bash
git add .
git commit -m "충돌 해결"
git push
```

---

## 11. `GH007: Your push would publish a private email address`

## 상황

```text
remote: error: GH007: Your push would publish a private email address.
```

## 의미

GitHub가 내 개인 이메일 공개를 막고 있어서 push가 거부된 것이다.

## 해결 방향

GitHub에서 제공하는 noreply 이메일을 Git 설정에 넣어야 한다.

현재 Git 이메일 확인:

```bash
git config user.email
```

전역 이메일 확인:

```bash
git config --global user.email
```

이메일 변경:

```bash
git config --global user.email "GitHub에서 제공한 noreply 이메일"
```

변경 확인:

```bash
git config --global user.email
```

그다음 다시 커밋하고 push한다.

이미 잘못된 이메일로 커밋했다면 커밋 수정이 필요할 수 있다.

최근 커밋 이메일만 고칠 때:

```bash
git commit --amend --reset-author
```

이때 vim이 뜨면:

```text
Esc
:wq
Enter
```

그다음:

```bash
git push
```

---

## 12. `fatal: remote origin already exists`

## 상황

```text
fatal: remote origin already exists
```

## 의미

이미 `origin`이라는 원격 저장소가 등록되어 있다는 뜻이다.

## 현재 원격 저장소 확인

```bash
git remote -v
```

## 해결 1: 기존 origin 주소 변경

```bash
git remote set-url origin https://github.com/rjsxo943-gif/mycodehouse.git
```

## 해결 2: 기존 origin 삭제 후 다시 추가

```bash
git remote remove origin
git remote add origin https://github.com/rjsxo943-gif/mycodehouse.git
```

확인:

```bash
git remote -v
```

---

## 13. `src refspec main does not match any`

## 상황

```text
error: src refspec main does not match any
```

## 의미

`main` 브랜치가 없거나, 아직 커밋이 하나도 없을 때 발생할 수 있다.

## 해결 1: 현재 브랜치 확인

```bash
git branch
```

## 해결 2: 브랜치 이름을 main으로 변경

```bash
git branch -M main
```

## 해결 3: 첫 커밋 만들기

```bash
git add .
git commit -m "first commit"
git push -u origin main
```

---

## 14. `Please tell me who you are`

## 상황

```text
Author identity unknown
Please tell me who you are.
```

## 의미

Git에 사용자 이름과 이메일이 설정되어 있지 않다는 뜻이다.

## 해결

```bash
git config --global user.name "rjsxo943-gif"
git config --global user.email "GitHub에서 제공한 noreply 이메일"
```

확인:

```bash
git config --global user.name
git config --global user.email
```

---

## 15. `Permission denied`

## 상황

```text
Permission denied
```

## 의미

권한 문제이다.

원인은 여러 가지다.

```text
폴더 권한 문제
GitHub 인증 문제
SSH key 문제
관리자 권한 문제
```

## 해결 1: HTTPS 주소 확인

```bash
git remote -v
```

HTTPS 주소를 쓰고 있다면 보통 이런 형태여야 한다.

```text
https://github.com/rjsxo943-gif/mycodehouse.git
```

## 해결 2: GitHub 로그인 다시 하기

Git Credential Manager가 뜨면 GitHub 계정으로 로그인한다.

## 해결 3: 폴더 권한 문제면

OneDrive나 보호된 폴더가 아닌 일반 작업 폴더에서 다시 시도한다.

예시:

```text
C:\Users\rjsxo\bootcamp
```

---

## 16. `Authentication failed`

## 상황

```text
Authentication failed
```

## 의미

GitHub 로그인 인증이 실패했다는 뜻이다.

요즘 GitHub는 비밀번호로 push하지 않고 토큰이나 Git Credential Manager 로그인을 사용한다.

## 해결

1. GitHub 로그인 창이 뜨면 브라우저에서 로그인한다.
    
2. 잘못 로그인된 계정이면 Windows 자격 증명 관리자에서 GitHub 정보를 삭제하고 다시 로그인한다.
    
3. 원격 주소 확인:
    

```bash
git remote -v
```

---

## 17. 브랜치 확인과 이동

## 현재 브랜치 확인

```bash
git branch
```

현재 브랜치는 앞에 `*` 표시가 붙는다.

```text
* main
```

## 브랜치 이동

```bash
git switch 브랜치이름
```

예시:

```bash
git switch main
```

## 새 브랜치 만들고 이동

```bash
git switch -c 새브랜치이름
```

예시:

```bash
git switch -c practice/0629
```

---

## 18. 실수로 다른 브랜치에 들어갔을 때

## 현재 브랜치 확인

```bash
git branch
```

## main으로 돌아가기

```bash
git switch main
```

## 이동이 안 될 때

작업 중인 변경사항이 있어서 이동이 막힐 수 있다.

먼저 상태 확인:

```bash
git status
```

변경 내용을 저장하려면:

```bash
git add .
git commit -m "작업 저장"
git switch main
```

변경 내용을 버리고 이동하려면 조심해서 사용:

```bash
git restore .
git switch main
```

---

## 19. 방금 수정한 파일 되돌리기

## 특정 파일 되돌리기

```bash
git restore 파일명
```

예시:

```bash
git restore README.md
```

## 전체 수정 내용 되돌리기

주의: 저장하지 않은 변경사항이 사라진다.

```bash
git restore .
```

---

## 20. add한 파일 다시 빼기

## 상황

`git add .`를 했는데 커밋에 넣고 싶지 않은 파일이 있다.

## 해결

```bash
git restore --staged 파일명
```

예시:

```bash
git restore --staged README.md
```

전체 staged 취소:

```bash
git restore --staged .
```

---

## 21. 직전 커밋 메시지 수정

## 상황

커밋 메시지를 잘못 썼다.

## 해결

```bash
git commit --amend -m "새 커밋 메시지"
```

아직 push 전이면 안전하다.

이미 push 후라면 조심해야 한다.

---

## 22. push 기본 세팅

처음 push할 때는 이렇게 쓴다.

```bash
git push -u origin main
```

그다음부터는 보통 이렇게만 써도 된다.

```bash
git push
```

---

## 23. GitHub 저장소 처음 연결할 때

기존 로컬 폴더를 GitHub에 처음 연결하는 흐름:

```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/rjsxo943-gif/mycodehouse.git
git push -u origin main
```

이미 `origin`이 있다고 나오면:

```bash
git remote set-url origin https://github.com/rjsxo943-gif/mycodehouse.git
git push -u origin main
```

---

## 24. GitHub 저장소를 로컬로 처음 받을 때

```bash
git clone https://github.com/rjsxo943-gif/mycodehouse.git
```

원하는 폴더에 받고 싶으면 먼저 그 폴더로 이동한다.

예시:

```powershell
cd C:\Users\rjsxo\bootcamp
git clone https://github.com/rjsxo943-gif/mycodehouse.git
```

그러면 아래 폴더가 생긴다.

```text
C:\Users\rjsxo\bootcamp\mycodehouse
```

들어가기:

```powershell
cd C:\Users\rjsxo\bootcamp\mycodehouse
git status
```

---

## 25. 진짜 헷갈릴 때 쓰는 안전 루틴

Git에서 뭔가 이상하면 바로 이 순서로 확인한다.

```bash
pwd
git status
git branch
git remote -v
```

각 명령어 의미:

|명령어|의미|
|---|---|
|`pwd`|내가 지금 어느 폴더에 있는지 확인|
|`git status`|현재 Git 상태 확인|
|`git branch`|현재 브랜치 확인|
|`git remote -v`|연결된 GitHub 주소 확인|

---

## 26. 매일 쓰는 안전 업로드 루틴

수업 끝나고 GitHub에 올릴 때는 아래 순서만 따라간다.

```bash
git status
git add .
git status
git commit -m "날짜 학습 내용"
git push
```

예시:

```bash
git status
git add .
git status
git commit -m "0706 파이썬 함수 실습"
git push
```

중간에 이상하면 바로 멈추고 `git status`를 다시 확인한다.

---

## 27. 명령어별 한 줄 요약

|명령어|의미|
|---|---|
|`git status`|현재 상태 확인|
|`git add .`|변경 파일 전체 추가|
|`git add 파일명`|특정 파일만 추가|
|`git commit -m "메시지"`|변경사항 저장|
|`git push`|GitHub로 업로드|
|`git pull`|GitHub 내용 가져오기|
|`git clone 주소`|GitHub 저장소 다운로드|
|`git branch`|브랜치 목록 확인|
|`git switch 브랜치명`|브랜치 이동|
|`git switch -c 브랜치명`|새 브랜치 만들고 이동|
|`git remote -v`|원격 저장소 주소 확인|
|`git log`|커밋 기록 확인|
|`q`|`git log` 화면에서 나가기|

---

## 28. 내 기준 Git 사고방식

```text
git status = 지금 상황판 보기
git add = 저장할 파일 고르기
git commit = 내 컴퓨터 Git에 저장하기
git push = GitHub에 올리기
git pull = GitHub에서 가져오기
git branch = 작업 라인 확인하기
git switch = 작업 라인 이동하기
```

---

## 29. 절대 조심할 명령어

아래 명령어들은 내용을 날릴 수 있으므로 아무 생각 없이 치지 않는다.

```bash
git reset --hard
git clean -fd
git push --force
git restore .
```

특히 아래 명령어는 수정한 내용이 사라질 수 있다.

```bash
git restore .
```

쓰기 전에 반드시 확인한다.

```bash
git status
```

---

## 30. 최종 응급처치

뭔가 이상하다 싶으면 바로 이것만 한다.

```bash
git status
```

그리고 화면 내용을 복사해서 질문한다.

절대 바로 아래 명령어부터 치지 않는다.

```bash
git reset --hard
git push --force
```

---

## 🏷️ 태그

#git #github #에러노트 #터미널 #push #commit