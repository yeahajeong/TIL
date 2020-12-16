# 연결 리스트 (Linked List)

## ✔ 추상적 자료구조 (Abstract Data Structures)

자료구조의 내부 구현을 숨겨두고 밖에서 보이는 것들 (두 가지)을 말함

- **Data** : 정수, 문자열, 레코드...
- **A set of operations** : 삽입, 삭제, 순회... 정렬, 탐색...



## ✔ 기본적 연결 리스트

앞에 있는 놈이 뒤에 있는 놈을 가르키는 형식으로 늘어놓은 것이 연결 리스트라고 한다.

![image](https://user-images.githubusercontent.com/58287684/102360497-6d67f900-3ff5-11eb-82cd-a92cea90807f.png)

- Head : 리스트의 맨 처음 노드
- Tail : 리스트의 맨 마지막 노드 (리스트에 노드를 추가할 때 Tail을 사용한다.)
- of nodes : 노드가 몇개 있는지도 기록해두는 것이 좋다



![image](https://user-images.githubusercontent.com/58287684/102360686-abfdb380-3ff5-11eb-98ae-c3f0baca3944.png)

- 노드는 Data와 Link(Next)를 가지고 있다.
- 노드 내의 데이터는 다른 구조로 이루어질 수 있다 (문자열, 레코드, 또 다른 연결 리스트 등)



## ✔ 자료구조 정의

#### 💡 Node 클래스

![image](https://user-images.githubusercontent.com/58287684/102360826-da7b8e80-3ff5-11eb-9a5a-19339964e117.png)

```python
# Node 클래스
class Node:
    # 생성자
    def __init__(self, item):
        self.data = item
        self.next = None
```



#### 💡 LinkedList 클래스

![image](https://user-images.githubusercontent.com/58287684/102364147-7eb30480-3ff9-11eb-8fdf-6b274e715f67.png)

```python
# LinkedList 클래스
class LinkedList:
    def __init__(self):
        self.nodeCount = 0
        self.head = None
        self.tail = None
```



## ✔ 배열과 비교한 연결 리스트

![image](https://user-images.githubusercontent.com/58287684/102361071-29c1bf00-3ff6-11eb-9cc2-bdd695ac3e8d.png)

#### 💡 선형 배열에 비해 연결 리스트가 가지는 이점은?

연결 리스트에서는 원소들이 링크(link)라고 부르는 고리로 연결되어 있으므로, 가운데에서 끊어 원소 하나를 삭제하거나, 삽입하는 것이 선형 배열의 경우보다 빠른 시간내에 처리할 수 있다. 따라서 원소의 삽입/삭제가 빈번히 일어나는 응용에서 연결 리스트가 많이 이용된다. 컴퓨터 시스템을 구성하는 중요한 요소인 운영체제(operating system)의 내부에서도 이러한 연결 리스트가 여러 곳에서 이용되고 있다.

#### 💡 그렇다면 단점은?

선형 배열에 비해서 데이터 구조표현에 소요되는 저장 공간(메모리) 소요가 크다. 또 "k번째 원소"를 찾아가는데 선형 배열보다 오랜시간이 걸린다. (앞에서부터 특정원소까지 하나씩 링크를 따라가며 찾아야 하니까)



## ✔ 연산정의

1. 특정 원소(k번째) 참조
2. 리스트 순회
3. 길이 얻어내기
4. 원소 삽입
5. 원소 삭제
6. 두 리스트 합치기



#### 💡 특정 원소 참조 getAt

![image](https://user-images.githubusercontent.com/58287684/102361294-6e4d5a80-3ff6-11eb-9bbd-161911f771f0.png)

```python
	...
    # 1. 특정 원소 참조
    def getAt(self, pos):
        # 특정위치가 0보다 작거나 노드의 길이보다 크면 None을 반환
        if pos <= 0 or pos > self.nodeCount:
            return None
        
        i = 1
        curr = self.head # 연결리스트의 첫번째 노드를 가르킴
        
        # i가 pos보다 작은 동안에 i를 하나씩 증가시키면서 curr를 curr의 next를 가르키게 한다.
        # 즉 pos-1번 만큼 전진하면 그때 curr가 가르키는 것이 내가 리턴하려는 pos번째 노드가 된다.
        while i < pos: 
            curr = curr.next
            i += 1
        
        return curr
```



#### 💡 리스트 순회 traverse

```python
	...
    # 2. 리스트 순회
    def traverse(self):
        result = []
        curr = self.head
        while curr is not None:
            result.append(curr.data)
            curr = curr.next
        return result
```



#### 💡 길이 얻어내기 getLength

```python
	...
    # 3. 길이 얻어내기
    def getLength(self):
        return self.nodeCount
```



#### 💡 원소의 삽입 insertAt

원소가 삽입될 수 있는 조건 1 <= pos <= nodeCount + 1 이 범위 안에만 삽입할 수 있다.

newNode를 삽입하고 성공/실패에 따라 True/False를 리턴한다.



###### 🗣 원소의 삽입 흐름

![image](https://user-images.githubusercontent.com/58287684/102361999-372b7900-3ff7-11eb-9019-05aadb8dfbd1.png)

![image](https://user-images.githubusercontent.com/58287684/102362102-54604780-3ff7-11eb-916a-ebc38b98c59e.png)

1) 과 2) 의 순서를 바꾸면 안된다.



###### 🗣 코드 구현시 주의사항

1. 삽입하려는 위치가 리스트 맨 앞일 때
   - prev 없음
   - Head 조정 필요
2. 삽입하려는 위치가 리스트 맨 끝일 때
   - Tail 조정 필요
3. 빈 리스트에 삽입할 때
   - 이 두 조건에 의해 처리됨



###### 🗣 파이썬 코드 구현

```python
	...
	# 4. 연결리스트 연산 - 원소의 삽입
    def insertAt(self, pos, newNode):
        # pos의 위치가 유효한지 확인
        if pos < 1 or pos > self.nodeCount + 1 :
            # pos위치가 삽입할 수 있는 범위 밖에 있을 때 False 반환
            return False
        
        # 노드를 맨 처음 위치에 삽일할 때(prev없음)
        if pos == 1: # (빈 노드의 삽입할 조건에 걸림)
            newNode.next = self.head # 새로운 노드의 next는 head
            self.head = newNode # 헤드가 새로운노드가 된다
        
        # 삽입하려는 위치가 처음이 아닐 때
        else: 
            if pos == self.nodeCount + 1: # 삽입하려는 위치가 맨끝일 때
                prev = self.tail # prev == tail과 같음(앞에서 부터 찾을 필요 없음)
            else: # 삽입하려는 위치가 처음도 아니고 맨끝도 아닐 때
                prev = self.getAt(pos-1) # 끼워넣으려는 직전의 위치를 얻어낸다
            
            newNode.next = prev.next # 새로운 노드가 prev.next를 가르키도록한다.
            prev.next = newNode # prev.next를 newNode로 한다
        
        # 맨 마지막 위치에 삽입 할 때 (빈 노드의 삽입할 조건에 걸림)
        if pos == self.nodeCount + 1:
            self.tail = newNode # Tail을 새로운 노드로 변경
            
        # 마지막으로 노드의 갯수 증가
        self.nodeCount += 1
        return True
```



###### 🗣 시간 복잡도

- 맨 앞에 삽입하는 경우 O(1)
- 중간에 삽입하는 경우 O(n)
- 맨 끝에 삽입하는 경우 O(1) -> tail을 가지고 있기 때문에



#### 💡 원소의 삭제 def pop(self, pos)

pos의 위치가 1<= pos <= nodeCount 안에 위치해야한다.

노드를 삭제하고 그 노드의 데이터를 리턴



###### 🗣 원소의 삭제 흐름

![image](https://user-images.githubusercontent.com/58287684/102362778-1e6f9300-3ff8-11eb-9644-209708ca1596.png)

![image](https://user-images.githubusercontent.com/58287684/102362850-30e9cc80-3ff8-11eb-9861-7f858094fd8b.png)

![image](https://user-images.githubusercontent.com/58287684/102362924-44953300-3ff8-11eb-911e-38ac85f92803.png)

###### 🗣 코드 구현 주의사항

1. 삭제하려는 node가 맨 앞의 것일 때
   - prev가 없음
   - Head 조정 필요
2. 리스트의 맨 끝의 node를 삭제할 때
   - Tail 조정 필요
3. 유일한 노드를 삭제할 때
   - 이 두 조건에 의해 처리되는가?

삭제하려는 node가 마지막 node일 때, 즉 pos == nodeCount인 경우?

삽입하는 경우처럼 tail로 한 번에 처리할 수 없다. prev를 찾을 방법이 없으므로 앞에서부터 찾아와야한다.



###### 🗣 파이썬 코드 구현

```python
	...
    # 5. 연결리스트 연산 - 원소의 삭제
    def popAt(self, pos):
        # pop 값이 유효한지 확인 적당한 값이 아닐 경우 에러발생
        if pos < 1 or pos > self.nodeCount:
            raise IndexError
            
        # 맨 앞의 노드를 삭제하는 경우
        if pos == 1:
            curr = self.head
            self.head = self.getAt(pos+1)
            
            # 유일한 노드인 경우
            if self.nodeCount == 1:
                self.tail = None
                self.head = None
        
        # 맨 앞의 노드가 아닐 때
        else:
            prev = self.getAt(pos-1)
            curr = self.getAt(pos)
            prev.next = curr.next
            
            # 맨 끝 노드일 때
            if pos == self.nodeCount:
                self.tail = prev
                
        r = curr.data
        self.nodeCount -= 1
        
        return r
```



###### 🗣 시간 복잡도

- 맨 앞에서 삭제하는 경우 O(1)
- 중간에서 삭제하는 경우 O(n)
- 맨 끝에서 삭제하는 경우 O(n)



#### 💡 두 리스트의 연결 def concat(self, L)

연결 리스트 self 의 뒤에 또 다른 연결 리스트인 L 을 이어붙임



###### 🗣 두 리스트의 연결 흐름

![image](https://user-images.githubusercontent.com/58287684/102363624-ed439280-3ff8-11eb-9581-6e807bd11fef.png)



###### 🗣 파이썬 코드 구현

```python
	...
    # 6. 연결 리스트 연산 - 두 리스트의 연결
    def concat(self, L):
        # 원래 리스트의 맨 끝이 이어붙이려는 리스트의 처음으로
        self.tail.next = L.head
        
        # L.tail이 none인 경우 실행 안됨
        if L.tail:
            self.tail = L.tail
        self.nodeCount += L.nodeCount
```

뒤에 이어붙이려는 리스트 L이 빈 리스트인 경우 tail이 None값이 되어버리기 때문에 조건을 체크해주어야한다. L.tail이 유효한 경우에만 self.tail = L.tail로 해준다.
