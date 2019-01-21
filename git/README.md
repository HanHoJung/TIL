#  Git

[TOC]

![1547378228356](https://i.stack.imgur.com/caci5.png)



## git의 원리

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

- git add f1.txt f2.txt를 하면 .git 디렉토리 내에 **index ** 파일과   **./objects**   디렉터리가 생성됩니다.

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

![commit(4)](D:./assets/commit(4).PNG)

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



