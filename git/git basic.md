# git 
## 220716 git 기본기 정리
### 목표
* git 사용법을 익히고 익숙해질 때까지 참고
* 따라할 수 있게 순서대로 작성


### backgraound
* git : 분산 버전 관리 프로그램
  * 코드의 history(version)를 관리하는 도구
  * 개발되어온 과정을 파악
  * 이전 버전과의 변경 사항 비교 및 분석

* github : git 기반의 저장소 서비스를 제공하는 곳 (+gitlab, bitbuket)

* commit은 3가지 영역으로 바탕으로 동작
  * working directory : 
    * 내가 작업하고 있는 실제 디렉토리
  * staging area : 
    * commit으로 남기고 싶은, 특정 버전으로 관리하고 싶은 파일이 있는 곳
    * commit하고 싶은 file 맞는지 중간에서 확인하는 공간
    * 실질적으로 버전 관리 대상에서는 제외
    * ex) 버전 관리할 필요 없는 참고용 파일, 아직 개발중인 파일 등등
  * repository : 
    * commit들이 저장되는 곳
    * repository에 저장하는 것을 commit이라고 함
    * 개인 pc는 local repository 라고 함
    * github 같은 저장소는 remote repository 라고 함


### git을 사용해 보자
#### 최초 사용
* git init
  * 해당 디렉토리 git으로 관리 선언
  * 최초에 한번 실행

* git status
  * 현재 git의 상태를 확인하는 명령어
  * untracked 상태인 file 표시
  * 가장 많이 쓰는 명령어
  * master는 branch이다
  * use "git rm --cached ...

* git add "이름"
    * file이 staging area에 위치
    * use "git rm --cached ...

* git add .
  * 현재 디렉토리의 모든 파일을 staging area로 업로드

* git commit
  * 최초 commit의 경우 user 정보가 없으므로 추가해야 함

* git config --global user.email "메일주소"
* git config --global user.name "username"
  * 오타 주의!!!!
  * 잔디가 심기지 않는다면 email 주소가 틀린 것

* git config --global --list
  * 작성된 리스트 확인
  * global은 전역 설정
  * 공용 pc에서 사용한다면 global 빼기

* git commit
  * commit 하기
  * 위서 user 정보를 작성했으므로 commit 진행
  * commit massage 작성하기

* vim
  * edit 모드 : insert키나 i키
  * command 모드 : esc로 빠져나오기
  * :wq  : 저장 후 종료
  * :q   : 저장 안 하고 그냥 종료
  * ! 붙이면 강제 실행 ex) :wq! , :q!

* git commit -m "commit_massage"
  * 위의 과정 생략하기 위해 -m 사용
  * commit 한 것이 무엇인지 확인하기 위해서 메세지 작성
  * 협업할 시 팀별로 massage 작성 규칙 정해서 지키기

* git log
* git log --oneline
  * history 확인
  * --oneline 한 줄로 요약

* git diff
  * gif diff (최근)해쉬앞6자리 (과거)해쉬앞6자리

* git push origin master
  * github 으로 push
  * pc 에 remote repository(github)의 위치를 등록해야 진행 가능

* git remote add "repo별명" "repo주소"
  * ex) git remote add origin https://github.com/ctrlss11/test
  * remote repository 위치 등록

* git remote -v
  * 제대로 되었는지 확인하기

* git push "repo별명" "branch이름"
  * ex) git push origin master
  * 보편적으로 repo이름을 origin으로 작성

* 등록한 remote repository의 url(github)로 연동 진행


#### github에서 local PC로 내려받아보자!
* git clone "repo주소"
  * ex) git clone https://github.com/ctrlss11/test
  * repo주소에 있는 git 복제
  * 복제 최초에 내려받을 때 사용
  * 이후에는 git pull origin master 사용

#### 수정 완료 후 github에 다시 올려보자!
* git add .
* git status
* git commit -m "commit_massage"
* git log

* git push origin master
  * github으로 올리는 것을 push
  * .git 폴더가 존재하는 경로가 맞는지 체크하기!!!
  * (master)가 보인다면 경로가 맞다


#### 수정된 내용을 github에서 받아보자!
* git pull origin master
  * github에서 내려받는 것을 pull
  * 현재의 brunch와 merge 해준다

* 이후에는
  * pull $\rightarrow$ add $\rightarrow$ commit $\rightarrow$ push $\rightarrow$ pull ... 반복

#### 주의사항
* 사용할 때는 sync를 맞춰 줘야 한다!
  * 항상 github을 기준으로
  * 순서를 지키지 않으면 conflict 발생

* conflict 발생 시
  * 

>이미지 추가 예시

![그림!](./img/%EC%8B%9C%EA%B3%A0%EB%A5%B4%EC%9E%90%EB%B8%8C%EC%A2%85.jpg)