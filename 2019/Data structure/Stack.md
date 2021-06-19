# Stack

[TOC]

## 1. 스택(Stack)이란

**스택**이란, 데이터를 일시적으로 저장하기 위해 사용하는 자료구조로, 데이터의 입출력 순서는 LIFO(Last In First Out) 구조를 따릅니다.

**스택**

- push: 스택에 데이터를 넣는 작업
- pop: 데이터를 꺼내는 작업
- bottom: 스택에 가장 밑바닥



## 2. 수식의 표기법

### - Prefix notation(전위 표기법)

- 연산자를 피연산자 앞에 표기하는 방법
- +5/27



### - Infix notation(중위 표기법)

- 연산자를 피연산자 가운데에 표기하는 방법
- 5+2/7



### - Postfix notation(후위 표기법)

- 연산자를 피연산자 뒤에 표기하는 방법
- 527/+
- 후위 표기법 계산법
  - 피연산자는 무조건 스택으로 옮긴다.
  - 연산자를 만나면 스택에서 두 개의 피연산자를 꺼내서 계산한다.
  - 계산결과는 다시 스택에 넣는다.
  - 스택에서 먼저 꺼낸 피연사자가 두 번째 피연산자가 되고(오른쪽 피연산자) 나중에 끄낸 연산자는 첫번째 피연산자(왼쪽 피연산자)가 된다. 



**전위 표기법**과 **후위 표기법**은 수식의 연산자의 배치순서에 따라서 연산순서가 결정되기 때문에 수식을 계산하기 위해서 연산자의 우선순위를 알 필요가 없고, 소괄호도 삽입되지 않으니 소괄호에 대한 처리도 불필요하다. (연산자 우선순위, 소괄호 처리 신경 써줄 필요가 없다.)



### 중위표기법을 후위표기법으로 변경하는 로직

- Infix, Postfix, Operator배열

- Infix 배열에서, 피연산자는 Postfix에 저장한다.

- Infix 배열에서, 연산자는 Operator 배열에 저장한다.

  - Infix 배열의 연산자 우선순위 > Operator의 연산자 우선순위 

    => Infix 배열의 연산자를 Opeartor 배열에 push

  - Infix 배열의 연산자 우선순위 < Operator의 연산자 우선순위 

    =>Opeartor 배열 pop한 데이터를 Postfix 배열에 push

       (Infix 배열의 연산자 우선순위 > Operator의 연산자 우선순위 될 때  또는, Operator empty 가 될 때 까    지)

    =>그 후, Infix배열 연산자 Opertor 배열에 push

  - 연산자 우선순위가 같으면 Operator 안에 연산자가 pop

  - Infix배열의 연산자가 '(' 이면 연산자 우선순위와 관계없이 무조건 Operator 배열에 push

  - Infix배열의 연산자가 ')' 이면 Operator 배열의 '('가 될 때까지 pop

cf)

(1*2+3) / 4



후위 표기식 문제

https://vitamindragon.github.io/algorithm/Algorithm-9/





