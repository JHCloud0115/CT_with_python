
# Shortest Path

##  다익스트라 최단 경로

그래프에서 여러 개의 노드가 있을 때, 특정한 노드에서 출발하여 다른 노드로 가는 각각의 최단 경로를 구해주는 알고리즘

### 1.간단한 다익스트라 
```python
import sys
input = sys.stdin.readline
INF = int(1e9)

#초기값 설정
n,m = map(int,input().split())
start = int(input())
  #n+1로 하는 이유는 노드 번호와 인덱스 번호 맞추기 위한 설정 
graph = [[] for i in range(n+1)]
visited = [False]*(n+1)
distance = [INF]*(n+1)

for _ in range(m):
    #a는 노드번호 b,c는 노드가 b로 갈때의 거리값c 입력 
    a,b,c = map(int,input().split())
    graph[a].append((b,c))

def get_smallest_node():
    #노드 번호와 거리가 들어간 표 설정 
    min_value = INF
    #불러올 인덱스 초기값 설정 
    index = 0 
    for i in range(1,n+1):
        if distance[i] < min_value and not visited[i]:
            index = i
    return index
    
def dijkstra(start):
    #시작 설정 초기화 
    distance[start] = 0  #시작 노드의 거리는 0으로 설정 
    visited[start] = True
    for j in graph[start]:
        distance[j[0]] = j[1]
    for i in range(n-1):
        #현재 값 중 가장 작은 노드 불러올 수 있도록 + 방문처리 
        now = get_smallest_node()
        visited[now] = True
        for j in graph[now]:
            cost = distance[now]+j[1]
            if cost < distance[j[0]]:
                distance[j[0]] = cost
#다익스트라 수행               
dijkstra(start)

#모든 노드 가기 위한 최단 거리 출력 
for i in range(n,n+1):
    if distance[i] == INF:
        print('INFINITY')
    else:
        print(distance[i])
```

### 2. 개선된 다익스트라 
``` python
import heapq
import sys
input = sys.stdin.readline

n.m = map(int,input().split())
start = int(input())
graph = [[] for i in range(n+1)]
distance = [INF] *(n+1)

for _ in range(m):
  a,b,c = map(int,input().split())
  graph[a].append((b,c))

def dijkstra(start):
  q = []
  #거리 노드 순으로 입력 
  heapq.heappush(q,(0,start))
  distance[start] = 0
  while q:
      dist,now = heapq.heappop(q)
      if distance[now]<dist:
         continue
      for i in graph[now]:
        cost = dist+i[1]
        if cost < distanc[i[0]]:
          distance[i[0]] = cost
          heapq.heappush(q,(cost,i[0]))

dijkstra(start)

for i in range(1,n+1):
  if distance[i] == INF :
     print('INFINITY')
  else:
     print(distance[i]) 

```


### 플로이드 워셜 알고리즘 
모든 지점에서 다른 모든 지점까지의 최단 경로 구해야하는 경우 사용 

```python 
INF = int(1e9)
n = int(input())
m = int(input())
graph = [[INF]*(n+1) for _ in range(n+1)]

for a in range(1,n+1):
    for b in range(1,n+1):
       if a == b:
       graph[a][b] = 0
       
 for k in range(1,n+1):
    for a in range(1,n+1):
       for b in range(1,n+1):
           graph[a][b] = min(graph[a][b],graph[a][k]+graph[k][b])

 for a in range(1,n+1):
    for b in range(1,n+1):
        if grapph[a][b] == INF :
            print('INFINITY')
        else:
            print(graph[a][b],end = '')
    print()
```
### 미래도시 
  - 한 지점에서 다른 지점으로 갈때 k 들려서 모든 경우 생각함으로 ``플로이드워셜 알고리즘`` 사용 
```python 
INF = int(1e9)

n,m = map(int,input().split())
graph = [[INF] for _ in range(1,n+1)]

#자기가 자기한테 갈 때 값 0으로 설정
for a in range(1,n+1):
   for b in range(1,n+1):
       if a == b : 
            graph[a][b] = 0
            
 
for _ in range(m): 
    a,b = map(int,input().split())
    #서로에게 가는 비용 1로 설정
    graph[a][b] =1
    graph[b][a] =1

x,k = map(int,input().split())

for k in range(1,n+1):
    for a in range(1,n+1):
       for b in range(1,n+1):
           graph[a][b] = min(graph[a][b],graph[a][k]+graph[k][b])

distance = graph[1][k] + graph[k][x]

if distance >= INF :
    print('-1')
else:
    print(distance)
```
### 전보 
```python 
import heaqp
import sys

input = sys.stdin.readline
INF = int(1e9)

n,m,start = map(int,input().split())
graph = [[] for _ in range(n+1)]
distance = [INF]*(n+1)

for _ in range(1,n+1):
   x,y,z = map(int,input().split())
   graph[x].append((y,z))

def dijkstra(start):
   q = []
   heaqp.heappush(q,(0,start))
   distance[start] = 0
   while q :
       dist,now = heap.heappop(q)
       if distance[now] < dist :
           continue
       for i in graph[now]:
          cost = dist+i[1]
          if cost < distance[i[0]]:
             distance[i[0]] = cost
             heapq.heappush(q,(cost,i[0]))

dijkstra(start)

cnt = 0
max_distance = 0
for d in distance:
    if d != INF:
       cnt+=1
       max_distance = max(max_distance,d)

print(cnt-1,max_distance)

```

