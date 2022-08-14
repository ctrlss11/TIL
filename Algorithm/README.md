# Algorithm

## 작성 방법 
* 오늘 공부한 알고리즘 개념 정리 후, README에 항목 추가하기
* 나만의 템플릿 만들어서 작성
  * 템플릿으로 빠르게 구현할 수 있도록 연습
* 다시 찾아보기 쉽게 작성
* 다시 봤을 때 이해할 수 있게 주석 작성
* 검색하기 쉽도록 키워드 작성
* 알고리즘 내용에 해당하는 문서로 링크

## 분류
## Search
### [2 dimensional array](./Algorithm_0808.md)
* 입력
```python
# 2차원 배열을 입력 받을 때
# 3 4           # (3 x 4 배열)
# 1 2 3 4
# 4 5 6 7
# 7 8 9 10

N, M = int(input().split())
arr = [list(map(int, input().split())) for _ in range(N)]
```
* 탐색
```python
# row 우선, col 우선
for i in range(N):
    for j in range(M):
        print(arr[i][j], end=' ') # row 우선
        # print(arr[j][i], end=' ') # col 우선
    print()

# zigzag
for i in range(N):
    for j in range(M):
        arr[i][j + (M-1-2*j) * (i%2)]
```
* 델타
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
            ni = i + di
            nj = j + dj
            if 0 <= N and 0 <= nj < N:
                arr[ni][nj] ...
            
# 혹은 move 배열을 만들어서 사용
move = [[0, 1], [1, 0], [0, -1], [-1, 0]]
for di, dj in move:
    ni, nj = i + di, j + dj
    if indexError 확인
        arr[i][j]처리
```
* transverse 전치
```python
# arr = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
# zip, * 사용
arr_T = list(zip(*arr))

# for문
for i in range(N):
    for j in range(M):
        if i < j:
            arr[i][j], arr[j][i] = arr[j][i], arr[i][j]
```

### [binary search](./Algorithm_0810.md)

### [bit operator n subset](./Algorithm_0810.md)
* 비트 연산자로 부분 집합 생성
```python
# 비트 연산자로 부분집합 생성
arr = [3, 6, 7, 1, 5, 4]
n = len(arr)

for i in range(1<<n):           # 0부터 2^n-1 까지
    for j in range(n):          # j번 비트
        if i & (1<<j):          # i의 j번 비트가 1이면 
            print(arr[j], end='')
    print()
print()
```

### [exaustive search](./Algorithm_0808.md) 
* 완전 검색

### [greedy algorithm](./Algorithm_0808.md)
* 탐욕 알고리즘

### [pattern searching algorithm](./Algorithm_0812.md)
* 패턴 검색 알고리즘
* 문자열 탐색
* brute force
```python
# t : target , p : pattern
def bf(p, t):
    M = len(p)
    M = len(t)

    for i in range(N - M + 1):
        for j in range(M):
            if p[j] != t[i]:
                break
        else:
            return i
    else:
        return -1
```
* KMP
```python
# 최적화 후 추가
```
* Boyer-Moore
```python
# 최적화 후 추가
```
### [sort](./Algorithm_0808.md)
* bubble sort
```python
def bubbleSort(lst):
    for i in range(len(lst)-1, 0, -1):
        for j in range(0, i):
            if lst[j] > lst[j+1]:
                lst[j], lst[j+1] = lst[j+1], lst[j]
    return lst
```
* counting sort
```python
def countSort(lst):
    c = [0 for _ in range(len(lst))]
    ret = [0 for _ in range(len(lst))]
    
    # lst원소를 count하는 배열 작성
    for i in range(len(lst)): c[i] += 1

    # 누적 합으로 수정
    for i in range(1, len(c)): c[i] += c[i-1]

    # lst를 뒤에서부터 탐색하여, --후 ret에 추가
    for i in range(len(ret)-1, -1, -1):
        c[lst[i]] -= 1
        ret[c[lst[i]]] = lst[i]

    return ret
```
* [selection sort](./Algorithm_0810.md)
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