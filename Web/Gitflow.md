# [Git] 브랜치 관리와 고급 기능

🎯 **Achievement Goals**

- Git 브랜치의 개념을 이해할 수 있다.
- Git 으로 협업하며 브랜치를 나누는 이유를 이해할 수 있다.
- Git 으로 프로젝트를 관리하며 브랜치를 생성, 전환, 병합할 수 있다.

---

## Git의 브랜치(Branch)

- 여러 사람이 동일한 소스코드를 기반으로 서로 다른 작업을 할 때에는 각각 서로 다른 버전의 코드가 만들어 질 수 밖에 없습니다.
- 여러 개발자가 동시에 서로 다른 작업을 할 수 있게 만들어 주는 기능이 바로 '브랜치(Branch)' 입니다.

### ✅ 브랜치

- 독립적으로 어떤 작업을 진행하기 위함
- 코드를 여러 개로 복사해야 하는 일이 발생하여 브랜치 기능을 활용하면, 코드를 통째로 복사한 후 원래 코드가 변결될 우려 없이 독립적으로 개발할 수 있다.
- 각각의 브랜치는 다른 브랜치의 영향을 받지 않기 때문에, 여러 작업을 동시에 진행할 수 있다.

**장점**

- 한 소스코드에서 동시에 다양한 작업을 할 수 있게 해준다.
- 소스코드의 한 시점과 동일한 상태를 만들고, 브랜치를 넘나들며 작업을 수행할 수 있다.
- 각각의 브랜치에서 생긴 변화가 다른 브랜치에 영향을 주지 않고 독립적으로 코딩을 진행할 수 있다.

**종류**

- 통합 브랜치(Integration Branch)

배포될 소스 코드가 기록되는 브랜치.
Github Repository를 생성하게 되면 기본적으로 main 브랜치가 생깁니다. (기존 Repository의 경우 master로 되어 있는 곳도 많습니다.)
해당 프로젝트의 모든 기능이 정상적으로 작동하는 상태의 소스코드가 담겨 있습니다.

- 피처 브랜치(Feature Branch)

기능 추가, 버그 수정과 같이 단위 작업을 위한 브랜치.
통합 브랜치로부터 만들어내며, 피처 브랜치에서 하나의 작업이 완료가 되면 다시 통합 브랜치에 병합하는 방식으로 진행됩니다. 토픽 브랜치라고도 합니다.

### ✅ 브랜치 명령어 모음

**새로운 브랜치 생성**

- `$ git branch 새로운 브랜치 이름`

**새로운 브랜치 생성 후 해당 브랜치로 전환**

- `$ git switch -c 새로운 브랜치 이름`
- `$ git checkout -b 새로운 브랜치 이름`

**브랜치 목록 확인**

- `$ git branch`

**브랜치 목록과 각 브랜치의 최근 커밋 확인**

- `$ git branch -v`

**브랜치 삭제**

- `$ git branch -d 삭제할 브랜치 이름`
- `$ git branch -D` 해당 명령어는 병합하지 않은 브랜치를 강제 삭제하는 방법입니다.

**브랜치 전환**

- `$ git switch 브랜치 이름`
- `$ git checkout 브랜치 이름`

**브랜치 병합**

- master 브랜치로 dev 브랜치를 병합할 때 (master ← dev)
1. `$ git checkout master`
2. `$ git merge dev`

**로그에 모든 브랜치를 그래프로 표현**

- `$ git log --branches --graph --decorate`

**아직 commit 하지 않은 작업을 스택에 임시로 저장**

- `$ git stash`

## 프로젝트 workflow

[Dangit, Git!?!](https://dangitgit.com/ko)

혼자 작업하기

- git clone : repository 가져오기
- git status : 상태 확인
- git add . : 관리하에 둠
- git commit -m '' : 커밋
- git reset HEAD^ : 최근 커밋 취소
- git reset --hard 커밋 넘버 : 병합 취소/ 이전 커밋으로 돌아가기
- git push origin main : push
- git log : 커밋 로그 확인
- rebase : 커밋의 베이스를 다시 정하고 싶은 경우
- squash : 여러 개의 커밋 로그를 하나로 묶고 싶은 경우
- revert : 커밋 여러 개의 변경 사항을 취소하고 싶은 경우
- —amend : 최근 커밋 메시지를 수정하고 싶은 경우

함께 작업하기

1. Git 연결 git init
2. 리모트 연결 (origin) git remote add origin <repository address>
3. Push 1 git push origin main
4. 리모트 연결 (pair) git remote add pair <repository address>
5. 리모트 확인 git remote -v
6. Pull 1 git pull pair main
7. Push 2 git push origin main
8. Staging area: 버전 관리하에 둠 1 git add .
9. Commit 1 git commit -m ''
10. Pull 2 git pull pair main
11. 충돌 해결하기 비쥬얼 스튜디오 코드에 들어가서 충돌을 해결해 줌
12. Staging area: 버전 관리하에 둠 2 git add .
13. Commit 2 git commit ⇒ merge commit 자동 생성
14. Push 3 git push origin main
15. 완료

브랜치

1. 브랜치 생성 1 

새로운 브랜치 생성 git checkout <branch name>

새로운 브랜치를 생성하고 생성한 브랜치로 이동 git checkout -b <branch name> or git switch -c <branch name>

1. 브랜치 목록 git branch
2. 브랜치 생성 2 git checkout -b feat/signup-oauth
3. 브랜치 이동/전환

git switch <branch name>

git checkout <branch name>

1. 브랜치 병합 git merge feat/signup-oauth
2. Push git push origin feat/signup
3. 작업 임시 저장 git stash
4. 완료

[https://www.notion.so/Git-Merge-9312bb14511e4643b0729ac8546d2ee3](https://www.notion.so/Git-Merge-9312bb14511e4643b0729ac8546d2ee3)