---
layout: post
title: "parameter와 argument의 차이"
author: optboy
categories: [Programming]
---

프로그래밍을 하다보면 parameter(매개변수)와 argument(전달인자)라는 용어를 자주 접할 수 있다. 이 두 용어는 거의 구분없이 사용되는 경우가 많다. 어디에선 parameter로 불리던 것이 어디에선 argument로 불리곤 한다. 오늘은 이 두 용어의 정학한 차이에 대해 알아보겠다.

## Parameter(매개변수)와 Argument
- 아래 코드에서 `a`,`b`는 `plus` 함수의 parameter(매개변수)다.  
  
- 아래 코드에서 `1`,`2`는 `plus` 함수의 argument(전달인자)다.
  
    ```python
    def plus(a,b)
        return a+b

    plus(1,2)
    # 3
    ```

## Parameter(매개변수)
- 프로그래밍에서, parameter은 **변수**의 한 종류로, 함수 등의 인풋으로 사용되는 변수를 말한다.  
  
- 짧게 말해, parameter은 **변수(variable)**다.
  
## Argument(전달인자)
- Argument는 함수를 호출할 때 전달되는 실제 값을 의미한다.  
  
- 짧게 말해, argument는 **값(value)**다.

#### 참고
- [위키피디아](https://ko.wikipedia.org/wiki/%EB%A7%A4%EA%B0%9C%EB%B3%80%EC%88%98_(%EC%BB%B4%ED%93%A8%ED%84%B0_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)#%EB%A7%A4%EA%B0%9C%EB%B3%80%EC%88%98%EC%99%80_%EC%A0%84%EB%8B%AC%EC%9D%B8%EC%9E%90)
- [초보몽키의 개발공부로그](https://wayhome25.github.io/etc/2017/12/31/parameter-argument/)
  
    
