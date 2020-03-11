---
layout: post
title: "[python] 파이썬 reduce"
author: optboy
categories: [Python]
---

lambda, map에 이어 이번에는 reduce에 대해서 알아보겠다. 

## reduce란?
- reduce는 인자로 **함수**와 리스트, 튜플과 같은 **순서형 자료(iterable)**이 들어간다. 
- `reduce(함수, 순서형 자료)`와 같은 모습으로 쓰인다.
- reduce는 인자로 받은 **순서형 자료**의 원소들을 누적적으로 함수에 적용시킨다.

## reduce 사용법 
- `import functools`를 해줘야한다. `functools.reduce(함수, 순서형자료)`로 쓸 수 있다.
- 함수 인자 부분에는 람다가 들어갈 수도 있고, 함수가 들어갈 수도 있다. 
- reduce는 하나의 값을 리턴한다.

    ```python
    import functools

    li = [1,2,3,4,5]

    functools.reduce(lambda x,y:x+y, li)
    # 15
    ```

## reduce없이 구현한다면?  

```python
li = [1,2,3,4,5]

result = 0

for i in li:
    result += i

result
# 15
```

#### 참고
- [왕초보를 위한 Python - 3.5](https://wikidocs.net/64)