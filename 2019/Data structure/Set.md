# 집합(Set)

[TOC]

## 집합(Set)

> 비트마스크

비트마스크를 이용하면 집합을 표현할 수 있습니다.

어떤 그룹을 나눌 때 특정 값이 있다, 없다라는 개념으로 원소의 유/무를 판단합니다. 비트마스크는 0과 1 2진수를 통하여 집합의 원소의 유무를 나타낼 수 있습니다.

- 비트마스크는 정수 하나로 부분집합을 모두 표현할 수 있습니다.
- 합집합, 차집합, 교집합 등을 비트 연산을 통하여 나타낼 수 있습니다.



```
비트마스크 s1, s2가 존재할 때
<합집합>
s1 | s2//집합 s1와 집합 s2의 합집합

<교집합>
s1 & s2 //집합 s1과 집합 s2의 교집합

<차집합>
s1 & ~s2 //집합 s1과 집합 s2의 차집합

<해당 수 포함 여부 검사>
s1 &(1<<k) //k라는 원소가 집합 s1에 있는지 검사
             결과가0 0이면 없음 (1<<i)이면 있음
             
<새로운 수 추가>
s1 | (1<<i)

<제거 연산>
s1 & ~(1<<i)

<토글 연산>//모든 원소를 1을 0으로 0을 1로
s1 ^ (1<<i)

<전체 집합>
(1<<N)-1 

<공집합>
S1=0


```

