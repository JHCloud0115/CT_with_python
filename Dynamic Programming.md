# Dynamic Programming:다이나믹 프로그래밍

다이나믹 프로그래밍을 사용할 수 있는 조건
- 큰 문제를 작은 문제로 나눌 수 있을 때 
- 작은 문제에서 구한 정답은 그것을 포함하는 크 문제에서도 동일할 때 

### 피보나치 수열 
다이나믹 프로그래밍을 사용할 수 있는 대표적인 문제  
``메모제이션 기법``을 사용 - 한 번 구현한 결과를 메모리 공간에 두고 같은 식을 다시 호출하면 메모한 결과를 그대로 가져오는 기법  


```python
#재귀 사용  - 탑다운 방식

d = [0]*100

def fibo(x):
    if x == 1 or x == 2 :
        return 1
    if d[x] != 0:
        return d[x]
    d[x] = fibo(x-1)+fibo(x-2)
    return d[x]

print(fibo(99))
```

    218922995834555169026
    


```python
#반복문 사용  - 보텀업 방식

d = [0]*100
d[1] = 1
d[2] = 1
n = 99

for i in range(3,n+1):
    d[i] = d[i-1]+d[i-2]
    
print(fibo(99))
```

    218922995834555169026
    

### #1로 만들기 


```python
d = [0]*30001
x = int(input())

for i in range(2,x+1):
    #+1은 함수의 호출 횟수를 구하기 위해서 
    d[i] = d[i-1]+1
    if i % 5 ==0:
        d[i] = min(d[i],d[i//5]+1)
    if i % 3 ==0:
        d[i] = min(d[i],d[i//3]+1)
    if i % 2 ==0:
        d[i] = min(d[i],d[i//2]+1)
print(d[x])
    
    
```

    26
    3
    

### #개미전사


```python
n = int(input())
nums = list(map(int,input().split()))

d = [0]*1001
d[1] = max(nums[0],nums[1])

for i in range(2,n):
    d[i] = max(d[i-1],d[i-2]+nums[i])
print(d[n-1])
    

```

    4
    1 3 1 5
    8
    

개미전사가 dp로 풀 수 있는 이유는 
- i-1과 i-2까지의 최적의 해를 이용해서 구하기 때문에 
- 큰 문제(현재까지 더한 값들의 큰 값)를 해결하기 위해 작은 문제(그 이전의 더한 값들) 두개(i-2,i-1까지의 더한 값들)를 사용하기 때문에 

### #바닥공사 


```python
n = int(input())
d = [0]*1001

d[1]=1
d[2]=3
for i in range(3,n+1):
    d[i] = (d[i-1]+2*d[i-2])%796796
print(d[i])
    
```

    3
    5
    

### #효율적인 화폐 구성


```python
n,m = map(int,input().split())
array = []
for i in range(n):
    array.append(int(input()))
    
d = [10001]*(m+1)

d[0] = 0
for i in range(n): #화폐단위 확인
    for j in range(array[i],m+1): #금액 확인 
        if d[j-array[i]] != 10001: #현재 금액에서 현재 확인하고 있는 화폐 단위로 값을 만들 수 있는 경우
            d[j] = min(d[j],d[j - array[i]]+1)

            
if d[m] == 10001:
    print(-1)
else:
    print(d[m])
```

    3 7
    2
    3
    5
    2
    

`if d[j-array[i]] != 10001 `은 현재 금액에서 현재 확인하고 있는 화폐 단위를 통해 만들 수 있는 값일 경우에  
`d[j]`와 `d[j - array[i]]+1`중 작은 값을 확인한다는 것인데, 예를 들어 현재 금액이 7이고 화폐 단위가 5인 경우를 예를 들 때,  
현재 array에 화폐 단위 2와 3으로 만들 수 있던 갯수를 더해둔 값과 확인하는 화폐 단위인 5를 7에서 뺀 경우 array값이 10001이 아닌 값 중 작은 값을 구한 값이 `d[j]`란 소리 
