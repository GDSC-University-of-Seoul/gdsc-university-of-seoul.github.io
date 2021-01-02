---
layout: post
title: "[fall-intro team, Dec] 조합 함수와 def 함수 배우고 적용하기!"
authors: [hyeinPark]
tags: ["intro"]
image: 
description: "DSC intro team 12월 활동 정리."
featured: false
---



12월 한 달 동안은 <u>def 와 for 을 이용한 조합 함수</u>와 <u>def 함수</u>를 응용해서 과제를 해결하는 시간을 

가졌습니다!


------



과제4의 마지막 문제인 (5)번은 저에게 문제 이해부터 막혔던.... 정말 어려웠던 문제였습니다.

**combination 함수를 사용하지 않고** 아래의 코드를 출력해야 하는 문제였는데요.



＊출력

``` 01 02 03 ... 09 12 13 ... 78 79 89
01 02 03 ... 09 12 13 ... 78 79 89
```



문제를 이해하고자 삽질을 정말 많이 해보았으나.... 해답을 찾지 못하였고  intro 팀원인 김수빈 선배님의 힌트 덕분에 문제에 규칙성이 있다는 것은 알게 되었으나, 숫자 갯수에 대한 규칙성에 집착한 나머지 ''자릿수의 크기에 규칙성''이 있다는 것을 뒤늦게 깨달았습니다. 



이 문제의 핵심은 십의 자리가 일의 자리보다 작아야 한다는 것이었죠! (십의 자리 < 일의 자리)



문제 이해는 해결하였으나 combination 함수 없이 코드를 짜는 것이 어려웠습니다.

아래 코드를 통해 조합 부분을 해결하고,

```python def comb(arr):
def comb(arr):
    result=[]
    for i in range(len(arr)):
        for j in arr [i+1:]:
            result.append(str(i)+str(j))
    return result
```



함수에서 return 하는 것을 따로 저장해서 for문으로 출력하기 위해, 다음 코드를 구현하여 해결하였습니다!

```python
lst=[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
op = comb(lst)
for i in range(len(op)):
    print(op[i], end=' ')
```



------



다음으로 def 함수를 이용하여 과제5를 해결하였는데요!

과제4의 마지막 문제에서 고전했던 탓인지 과제5는 ~~생각보다 괜찮은데 싶을 정도로~~ 수월하게 해결할 수 있었습니다 :)



우선, 과제5 (1) 문제는 print_hello()를 이용하여 Hello World!를 출력하는 def 함수 안에 함수 만들기였습니다.



```python
def print_hello():
    hello = 'Hello World!'
    def print_add():
        print(hello)
    print_add()
print_hello()
```



print_hello() 에서 hello를 정의해주고, 안에 def 함수 print_add를 만들어서 print_hello를 정의하고 print_add를 출력하는 함수를 정의하였습니다.

함수를 만들었으니, 마지막으로 print_hello를 출력함으로써 Hello World!를 출력하는 코드를 세울 수 있었습니다. 



*출력

```Hello World!
Hello World!
```



2번째 문제는 언더바를 이용해서 문자열을 연결하는 함수를 만드는 것이었습니다.

return을 이용하여 기존에 학습했던 +를 이용하여 문자열을 합치는 코드를 구현해보았습니다.



```python
def insert_underbar(x, y):
    return x + '_' + y
result = insert_underbar(x= 'py', y= 'thon')
print(result)
```



*출력

``` 
py_thon
```



3번째 문제는 섭씨 온도를 화씨 온도로 변환하는 코드를 구현하는 것이 문제였습니다!

섭씨는 알지만.... 익숙하지 않은 화씨가 갑자기 나와서 당황했던 문제인데요.



**섭씨 → 화씨 변환 공식**

(**°C** × 9/5) + 32 = **°F**



```python
def ctof(n) :
    m = 9*n/5+32
    return m

print(ctof(100))
```

:  n= 섭씨, m= 화씨



return과 섭씨에서 화씨로 변환하는 공식을 이용하여,

섭씨가 100º일 때, 화씨가 212º라는 것을 알 수 있었습니다.



*출력

```
212.0
```



마지막으로, 과제5의 4번 문제는 재귀 호출을 이용하여 피보나치 수열 코드를 만드는 것이었습니다!



피보나치 수열의 공식은,

**f(n) = 1 (n <=2 일 때)**

**f(n) = f(n-2) + f(n-1) (n>2 일 때)** 이런 식으로 나타낼 수 있는데요.



저는 피보나치 수열 공식을 이용해서 

```python
def fibo(n):
    if n < 3:
        return 1
```

: n <=2 일 때, 결과값은 1



```python
    else :
        return fibo(n-1) + fibo(n-2)
```

: n>2 일 때, 피보나치 수열 공식을 이용해서 코드를 구현하여 과제를 해결하였습니다.



```python
def fibo(n):
    if n < 3:
        return 1
    else :
        return fibo(n-1) + fibo(n-2)
    
print(fibo(10))
```



*출력 

```
55
```





------


9월부터 12월까지 과제를 하면서 파이썬 문법에 대해 익혀왔는데요!

과제 문제와 git 문제로 삽질하면서 공부했던 시간이 짧다면 짧고 길다면 긴 시간이겠지만 점점 감을 잡아가는 것 같아서 뿌듯하기도 하고, 아직 새발의 피겠지만... 파이썬 문법을 점점 알아가는 것을 직접 느끼다보니 더 성장했다는 것을 체감하고 있습니다!

인트로 팀의 호준 선배님께서 늘 해주시는 말로 글 마무리짓도록 하겠습니다.



**Don't panic!**