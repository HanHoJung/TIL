# 트리(Tree)

[TOC]

## 트리(Tree)

> 정의

Tree는 node로 이루어진 자료구조 입니다.

1. 하나의 root node를 갖는다.
2. root node는 0개 이상의 child node를 가집니다.
3. child node 또한 0개 이상의 자식 노드를 가집니다(반복적으로 정의 됩니다.)
4. Tree는 cycle이 존재하지 않습니다.
5. 비선형 자료구조로 계층적인 관계를 표현할 때 자주 사용됩니다.
6. cycle이 없는 하나의 Connected Graph(연결그래프)



> 용어

![](https://cdn-images-1.medium.com/max/800/1*5448MFrRZxxkHm-GQIxkdQ.png)

- root node: 트리 구조의 최상위 위치한 node
- leaf node(terminal node): 자식이 없는 node
- internal node(nonterminal node): leaf node가 아닌 node
- sibling node: 부모가 같은 node의 집합
- level: 트리의 각층의 번호
- height: Tree의 최대 level
- degree: 한 node가 가지고 parent node의 개수
- sub tree: 큰 tree에 속하는 작은 tree



> 종류

**Binary Tree(이진트리)**

- root node를 중심으로 두 개의 sub tree로 나누어진다.
- 나누어진 두 sub tree도 모두 Binary tree여야 한다.
- node가 존재할 수 있는 곳에 node가 존재하지 않는다면, empty set node가 존재하게 됩니다.

![](./img/tree.PNG)



**Binary Search Tree(이진 탐색 트리)**

- 노드의 왼쪽 서브트리에는 그 노드의 값보다 작은 값들을 지닌 노드들로 이루어져 있다.
- 노드의 오른쪽 서브트리에는 그 노드의 값과 같거나 큰 값들을 지닌 노드들로 이루어져 있다.
- 좌우 하위 트리는 각각이 다시 이진 탐색 트리여야 한다.



![ì´ì§íìí¸ë¦¬ ì ìì ëí ì´ë¯¸ì§ ê²ìê²°ê³¼](https://t1.daumcdn.net/cfile/tistory/99ACAF335989659B19)



**Full Binary Tree(정 이진 트리)**

- node들의 child node가 하나도 없거나 또는 두 개를 가진 형태로 구성된 tree를 Full Binary Tree라 정의힌다.

  (즉, node는 child node를 단 한개만 가질 수 없음 아이에 없거나 두 개를 가져야 한다.)



**Perfect Binary Tree(포화 이진 트리)**

- 모든 level이 꽉 찬 Binary Tree를 Full Binary Tree라고 정의한다.

- Full Binary Tree는 Complete Binary Tree이다. (역은 성립하지 않음)

- height가 h일때 2<sup>h</sup>-1개의 node를 가집니다.

- node의 총 개수가 n일 때 높이 h는 log(n+1) =h(밑이 2인로그) 입니다.

  ```
  height 0
  1개
  
  height 1
  2개
  
  height 2
  4
  ...
  
  height h-1
  2^(h-1)
  
  1+2+4+..+2^(h-1)
  
  
  노드의 총합을 n이라고 할 때
  2^h-1 = n
  2^h = n+1
  log로 변한하면
  log(n+1)=h
  ```

  

![Types of Binary Tree](http://www.csie.ntnu.edu.tw/~u91029/BinaryTree2.png)



**Complete Binary Tree(완전 이진 트리)**

- Full Binary Tree 처럼 모든 level에 node가 찬 상태는 아니지만 위에서 아래로 왼쪽에서 오른쪽의 순서를 가진 tree를 Complate Binary Tree라 정의한다.
- 모든 sub tree의 레벨이 같아야 하고 마지막 레벨의 node는 반드시 왼쪽 부터 채워져야 합니다.

![](./img/complete.PNG)



> 트리의 구현 방법

![](./img/tree3.PNG)