# Algorithm
## 220808 220810 list
### 목표
* 알고리즘 문제 풀이 방법 익히기
* list 관련 문제 풀이


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

# 주변 2칸이상을 탐색
for i in range(N):
    for j in range(M):
        for A in range(1, 3): # 1칸 순회 후, 2칸 순회
            for k in range(4):
                # for A in range(1, 3): 2칸씩 먼저 하려면 아래에 추가
                ni = i + di * A
                nj = j + dj * A
                if 0 <= N and 0 <= nj < N:
                    arr[ni][nj] ...
```
#### transpose matrix 전치 행렬
* zip을 활용
```python
arr = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# zip 활용
arr1 = list(zip(*arr))

# for문
for i in range(N):
    for j in range(M):
        if i < j:
            arr[i][j], arr[j][i] = arr[j][i], arr[i][j]
```
#### 예제


### subset 부분집합
* 모든 부분집합을 생성하는 방법
  * n중 for문
  * 비트 연산자
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

#### 예제 : 부분집합의 합이 0인 부분집합이 존재?
* 완전검색 기법
  * 모든 경우의 수 생성 후, 합 확인


### search 검색
* 자료에서 원하는 것을 key로 검색
* sequential search 순차 검색
* binary search 이진 검색
* hash 해시

#### sequential search
* 정렬되지 않은 배열 검색
* O(n)






















