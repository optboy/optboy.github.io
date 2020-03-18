---
layout: post
title: "[python] 정규표현식 컴파일 옵션"
author: optboy
categories: [Python]
---

이번에는 정규식을 컴파일할 때 사용할 수 있는 여러가지 옵션에 대해 알아보겠다.  
이번 글에서도 역시 [점프 투 파이썬](https://wikidocs.net/4308)을 참고하며 공부했다. 

## 컴파일 옵션
1. `DOTALL`, `S` : 줄바꿈 문자를 포함하여 모든 문자와 매치할 수 있도록 한다.  
  
2. `IGNORECASE`, `I` : 대소문자에 관계없이 매치할 수 있도록 한다.  
  
3. `MULTILINE`, `M` : 여러 줄과 매치할 수 있도록 한다.  
  
4. `VERBOSE`, `X` : verbose 모드를 사용할 수 있도록 한다. (정규식을 보기 편하게 만들 수 있고, 주석을 사용할 수도 있다.)  

## 컴파일 옵션 사용 방법
- 기본적으로 컴파일 옵션은 다음과 같이 컴파일 당시 인자로 넣어준다.  

    ```python
    import re
    p = re.compile('a.b', re.DOTALL)
    ```

### 줄바꿈 포함 `DOTALL`, `S`
- `.`메타 문자는 줄바꿈 문자를 제외한 모든 문자와 매치된다. 하지만 `re.DOTALL`이나 `re.S` 옵션을 사용한다면 `\n`문자도 포함하여 매치한다.  

- `DOTALL`옵션 없이 `\n`이 포함된 문자열을 매치시키면 매치되지 않는다.  
  
    ```python
    import re
    p = re.compile('a.b')
    m = p.match('a\nb')
    print(m)
    # None
    ```

- 하지만 다음과 같이 `DOTALL` 옵션을 넣으면 `\n`이 포함된 문자열과도 매치가 된다.  
  
    ```python
    p = re.compile('a.b', re.DOTALL)
    m = p.match('a\nb')
    print(m)
    # <_sre.SRE_Match object; span=(0, 3), match='a\nb'>
    ```

### 대소문자 구분 없이 `IGNORECASE`, `I`
- `re.IGNORECASE`와 `re.I`는 대소문자와 관계없이 매치하고자 할 때 쓸 수 있다.  
  
- [a-z]는 소문자만을 의미하지만 `re.I`옵션 덕분에 대문자도 매치된다.  
  
    ```python
    p = re.compile('[a-z]*', re.I)
    print(p.match('python'))
    <_sre.SRE_Match object; span=(0, 6), match='python'>
    print(p.match('Python'))
    <_sre.SRE_Match object; span=(0, 6), match='Python'>
    print(p.match('PYTHON'))
    <_sre.SRE_Match object; span=(0, 6), match='PYTHON'>
    ```

### 여러 줄에 대해서 매치 `MULTILINE`, `M`
- `re.MULTILINE`과 `re.M`옵션은 메타문자 `^`,`$`와 자주 쓰인다.  
  
- `^`,`$`에 대해서는 [정규표현식 메타문자]({% post_url 2020-03-16-python_standard_expression %})설명에 간략히 나와있다.  
  
- 다음 예시에서 정규식 `^python\s\w+`는 문자열이 python으로 시작하고, 공백 하나, 단어 하나가 와야한다는 의미다.  
  
    ```python
    import re 
    p = re.compile('^python\s\w+')

    data = '''python one
    life is too short 
    python two
    you need python
    python three
    '''

    print(p.findall(data))
    # ['python one']
    ```

- 이와 같은 결과가 나오는 이유는 첫번째 라인만 매치가 되었기 때문이다.  
  
- 하지만 `re.MULTILINE` 옵션을 붙이게 되면 각 라인마다 정규식이 인식되게 된다.  
  
    ```python
    import re 
    p = re.compile('^python\s\w+', re.MULTILINE)

    data = '''python one
    life is too short 
    python two
    you need python
    python three
    '''

    print(p.findall(data))
    # ['python one', 'python two', 'python three']
    ```

추후 업데이트 예정.. 


