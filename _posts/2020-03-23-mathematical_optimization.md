---
layout: post
title: "Mathematical Optimization - 수리최적화"
author: optboy
categories: [Optimization]
---

아직도 내 전공에 대해서 제대로 아는게 많지 않고, 배웠던 것도 조금만 시간이 지나면 잊어버리기 때문에, 전공관련 내용을 기초부터 차근차근 정리해보기로 했다.  
   
이번에는 나의 전공인 **수리최적화**가 무엇인지부터 알아보겠다.

## 수리최적화?
- 현실에 존재하는 복잡한 의사결정문제를 수리 모델로 만들고, 그 모델을 통해 최적의 답을 찾아내는 방법이다.  
  
- 간단히 말해, 의사결정에 쓰이는 도구다.  

## 수리 모형의 요소
- 수리 모형에는 크게 세가지 구성요소가 있다. 아래의 예시와 함께 알아보자.

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
      
    - 위의 예시에서는 $$x_1$$, $$x_2$$, $$x_3$$가 결정변수다.  
      
    - 예를 들어, 어떤 물건을 얼마나 생산해야 하는 지 알고자 한다면, 그것이 결정변수가 될 수 있다.  
  
2. **제약식(constraints)**  
  
    - 문제에 존재하는 **제약(조건)**을 식으로 표현한 것이다.  
      
    - 제약은 부등호 혹은 등호로 표현된다. 

    - 위 예시에서 2번째, 3번째 식이 제약식 역할을 한다.

    - 4번째 식 역시 제약식이나, non-negativity 제약, 비음제약이라고 불리는 조금 특별한 제약식이다.
  
3. **목적함수(Objective function)**  
  
    - **최적화하고자 하는 것**이다. 최소화(Minimize) 혹은 최대화(Maximize)할 수 있다. 

    - 일정 계수를 곱한 변수들의 합으로 표현된다.  

    - 위의 예제에서 첫번째 식이 목적함수 역할을 한다. 여기선 minimize하는 문제인 것이다.
  
    - 목적함수는 문제의 목적에 맞게 설정될 수 있다. 예를 들어, 비용으로 정의한다면 최소화해야할 것이고, 이익으로 정의한다면 최대화하는 식으로 말이다.
  
## 수리모형의 종류  
  
수리모형은 특성에 따라 여러가지 종류로 구분된다. 여기서는 아주 대표적인 수리모형의 특징만을 간단하게 알아보고, 추후에 좀 더 자세히 다루도록 하겠다. 
  
### Linear Programming(LP) - 선형계획법  
  
- 목적함수가 linear(선형)이고 제약식이 linear inequality 혹은 linear equality인 모델  
  
- 연립방정식을 푸는 것과 유사하다. 차이점으로는 연립방정식은 미지수의 개수가 식의 개수보다 작거나 같지만, 이 경우에는 미지수의 개수가 더 많다.  
  
- Simplex 알고리즘을 이용해서 풀 수 있다. 
  
### Integer Programming(IP) - 정수계획법  
  
- Decision variable(결정변수)이 **정수값**을 갖는다는 조건을 가진 수리 모형이다. 

- 일부 변수에 대해서만 정수 조건을 갖는 경우도 있는데, 이는 **Mixed Integer Programming(MIP)**라고 불린다.

- LP에 비해서 문제 난이도가 상당히 높다. 

### Non-linear Programming(NLP) - 비선형계획법  
  
- 목적함수나 제약식이 선형함수가 아닌 경우다.  
  
- 특히 함수가 non-convex인 경우 문제를 풀기가 굉장히 까다롭다.

### Constraint Programming(CP)  
  
- 최적을 찾기보다는, 많은 조합에 대해서 feasible한 해답을 찾는데 사용된다.  
  
- 목적함수보다는 제약식과 Decision variable에 초점을 둔다. 실제로, 목적함수가 없을 수도 있다. 


### 참고
- [JunFan님의 네이버블로그](https://m.blog.naver.com/PostView.nhn?blogId=seedkjb&logNo=140019480924&proxyReferer=https%3A%2F%2Fwww.google.com%2F)
- [Linear Programming Terminology](http://www.me.utexas.edu/~jensen/or_site/models/unit/lp_model/lp_terms/lp_terms.html)
- [wikipedia](https://en.wikipedia.org/wiki/Linear_programming)
- [chocoberry님의 블로그](https://chocoberry12.github.io/Study/%EC%88%98%EB%A6%AC%EA%B3%84%ED%9A%8D%EB%B2%95/)