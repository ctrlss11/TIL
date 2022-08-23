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
* 2 dimensional array 2차원 배열
  * 탐색
  * 델타
  * 전치
* back tracking 백트래킹
* binary search 이진 검색
* dfs 깊이 우선 탐색
* dynamic programming 동적 계획법
  * bottom-up
  * top-down
* exaustive search 완전 검색
* graph 그래프
* greedy algorithm 그리디 알고리즘
* pattern searching algorithm 패턴 검색
  * brute-force
  * KMP
  * boyer-moore
* permutation 순열
* sort 정렬
  * bubble sort 거품 정렬
  * counting sort 계수 정렬
  * selection sort 선택 정렬
* stack 스택
* subset 부분 집합 생성
  * back tracking
  * bit operator
  * for문

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
```
* transverse 전치
```python
# arr = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
# zip, * 사용
arr_T = [list(x) for x in zip(*arr)]

# for문
for i in range(N):
    for j in range(M):
        if i < j:
            arr[i][j], arr[j][i] = arr[j][i], arr[i][j]
```

### [back tracking](Algorithm_0822.md)

### [binary search](./Algorithm_0810.md)

### [dfs](./Algorithm_0817.md)
* stack
```python
def dfs(now):
stack = [now]
while stack:
    # 1. 방문 표시
    visited[now] = 1
    # 2. 인접 정점 확인
    for nxt in range(N+1):
        # 3. 이전에 방문했던 곳인지 확인
        if graph[now][nxt] == 1 and visited[nxt] == 0:
            # 4. 안했다면 방문하여 stack에 push
            stack.append(now)
            now = nxt
            result.append(nxt)
            break
    # 5. 인접 정점의 방문이 끝나면 stack에서 pop, 이전 최근 정점에서 1. 반복
    else:
        now = stack.pop()

visited = [0]*(N+1)
graph = [[0]*(N+1) for _ in range(N+1)] # graph 정보
for i in range(E): # 인접 행렬 만들기
    graph[lst[i*2]][lst[i*2+1]] = 1
    graph[lst[i*2+1]][lst[i*2]] = 1 # 양방향일 경우

start = 1
result = [start]
dfs(start)
print(*result)
```
* recursion
```python
def dfs(now):
    visited[now] = 1
    result.append(now)
    for nxt in range(N+1):
        if graph[now][nxt] == 1 and visited[nxt] == 0:
            dfs(nxt)

visited = [0] * (N+1)
graph = [[0] * (N+1) for _ in range(N+1)]
for i in range(E):
    graph[lst[i*2]][lst[i*2+1]] = 1
    graph[lst[i*2+1]][lst[i*2]] = 1  # 양방향

result = []
start = 1
dfs(start)
print(*result)
```

### [dynamic programming](./Algorithm_0817.md)
* bottom-up tabulation
```python
# bottom-up tabulation
d = [0]*101

d[1] = 1
d[2] = 1

n = 100
for i in range(3, n+1):
    d[i] = d[i-1] + d[i-2]

print(d[n])
```
* top-down memoization
```python
# top-down memoization
d = [0]*101

def fibo(a):
    if a == 1 or a == 2:
        return 1

    if d[a] != 0:
        return d[a]

    d[a] = fibo(a-1) + fibo(a-2)
    return d[a]

print(fibo(100))
```

### [exaustive search](./Algorithm_0808.md) 
* 완전 검색

### [graph](./Algorithm_0817.md)

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

### permutation 순열
```python
```

### [sort](./Algorithm_0808.md)
* bubble sort
```python
def bubbleSort(lst):
    for i in range(len(lst)-1, 0, -1):
        for j in range(i):
            if lst[j] > lst[j+1]:
                lst[j], lst[j+1] = lst[j+1], lst[j]
    return lst
```
* counting sort
```python
def countingSort(lst):
    n = len(lst)
    c = [0]*(n+1)
    ret = [0]*(n)

    for i in range(len(lst)):      # lst원소를 count하는 배열 작성
        c[lst[i]] += 1

    for i in range(1, len(c)):     # 누적 합으로 수정
        c[i] += c[i-1]

    for i in range(n-1, -1, -1):    # lst를 뒤에서부터 탐색하여, --후 ret에 추가
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

### [subset]
* [back tracking](./Algorithm_0822.md) 백트래킹
```python

```
```python
def powerset(idx):                  # 몇 번째 idx가 선택o / 선택x
    if idx < len(lst):              # 사용되는 숫자를 정할 수 있음
        selected[idx] = True
        powerset(idx+1)
        selected[idx] = False
        powerset(idx+1)
    else:
        # 부분 집합을 생성
        res = []
        for i in range(len(lst)):
            if selected[i]:
                res.append(lst[i])
        # print(res)
        result.append(res)

lst = list(range(1, 6))
selected = [False]*len(lst)
result = []

powerset(0)
print(result)
print(len(result))
```

* [bit operator](./Algorithm_0810.md) 비트 연산자로 부분 집합 생성
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

* for문
```python
bit = [0, 0, 0, 0]
for i in range(2):              # idx 0
    bit[0] = i
    for j in range(2):          # idx 1
        bit[1] = j
        for k in range(2):      # idx 2
            bit[2] = k
            for l in range(2):  # idx 3
                bit[3] = l
                print(bit)
```

### [stack](./Algorithm_0817.md)