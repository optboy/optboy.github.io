---
layout: post
title: "Mathematical Optimization - 수리최적화"
author: optboy
categories: [Optimization]
---

내 전공은 최적화다. 최적화 중에서도 **수리최적화**다.  
나는 아직 이 분야에 대해 모르는 것이 너무도 많다. 전공인데도 불구하고 말이다.  
물론 이제 막 석사과정을 시작하긴 했지만, 확실하게 알고 있는 것이 없다는 생각이 자꾸 든다.  
그래서 누군가 나에게 전공을 물어본다면 당당하게 말할 수 있을 때까지 확실하게 공부해보고자 한다.  
  
그래서 이번에는 내가 전공하고 있는 **수리최적화**가 무엇인지부터 정리해보겠다.

## 수리최적화?
- 현실에 존재하는 복잡한 의사결정문제를 수리 모델로 만들고, 그 모델을 통해 최적해를 찾아내는 방법이다.  
  
- 간단히 말해, 의사결정에 쓰이는 도구다.  
  
- 수리 모델을 일반화하면 다음과 같은 식으로 표현된다.  
  
$$
\eqalignno{
    min/max &\ f(x)  \\
    s.t &\ g_i(x) \leq 0, \quad i = 1,...,m \\
    &\ (h_j(x) = 0, \quad j = 1,...,k)\\
    &\ (x \in X \subset R^n)
}
$$  


## 수리모형의 요소
- 수리모형에는 크게 세가지 구성요소가 있다. 다음 예제와 함께 알아보자.

$$
\eqalignno{
    min &\ 12x_1 + 15x_2 + 5x_3 \\
    s.t &\ 2x_1 + 2x_2 + x_3 \leq 8 \\
    &\ x_1 + 4x_2 - 3x_3 \leq 12 \\ 
    &\ x_1,x_2,x_3 \geq 0
}
$$
  
1. **결정변수(Decision Variable)**  
  
    - 문제에서 아직 모르는 것, **알고자 하는 것**이다.  
      
    - 위의 예제에서는 $$x_1$$, $$x_2$$, $$x_3$$가 결정변수다.  
      
    - 예를 들어, 어떤 물건을 얼마나 생산해야 하는 지 알고자 한다면, 그것이 결정변수가 될 수 있다.  
  
2. **제약식(constraints)**  
  
    - 문제에 존재하는 **제약(조건)**을 식으로 표현한 것이다.  
      
    - 제약은 부등호 혹은 등호로 표현된다. 

    - 위의 예제에서 2번째, 3번째 식이 제약식 역할을 한다.

    - 4번째 식 역시 제약식이다. 하지만 조금 특별한 제약식이다. non-negativity 제약, 비음제약이라고 불린다.
  
3. **목적함수(Objective function)**  
  
    - **최적화하고자 하는 것**이다. 최소화(Minimize) 혹은 최대화(Maximize)할 수 있다. 

    - 일정 계수를 곱한 변수들의 합으로 표현된다.  

    - 위의 예제에서 첫번째 식이 목적함수 역할을 한다.
  
    - 예를 들어, 목적함수가 비용으로 정의되었다면 최소화, 이익이라면 최대화시키는 것이다.  
  
## 수리모형의 종류
추후 업데이트 예정..
  
### 참고
- [JunFan님의 네이버블로그](https://m.blog.naver.com/PostView.nhn?blogId=seedkjb&logNo=140019480924&proxyReferer=https%3A%2F%2Fwww.google.com%2F)
- [Linear Programming Terminology](http://www.me.utexas.edu/~jensen/or_site/models/unit/lp_model/lp_terms/lp_terms.html)