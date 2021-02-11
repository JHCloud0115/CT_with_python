# Sorting : 정렬 
데이터를 특정한 기준에 따라서 순서대로 나열하는 것
- 선택 정렬
- 삽입 정렬
- 퀵 정렬
- 계수 정렬

## 선택정렬 



```python
li = [7,5,9,0,3,1,6,2,4,8]

for i in range(len(li)):
    min_n = i
    for j in range(i+1,len(li)):
        #앞에 정렬된 것 이외의 나머지부터 정렬하기 위해서 i+1로 설정 
        if li[min_n]>li[j]:
            min_n = j #새로 선택한 가장 작은 원소의 인덱스 설정 
            li[min_n],li[j] = li[j],li[min_n]
print(li)
    
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    

## 삽입정렬


```python
li = [7,5,9,0,3,1,6,2,4,8]

for i in range(1,len(li)):
    #i까진 정렬 / i부터 왼쪽으로 이동하면서 값 비교 
    for j in range(i,0,-1):
        if li[j]<li[j-1]:
            li[j],li[j-1] = li[j-1],li[j]
        else:
            break
            
print(li)
            
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    

## 퀵정렬 


```python
li = [5,7,9,0,3,1,6,2,4,8]

def quick_sort(li,start,end):
    if start >=end:
        return 
    pivot = start 
    left = start+1
    right = end
    while left <= right:
        while left <= end and li[left]<= li[pivot]:
            left +=1
        while right > start and li[right] >= li[pivot]:
            right-=1
        if left > right :
            li[right],li[pivot] = li[pivot],li[right]
        else:
            li[right],li[left] = li[left],li[right]
        quick_sort(li,start,right -1)
        quick_sort(li,right+1,end)

quick_sort(li,0,len(li)-1)
print(li)

# 좀 더 빠르게 구현한 퀵 정렬

def quick_sort2(li):
    if len(li)<=1:
        return li
    pivot = li[0] #첫번째 원소 기준점으로 설정
    tail = li[1:] #나머지 보관
    
    left_side = [x for x in tail if x<= pivot] #기준점보다 작은 값들 보관
    right_side = [x for x in tail if x>pivot]  #기준점보다 큰 값들 보관
    
    return quick_sort2(left_side)+[pivot]+quick_sort2(right_side) #크고 작은 값들 보관한거 다시 정렬 + 기준값 =>전체 불러오기 
print(quick_sort2(li))
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    

## 계수정렬


```python
li = [7,5,9,0,3,1,6,2,9,4,8,0,5,2]
#현재 0부터 9까지 담을 수 있는 범위 10의 리스트 생성
count = [0]*(max(li)+1) 

#10번 돌리면서 해당 값의 수 +1씩 
for i in range(len(li)):
    count[li[i]]+=1
    

for i in range(len(count)): #10번 돌리면서 
    for j in range(count[i]): #반복된 만큼 수 보여주기 
        print(i,end=' ')
```

    0 0 1 2 2 3 4 5 5 6 7 8 9 9 

### #위에서 아래로 


```python
n = int(input())
li =[]

for i in range(n):
    li.append(int(input()))
    li.sort()

for i in li:
    print(i,end=' ')
```

    3
    15
    27
    12
    12 15 27 

### #성적이 낮은 순서로 학생 출력하기


```python
n = int(input())
students =[]

for i in range(n):
    students.append(input().split())

students.sort()

for i in students:
    print(i[0],end=' ')
```

    2
    홍길동 95
    이순신 77
    이순신 홍길동 


```python
n = int(input())

array = []
for i in range(n):
    input_data=input().split()
    array.append((input_data[0],int(input_data[1])))
    
array = sorted(array,key=lambda student:student[1])

for student in array:
    print(student[0],end=' ')
```

    2
    홍길동 95
    이순신 77
    이순신 홍길동 

### #두 배열의 원소 교체 


```python
n,k = map(int,input().split())
cnt = k

for i in range(2):
    if i == 0 :
        a = list(map(int,input().split()))
        a = sorted(a)
    else:
        b = list(map(int,input().split()))
        b = sorted(b,reverse=True)

for i in range(k):
    if a[i] < b[i]:
        a[i],b[i] = b[i],a[i]
    else:
        break
        
print(sum(a))
```

    5 3
    1 2 5 4 3
    5 5 6 6 5
    26
    
