# Greedy : 그리디 

### #1 거스름돈 
음식점의 계산을 도와주는 직원으로, 500원 100원 50원 10원짜리 동전이 무한히 존재.  
손님에게 거슬러 줘야 할 돈이 N원일 때 **거슬러줘야할 동전의 최소 개수**를 구해라  
(단, 거슬러 줘야 할 돈N은 항상 10의 배수)


```python
n = int(input())
count=0
list = [500,100,50,10]

for i in list:
    count+=n//i
    n %=i

    
print(count)
    
```

    3000
    6
    

위의 문제가 그리디 알고리즘으로 해결되는 이유는  
가지고 있는 동전 중 큰 단위가 항상 작은 단위의 배수로 작은 단위의 동전들을 종합해 다른 해가 나올 수 없기 때문이다 

### #2 큰수의 법칙


```python
# 1
n,m,k = map(int,input().split())
nums = list(map(int,input().split())
nums.sort()
result = 0

while True:
    for i in range(k):
        if m == 0:
            break
        result+=nums[-1]
        m-=1
    if m == 0:
            break
    reult+=nums[-2]
    m-=1

print(result)
```


```python
# 2 반복되는 수열 파악해서 문제풀기 

n,m,k = map(int,input().split())
nums = list(map(int,input().split())
nums.sort()


#가장 큰 수가 더해지는 횟수 계산
count = int(m/(k+1))+k
count+=m%(k+1)

result=0
result+=(count)*nums[-1]
result+=(m-count)*nums[-2]
            
print(result)
```

반복되는 수열을 파악해서 푸는 이유는 m의 크기가 100억 이상처럼 커지면 시간 초과 판정을 받을 수 있음    
따라서, m을 k+1로 나눈 몫이 수열이 반복되는 횟수로 여기에 k를 곱해주면 가장 큰 수가 등장하는 횟수 알 수 있음  
m이 k+1로 나누어떨어지지 않을 경우도 고려하기 위해서 m을 k+1로 나눈 나머지만큼 가장 큰 수 추가로 더해지는 경우 고려  
두번째로 큰 수는 m에서 count 수 빼면 두번째로 큰 수가 등장하는 횟수를 알 수 있음 

### #3 숫자 카드게임 


```python
# 이중 반복문 구조 이용
r,c = map(int,input().split())
nums=[]
for i in range (r):
    nums.append(list(map(int,input().split())))
    nums.sort()
    for j in range(c):
        result = nums[0][0]
        if result > nums[i][j]:
            result = nums[i][j]
        else:
            result = result 

print(result)
```


```python
# min()사용 이용
r,c = map(int,input().split())
result = 0
for i in range(n):
    data = list(map(int,input(),split()))
    min_value=min(data)
    result = max(result,min_value)
print(result)
```

### #1이 될 때까지 


```python
n, k = map(int,input().split())
cnt=0
while n !=1 :
    if n % k == 0:
        n = n/k
        cnt+=1
    else :
        n = n-1
print(cnt)
```


```python

```
