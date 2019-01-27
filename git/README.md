#  Git

[TOC]

![1547378228356](https://i.stack.imgur.com/caci5.png)



## git의 원리(Add,Commit,Status)

해당 공부는 git이 내부적으로 어떻게 동작하는지 알아보기 위한 학습 입니다.

**gistory**라는 tool을 사용하여 git의 내부 동작을 살펴보는 형식으로 진행 하였습니다.



### Install&Excute

> Install

```bash
pip install gistory
mkdir 파일명
cd 파일명
git init
cd .git
gistory
http://localhost:8805/
```



### **ADD**

> git add의 원리

```bash
cd .git
gistory
```

![add(1)](./assets/add(1).PNG)

- .git 디렉토리 안에 들어있는 파일 또는 디렉토리의 모습이다.



```bash
vim f1.txt
vim f2.txt
git add f1.txt f2.txt
cd .git
gistory
```



![add(1)](./assets/add(2).PNG)

- git add f1.txt f2.txt를 하면 .git 디렉토리 내에 **index** 파일과   **./objects**   디렉터리가 생성됩니다.

- **./objects** 디렉터리 내에 생긴 각각 파일은 f1.txt f2.txt 파일을 의미합니다. 또한, 그 파일의 내용은

  f1.txt에 작성된 내용 f2.txt에 작성된 내용이 저장되어 있습니다.

- **index** 파일은 각 object 들의 경로와 파일명이 저장되어 있습니다.



```bash
cp f1.txt f3.txt
git add f1.txt f2.txt
cd .git
gistory

```

![add(3)](./assets/add(3).PNG)

- f1.txt를 복사한 f3.txt는 objects 파일은 파일명을 달라도 내용이 같으면 같은 object 파일을 가르킨다.
- 만약, f1.txt를 10000번 복사한다고 했을때도 하나의 object 파일만 존재하지 어마어마한 중복을 제거할 수 있는 장점을 가진다.
- 정리하자면 git에서 어떠한 파일을 생성하고 만들어지는 과정을 대략 이렇다.
  - 파일이 생성하고 add 명령을 하면 **파일 안에 저장되어 있는 내용**과 **부가 정보**를 압축한다.
  - 그  후 sha1 알고리즘을 적용하여 일정한 길이의 텍스트를 얻어낸다.
  - 그 결과 나온 앞 두자리가 디렉토리가 되고 나머지 뒤가 파일명이 된다.
  - 또한, index 파일에 추가된 파일의 object 파일명 주소와 파일이름을 같이 저장한다.



### COMMIT

> git commit의 원리

```bash
vim f1.txt
vim f2.txt
git add *
```

![commit(1)](./assets/commit(1).PNG)

```bash
git commit -m "1"
```

![commit(2)](./assets/commit(2).PNG)

- commit을 하면, 두 개의 object 파일이 생성된다.

  1. commit 시점의 f1.txt와 f2.txt 파일명을 가리키는 object 파일이 생성된다.

  2. 1번 파일명을 가리키는 파일, commit 메시지 , 작성자를 저장하는 object 파일이 생성된다.



```bash
f1.txt 내용 수정
git add f1.txt
```



![commit(3)](./assets/commit(3).PNG)

```bash
git commit -m 2
```

![commit(4)](./assets/commit(4).PNG)

- objects 파일의 종류
  1. 파일의 내용을 담고 있는 파일(blob)
  2. blob 파일의 이름과 파일명을 가르키는 파일(tree)
  3. tree, parent(이전 commit), commit 작성자, commit 내용을 저장하는 파일(commit)

- commit을 하게 되면 즉, 버전이 생성되면 버전마다 각각의 tree 파일을 가지고 있다. 우리는 tree 파일을 통하여 그 시점의 프로젝트 내의 폴더의 현재 내용을 알 수 있다. 이러한 것을 스냅샷이라고 한다. 



### STATUS

> status의 원리

![status(1)](./assets/status(1).PNG)

- 현재 상태는 working director 영역과 Index, repository 영역의 파일의 내용이 모두 같은 상태를 의미합니다.

  즉, 디렉토리 내의 변화가 이루어지지 않은 상태를 나타냅니다. 



![status(2)](./assets/status(2).PNG)

- 파일이 수정 되었음을 감지하는 방법을 추정해보면 대략 이렇다. Index 파일은 항상 파일의 최신 상태를 나타내고 있습니다. 만약 file이 수정되면 파일의 내용을 sha1 알고리즘으로 해시 한 파일명과 Index 파일 내용과 다르면 파일이 수정됨을 알 수 있습니다.

![status(3)](./assets/status(3).PNG)

- git은 Index라는 object 파일과 최신 commit을 나타내는 object 파일의 내용 비교를 통하여 그 내용이 일치하면 **commit할 내용이 없는 것**이고 일치하지 않는다면 **commit 대기 상태**를 나타냅니다.







## git의 원리(branch)

### branch 만들기

> branch

**브랜치의 목록을 볼 때**

`git branch`

**브랜치를 생성할 때** 

`git branch "새로운 브랜치 이름"`

**브랜치를 삭제할 때**

`git branch -d "브랜치 이름" `

**병합하지 않은 브랜치를 강제 삭제할 때** 

`git branch -D "브랜치 이름"` 

**브랜치를 전환(체크아웃)할 때**

`git checkout "전환하려는 브랜치 이름"`

**브랜치를 생성하고 전환까지 할 때** 

`git checkout -b "생성하고 전환할 브랜치 이름"`





### branch 정보확인

> branch 비교

**브랜치 간에 비교할 때**

`git log "비교할 브랜치 명 1".."비교할 브랜치 명 2"`

```bash
git log master..exp
//master에는 없고 exp에 있는것만 보여줌

git log exp..master
//exp 없고 master에 있는것만 보여줌
```

`git log -p "비교할 브랜치 명 1".."비교할 브랜치 명 2"  `(소스코드 까지 보여줌)



**브랜치 간의 코드를 비교 할 때** 

`git diff "비교할 브랜치 명 1".."비교할 브랜치 명 2"`

```bash
git diff mater..exp
//exp에 있는것은 +로 표시 없는것은 -로 표시

git diff exp..master
//master에 있는것은 +로 표시 없는것은 -로 표시
```



**로그에 모든 브랜치를 표시하고, 그래프로 표현하고, 브랜치 명을 표시하고, 한줄로 표시할 때** 

`git log --branches --graph --decorate --oneline`



### branch 병합

> branch 병합

 **A 브랜치로 B 브랜치를 병합할 때 (A ← B)**

`git checkout A`

`git merge B`





### branch 수련

> fast forward

 A 브랜치에서 다른 B 브랜치를 Merge 할 때 B 브랜치가 A 브랜치 이후(B브랜치가 앞 서 있는 상황)의 커밋을 가리키고 있으면 그저 A 브랜치가 B 브랜치와 동일한 커밋을 가리키도록 이동시킬 뿐이다.

별도의 commit을 생성하지 않음



> merge commit

공통인 부모가 다르면 fast commit을 할 수 없습니다. 이 때는 merge commit을 하게 됩니다.

Git은 각 브랜치(master,iss53)가 가리키는 공통 조상 commit을 찾고 이를 이용하여 3-way Merge를 수행 합니다.

3-way Merge의 결과로 별도의 커밋을 만들고나서 해당 브랜치(병합의 주체.여기서는 master)가 그 commit을 가리키도록 이동 합니다. 이렇게 병합된 commit은 부모가 여러개고 Merge commit이라고 부릅니다.

cf)

fast forward은 commit을 생성하지 않음 



![merge](./assets/merge(1).PNG)

![merge](./assets/merge(2).PNG)

![merge](./assets/merge(3).PNG)

![merge](./assets/emerge(4).PNG)

![merge](./assets/merge(5).PNG)

![](https://git-scm.com/book/en/v2/images/basic-merging-1.png)

![](https://git-scm.com/book/en/v2/images/basic-merging-2.png)

https://git-scm.com/book/ko/v2/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%B8%8C%EB%9E%9C%EC%B9%98%EC%99%80-Merge-%EC%9D%98-%EA%B8%B0%EC%B4%88



### branch 병합 시 충돌해결

> conflict

자동으로 합칠 수 없는 경우에는 conflict 해결을 사용자가 직접 해주어야 한다.

![](./assets/conflict.PNG)

![conflict2](./assets/conflict2.PNG)

cf)

'<<<<<<< HEAD' 부터 '======='  사이의 구간이 현재 checkout된 브랜치의 파일의 내용이고 '=======' 부터 '>>>>>>> exp'  구간이 병합하려는 대상인 exp 브랜치 파일의 코드 내용 입니다.



## stash

> stash

다른 branch로 checkout 해야 하는데 아직 현재 브랜치의 작업이 끝나지 않은 경우 commit 하기가 애매 합니다.

이러한 경우 stash를 이용하면 작업중이던 파일을 임시로 저장해둘 수 있습니다. 그 후 다른 branch로 이동하고 작업을 끝낸 후에 원래 branch로 복귀한 후에 이전에 작업한 내용을 stash를 통해 복구할 수 있습니다.

- stash는 stack처럼 최근에 stash한 내용을 저장한다.(stack자료구조)

- stash는 working copy(즉, 한 번이라도 add한 파일)에 한 번이라도 올라온 파일만 저장한다.

- git stash를 적용하면 우리가 작업한 내용을 숨길 수 있음

  

**stash 수행**

`git stash` 또는 `git stash --save`



**stash 목록**

`git stash list`



**stash 적용**

`git stash apply`



**stash 삭제**

`git stash drop`



**stash 적용하고 삭제**

`git stash pop`//git stash apply; git stash drop;





## git의 원리(branch2)

> branch

이번 chapter에서는 branch의 동작 원리에 대하여 알아보도록 하겠습니다.

```bash
git init
```

![](./assets/branch(1).PNG)

- git init을 하게 되면 HEAD라는 텍스트 파일이 생성 됩니다.
- HEAD라는 텍스트 파일의 내용은 **ref:refs/heads/master** 라는 내용이 적혀있습니다.



```bash
vim f1.txt
git add f1.txt
```

![](./assets/branch(1).PNG)

- 파일 하나를 만들고 add 명령을 통해 추적을 해도 HEAD 파일의 내용은 변하지 않습니다.

```bash
git commit f1.txt -m "1"
```

![](./assets/branch(2).PNG)

- commit을 한 시점부터 refs/heads/master 파일이 생성 됩니다.
- refs/heads/master 파일은 최신 commit의 object id를 가르키고 있습니다.
  - commit 파일과 commit 파일 안에 object(tree)파일 또 그 안을 들어가 object(blob )파일을 통해 우리는 현재 시점의 파일의 상태를 알아볼 수 있습니다.

```bash
vim f2.txt
git add f2.txt
git commit f2.txt -m '2'
```

![](./assets/branch(3).PNG)

- commit을 수행한 순간 refs/heads/master 파일의 내용은 최신 commit을 가르키고 있습니다. 이로서 우리는 ref:refs/heads/master라는 파일은 항상 최신 commit의 object id를 가르킴을 알 수 있습니다.

```bash
git branch exp
git checkout exp
```

![](./assets/branch(4).PNG)

- branch를 수행하면 refs/heads/exp라는 파일이 생성됩니다.

- git checkout을 수행하면 HEAD 파일이 refs/heads/exp를 가르킴니다.

- 이로서 우리가 checkout을 할 때에 파일이 내용이 바뀌는 원리에 대해 추측해 볼 수 있습니다.

  HEAD라는 파일을 통해 해당 branch가 변경되고 각각 branch들이 가지고 있는 refs/heads/브랜치명

  파일이 가리키는 commit 파일을 통하여 우리는 그 시점(snap shot)의 파일의 상태를 알 수 있습니다.

- 더불어, .git/refs/heads/exp를 지우면 exp라는 branch가 삭제 됩니다.

  반대로 .git/refs/heads/exp를 생성하고 commit object id를 저장하면 branch가 생성됩니다.



> reset과 checkout

이전 commit으로 돌아가고 싶을 때는 `reset` 이라는 명령어를 사용하면 과거로 돌아갈 수 있습니다.

<명령어>

`git reset --hard "commit object id" `

예를 들어서 상황을 설명해보도록 하겠습니다. 현재 4개의 commit을 수행한 상태입니다. 이 상태에서 2번 commit의 상태로 돌아가보도록 하겠습니다.

![](./assets/branch(5).PNG)

```bash
git reset --hard 43e8787ae3c9bafe91b7888e7b7492886b736d03
```

![](./assets/branch(6).PNG)

- refs/heads/master라는 파일은 4번 commit object id에서 2번 commit의 object id를 가르키고 있습니다.

- 이렇게 reset 명령어는 해당 branch의 refs/heads/master의 내용을 변경하여 이전의 상태로 돌아가게 됩니다.

- 또한, reset을 하더라도 4번 log는 삭제되지 않습니다.

- ORIG_HEAD 파일과  .\logs\refs\heads\브랜치명 파일에는 우리가 명령을 수행했던 log들이 남아 있습니다.

  - ORIG_HEAD

    ```bash
    위험한 명령(정보를 제거할만한 명령 )을 수행하기 전에 ORIG_HEAD 파일 내에 현재 checkout branch가 가리키는 최신 commit id를 기록한다음에 reset 명령을 수행합니다.
    
    git reset --hard ORIG_HEAD //reset 이전 상태로 돌아갈 수 있습니다.
    ```

  - .\logs\refs\heads\브랜치

    ```bash
    checkout branch에서 했었던 명령들에 대한 기록들이 저장되어 있습니다.
    
    git reflog //이 명령어를 통해 ./logs/refs/브랜치 log 파일의 정보를 볼 수 있습니다.
    git reset HEAD@{1} //해당 상태로 돌아갈 수 있다.
    ```

    

![](./assets/branch(7).PNG)



- checkout commit id를 통하여 특정 commit 을 가리키는 detached  상태로 돌아갈 수 있다.

  이렇게 전환 branch는 HEAD 파일이 특정 commit을 가르킴(branch의 경우 refs/heads/브랜치를 가르킴)

  (실제 브랜치는 아님)

  ```bash
  git checkout "commit id"
  ```

  ![](./assets/branch(8).PNG)





> reset

- git reset에는 다양한 옵션이 존재합니다.(soft, mixed, hard)
- hard는(working directory, index, repository의 내용이 모두 삭제)
- mixed(index, repository의 내용이 모두 삭제)
- soft(repository 내용만 삭제)

![img](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/2676/5131.png)



> merge & conflict

```bash
1번 commit(master branch)
f1.txt
function(){
    return 'common'
}

2번 commit(exp branch)
f1.txt
function(){
    return 'exp'
}

3번 commit(master branch)
function(){
    return 'master'
}

git merge exp 
충돌이 발생
```

![](./assets/branch(9).PNG)

- conflict가 발생한 상황에서  index 파일에 번호가 붙게 된다.

  - 1번으로 적힌 파일은 master와 exp 공통인 조상의 파일의 내용이다.

    ```c
    function(){
        return 'common'
    }
    ```

  - 2번으로 적힌 파일은 exp 파일의 내용이다.

    ```c
    function(){
        return 'exp'
    }
    ```

  - 3번으로 적힌 파일 master 파일의 내용이다.

    ```c
    function(){
        return 'master'
    }
    ```

    

- ORIG_HEAD 파일도 병합은 위험한 작업이니 현재 commit object id를 저장하고 병합작업을 수행한다.

- MERGE_HEAD 파일은 merge가 될 브랜치의 최신 commit을 가리킨다.(여기서는 exp branch의 commit)

- 충돌 파일의 내용을 가리키는 object(blob) 파일도 생성된다.

- git mergetool 명령어를 통해 충돌부분을 해결할 수 있습니다.

  ![](./assets/branch(10).PNG)





> 3way-merge

- BASE는 ME와 Other의 공통의 조상

- 2way merge 방식은 Base는 보지않고 Me와 Other를 비교해서 병합하는 방식 입니다.
- 3way merge는 Base 참고하여 Me, Other를 비교해서 병합하는 방식 입니다.
  - 3way는 Me, Base, Other이 모두 다를때만 conflict 발생

![img](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/2676/5133.png)



```
3way merge에서, ME에서 OTHER로 병합할 때
ME  BASE OTHER
A     A
결과는 빈칸이다. ME는 BASE로 부터 파일을 수정하지 않았고 Other는 수정했으므로 다른 사람이 채택된것이 채택된다.

ME  BASE OTHER
     D     D
결과는 빈칸이다. ME만 원래에서 바겼기 때문입니다.     
```

