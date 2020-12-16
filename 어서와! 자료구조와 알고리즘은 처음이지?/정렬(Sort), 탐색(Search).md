# 정렬(Sort), 탐색(Search)

## ✔ 정렬(sort) 이란?

복수의 원소로 주어진 데이터를 정해진 기준에 따라 새로 늘어놓는 작업이다. 파이썬의 리스트를 이용하면 직접 정렬 알고리즘을 구현할 필요가 없다.

- 파이썬 내장 함수 `sorted()`
- 리스트에 쓸 수 있는 메서드 `.sort()`

정렬의 순서를 반대로하길 원할 때 인자로 `reverse = True`를 넣어준다.

문자열로 이루어진 리스트의 경우 정렬 순서는 사전순서(알파벳 순서)를 따른다. 문자열 길이가 긴 것이라고 해서 더 큰 것이 아니다. 문자열 길이 순서로 정렬하고 싶다면 정렬에 이용하는 `키(key)`를 지정해준다.

 ```python
L = ['abcd', 'xyz', 'spam']
# 문자열 길이로 정렬
sorted(L, key=lambda x: len(x))

L = [ {'name': 'john', 'score': 88},
    {'name': 'paul', 'score': 92} ]

# 레코드들을 이름 순서대로 정렬
L.sort(key = lambda x : x['name'])

# 레코드들을 점수 높은 순으로 정렬
L.sort(key=lambda x : x['score'], reverse=True)
 ```



## ✔ 탐색(search) 이란?

복수의 원소로 이루어진 데이터에서 특정 원소를 찾아내는 작업으로 여러가지 방법이 있지만 아주 기본적인 두 가지가 있다.

#### 💡 선형 탐색 (Linear Search) or 순차 탐색 (sequential search)

순차적으로 모든 요소들을 탐색하여 원하는 값을 찾아내는 방법, 배열의 길이에 비례하는 시간이 걸리므로 최악의 경우에는 배열에 있는 모든 원소를 다 검사해야할 수 있다. O(n)

#### 💡 이진탐색(binary search) 

탐색하려는 배열이 이미 정렬되어있는 경우에 사용, 크기 순으로 정렬되어있다는 성질을 이용해 한 번에 절반씩 배열을 잘라서 비교해서 찾는다. 한 번 비교가 일어날 때마다 리스트를 반씩 줄인다. O(logN)

```python
# 선형 탐색
def linear_search(L, x):
    i = 0
    while i < len(L) and L[i] != x:
        i += 1
    if i < len(L):
        return i
    else:
        return -1

# 이진 탐색
def binary_search(L, x):
    answer = -1
    
    lower = 0
    upper = len(L) -1
    
    while lower<=upper:
        middle = (lower+upper)//2
        
        if L[middle] == x:
            answer = middle
            break
        elif L[middle] < x:
            lower = middle + 1
            middle = (lower + upper)//2
        else:
            upper = middle -1
            middle = (lower + upper)//2
    
    return answer
```