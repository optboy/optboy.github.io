---
layout: post
title: "[python] 파이썬 line_profiler"
author: optboy
categories: [Python]
---

어느정도 코딩을 하다보면 어느샌가 알고리즘의 속도가 중요해지는 순간이 온다. 속도를 줄이기 위해서는 어떤 부분이 시간을 오래 잡아먹는지 찾아내고 해당 부분을 개선시켜야 하는데, 이게 쉽지 않을 때가 있다.   

그럴때 도움을 받을 수 있는 것이 프로파일링(profiling)이다. 프로파일링이란 프로그램의 시간 복잡도, 메모리 정보, 함수 호출 주기, 빈도 등을 분석하는 것이며, 파이썬에서는 기본적으로 `cprofile`이나 `profile`과 같은 모듈을 제공하고 있다. 하지만 이번에는 파이썬 기본 모듈은 아니지만 코드를 한줄씩 프로파일링 할 수 있는 `line_profiler`을 소개하고자 한다.

## 설치법  

- 터미널에서 다음 명령어를 통해 간단하게 설치할 수 있다.
    ```bash
    $ pip install line_profiler
    ```

## 사용법

- 프로파일링을 하기 위해서는 다음 예시와 같이 함수 위에 데코레이터 `@profile`을 달아줘야 한다.  
    ```python
    # test.py  
    @profile
    def fib(n) :
    if n == 1 or n == 2 :
    return 1
    return fib(n - 1) + fib(n - 2)
    ```

- 다음으로, 터미널에서 해당 python 파일을 kernprof를 이용해서 돌려준다.  

    ```bash
    $ kernprof -l -v test.py
    ```  
    
- `-l` 옵션은 함수 단위가 아닌, 라인 단위로 프로파일링을 하겠다는 뜻이다.  

- `-v` 옵션은 기본적으로 `line_profiler`은 결과를 파일로 저장하는데, 결과를 터미널에서 바로 보겠다는 뜻이다.

- 만약 결과를 파일로 저장했다면, 다음과 같이 txt파일로 변환 후 결과를 확인할 수 있다.
  
    ```bash
    $ python -m line_profiler RP.py.lprof > results.txt
    ```

- 실행 결과는 다음과 같다.  

    ```bash
    Wrote profile results to test.py.lprof
    Timer unit: 1e-06 s

    Total time: 0.000116 s
    File: test.py
    Function: fib at line 1

    Line #      Hits         Time  Per Hit   % Time  Line Contents
    ==============================================================
        1                                           @profile
        2                                           def fib(n) :
        3       109         46.0      0.4     39.7   if n == 1 or n == 2 :
        4        55         14.0      0.3     12.1      return 1
        5        54         56.0      1.0     48.3   return fib(n - 1) + fib(n - 2)
    ```

- 위 결과를 보면, 해당 함수가 실행된 총 시간과 라인별 시간 차지 비율을 볼 수 있다.  


