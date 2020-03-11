---
layout: post
title: "[python] 파이썬 filter"
author: optboy
categories: [Python]
---

lambda와 자주 쓰이는 함수 중에는 filter도 있다.

## filter란?
- filter은 인자로 **함수**와 **순서형 자료**를 받는다.
- 즉, `filter(func, iterable)`로 표현된다.
- filter은 순서형 자료에서 특정 조건을 만족하는(함수의 결과가 참이라면) 요소들만 뽑아 새로운 리스트를 만든다. 
- filter함수는 filter객체를 반환하기 때문에 `list`로 변환시켜 줘야한다. 

## filter 사용법
- filter은 파이썬이 정상적으로 설치되어 있다면 바로 쓸 수 있다. 

    ```python
    li = list(range(10))
    list(filter(lambda x:x % 2 != 0, li))
    # [1, 3, 5, 7, 9]
    ```

## filter을 사용하지 않는다면?
```python
li = list(range(10))

result = []
for i in li:
    if i % 2 != 0:
        result.append(i)
result
# [1, 3, 5, 7, 9]
```

#### 참고 
- [왕초보를 위한 Python - 3.5](https://wikidocs.net/64)