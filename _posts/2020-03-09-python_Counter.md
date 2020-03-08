---
layout: post
title: "[python] Counter"
author: optboy
---

이번에는 리스트 요소의 개수를 셀 때 유용한 collections패키지의 Counter에 대해서 공부해보았다.
물론 딕셔너리를 이용해서 개수를 세는 함수를 직접 만들 수도 있다. 하지만 Counter 클래스는 여러가지 유용한 기능을 제공하며 코드도 간결하게 만들 수 있기에 익혀두기로 했다.

## Dictionary를 이용하여 Counter 구현
```python
def count(li):
    count_dic = {e:0 for e in set(li)}

    for element in li:
        count_dic[element] += 1
        
    return count_dic     

test_l = ['a', 'b', 'c', 'a']
count(test_l)

# {'c': 1, 'b': 1, 'a': 2}
```

## Counter 사용
```python
import collections

test_l = ['a', 'b', 'c', 'a']
collections.Counter(test_l)

# Counter({'a': 2, 'b': 1, 'c': 1})
```

## Counter 사용법
- Counter은 파이썬의 기본 모듈인 `collections`의 클래스이다. 따라서 파이썬만 정상적으로 설치되어 있다면 `collections`를 import하여 사용이 가능하다.  

## Counter의 기능
- 기본적으로 Counter는 파이썬 딕셔너리의 확장이기 때문에 딕셔너리의 모든 기능을 사용할 수 있다.

- **most_common()** :  
  
    - 데이터의 개수가 많은 순으로 정렬된 배열을 리턴한다.  
      
    - 인자로 정수 `k`를 넣으면 상위 `k`개 만큼만 배열에 넣어 리턴한다.  
  
        ```python
        test_l = ['a', 'b', 'c', 'a']

        test_counter = collections.Counter(test_l)

        test_counter.most_common()
        # [('a', 2), ('b', 1), ('c', 1)]

        test_counter.most_common(1)
        # [('a', 2)]
        ```

- **subtract** :  
  
    - 카운터끼리 뺄셈 연산을 한다. 같은 요소의 데이터 갯수를 빼는 것인데, 이때 `-`을 이용해서 연산을 했다면 연산 이후 양수값을 가진 요소들만을 가지며, `subtract()` 메소드를 이용한다면 0, 음수값을 가지는 요소를 포함한다.  

        ```python
        import collections

        name_l1 = ['Lee', 'Park', 'Lee']
        name_l2 = ['Lee', 'Park', 'Choi']

        counter_1 = collections.Counter(name_l1)
        counter_2 = collections.Counter(name_l2)

        subtract_test = counter_1 - counter_2
        # Counter({'Lee': 1})

        counter_1.subtract(counter_2)
        # counter_1 = Counter({'Lee': 1, 'Park': 0, 'Choi': -1})
        ```
     
- **기본연산** :

    - 카운터끼리의 기본적인 연산이 가능하다.  
  
        ```python
        c = Counter(a=3, b=1)
        d = Counter(a=1, b=2)

        c + d                       # add two counters together:  c[x] + d[x]
        # Counter({'a': 4, 'b': 3})

        c - d                       # subtract (keeping only positive counts)
        # Counter({'a': 2})
        
        c & d                       # intersection:  min(c[x], d[x])
        # Counter({'a': 1, 'b': 1})
        
        c | d                       # union:  max(c[x], d[x])
        # Counter({'a': 3, 'b': 2})
        ```

#### 참고
- [Python Document - collections](https://docs.python.org/2/library/collections.html)

