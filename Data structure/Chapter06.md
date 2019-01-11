# Chapter06 정렬(Sorting)

[TOC]

> ## 정렬(Sorting)

정렬이란 **key(이름, 학번, 키 등)의 대소**를 이용하여 **데이터 집합**을 **일정한 순서로** **나열**하는 작업을 의미한다.



> ## 정렬 알고리즘 분류

- stable 알고리즘

​       stable 정렬 알고리즘이란, **같은 값의 키**를 가진 요소의 순서가 **정렬 전후에도 그 순서가 유지**되는 것을 의미합

​       니다.

- unstable 알고리즘

  un stable 정렬 알고리즘이란, **같은 값의 키**를 가진 요소의 순서가 **정렬 전후에도 그 순서가 유지** 되는 것을 보장 할 수 없습니다. 



### 버블정렬

> 정의: 이웃한 두 요소의 대소 관계를 비교하여 교환을 반복한다. => stable한 알고리즘

**방법**

- 인접한 두 요소의 값 비교

- 앞의 값> 뒤에 값(오름차순으로 정렬하고 싶은 경우)

  앞의 값<뒤에 값(내림 차순으로 정렬하고 싶은 경우)

- 더 이상 비교할 대상이 없을 때 까지 반복적으로 수행

**장점**

- 구현이 간단함

- 데이터를 하나씩 비교할 수 있어서 정밀한 비교 가능


**단점**

- 비교횟수가 많기 때문에 성능이 떨어짐
- 이미 정렬되어 있더라도 계속 비교연산 함



**시간 복잡도**

O(n<sup>2</sup>)

```
1회 n-1 번 비교연산

2회 n-2 번 비교연산

...

n-1회 1번 비교연산

1+2+...+n-1 = (n-1)(1+n-1)/2 = n(n-1)/2
```



```c++
#include <iostream>
#include <vector>
using namespace std;

void show(vector<int> &arr, int n) {

	for (int i = 0; i < n; i++) {
		cout << arr[i] << " ";
	}
	cout << "\n";
}


//오름차순
void bubble(vector<int> &arr) {
	int n = arr.size();
	for (int i = 0; i < n - 1; i++) {
		for (int j = i + 1; j < n; j++) {
			if (arr[i] > arr[j]) {
				int temp = arr[j];
				arr[j] = arr[i];
				arr[i] = temp;
				show(arr, n);
			}

		}


	}
}

////내림차순
void bubble2(vector<int> &arr) {
	int n = arr.size();
	for (int i = 0; i < n - 1; i++) {
		for (int j = i + 1; j < n; j++) {
			if (arr[i] < arr[j]) {
				int temp = arr[j];
				arr[j] = arr[i];
				arr[i] = temp;
				show(arr, n);
			}


		}
	}
}

int main(void) {

	int n;
	cin >> n;
	vector<int> arr(n);

	for (int i = 0; i < n; i++) {
		int input;
		cin >> input;
		arr[i] = input;
	}

	bubble(arr);


}
```



### 선택정렬

> 정의: 데이터의 가장 작은 요소/큰요소를 선택해 맨 앞/뒤로 보내서 정렬하는 알고리즘=>unstable 알고리즘

=>서로 떨어져 있는 요소를 교환하기 때문이다.

```
unstable 예시=>같은 값 요소에 대하여 순서가 뒤 바뀜
3(L) 4  2 3(R) 1

1 4 2 3(R) 3(L)

1 2 4 3(R) 3(L)

1 2 3 4(R) 3(L)
```



**방법**

- 아직 정렬하지 않은 부분에서, 가장 작은/큰 key 값을 선택
- 탐색후, 아직 정렬하지 않은 부분의 첫 요소와 교환
- 더 이상 비교할 대상이 없을 때 까지 반복



**장점**

- 비교 횟수는 많지만, 교환 횟수가 적기 때문에 데이터 교환이 많이 이루어져야하는 데이터 상태에서 가장 효율적이다.
- 데이터의 양이 적을 때 성능이 좋음



**단점**

- unstable 하다.(즉, 값이 같은 경우에 상대적인 위치가 바뀔 수 있다.)


**시간 복잡도**

O(n<sup>2</sup>)

```
1회 n-1 번 비교연산

2회 n-2 번 비교연산

...

n-1회 1번 비교연산

1+2+...+n-1 = (n-1)(1+n-1)/2 = n(n-1)/2
```



```c++
#include <iostream>
#include <vector>
using namespace std;

void show(vector<int> &arr, int n) {

	for (int i = 0; i < n; i++) {
		cout << arr[i] << " ";
	}
	cout << "\n";
}


//오름차순
void select(vector<int> &arr) {
	int n = arr.size();
	for (int i = 0; i < n - 1; i++) {
		int min = i;
		for (int j = i + 1; j < n; j++) {

			if (arr[min] > arr[j]) {
				min = j;
			}
		}
		int temp;
		temp = arr[min];
		arr[min] = arr[i];
		arr[i] = temp;
		show(arr,n);

	}
}

////내림차순
void select2(vector<int> &arr) {
	int n = arr.size();
	for (int i = 0; i < n - 1; i++) {
		int max = i;
		for (int j = i + 1; j < n; j++) {

			if (arr[max] < arr[j]) {
				max = j;
			}
		}
		int temp;
		temp = arr[max];
		arr[max] = arr[i];
		arr[i] = temp;
		show(arr, n);

	}
}

int main(void) {

	int n;
	cin >> n;
	vector<int> arr(n);

	for (int i = 0; i < n; i++) {
		int input;
		cin >> input;
		arr[i] = input;
	}

	select(arr);


}
```



### 삽입정렬

> 정의: 선택한 요소를 그 보다 더 앞쪽의 알맞은 위치에 삽입하는 작업을 반복하여 정렬하는 알고리즘

=>stable 알고리즘

**방법**

- 선택한 요소(정렬이 되지 않은 요소)의 앞 요소(정렬이 된 요소)와 크거나 /작은 요소를  비교 합니다.
- 선택한 요소 보다 정렬된 기준에 맞지 않으면 교환 합니다.
- 정렬이 모두 완료될 까지  해당 방법을 반복합니다.

**장점**

- 정렬되어 있는 경우를 비교를 하지 않아 버블정렬의 비교 횟수를 줄임



**단점**

- 배열의 크기가 커질수록 효율이 떨어짐



**시간 복잡도**

O(n<sup>2</sup>)

```
1회 1 번 비교연산

2회 2 번 비교연산

...

n-1회 n-1 번 비교연산

1+2+...+n-1 = (n-1)(1+n-1)/2 = n(n-1)/2
```



```c++
#include <iostream>
#include <vector>
using namespace std;

void show(vector<int> &arr, int n) {

	for (int i = 0; i < n; i++) {
		cout << arr[i] << " ";
	}
	cout << "\n";
}


//오름차순
void insert(vector<int> &arr) {
	int n = arr.size();
	for (int i = 1; i < n; i++) {
		for (int j = i; j >= 1 ; j--) {
			if (arr[j - 1] > arr[j]) {
				int temp;
				temp = arr[j];
				arr[j] = arr[j - 1];
				arr[j - 1] = temp;
			}
			else {
				break;
			}
			show(arr,n);
		}

	}
}

////내림차순
void insert2(vector<int> &arr) {
	int n = arr.size();
	for (int i = 1; i < n; i++) {
		for (int j = i; j >= 1; j--) {
			if (arr[j - 1] < arr[j]) {
				int temp;
				temp = arr[j];
				arr[j] = arr[j - 1];
				arr[j - 1] = temp;
			}
			else {
				break;
			}
			show(arr, n);
		}

	}
}

int main(void) {

	int n;
	cin >> n;
	vector<int> arr(n);

	for (int i = 0; i < n; i++) {
		int input;
		cin >> input;
		arr[i] = input;
	}

	insert2(arr);


}
```





