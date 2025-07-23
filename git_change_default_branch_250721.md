# Git 에서 Default branch를 변경했을 때 로컬에서 해야할 업데이트
1. git branch -m <이전 branch> <새로운 branch>
    - 이전 branch를 새로운 branch로 Rename한다. 
2. git fetch origin
    - 변경된 remote Repo를 패치한다.
3. git branch -u <리모트 branch> <로컬 branch>
    - 예) git branch -u origin/master master
    - 리모트 branch가 로컬 branch를 추적하도록 설정
4. git remote set-head <리모트 Repo 별명> -a
    - 원격 저장소의 기본 branch(HEAD)가 어디를 가르키는지 자동으로 감지하고 로컬에 반영
