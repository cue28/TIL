# Linux 기초

### CLI 기본 명령어

- GUICLI (Command-Line Interface) - terminal
- 입력하는 글자와 출력되는 글자로 컴퓨터와 소통
- 프롬프트(prompt) 키보드의 입력을 확인하고 편집할 한 줄의 공간

### **기본적인 명령어**

- `pwd` (print working directory`폴더`) 현재 위치 확인
- `mkdir` 새로운 폴더 생성
- `ls` (list) 폴더, 파일 목록 출력
    - 옵션 `l` : `ls-l` 폴더나 파일의 포맷을 전부 표현
    - 옵션 `a` (all) : `ls-a` 숨어있는 폴더나 파일을 포함한 모든 항목을 터미널에 출력
    - 옵션 입력 시 `` 를 이용해 옵션을 입력했다고 컴퓨터에 전달
    - 출력 시, `d` (폴더) / `` (파일)
- `open` 현재 폴더를 파일 탐색기로 여는 명령어 (open .)
- `cd` 폴더에 진입`cd .` 현재 폴더`cd ..` 상위 폴더`cd ./hi` 현재 폴더(`./`) 아래의 hi 폴더로 진입
- `touch` 새로운 파일 생성 (ex. hi.txt)
- `cat` 파일의 내용 터미널 출력
- `rm` (remove) 폴더나 파일 삭제 (즉시 삭제)
    - `rm` `bye.txt` (파일 삭제)
    - `rm` `rf bye` (폴더 삭제)
    - 옵션 `r` (recutsive:폴더 지울 때)옵션 `f` (force:질문 받지 않고 삭제)
- `mv` (move) 폴더나 파일 위치 이동, 이름 변경
    - `mv` `폴더나 파일 이름` `도착 폴더 이름`(ex. mv bye.txt bye/)
    - `mv` `변경할 이름` `변경될 이름`(ex. mv bye.txt helloworld.txt)
- `cp` (copy) 폴더나 파일 복사`cp` `원본 파일 이름` `복사할 파일 이름`
- `sudo` 관리자 권한 이해관리자 권한을 획득하는 명령어절대 경로 : `pwd` 로 확인 , 루트폴더(`/`)상대 경로 : 현재 위치로부터 상대적인 위치
- `clear` 터미널 청소
- `/` 루트 디렉토리 (절대 경로의 시작)
- `~` 홈 디렉토리 (상대 경로의 시작)

### **nano**

- `nano` `hello.js` 실행

### 패키지와 패키지 매니저

- 패키지 : 여러 파일을 하나의 파일로 저정한 압축 파일
- 패키지 매니저 : 패키지의 설치, 변경, 삭제 등 관리를 편하게 해주는 도구 like 앱스토어모든 패키지의 저장소 위치 저장
- Homebrew 패키지
    - `brew update` 업데이트 여부
    - `brew outdated` 필요한 파일 조회
    - `brew upgrade 프로그램이름` 업데이트
    - `brew info 프로그램이름` 정보 확인
    - `brew install 프로그램이름` 설치
    - `brew list` 설치된 항목 보기
    - `brew uninstall 프로그램이름` 삭제
    - `brew search 검색어` 검색

### Node.js

- nvm, Node.js, npm
- node 명령어를 사용하여 JavaScript 파일 실행
- 깃허브 해당 프로그램 discussions에서 error를 찾아주어진 명령어 실행시켜 진행할 수 있었다.
- 터미널로 버전 확인 완료 !
- `namo 파일이름.js` (텍스트 에디터 열기) -> JS로 명령 가능
- `npm run 스크립트 이름`
- `npm run start node.js` 앱 실행

### Git 기초

### 버전 관리 시스템

- 작업한 코드(내용)을 보존해 주는 시스템(Version Control System)
- 버전 관리 시스템의 필요성
    - 각 버전별로 변경된 이력을 저장하여, 이전 버전으로 돌아가야할 상황이 발생항 경우 그 기록으로 돌아갈 수 있다.
    - 백업, 협업에 용이

### **Github와 Git의 관계**

- 코드를 효율적으로 관리하기 위함 분산형 버전 관리 시스템
- 백업 복사본 (스냅샷)스냅샷을 만들어주는 과정 (commit)
- Git Repository(저장소)를 관리할 수 있는 클라우드 기반 서비스
- Local Repository : 내 컴퓨터의 개인 저장소
- Remote Repository : 원격 온라인 서버 저장소 (공유 가능)
- Github의 Git명령어
    - Fork : 원격 저장소를 내 원격 저장소로 가지고 오는 작업
    - Clone : 내 컴퓨터로 가지고 오는 작업
    - commit : 변경된 내용 저장
    - Push : Remote Repository에 올려주는 작업
    - Pull request : 제안한 코드 변경사랑 반영 여부 요청
- Git 환경설정

```
git config --global user.name "나의 사용자 이름"
git config --global user.email "내 이메일 주소"
```

### Git

- Github의 기능과 Git 명령어
    - clone : 원격 Repository ➡️ 내 로컬에 복사
    - status :commit되기 전 까지의 상태
    - restore : commitm staged 변경사랑을 폐기ex. `git restore <파일명>`구현 중 잘못되었다는 걸 감지했을 떄 내가 작업한 코드를 밀어버릴 수 있음.
    - add :Work space에서 Staging area로 파일을 옮겨commit 할 수 있는 상태로 만들어 줌ex. `git add <파일명>` / `git add.` 모든 파일
    - `git commit -m '코멘트'` 코멘트 작성
    - reset : Remote Repository에 업로드 되지 않고 Local Repository에만 commit 해 놓은 기록이라면 commit 취소하는 명령어ex. `git reset HEAD^` 가장 최신의 commit 취소
    - push : Remote Repository에 업로드ex. `git push origin branch`
    - `git log` 현재까지 commit된 내역 확인
    - Pull Request(PR) : 내가 push한 변경 사항에 대해서 다른 사람들에게 알리는 것 ➡️ Github 웹사이트 상의 Compare & pull request
- 함께 작업
    - `git init` 기존 디렉토리를 Git Repository로 변환하거나 Repository를 초기화하는 데 사용합니다.
    - `git remote add origin <나의 Repository주소>` 나의 Remote Repository에 연결
    - `git remote add pair <상대방의 Repository주소>` pair의 Remote Repository에 연결
    - `git pull <shortname> <branch>` 내용 가져오기 -> 자동으로 병합
    - 충돌 ( 자동 병합이 불가능한 경우 - ex)동일한 라인을 수정한 파일..)`git status` 어떤 파일이 충돌하고 있는지 -> 파일 수정 후 staging area로 추가해야합니다.
    - `git add` ➡️ `git commit` ➡️ `git push orgin master`
- Git(Local Repository)의 세 가지 영역 및 상태
    - Committed
    - modified / unmodified기존에 commit했던 파일을 수정한 상태 / 수정하지 않은 상태
    - stagedcommit이 가능한 상태 (staged area에 add하는 작업 필요)
- Remote Repository 페어와 공유하며 협업하기