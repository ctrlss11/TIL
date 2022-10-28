## git undoing
* 되돌리기 작업
* 작업 상태에 따라 분류
  * working directory : 
  * staging area : 
  * repository : commit 해버린 경우

## working directory
* git restore {file name}
* 수정한 파일(modified 단계)을 수정 전으로 되돌리기
* 이미 버전 관리가 되고 있는 파일만 되돌리기 가능
* git resotre 로 되돌리면, 해당 내용은 복원x

### git stash
* git stash {file name}
* 수정한 파일(modified 단계)을 stash 공간으로 옮겨 임시 보관
* git stash list
* stash 리스트 확인
* git stash apply {stash ID}
* stash 가져오기
* restore는 복원 불가지만, stash 는 다시 가져올 수 있음

## staging area
* git add를 잘못한 경우
* staging area에 반영된 파일을 working directory로 되돌리기
* unstage
* root-commit 여부에 따라서 (한번도 커밋한적이 없는 파일인가 아닌가)
* root-commit 없는 경우 : 
* git rm --cached {file name}
* root-commit 있는 경우 : 
* git restore --staged {file name}

### git rm --cached 
* to unstage and remove paths only from the staging area
* root-commit이 없는 경우 
* 한번도 커밋을 안한 새로운 파일인 경우
* 혹은 이미 git으로 관리되고 있는 파일 중 앞으로 더이상 관리 안하려고 할 때
* git rm --cached {file name}
* --cached 안쓰면 rm 으로 파일 삭제해버리기 때문에 주의!

### git restore --staged
* the contents are restored from HEAD
* 가장 최근 커밋 상태로 복원
* root-commit이 있는 경우
* 커밋이 한개라도 있을 때
* git restore --staged {file name}

## repository
* 커밋을 완료한 파일을 staging area로 되돌리기
* git commit --amend
* staging area의 상태에 따라서
* staging area에 새로 올라온 내용이 없7다면 :
* 직전 커밋의 메시지만 수정
* staging area에 새로 올라온 내용이 있다면 :
* 직전 커밋을 덮어쓰기
* 이전 커밋을 완전히 수정해서 새 커밋으로 변경하여
* 이전 커밋을 일어나지 않은 일이 되어 히스토리에 남지 않으니 주의
* 팀으로 작업시에는 --amend 사용 지양
* 같은 branch에서 commit이 달라질 수 있음
* 그래서 팀작업시 --amend 로 수정후에는 모든 팀원이 pull로 commit 버전을 맞춘 후 작업

## git reset, git revert
* 특정 시간으로 되돌리기
* 되돌리기를 commit으로 남길지 말지 여부에 따라
* rest : 기록x
* revert : 기록o

### git reset
* 프로젝트를 특정 커밋버전으로 되돌리기
* 특정 커밋으로 되돌아가면, 해당 커밋 이후로 쌓았던 커밋은 모두 사라짐
* git rest [option] {commit ID}
* option에는 soft, mixed, hard
* commit ID는 커밋버전의 hash값, git log --oneline 했을 때 나오는 7자리로 사용해도 무방
* 혹은 git reset HEAD~{숫자}
* HEAD부터 몇 번째 commit으로 되돌아갈지 

* --soft
* 해당 커밋으로 되돌아가고
* 되돌아간 커밋 이후의 파일들을 staging area로 돌려놓음

* --mixed
* 해당 커밋으로 되돌아가고
* 되돌아간 커밋 이후의 파일들을 working directory로 돌려놓음
* option의 default 값

* --hard
* 해당 커밋으로 되돌아가고
* 되돌아간 커밋 이후의 파일들을 모두 working directory에서 삭제
* 기존의 untracked 파일은 사라지지 않고 untracked로 남아있음
* 파일들이 삭제되니 사용시 주의할 것
* git reflog를 사용하여 hash값으로 삭제한 파일 복구 가능

### git reflog
* git reset hard 옵션으로 삭제
* git reflog 으로 reset 이전의 커밋 내역 조회 가능
* 위 커밋 내역에서 hash값으로 reset 하면 hard로 삭제한 파일 복구 가능

### git revert
* 과거를 없었던 일로 만드는 행위, 이전 커밋을 취소한다는 새로운 커밋을 생성
* 해당 커밋을 취소 후 취소를 기록으로 남김
* git rever {commit ID}
* 취소하고 싶은 커밋ID
* 협업시 reset보다 revert 사용 지향

###
* reset은 커밋 내역을 삭제하는 반면, revert는 새로운 커밋을 생성함
* revert는 github 이용해 협업할 때, 커밋 내역의 차이로 인한 충돌 방지 기능
* git reset {commit ID} : 
  * commit ID 에 해당하는 커밋으로 되돌린다
* git revert {commit ID} : 
  * commit ID 에 해당하는 커밋 한 개를 취소
  * commit ID 를 취소 했다는 내용의 새로운 커밋 생성


## branch
* 여러 갈래로 작업 공간을 나누어 독립적으로 작업할 수 있는 git 도구

* 장점
* branch로 독립 공간을 형성하기 때문에 master(원본)에 대해 안전함
  * 정상적으로 동작하는 버전
  * 서비스가 가능한 버전
  * 배포할 수 있는 버전
  * 을 master 에 놔두고
  * branch 를 생성하여 새로운 작업 진행
* 하나의 작업은 하나의 브랜치로 나누어 진행되므로 체계적인 개발 가능
* 빠른 속도, 적은 용량으로 branch 생성

* 조회
* git branch : 로컬 저장소의 브랜치 목록 확인
* git branch -r : 원격 저장소의 브랜치 목록 확인
* 생성
* git branch {branch name} : 새로운 브런치 생성
* git branch {branch name} {commit ID} : 특정 커밋 기준으로 브런치 생성
* 삭제
* git branch -d {branch name} : 병합된 브런치만 삭제 가능
* git branch -D {branch name} : 브런치 강제 삭제
* 흐름
1. 새로운 기능 개발 필요
2. branch 생성하여 그 곳에서 작업
3. 기능 개발 완료
4. master와 merge
5. branch 삭제

###
* git switch
* 현재 브랜치에서 다른 브랜치로 이동하는 명령
* git switch {branch name} : 다른 브랜치로 이동
* git switch -c {branch name} : 브랜치를 새로 생성 및 이동
* git switch -c {branch name} {commit ID} : 특정 커밋 기준으로 브랜치 생성 및 이동
* 생성과 동시에 이동하므로 -c 옵션으로 주로 사용
* switch전에, 해당 브런치의 변경 사항을 반드시 커밋해야함 주의!
* 커밋하지 않은 상태에서 switch하면 브랜치를 이동했음에도 해당 파일이 그대로 남아있음

###
* git log --oneline --all --graph

## git merge
* 분기된 브랜치들을 하나로 합치는 명령어
* master 브랜치가 상용이므로, 주로 master 브랜치에 병합
* git merge {합칠 브랜치 이름}
  * 병합하기 전에 브랜치를 합치려고 하는 메인 브랜치로 switch 해야함
  * 병합의 세 종류
  1. fast-forward
  2. 3-way merge
  3. merge conflict
  
### Fast-Forward
* 마치 빨리감기처럼 브랜치가 가리키는 커밋을 앞으로 이동시키는 방법

### 3-way merge
* 각 브랜치의 커밋 두 개와 공통 조상 하나를 사용하여 병합하는 방법

### Merge Conflict
* 두 브랜치에서 같은 부분을 수정한 경우
* git이 어느 브랜치 내용으로 작성해야 하는지 판단하지 못해 충돌이 발생
* conflict를 해결하며 병합하는 방법
* 보통 같은 파일의 같은 부분을 수정했을 때 자주 발생
* conflict 해결 후, add . , commit 까지 

## shared repository model
* 원격 저장소가 자신의 소유이거나 collaborator로 등록되어 있는 경우
* master 브랜치에 직접 개발하는 것이 아니라
* 기능별로 브랜치를 따로 만들어 개발
* 기능 개발이 완료되면 원격저장소의 본인 branch에 push
* git push origin {branch name}
* Pull Request를 사용하여 master에 반영해달라는 요청을 보냄
* 팀원 간 변경 내용에 대한 소통 진행
* 병합이 완료된 브랜치는 원격 저장소에서 삭제

1. clone
2. branch 생성 / branch 에서 기능 개발
3. 구현 완료 후 본인 branch 에 push
4. github에서 Pull Request
5. master로 변경
6. merge가 완료된 master를 pull
7. 본인 branch 삭제

###
* 오픈 소스 프로젝트와 같이, 자신의 소유가 아닌 원격 저장소인 경우
* Fork 하기 : 원본 원격 저장소를 그대로 내 원격 저장소에 복제
* 기능 완성 후 복제한 내 원격 저장소에 push
* Pull Request 를 통해 원본 원격 저장소에 반영할 수 있도록 요청 -> contributor

* 원본 원격 저장소를 동기화 하기 위해 원본 주소 remote 로 등록
* 기능 구현 후 내 원격 저장소에 push
* 원본 원격 저장소에 Pull Request 

### git-flow
* git 브런치 전략
* 5개의 branch로 나누어 소스코드를 관리
  * master : 제품으로 출시될 수 있는 브런치
  * develop : 다음 출시 버전을 개발하는 브런치
  * feature : 기능을 개발하는 브런치
  * release : 이번 출시 버전을 준비하는 브런치
  * hotfix : 출시 버전에서 발생한 버그를 수정 하는 브런치
* 대규모 프로젝트에 적합한 브런치 전략

### github-flow
* PR 활용
* 병합 후 자동으로 배푸

### gitlab-flow
* master, product, preproduct 따로

### 
* 팀별로 협의해서 branch 전략 수립
* branch 자주 사용 할 것을 권장