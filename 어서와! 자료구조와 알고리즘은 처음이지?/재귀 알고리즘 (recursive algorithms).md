# 재귀 알고리즘 (recursive algorithms)

알고리즘들 중에는, 재귀 알고리즘이라고 불리는 것이 있다. 이것은 알고리즘의 이름이 아니라 성질이다. 주어진 문제가 있을 때 이것을 같은 종류의 보다 쉬운 문제의 답을 이용해서 풀 수 있는 성질을 이용해서 같은 알고리즘을 반복적으로 적용함으로써 풀어내는 방법이다.



## ✔ 재귀함수 (recursive functions)란 ?

하나의 함수에서 자신을 다시 호출하여 작업을 수행하는 것으로 생각보다 많은 종류의 문제가 재귀적으로 해결이 가능하다. 

```python
# n! 팩토리알
def what(n):
    if n <= 1:
        return 1
    else:
        return n * what(n-1)
```





#### ✍ 문제설명

인자로 0 또는 양의 정수인 x 가 주어질 때, Fibonacci 순열의 해당 값을 구하여 반환하는 함수 solution() 을 완성하세요.

Fibonacci 순열은 아래와 같이 정의됩니다.
F0 = 0
F1 = 1
Fn = Fn - 1 + Fn - 2, n >= 2

재귀함수 작성 연습을 의도한 것이므로, 재귀적 방법으로도 프로그래밍해 보고, 반복적 방법으로도 프로그래밍해 보시기 바랍니다.

```python
def fibonacci(x):
    if x==0:
        return 0
    elif x==1:
        return 1
    else:
        return solution(x-1) + solution(x-2)
```

