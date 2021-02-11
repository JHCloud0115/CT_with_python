# Search :탐색

### Data Structure : 자료구조 
데이터를 표현하고 관리하고 처리하기 위한 구조  
- Stack
- Queeue

#### Stack
선입선출 구조 / 후입선출 구조  
별도의 라이브러리 필요 없이 append와 pop메서드 사용

in(5 - 2 - 3 - 7) --> out(7) --> in(1 - 4 ) -->out(4)


```python
stack = []
stack.append(5)
stack.append(2)
stack.append(3)
stack.append(7)
stack.pop()
stack.append(1)
stack.append(4)
stack.pop()
print(stack)
print(stack[::-1])
```

    [5, 2, 3, 1]
    [1, 3, 2, 5]
    

#### Queue
선입선출 구조  
``collections``모듈에서 제공하는 deque 자료구조 활용 


```python
from collections import deque

queue = deque()

queue.append(5)
queue.append(2)
queue.append(3)
queue.append(7)
queue.popleft()
queue.append(1)
queue.append(4)
queue.popleft()

print(queue)
queue.reverse() #역순으로 바꾸기 (=stack[::-1])
print(queue)
```

    deque([3, 7, 1, 4])
    deque([4, 1, 7, 3])
    

# DFS / BFS

## DFS : 깊이 우선 탐색

1. 탐색 시작 노드를 스택에 삽입하고 저장
2. 스택의 최상단에 방문하지 않은 노드 넣고 방문처리   
   방문하지 않은 인접 노드 없으면 최상단 노드 꺼내기 
3. 2번 과정 수행할 수 없을때까지 반복


```python
def dfs(graph,v,visited):
    visited[v]=True
    print(v,end='')
    for i in graph[v]:
        if not visited[i]:
            dfs(graph,i,visited)
graph = [
    [],
    [2,3,8],
    [1,7],
    [1,4,5],
    [3,5],
    [3,4],
    [7],
    [2,6,8],
    [1,7]
]

visited = [False]*9
dfs(graph,1,visited)
```

    12768345

## BFS : 넓이 우선 탐색

1. 탐색 시작 노드 큐에 삽입
2. 큐에서 노드 꺼내 해당 노드의 인접 노드 중 방문하지 않은 노드  
   모두 큐에 삽입하고 방문 처리 
3. 2번 과정 수행할 수 없을때까지 반복


```python
from collections import deque

def bfs(graph,start,visited):
    queue = deque([start])
    visited[start] = True
    while queue:
        v = queue.popleft()
        print(v,end='')
        for i in graph[v]:
            if not visited[i]:
                queue.append(i)
                visited[i]=True
                
graph = [
    [],
    [2,3,8],
    [1,7],
    [1,4,5],
    [3,5],
    [3,4],
    [7],
    [2,6,8],
    [1,7]
]

visited = [False]*9
bfs(graph,1,visited)
```

    12387456

## #음료수 얼려 먹기(DFS)


```python
n,m = map(int,input().split())
li=[]

for i in range(n):
    li.append(list(map(int,input())))
            
def dfs(x,y):
    if x<=-1 or x>=n or y<=-1 or y>=m :
        return False
    if li[x][y]==0:
        li[x][y] =1
        dfs(x-1,y)
        dfs(x,y-1)
        dfs(x,y+1)
        dfs(x+1,y)
        return True
    return False

result = 0
for i in range(n):
    for j in range(m):
        if dfs(i,j)== True:
            result+=1
            
print(result)
               
```

    4 5
    00110
    00011
    11111
    00000
    3
    

## #미로탈출(BFS)


```python
from collections import deque

n,m = map(int,input().split())
graph = []

for i in range(n):
    graph.append(list(map(int,input())))
    
dx = [1,0,-1,0]
dy = [0,-1,0,1]

def bfs(x,y):
    queue = deque()
    queue.append((x,y))
    while queue:
        x,y = queue.popleft()
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            if nx<0 or ny<0 or nx>=n or ny>=m :
                continue
            if graph[nx][ny]== 0:
                continue
            if graph[nx][ny] == 1:
                graph[nx][ny] = graph[x][y]+1
                queue.append((nx,ny))
    return graph[n-1][m-1]
    
print(bfs(0,0))                
```

    3 3
    110
    010
    011
    5
    
