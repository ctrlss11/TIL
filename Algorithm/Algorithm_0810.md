# Algorithm
## 220810 list
### 목표
* 알고리즘 문제 풀이 방법 익히기
* 2차원 배열 관련 문제 풀이


### 2차원 배열
* 입력 출력
```python
# 입력
# 3 4
# 1 2 3 4
# 4 5 6 7
# 7 8 9 10

N, M = int(input().split())
arr = [list(map(int, input().split())) for _ in range(N)]

for i in range(N):
    for j in range(M):
        print(arr[i][j], end=' ')
    print()
```
* 접근
```python
# row 우선
for i in range(N):
    for j in range(M):
        print(arr[i][j], end=' ')
    print()

# col 우선
for j in range(M):
    for i in range(N):
        print(arr[i][j], end=' ')
    print()

# zigzag
for i in range(N):
    for j in range(M):
        arr[i][j + (M-1-2*j) * (i%2)]
```

#### 델타를 이용한 접근
* 한 좌표에서 인접 배열을 탐색
```python
# 탐색을 위한 delta 배열
# delta : di dj
# neighbor : ni nj

# 상하좌우를 탐색 하는 경우
di = [0, 0, -1, 1]
dj = [-1, 1, 0, 0]

for i in range(N):
    for j in range(M):
        for k in range(4):
            ni = i + di[k]
            nj = j + dj[k]
            if 0 <= N and 0 <= nj < N:
                arr[ni][nj] ...
            
# 혹은 move 배열을 만들어서 사용
move = [[0, 1], [1, 0], [0, -1], [-1, 0]]
for di, dj in move:
    ni, nj = i + di, j + dj
    if indexError 확인
        arr[i][j]처리

# 주변 2칸이상을 탐색
for i in range(N):
    for j in range(M):
        for A in range(1, 3): # 1칸 순회 후, 2칸 순회
            for k in range(4):
                # for A in range(1, 3): 2칸씩 먼저 하려면 아래에 추가
                ni = i + di[k] * A
                nj = j + dj[k] * A
                if 0 <= N and 0 <= nj < N:
                    arr[ni][nj] ...
```
#### transpose matrix 전치 행렬
* zip 활용 잘하기!!!
  * **unpacking** 위해서 * 사용하기!!
```python
arr = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# zip 활용
arr_T = [list(x) for x in zip(*arr)]

# for문
for i in range(N):
    for j in range(M):
        if i < j:
            arr[i][j], arr[j][i] = arr[j][i], arr[i][j]
```
#### 주변 탐색
* 2차원 배열에서 이웃을 탐색할 때
* index의 범위 항상 조심!!
* 혹은 2차원 배열 끝에 [0]을 추가하는 idea


### subset 부분집합
* 모든 부분집합을 생성하는 방법
  * n중 for문
  * **<u>비트 연산자</u>**
* **부분집합 문제 비트 연산자로 풀어 보기!!**
```python
# 비트연산자로 부분집합 생성
arr = [3, 6, 7, 1, 5, 4]
n = len(arr)

for i in range(1<<n):           # 0부터 2^n-1 까지
    for j in range(n):          # j번 비트
        if i & (1<<j):          # i의 j번 비트가 1이면 
            print(arr[j], end='')
    print()
print()
```
* 비트 연산자
  * & : AND
  * | : OR
  * << : 왼쪽 shift
  * \>> : 오른쪽 shift
* << 연산자
  * 1<<n : 2^n , 원소 n개인 집합의 모든 부분집합 수
* & 연산자
  * i&(1<<j) : i의 j번째 비트가 1인지 아닌지 검사
  * 순서대로
  * 0 0 0 0 0 1
  * 0 0 0 0 1 0
  * 0 0 0 0 1 1
  * 0 0 0 1 0 0
  * ... 방식으로 출력
 
#### 예제 : 부분집합의 합이 0인 부분집합이 존재?
* 완전검색 기법
  * 모든 경우의 수 생성 후, 합 확인
  * 비트 연산자를 이용하여 모든 부분집합을 만들어서 확인
* dp
  * dp로 풀이 해보기


### search 검색
* 자료에서 원하는 것을 key로 검색
* sequential search 순차 검색
* binary search 이진 검색
* hash 해시

### sequential search 순차 검색
#### 정렬되지 않은 배열 검색
* 처음부터 하나씩 key같은지 비교하며 검색
* 자료 구조의 끝까지 못찾으면 검색 실패
```python
def sequentialSearch(arr, key):
    n = len(arr)
    i = 0
    while i < n and arr[i] != key:
        i += 1

    if i < n : return i
    else: return -1
```
* 평균 : O(n)


#### 정렬된 배열 검색
* 오름차순/내림차순 으로 정렬된 자료를 검색
* 검색대상의 값이 key 값보다 크면 검색 종료 
```python
def sequentialSearchinSort(arr, key):
    n = len(arr)
    i = 0
    while i < n and arr[i] < key:
        i += 1

    if i < n and arr[i] == key: return i
    else: return -1
```
* 평균 : O(n)

### binary search 이진 검색
* 자료의 중앙 값을 키와 비교하여, 작으면 앞을 크면 뒤를 재탐색
* 정렬된 자료에서만 가능
* 자료를 추가하거나 삭제하는 경우, 재정렬 과정 필요
* 범위를 반으로 줄여나가며 빠르게 검색
```python
def binarySearch(arr, key):
    N = len(arr)
    s = 0       # start
    e = N-1     # end

    while s <= e:
        m = (s+e)//2    # middle
        if arr[m] == key: 
            # 필요한 작업을 하는 코드 작성 후 반환
            return True
        elif arr[m] > key: e = m-1      # 크면 m 뒤에서 검색
        else: s = m+1                   # 작으면 m 앞에서 검색
    return False
```
```python
# 재귀로 구현
def binarySearch(arr, s, e, key):
    if s > e: return False
    else:
        m = (s + e) // 2
        if key == arr[m]: return True
        elif key < arr[m]: return binarySearch(arr, s, m-1, key)
        elif key > arr[m]: return binarySearch(arr, m+1, e, key)
```

### selection sort 선택 정렬
* 첫 번째부터 최소값 찾기
* 첫 번째 원소와 최소값 위치 swap
* 두 번쨰부터 최소값 찾기
* 두 번째 원소와 swap, 이후 반복
```python
def selectionSort(lst):
    N = len(lst)
    for i in range(N-1):
        min_idx = i
        for j in range(i+1, N):
            if lst[min_idx] > lst[j]: min_idx = j
        lst[i], lst[min_idx] = lst[min_idx], lst[i]

    return lst
```
* O(N^2)

### selection algorithm
* 선택 알고리즘
* 자료구조에서 n번째로 큰/작은 원소를 찾는 방법
* 자료 구조를 정렬 후, n번째 idx로 원하는 값 선택

### 2차원 배열 연습
* NxM 행렬의 대각선 합 중 최대값
```python
N, M = map(int, input().split())
lst = [list(map(int, input().split())) for _ in range(N)]

max_lst = [0]*(N + M -1)
for i in range(N):
    for j in range(M):
        max_lst[i+j] += lst[i][j]

print(max(max_lst))
```

### 연속하는 1 확인
* 곱셈 idea
```python
# 세번 연속하는 1 찾기
if arr[i]*arr[i+1]*arr[i+2] == 1:
```
* n번 연속하는 1 찾기
```python
cnt = 0
temp = 1
for i in range(N):
    for j in range(1, n):
        temp *= arr[i+j]
    if temp == 1: 
```
```python
# 검색할 배열에 [0]*n 추가하기
cnt = 0
max1 = 0
for i in range(N):
    if arr[i] == 1:
        cnt += 1
        if max1 < cnt: max1 = cnt
    else:
        cnt = 0
```



















