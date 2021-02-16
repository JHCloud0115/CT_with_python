# Binary Search : 이진탐색 

- 반으로 쪼개면서 탐색하기 
- 배열 내부의 데이터는 정렬되어 있어야 함


```python
#재귀함수 사용 
def search(array,target,start,end):
    if start>end:
        return None
    mid = start+end//2
    if array[mid]== target:
        return mid
    if array[mid] >target : 
        #중간값이 더 클 경우 중간값보다 작은 값으로 끝 값 변경
        return search(array,target,start,mid-1)
    elif array[mid]<target:
        #중간값이 더 작을 경우 시작값을 중간값보다 큰 값으로 변경
        return search(array,target,mid+1,end)
    
n,target = list(map(int,input().split()))
array = list(map(int,input().split()))

result = search(array,target,0,n-1)
if result == None :
    print('No result')
else : 
    #위치임으로 1더해서 
    print(result+1)
```

    10 7
    1 3 5 7 9 11 13 15 17 19
    4
    


```python
#반복문 사용 
def search(array,target,start,end):
    while start <= end : 
        mid = (start+end) //2
        if array[mid] == target : 
            return mid
        elif array[mid]> target : 
            end = mid -1
        else : 
            start = mid+1
    return None

n,target = list(map(int,input().split()))
array = list(map(int,input().split()))

result = search(array,target,0,n-1)
if result == None : 
    print('X')
else:
    print(result+1)
```

    10 7
    1 3 5 7 9 11 13 15 17 19
    4
    

### #부품찾기


```python
n = int(input())
nums = list(map(int,input().split()))
nums = sorted(nums)
m = int(input()) 
w = list(map(int,input().split()))
result = []

for i in range(m):
    if w[i] in nums:
        result.append('yes')
    else:
        result.append('no')
                
            
for k in range(len(result)):
    print(result[k],end = ' ')
```

    5
    8 3 7 2 9
    3
    5 7 9
    no yes yes 


```python
#집합자료형 이용 
n = int(input())
array = set(map(int,input().split()))

m = int(input())
x = list(map(int,input().split()))

for i in x :
    if i in array:
        print('yes',end = ' ')
    else:
        print('no',end = ' ')
```

    5
    8 3 7 2 9
    3
    5 7 9
    no yes yes 

### #떡볶이 떡 만들기 


```python
n,m = map(int,input().split())
nums = list(map(int,input().split()))
nums = sorted(nums)

def search(nums,target,start,end):
    result = 0
    mid = start+end//2
    while result <= m : 
        if mid <= nums[mid]:
            result += nums[mid]- mid
            mid+=1
            return result
        else:
            continue
    return result

for i in nums:
    result = search(nums,i,0,n)
print(result)
```

    4 6
    19 15 10 17
    15
    


```python
n,m = list(map(int,input().split(' ')))
array = list(map(int,input().split()))

start = 0 
end = max(array)

result = 0 
while start<=end:
    total = 0 
    mid = (start+end)//2
    for x in array:
        if x>mid:
            total+=x-mid
    if total < m:
        end = mid-1
    else:
        result = mid
        start = mid+1
print(result)
```

    4 6
    19 15 17 10
    15
    
