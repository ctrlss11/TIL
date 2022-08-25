# Algorithm
## 220824 220825 queue
### 목표
* 알고리즘 문제 풀이 방법 익히기
* queue 구현 및 문제 풀이
* bfs 문제 풀이 방법 익히기


### queue
* FIFO First In First Out 선입선출
* 선형 자료 구조
* 큐의 삽입과 삭제는 한 방향으로 제한
  * 뒤에서 삽입, 앞에서 삭제
* python에서 deque 사용!
```python
from collections import deque
queue = deque()
```

#### 구현
* front : 첫 번째 원소, 다음에 삭제될 위치
* rear : 마지막 원소, 최근에 삽입된 위치
* enQueue : push 원소 삽입
* deQueue : pop front 원소 반환 후 제거 (꺼내기)
* createQueue : queue 생성
* isEmpty : 공백 확인
* isFull : 포화 확인
* Qpeek : front 원소 반환
```python
size = 10
queue = [0]*size

front = -1
rear = -1

# 선형큐
# enqueue(5)
rear += 1
q[rear] = 5

# dequeue()
front += 1
print(q[front])

# 원형큐 (덮어쓰기)
# enqueue(5)
rear = (rear+1)%size
q[rear] = 5

# dequeue()
front = (front+1)%size
print(q[front])
```
```python
from collections import deque

queue = deque()
q.append(5)
q.popleft()
# q.pop(0) # idx 0으로 pop하면 속도가 느림
```
* append, pop으로 구현하면 속도가 느림
  * 정확하게는 pop(index)가 느림
  * index위치를 pop하고 배열을 재조정하기 때문에 시간복잡도 O(N)
  * python 내장함수의 시간 복잡도 확인하기!
  * https://wiki.python.org/moin/TimeComplexity
  * https://www.ics.uci.edu/~pattis/ICS-33/lectures/complexitypython.txt
* 대량의 데이터를 사용할 때는 idx로 구현
* 혹은 python에서는 deque 활용
  * idx구현과 속도 비슷
  * deque은 linked-list로 구현되어 있음

* 이런 방식으로 구현하면, 포화상태가 되어갈수록 메모리가 낭비
* 원형 큐로 해결 가능

#### 원형 큐
* 배열의 처음과 끝을 연결하여 구현
* 나머지 연산자를 활용하여 idx 순환
* 처음과 끝을 구분하기 위해서 한자리는 항상 빈자리로 놔둠
* 여러 구현 방법 중에서,,,
  * 과거 데이터가 필요없다면
  * 포화상태가되면 앞부터 덮어쓰기(override) 하면서 순환

### priority queue 우선순위 큐
* 우선순위를 가진 항목들을 저장하는 큐
* 우선순위가 높은 순서대로 처리
* ex)
  * 시뮬레이션 시스템
  * 네트워크 트래픽 제어
  * 운영체제의 테스크 스케줄링

#### buffer 버퍼
* 데이터를 전송하는 동안 일시적으로 데이터를 보관하는 영역
* 버퍼링 : 버퍼를 활용하는 방식, 버퍼를 채우는 동작
* 입출력, 네트워크 기능에서 사용
* queue를 활용하여 순서대로 데이터를 입출력 및 전달

### BFS Breadth First Search 너비 우선 탐색
* 시작 점에서 같은 level의 인접 정점들을 차례대로 방문 후, 다음 level의 인접 정점을 차례대로 방문 반복
* queue를 활용하여 차례대로 인접 정점들을 방문 (선입선출 FIFO)
```python
def BFS(v, n, graph):       # BFS(시작점, 정점의 개수, 그래프)
    visited = [0]*(n+1)
    queue = []
    queue.append(v)
    visited[v] = 1
    while queue:
        t = queue.pop(0)
        visit(t)
        for i in graph[t]
            if not visited(i):
               visited[i] = visited[t] + 1  # bfs의 깊이를 표시할 수 있음!
```
* 최단거리를 물어보는 문제는 bfs로 풀이
  * visited에 거리정보(graph의 깊이)를 담아두면 거리 계산 가능
* graph에서 노드간의 거리별로 가장 많은 노드의 개수?
  * visited에 같은 거리인 node의 갯수를 확인

### 예제
```python
def bfs(v, N):
    visited = [0]*(N+1)
    queue = []
    queue.append(v)
    visited[v] = 1
    while queue:
        v = queue.pop(0)
        print(v, end=' ')
        for w in adjList[v]:
            if visited[w] == 0:
                queue.append(w)
                visited[w] = visited[v] + 1  # 시작점 부터의 거리 정보

V, E = map(int, input().split())
N = V + 1
adjList = [[] for _ in range(E)]
for _ in range(E):
    a, b = map(int, input().split())
    adjList[a].append(b)
    adjList[b].append(a)

bfs(1, N)
```

### 문제 풀이 적용
* 미로, 그래프 문제에서...
1. 시작점 -> 끝점 으로 가는 경로가 존재?
  * DFS, BFS
2. 시작점 -> 끝점 으로 가는 최단경로의 길이?
  * (주로)BFS, DFS
    * BFS : visited 에 +1 씩 더해서 거리정보 저장
    * DFS : 
3. 시작점 -> 끝점 으로 가는 경로의 개수?
  * DFS
    * 도착하면 경로 수 +1
    * 모든 경로 탐색 위해서
    * 분기점으로 되돌아 올 때, visited = False로 복귀
4. 여러개의 시작점에서 확산, 모두 확산되는 시간
  * BFS
    * 시작점에서 한칸씩 진행하면서 visited 에 +1 씩 더하기
    * 확산(탐색) 완료 후, 최대값에서 시작점 빼기


### 탐색 알고리즘 정리
* tree
  * 순회
* DFS
  * 재귀, 반복, stack
* graph
  * DFS, BFS
* optimization 최적화 문제
  * MST
  * Dijkstra
* BFS
  * 반복, queue
* 위상정렬