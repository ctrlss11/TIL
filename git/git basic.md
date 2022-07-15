# git 기본기 정리

* README.md
  * githup 프로젝트에서 가장 먼저 보는 문서
  * sw와 항상 함께 배포
  * README **대문자**로 작성
  * 프로젝트 할 때, 그 때 바로 쓰자. 안그러면 피눈물 흘린다 ㅠㅠ
  * 매번 README 쓰는 연습 하기!! 


* commit은 3가지 영역으로 바탕으로 동작
  * working directory : 
    * 내가 작업하고 있는 실제 디렉토리
  * staging area : 
    * commit으로 남기고 싶은, 특정 버전으로 관리하고 싶은 파일이 있는 곳
    * commit 하고싶은 file 맞는지 중간에서 확인하는 공간
    * 실질적으로 버전관리 대상에서는 제외
    * ex) 버전관리할 필요 없는 참고용 파일, 아직 개발중인 파일 등등
  * repository : 
    * commit들이 저장되는 곳
    * repository에 저장하는 것을 commit이라고 한다


* git init
  * 해당 디렉토리 git으로 관리 선언

* git status
  * 현재 git의 상태를 확인하는 명령어
  * 가장 많이 쓸 명령어!!!
    * branch는 master 이다
    * untracked 상태인 file 알려줌
    * use "git add ... 

* git add file명
    * file이 staging area에 위치
    * use "git rm --cached ...

* git add .
  * 현재 디렉토리의 모든 파일을 staging area로 업로드 하겠다

* git commit
  * 최초 commit의 경우 user 정보가 없어서 알려달라
* git config --global user.email "메일 계정"
* git config --global user.name "name"
  * 오타 주의!!!!
  * 잔디가 심기지 않는다면 email 주소가 틀린것

* git config --global --list
  * global은 전역설정
  * 공용 pc에서 사용한다면 global 삭제하고 쓰기
  * 리스트 확인

* git commit
  * massage 작성하기

* vim
  * edit 모드 : insert키나 i키
  * command 모드 : esc로 빠져나오기
  * :wq     : 저장후 종료
  * :q      : 저장 안하고 그냥 종료
  * ! 붙이면 강제 실행 ex) :wq! , :q!

* git commit -m "commit_massage"
  * 위의 과정 생략하기위해 -m 사용
  * commit 한 것이 무엇인지 확인하기 위해서 메세지 작성!

* git log
* git log --oneline
  * history 확인
  * --oneline 한줄로 확인

* git diff
  * gif diff (최근)해쉬앞6자리 (과거)해쉬앞6자리

* pc 에 remote repository의 위치를 등록
* git push origin master
    
* git remote add repo별명 repo주소
* git remote add origin https://github.com/ctrlss11/test

* git remote -v
  * 제대로 되었는지 확인하기

* git push repo별명 branch이름
* git push origin master

* github에서 허용 진행

* github에 올라와 있는 것을 local에 내려 받아보자!
* git clone repo주소
* git clone (https://github.com/ctrlss11/test)

* 수정완료후 github에 다시 올려보자!
* git push origin master
  * .git 있는 경로 맞는지 체크하기!!!


* github에서 수정된 내용을 받아보자!
* git pull origin master


* 수정하려면 sync를 맞춰 줘야한다!
  * 항상 github을 기준으로!!!
  * 순서를 지키지 않으면 conflict 발생


>이미지 추가하기

![그림!](./img/%EC%8B%9C%EA%B3%A0%EB%A5%B4%EC%9E%90%EB%B8%8C%EC%A2%85.jpg)