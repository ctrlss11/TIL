# Algorithm
## 220808 list
### 목표
* 알고리즘 문제 풀이 방법 익히기
* list 관련 문제 풀이


### 알고리즘 판단
1. 정확성 : 얼마나 정확한가?
2. 작업량 : 얼마나 적은 연산을 하는가?
3. 메모리 : 얼마나 적은 메모리를 사용하는가?
4. 단순성 : 얼마나 단순한가?
5. 최적성 : 얼마나 최적화 되었는가?

### big O notation
* 시간 복잡도로 알고리즘의 성능 비교
* 문제에서 주어진 **입출력**과 **제한시간**으로 어떤 알고리즘이 적절한지 **유추** 가능

### array 배열
* 동일한 자료형의 변수들을 연속적으로 나열하여 사용하는 자료구조
* index 접근
* 0배열 생성 방법
```python
N = 10
lst1 = [0 for _ in range(N)]
lst2 = [0]*N
```

#### 예제 : SWEA gravity
* 상자가 쌓여진 방을 90도 회전했을 때, 가장 큰 낙차를 반환
```python
def check(lst):
    ret = [0 for _ in range(len(lst) + 1)]
    for i in range(len(lst)):
        if lst[i] != 0:
            for j in range(i + 1, len(lst)):
                if lst[i] > lst[j]: ret[i] += 1
    return max(ret)

T = int(input())

for i in range(T):
    N = int(input())
    lst = list(map(int, input().split()))
    print(check(lst))

# input
# 1
# 9
# 7 4 2 0 0 6 0 7 0

# output
# 7
```

### 연습할겸 내장 함수 대신 직접 구현하여 사용해보자
* 최대값, 최대 값의 위치(여러 개인 경우 가장 오른쪽)
```python
N = list(map(int, input().split()))

max_val = 0
max_idx = 0
for i in range(len(N)):
    if lst[i] >= max_val:
        max_val = lst[i]
        max_idx = i

print(max_idx, max_val)
```

### sort 정렬
* bubble sort
* counting sort
* selection sort
* insertion sort
* quick sort
* merge sort


##### bubble sort
* 인접 원소끼리 자리를 계속 교환
* O(n^2)
* 구현
```python
def bubbleSort(lst):
    for i in range(len(lst)-1, 0, -1):
        for j in range(i):
            if lst[j] > lst[j+1]:
                lst[j], lst[j+1] = lst[j+1], lst[j]
    return lst
```

#### counting sort
* 배열의 원소의 중복 개수를 센 count배열을 만들고, count값을 이용하여 정렬
* O(n + k) 
* 구현
```python
def countingSort(lst):
    n = len(lst)
    c = [0]*(n+1)
    ret = [0]*n

    for i in range(len(lst)):      # lst원소를 count하는 배열 작성
        c[lst[i]] += 1

    for i in range(1, len(c)):     # 누적 합으로 수정
        c[i] += c[i-1]

    for i in range(n-1, -1, -1):    # lst를 뒤에서부터 탐색하여, --후 ret에 추가
        c[lst[i]] -= 1
        ret[c[lst[i]]] = lst[i]

    return ret
```

### 정렬 알고리즘 비교

|알고리즘|평균|최악|방법|특징|
|:--|:--|:--|:--|:--|
|bubble sort|O(n^2)|O(n^2)|비교, 교환|구현이 쉽지만 느림|
|counting sort|O(n+k)|O(n+k)|비교환|n이 작을때 유용|

### exaustive search 완전 검색
* 모든 경우의 수를 나열해보고 확인하는 기법
* brute-force , generate-and-test
* 경우의 수가 작을 때 유용
* 순열, 조합, 부분 집합을 사용하여 경우의 수 고려
* 속도는 느리지만, 실수할 확률이 적다
* 문제를 풀 때, 
  * 우선 완전 검색으로 접근하여 해답을 도출한 후,
  * 성능 개선을 위해 다른 알고리즘을 사용하고 해답을 확인하는 전략을 사용해보자

#### baby-gin 문제
#### 완전검색으로 풀이
* 뽑은 6가지의 숫자로 모든 경우의 수 나열
* 모든 경우의 수에서 baby-gin조건을 만족하는 경우의 수 확인

#### count배열로 풀이
* 뽑은 6가지의 숫자를 숫자별로 count하는 count배열 만듦
* count배열이 run을 만족하는지 확인. 만족한다면 run에 해당되는 수 빼기
* count배열이 triplet을 만족하는지 확인. 만족한다면 baby-gin만족
```python
num = int(input())
# triplet 비교시 i+2까지 하므로 편의를 위해 12까지 만든다
c = [0]*12              

for i in range(6):
    c[num%10] += 1
    num //= 10

# num이 몇 자리 수인지 모를 때
# while num:
#     c[num%10] += 1
#     num //= 10

i = 0
triplet = run = 0
while i < 10:
    if c[i] >= 3:
        c[i] -= 3
        triplet += 1
        continue
    
    if c[i] >= and c[i+1] >= 1 and c[i+2] >= 1:
        c[i] -= 1
        c[i+1] -= 1
        c[i+2] -= 1
        run += 1
        continue

    i += 1

print("Baby Gin") if run + tri == 2 else print("lose")
```

### permutation 순열
* nPr : 서로 다른 n개 중 r개를 뽑아서 한 줄로 나열하는 것
* nPr = n*(n-1)* ... *(n-r+1) = n!/(n-r)!
* 완전 검색에서 모든 경우의 수가 얼마인 지 가늠할 때, 순열로 예상하기

#### 단순하게 순열을 생성하는 방법
* 중복이 없을 때
```python
lst = [1, 2, 3]
for i1 in range(1, 4):
    for i2 in range(1, 4):
        if i2 != i1:
            for i3 in range(1, 4):
                if i3 != i1 and i3 != i2:
                    print(i1, i2, i3)
```

### greedy algorithm 탐욕 알고리즘
* 최적해를 구하는 데 사용되는 방법
* 여러 경우 중, 그 순간에 최적이라고 생각되는 것을 선택해 나가는 방식
* 각 시점에서의 최적이지, 전체의 최적이라는 보장은 없다

1. 해 선택 : 현재 상태에서 부분 문제의 최적 해를 구한 뒤, 이를 부분해 집합(solution set)에 추가
2. 실행 가능성 검사: 새로운 부분해 집합이 실행 가능한지를 확인한다. 문제의 제약 조건을 위반하지 않는지를 검사
3. 해 검사 : 새로운 부분해 집합이 문제의 해가 되는지를 확인한다.

#### 거스름돈 줄이기 문제
* 거스름돈으로 주는 지폐와 동전의 개수를 최소한으로 줄이기
1. 해 선택 
   * 가장 큰 단위의 동전을 골라 x에 추가
2. 실행 가능성 검사 
   * x가 거스름돈의 액수를 초과하는지 확인. 
   * 초과한다면 마지막에 추가한 동전을 거스름돈에서 뺴고, 
   * 1.로 되돌아가서 다음으로 큰 단위의 동전을 골라 거스름돈에 추가
3. 해 검사 
   * x가 거스름돈과 일치하는지 확인. 
   * 모자라면 1. 돌아가서 반복