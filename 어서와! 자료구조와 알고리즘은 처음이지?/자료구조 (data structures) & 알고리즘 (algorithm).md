# 자료구조 (data structures) & 알고리즘 (algorithm)

## ✔ 자료구조 (data structures) 이란?

```python
# max를 실행하는데 걸리는 시간 알아보기
import time

n = int(input("Number of elements: "))
haystack = [k for k in range(n)]

print("Searching for the maximum value...")

ts = time.time()
maximum = max(haystack)
elapsed = time.time() - ts

print("Maximum element = %d, Elapsed time = %.2f" %(maximum, elapsed))
```



## ✔ 알고리즘 (algorithm) 이란?

- 사전적 정의 - 어떤 문제를 해결하기 위한 절차, 방법, 명령어들의 집합
- 프로그래밍 - 주어진 문제의 해결을 위한 자료구조와 연산 방법에 대한 선택





해결하고자 하는 문제에 따라 (응용 종류와 범위에 따라) 최적의 해법은 서로 다르다. 이 선택을 어떻게 해야하느냐를 알기 위해 자료구조를 이해해야 한다.
