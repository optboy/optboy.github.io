---
layout: post
title: "[python] 파이썬 map"
author: optboy
categories: [Python]
---

앞선 포스팅에서는 `lambda`에 대해 알아보면서 람다는 다른 함수들의 인자로 많이 쓰이는 것을 알게 되었다. 그래서 이번에는 파이썬의 `map`에 대해 알아보고자 한다.

## map이란?
- 맵은 인자로 **"함수"**와 **"리스트"**를 받는다. `map(함수, 리스트)`와 같은 모습으로 쓰인다.
- 인자로 받은 리스트의 요소 하나하나를 함수에 적용시켜서 새로운 리스트를 만들어준다. 

## map 사용법
생각보다 간단하다. `map`의 함수 인자 부분에 람다 표현식을 넣어주면 된다. 이때 `map`은 기본적으로 map객체를 반환하기 때문에 list로 다시 바꿔주는 작업이 필요하다.
```python 
li1 = [1,2,3]
li2 = [4,5,6]

list(map(lambda x,y:x+y, li1, li2))
# [5, 7, 9]
```
위 코드에서는 람다에서 받는 인자가 `x`,`y` 두개이기 때문에 `map`의 인자로 두개의 리스트 `li1`,`li2`가 들어갔다.

## map과 lambda를 사용하지 않고 구현한다면??
```python
def plus(a,b):
    return a+b

li1 = [1,2,3]
li2 = [4,5,6]

new_li = []
for (i,j) in zip(li1,li2):
    new_li.append(i+j)

new_li
# [5,7,9]
```
이처럼 코드가 아주 길어지게 된다. 물론 더 짧게 만들 수도 있겠지만 극단적인 예시를 보여주고 싶었다.

#### 참고
- [코딩벌레님의 블로그](https://dpdpwl.tistory.com/86)
- [왕초보를 위한 python](https://wikidocs.net/64)
