---
layout: post
title: "[python] 정규표현식 사용하기"
author: optboy
categories: [Python]
---

저번 글에서는 [메타문자]({% post_url 2020-03-16-python_standard_expression %})에 대해서 알아보았다. 이번에는 파이썬 상에서 메타문자를 이용해서 정규표현식을 사용하는 방법에 대해 알아보겠다.  
이번 글에서도 저번 글에 이어 [점프 투 파이썬](https://wikidocs.net/4308)을 참고하며 공부했다.

## 파이썬 정규표현식 사용 방법

### 모듈 불러오기 `import re`
- 파이썬은 `re`모듈을 통해 정규표현식을 지원한다. 따라서 정규표현식을 사용하기 위해서는 다음과 같이 `import re`해주어야 한다.

    ```python
    import re

    p = re.compile('ab*')
    ```
- `re.compile`을 이용해 컴파일된 **패턴 객체**를 `p`라는 변수에 담아 여러가지 방법으로 정규표현식을 이용할 수 있다.

### 문자열 검색
- 앞서 컴파일된 객체를 활용하여 문자열 검색을 할 수 있는데, 객체는 다음과 같은 메소드를 제공한다.  
  
    1. `match()` : 문자열의 처음부터 정규식과 매치되는지 조사한다.  
      
    2. `search()` : 문자열 전체를 검색하여 정규식과 매치되는지 조사한다.  
      
    3. `findall()` : 정규식과 매치되는 모든 문자열을 리스트로 리턴한다.  
      
    4. `finditer()` : 정규식과 매치되는 모든 문자열을 반복 가능한 객체로 리턴한다.

### 문자열 검색 예제
앞서 소개한 문자열 검색 메소드에 대한 예제를 살펴보자.  
가장 먼저, 패턴 객체를 하나 만들어야 한다.  
```python
import re

p = re.compile('[a-z]+')
```
이번에 만든 객체는 모든 문자에 대해서 1번 이상 반복되는 문자열을 의미한다.
#### match()
- `match`는 문자열의 처음부터 정규식과 매치되는 지 조사한다.  
  
    ```python
    m = p.match('python')

    print(m)
    # <_sre.SRE_Match object; span=(0, 6), match='python'>
    ```

- 만약 처음부터 정규식과 매치되지 않는다면 `None`을 반환한다.  
  
    ```python
    m = p.match('3 python')

    print(m)
    # None
    ```

- 실제 코드에서 `match`메소드는 다음과 같은 방법으로 쓰인다고 한다.  
  
    ```python
    p = re.compile('[a-z]+')

    m = p.match('python')

    if m:
        print(m.group())
    else:
        print('No match')
    ```

- 코드에 나오는 `m.group`은 조금 있다 설명하겠다.  

#### search()
- `search`는 문자열 전체를 검색하여 정규식과 매치되는지 조사한다.  
  
    ```python
    m = p.search('python')

    print(m)
    # <_sre.SRE_Match object; span=(0, 6), match='python'>
    ```

- `search`는 전체 문자열에서 검색하기 때문에 `match`와 다르게, 처음에 매치되지 않는 문자가 있더라도 매치가 된다.  
  
     ```python
    m = p.search('3 python')

    print(m)
    # <_sre.SRE_Match object; span=(2, 8), match='python'>
    ```

- 하지만 `search` 경우에도, 아무 문자도 매치되지 않은 경우에는 `None`을 반환한다.

#### findall()
- `findall`은 정규식과 매치되는 모든 문자열을 리스트로 반환한다.  
  
    ```python
    result = p.findall('life is too short')

    print(result)
    # ['life', 'is', 'too', 'short']
    ```

#### [finditer()]
- `finditer`은 `findall`과 기능적으로는 같지만, 리턴값이 리스트가 아닌 반복 가능한 객체이다.  
  
    ```python
    result = p.finditer('life is too short')

    print(result)
    # <callable_iterator object at 0x11a3a0f28>

    for i in result:
        print(r)
    # <_sre.SRE_Match object; span=(0, 4), match='life'>
    # <_sre.SRE_Match object; span=(5, 7), match='is'>
    # <_sre.SRE_Match object; span=(8, 11), match='too'>
    # <_sre.SRE_Match object; span=(12, 17), match='short'>
    ```

### match 객체의 메소드  
- 앞서 `match()`와 `search()`메소드의 결과값으로 얻은 `match`객체는 다음과 같은 메소드를 가진다.  
  
    1. `group()`: 매치된 문자열을 리턴한다.  
      
    2. `start()`: 매치된 문자열의 시작 위치를 리턴한다.  
      
    3. `end()`: 매치된 문자열의 끝 위치를 리턴한다.  
      
    4. `span()`: 매치된 문자열의 (시작,끝)에 해당되는 튜플을 리턴한다.  
  
- 예시  
  
    ```python
    m = p.match('python')

    print(m.group())
    # python
    
    print(m.start())
    # 0

    print(m.end())
    # 6

    print(m.span())
    # (0,6)
    ```

## 컴파일없이 문자열 검색하기
- 패턴 객체를 여러번 사용해야 한다면 패턴 객체를 만들어놓고 여러번 사용하는 것이 편하다. 하지만 한번만 쓰는 경우라면, 컴파일과 문자열 검색을 동시에 하는 것이 편할 것이다.
  
- 다음과 같이 `re` 모듈에서 직접 `match`, `search`등의 메소드를 사용하면 된다.  
  
    ```python
    m = re.match('[a-z]+', 'python')
    ```  
  
  
  
이번에는 파이썬 정규표현식 사용 방법에 대해서 알아보았다. 다음에는 컴파일 옵션에 대해 알아보겠다.
    
#### 참고
- [점프 투 파이썬 7-2](https://wikidocs.net/4308)