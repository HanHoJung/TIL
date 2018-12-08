# Chapter05 재귀 알고리즘

[TOC]

## STORY 05-1 재귀의 기본

> 재귀란

- 어떤 사건이, **자기 자신을 포함**하고 **다시 자기 자신을 사용하여 정의** 될 때 재귀적(recursive)이라고 정의한다.

  ex)

  1은 자연수 입니다.

  자연수 n의 바로 다음 수도 자연수 이다.

> 재귀 호출이란

- "**자기 자신과 똑같은 함수**"를 호출하는 것

  > 직접 재귀(direct)=>자신과 같은 함수를 호출하는 것
  >
  > ```c++
  > void a(void){
  >     a();
  > }
  > ```
  >
  >
  >
  > 간접재귀(indirect)=>다른 함수를 통해 자기 자신과 같은 함수가 호출됨
  >
  > ```c++
  > void a(){
  >     b();
  > }
  > 
  > void b(){
  >     a()
  > }
  > ```
  >
  >

- 유클리드 호제법

  ```c++
  #include <iostream>
  using namespace std;
  int GCD(int a, int b) {
  	int val;
  	if (b == 0) {
  		return a;
  	}
  	return val = GCD(b, a%b);
  
  }
  
  int main(void) {
  	int a, b;
  	cin >> a >> b;
  
  	cout<<GCD(a, b);
  
  }
  
  /*
  22*8
  1. 짧은 변의 길이를 한 변으로 하는 정사각형으로 채움(8*8)
  2. 정사각형으로 나누어 떨어지는 것이 아닌 기준으로 또 정사각형으로 나눔
  3. 모든 사각형이 정하각형으로 구성되면 그 변의 길이가 최대공약수
  */
  
  ```

## STORY 05-2 재귀 알고리즘 분석

> Dynamic Programing(DP)

동적계획법

- 큰 문제를 작은 문제로 나눠서 푸는 알고리즘

- 분할 정복과 공통적은 큰 문제를 작은문제로 나눠서 푼다는 점이 공통점이지만, 분할 정복은 memoization이 필요하지 않는것이 차이가 있다.

> Memoization

   저장된 결과를 배열에 저장한 뒤, 다음에 계산이 필요한 때는 저장한 값을 불러와서 중복을 없애므로 시간 복잡도  

   가 줄어든다. 이러한 방법을 Memoization이라 한다.

  >  Top down(하향식 분석)

-  위에서 아래로 내려오는 방식
-  가독성이 좋고, 점화식을 이해하기 쉽다.

  > Bottom up(상향식 분석)

- for문을 이용해서 처음값부터 다음값을 계산해 나가는 방식

- 함수를 별도로 호출하지 않아 시간과 메모리를 절약할 수 있다.


## STORY 05-3 하노이탑

- 3개의 기둥이 존재한다.
- 모든 원반에서는 번호가 존재하고, 큰 원반 위에 작은 원반이 놓아져야 한다.(역전 되는 현상이 존재하면 안 된다.)
- 모든 원반을 한 쪽기둥으로 옮겨야 한다.

```
- 시작 기둥/ 중간 기둥/ 목표 기둥
- 쌓여있는 원반에서 n-1인 원반이 한 그룹이다.

원반의 갯수 2개 일때,
STEP01.그룹을 중간 기둥으로 옮긴다.
STEP02.원반 2를 목표 기둥으로 옮긴다.
STEP03.그룹을 목표기둥으로 옮긴다.

원반의 갯수 3개 일때,
STEP01.그룹을 중간 기둥으로 옮긴다.
STEP02.원반 3을 목표 기둥으로 옮긴다.
STEP03.그룹을 목표기둥으로 옮긴다.

원반의 갯수 4개 일때,
STEP01.그룹을 중간 기둥으로 옮긴다.
STEP02.원반 4를 목표 기둥으로 옮긴다.
STEP03.그룹을 목표기둥으로 옮긴다.

참고)
원반이 3개 있을때(1,2,3) top에 1이 있다 가정하고 1을 세번째로 옮길지 2번째 옮길지 고민이 될 수 있다. 그런데 원반 1을 세번째 기둥으로 옮기는 것이 최소 횟수로 하노이탑을 완성할 수 있다.
```

```c++
#include <iostream>
#define A 1
#define B 2
#define C 3
using namespace std;

void hanoi(int n, int srt, int des) {

	if (n > 1)
		hanoi(n - 1, srt, 6 - srt - des);

	printf("원반(%d)을 %d 기둥에서 %d 기둥으로 옮김\n", n, srt, des);

	if (n > 1)
		hanoi(n - 1, 6 - srt - des, des);
}

void hanoi2(int n, char s, char m, char d) {


	if (n > 1)
		hanoi2(n - 1, s, m, d);

	printf("원반(%d)을 %c 기둥에서 %c 기둥으로 옮김\n", n, s, d);

	if (n > 1)
		hanoi2(n - 1,m,s,d);
}


int main(void) {
	int n;
	printf("하노이의 탑\n");
	printf("원반 개수:");
	cin >> n;

	hanoi(n, 1, 3);
	hanoi2(n, 'A','B','C');

}
```



## STORY 05-4 8퀸 문제

- 8개의 퀸을 공격하지 못하게 체스판에 놓은 방법

> 원초적 접근

- 8*8판에 퀸을 1개 놓을 때 64칸 중 아무곳에나 둘 수 있다.
- 그 다음 부터 63, 62,...칸 둘 수 있다.
- 경우의 수: 64 * 63 * 62 * 61 * 60 * 59 * 58 * 57 = 178,462,987,637,760(가지 수)

> 각 열에 퀸을 1개만 배치한다.

- 8 * 8 * 8 * 8 * 8 * 8 * 8 * 8 = 16,777,216(가지 수)
- 가지 뻗기(모든 조합을 나열)
- 하노이탑이나 8퀸 문제 처럼 문제를 세분하고 세분된 작은 문제의 풀이를 결합해 전체 문제를 푸는 것을 Divide and conquer(분할 해결법)이라 한다.(ex. quick sort, merge sort)

```c++
#include <stdio.h>
int pos[8];

void print() {

	for (int i = 0; i < 8; i++) {
		printf("%2d", pos[i]);
	}
	printf("\n");

}


//i열, j행
void set(int i) {
	
	for (int j = 0; j < 8; j++) {
		pos[i] = j;
		if (i == 7)
			print();

		else
			set(i + 1);


	}

}

int main(void) {

	printf("8퀸 문제");
	set(0);
}
```



> 각 열에 퀸을 1개, 각 행에 퀸을 1개 배치한다.

> 대각선 배치 고려



모든 경우를 구하는 방법을 **가지뻗기(branching)**이라 한다. 이러한 가지에서 불필요한 조합을 없애는 것을 **한정(bounding)조작** 이라고 한다. 이 두 개를 조합해서 문제를 푸는 방법을 **분기 한정법(branching and bounding method)**이라한다. 



N-Queen 문제

https://www.acmicpc.net/problem/9663

```c++
#include<iostream>
#include<string.h>
using namespace std;
bool visit[15][15];

int n;
int num;
bool check(int i, int j) {

	int next_i = i;
	int next_j = j;
	//  / check
	while (true) {

		next_i = next_i - 1;
		next_j = next_j + 1;
		if (next_i < 0 || next_j >= n)
			break;

		if (visit[next_i][next_j] == true)
			return false;


	}


	next_i = i;
	next_j = j;

	//  \ check
	while (true) {
		next_i = next_i - 1;
		next_j = next_j - 1;

		if (next_i < 0 || next_j < 0)
			break;

		if (visit[next_i][next_j] == true)
			return false;

	}

	// ^|

	next_i = i;
	next_j = j;

	while (true) {
		next_i = next_i - 1;

		if (next_i < 0)
			break;

		if ((visit[next_i][next_j] == true))
			return false;


	}

	return true;

}



void solve(int node, int cnt) {
	bool decision = false;


	if (cnt == n) {
		num++;
		return;
	}


	for (int i = 0; i < n; i++) {

		if (visit[node][i] == false) {

			decision = check(node, i);

			if (decision == true) {
				visit[node][i] = true;
				solve(node + 1, cnt + 1);
				visit[node][i] = false;
			}


		}

	}


}



int main(void) {

	cin >> n;
	solve(0,0);
	cout << num;

}

```

