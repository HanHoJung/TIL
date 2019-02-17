# 검색



[TOC]



## 1. 검색이란

**검색**이란, 데이터의 집합에서 특정 키를 설정하고 조건에 맞는 데이터를 찾는것이다.

**검색의 3요소**

- 키:데이터에서 주목하는 항목
- 조건:찾을려는 요소를 키를 이용하여 연산자(논리연산자, 동등연산자 등)를 통해 표현
- 데이터의 집합



**검색에 사용되는 대표 자료구조**

- 배열
- 선형 리스트
- 이진검색트리



**검색 알고리즘 선택 조건**

데이터의 집합에서, 단순히 검색만 한다면 속도가 빠른 검색 알고리즘을 선택하면 됩니다. 하지만,  삽입/삭제등이 빈번하게 이루어지는 경우에는 검색 속도만 빠른 알고리즘을 선택하기 보다는 삽입/삭제에 소요되는 비용이 적은 알고리즘을 선택해야 합니다. 예를들어, 데이터 집합에서 삽입/삭제가 빈번하게 발생하는 경우에는 배열을 이용한 알고리즘 보다는 선형 리스트를 이용한 검색 알고리즘을 적용하는 것이 좋습니다.



때문에, 종합적으로 판단하여 효율적인 알고리즘을 선택하는것이 중요합니다. 

**cf)본 챕터에서는 배열을 이용하여 검색하는 방법을 위주로 설명되어 있습니다.**



## 2. 검색 알고리즘

- 정렬되지 않은 대상을 기반으로 하는 탐색(선형 검색)
- 정렬된 대상을 기반으로 하는 탐색(이진 검색)

### - 선형 검색(Linear Search)

정의:임의로 늘여놓은 배열에서 순차적으로 원하는 키 값을 찾는 알고리즘 입니다.

선형 검색은, 원하는 키 값을 만날 때까지 배열의 인덱스를 이동시키면서 탐색하는 알고리즘 입니다.



출처: http://abouteverything.tistory.com/11  (해당 블로그 그림을  보면 탐색과정을 쉽게 볼 수 있습니다.)



종료 조건

- 검색할 키 값을 찾은 경우
- 검색할 키 값을 발견하지 못한 경우



시간복잡도

- Best case

  해당 키값이 배열에 가장 앞 부분에 있어서 한 번에 찾은 경우 O(1) 입니다.

- Worst case

  크기가 n인 배열이 있을때(인덱스는 0부터 시작) 원하는 요소가 배열의 끝에 있는 경우

  또는, 배열에 찾는 요소가 없을 때 시간복잡도는 O(N) 입니다.



### - 이진 검색(Binary Search)

정의:요소가 오름차순 또는 내림차순으로 정렬된 배열에서 적용할 수 있는 검색 알고리즘 입니다. 

이진 검색법을 사용하면, **검색할 요소의 범위**를 절반씩 줄일 수 있는 장점이 있습니다.



- Mid=(Left+Right)/2 index를 의미한다.
- Left, Right는 index를 의미한다.



![binary1](./img/binary1.jpg)

![binary2](./img/binary2.jpg)

![binary3](./img/binary3.jpg)



종료조건

- 검색할 키 값을 찾은 경우
- 검색할 키 값을 발견하지 못한 경우





시간복잡도

- Best case

  해당 키값이 한 번에 찾은 경우 O(1) 입니다.

- Worst case

  ```
  입력의 개수 : N
  시행 횟수: K
  
  
  1회: N/2
  2회: N/2 * 1/2
  3회: N/2 * 1/2 * 1/2
  ...
  k회:(1/2)^k * N
  
  (1/2)^k * N  ≈ 1
  
  때문에,
  (1/2)^k * N  = 1이라고 가정을 하고
  양변에 2^K를 곱해주면
  N = 2^k
  logN = K (밑은 2임)=>입력의 개수 N에 따른 시행횟수
  시간복잡도 O(logN)
  
  ```



> Lower Bound

- 탐색값 k에 대하여, k 이상이 처음 나오는 위치를 찾는 과정



> Upper Bound

- 탐색값 k에 대하여, k 를 초과한 값이 처음 나오는 위치를 찾는 과정

  

> 차이

- 상한과 하한의 차를 이용하여 해당 수가 배열에 몇 개 있는지를 구할 수 있다.
- 상한-하한

```c++
int upper_bound(vector<long long> arr,int key) {
	
	int left = 0;
	int right = arr.size() - 1;

	while (left < right) {
		int mid = (left + right) / 2;
		if (arr[mid] <= key) {
			left = mid + 1;
		}
		else if (arr[mid] > key) {
			right = mid;
		}

	}
	return left;
}

int lower_bound(vector<long long> arr, int key) {

	int left = 0;
	int right = arr.size() - 1;

	while (left < right) {
		int mid = (left + right) / 2;
		if (arr[mid] >= key) {
			right= mid;
		}
		else if (arr[mid] > key) {
			left = mid + 1;
		}

	}

	return left;
}
```

https://chogahui05.blog.me/221235974287



> 보간 탐색

이진 검색은 찾는 대상이 중앙에 취하건 맨 앞에 위치하건 그 위치에 상관하지 않고 일관되게 반씩 줄여가며 탐색을 진행합니다. 때문에 찾는 대상의 위치에 따라서 탐색의 효율에 차이가 발생 합니다.  이를 보완한 알고리즘이 보간 탐색 입니다.

원리는, 중앙에서 탐색을 시작하는게 아니라 탐색 대상이 앞쪽에 있으면 앞쪽에서 데이터를 찾고 뒤쪽에 있으면 뒤쪽 부터 찾는 알고리즘 입니다.(대상에 비례하여 탐색의 위치를 결정)



<비례식 구성>

- low:탐색 대상의 시작 index
- high:탐색 대생의 마지막 index
- s:찾는 대상에 저장된 index
- x:arr[s]
- 오차율을 최소하하기 위해 s의 자료형은 실수형
- 보간탐색은 **데이터의 값**과 그 **데이터가 저장된 위치의 인덱스 값**이 비례한다고 가정

![binary3](./img/search.PNG)

```c++
#include <iostream>
#include <vector>
using namespace std;

int Isearch(vector<int> &arr, int left, int right, int target) {
	int mid;

	if (left > right)
		return -1; //-1은 탐색 실패

	mid = ((double)(target - arr[left]) / (arr[right] - arr[left])*(right - left)) + left;
	
	if (arr[mid] == target)
		return mid;

	else if (target < arr[mid])
		return Isearch(arr, left, mid - 1, target);
	else
		return Isearch(arr, mid + 1, right, target);

}
int main(void) {

	vector<int> arr = { 1,3,5,7,9 };
	int idx = Isearch(arr, 0, arr.size() - 1, 1);

	if (idx == -1)
		cout << "탐색 실패\n";
	else
		cout << idx << "\n";


	idx = Isearch(arr, 0, arr.size() - 1, 11);

	if (idx == -1)
		cout << "탐색 실패\n";
	else
		cout << idx << "\n";



	idx = Isearch(arr, 0, arr.size() - 1, 2);

	if (idx == -1)
		cout << "탐색 실패";
	else
		cout << idx << "\n";
}

```

단순히  mid 값을 찾는 경우를 보간법으로 바꾼다고 해서 보간탐색이 성되는것이 아닙니다.

예를 들어, Isearch(arr, 0, arr.size() - 1, 2); 호출한 경우 mid값이 계속 0이되어 Isarch(arr,1,4,2)가 계속 호출되는 경우가 발생하게 됩니다. 때문에 종료조건을 단순히 left>right 크다는 조건으로 해결할 수 없습니다.

즉, **arr[target]<arr[left] 또는 arr[target]>arr[right]**인 경우

이러한 결과가 발생하는 이유는 정렬된 탐색 대상의 범위를 좁혀가면서 정렬을 진행하기 때문 입니다.

( first와 last가 target을 향해서 점점 좁혀감)

```c++
#include <iostream>
#include <vector>
using namespace std;

int Isearch(vector<int> &arr, int left, int right, int target) {
	int mid;

	if (arr[left] > target || target>arr[right])
		return -1; //-1은 탐색 실패

	mid = ((double)(target - arr[left]) / (arr[right] - arr[left])*(right - left)) + left;
	
	if (arr[mid] == target)
		return mid;

	else if (target < arr[mid])
		return Isearch(arr, left, mid - 1, target);
	else
		return Isearch(arr, mid + 1, right, target);

}

int main(void) {

	vector<int> arr = { 1,3,5,7,9 };
	int idx = Isearch(arr, 0, arr.size() - 1, 1);

	if (idx == -1)
		cout << "탐색 실패\n";
	else
		cout << idx << "\n";


	idx = Isearch(arr, 0, arr.size() - 1, 11);

	if (idx == -1)
		cout << "탐색 실패\n";
	else
		cout << idx << "\n";



	idx = Isearch(arr, 0, arr.size() - 1, 2);

	if (idx == -1)
		cout << "탐색 실패";
	else
		cout << idx << "\n";
}
```



### - 해시법



### - 이진 탐색 트리

![binary3](./img/bin.PNG)



![binary3](./img/bin1.PNG)

이진 탐색 트리의 삭제의 경우

1. 삭제할 노드가 단말 노드인 경우(no child)

   ![binary3](./img/bin3.PNG)

2. 삭제할 노드가 하나의 자식 노드를 갖는 경우(one child)

   ![binary3](./img/bin4.PNG)

3. 삭제할 노드가 두 개의 자식 노드를 갖는 경우(two child)

   ![binary3](./img/bin5.PNG)

- 탐색 O(logn)
- 삽입 O(logn)
- 삭제 O(logn)