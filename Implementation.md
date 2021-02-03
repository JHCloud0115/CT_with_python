## Implementation : 구현

### 방향벡터 

시뮬레이션 및 완전 탐색 문제에서 2차원 공간에서의 방향벡터 활용 코드


```python
# 동,북,서,남
#예)동 dx[0]dy[0] =(0,1) -->오른쪽으로만 1만큼 움직여라 
dx = [0,-1,0,1]
dy = [1,0,-1,0]



#현재위치  
x,y = 2,2

#다음위치 
for i in range(4): #동서남북으로 방향 4개
    nx = x + dx[i]
    ny = y + dy[i]
    print(nx,ny)
```

    2 3
    1 2
    2 1
    3 2
    

### #1 상하좌우 


```python
n=int(input())
plan = input().split()
x,y = 1,1

dx = [0,0,-1,1]
dy = [-1,1,0,0]
move = ['L','R','U','D']

for i in plan : 
    for j in range(len(move)):
        if i == move[j]:
            nx = x+dx[j]
            ny = y+dy[j]
    if nx<1 or ny<1 or nx>n or ny>n :
        continue
    x,y = nx,ny
    
print(x,y)
```

    5
    R R R U D D
    3 4
    

### #2 시각


```python
n = int(input())
cnt = 0

for i in range (0,n+1,1):
    for j in range(0,60,1):
        for k in range(0,60,1):
            if str(n) in str(i)+str(j)+str(k):
                cnt+=1
print(cnt)
```

    5
    11475
    

### #3 왕실의 나이트 


```python
n =input()
r = int(n[1])
c = int(ord(n[0])) - int(ord('a'))+1

steps = [(-2,-1),(-1,-2),(1,-2),(2,-1),(2,1),(1,2),(-1,2),(-2,1)]

cnt = 0
for i in steps : 
    nxtR = r+i[0]
    nxtC = c+i[1]
    if nxtR >=1 and nxtR<=8 and nxtC>=1 and nxtC <=8:
        cnt+=1
print(cnt)
    
```

    a1
    2
    

### #4 게임개발


```python
n,m = map(int,input().split())
d = [[0]*m for _ in range(n)] #방문 위치 저장 위한 맵 생성 
a,b,direction = map(int,input().split())

for i in range(n):
    li = []
    i = input().split()
    li.append(i)

#북 동 남 서 
dx = [0,1,0,-1]
dy = [1,0,-1,0]

#왼쪽 회전 
def turn_left():
    global direction #함수 밖에서 사용된 direction 사용으로 global 사용
    direction -=1
    if direction == -1:
        direction = 3
            
cnt = 1
turn_time = 0
while True:
    turn_left()
    nx = a + dx[direction]
    ny = b + dy[direction]
    if d[nx][ny] == 0 and li[nx][ny] == 0:
        d[nx][ny] =1
        a = nx
        b = ny
        count+=1
        turn_time = 0 
        continue
    else:
        turn_time+=1
    if turn_time ==4:
        nx = a - dx[direction]
        ny = b - dy[direction]
        if li[nx][ny] == 0:
            a = nx
            b = ny
        else:
            break
        turn_time = 0
print(cnt)
```
