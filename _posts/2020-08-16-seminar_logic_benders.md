---
layout: post
title: "[논문 리뷰] Planning and Scheduling by Logic-Based Benders Decomposition"
author: optboy
categories: [Optimization]
---

이번 세미나에서 발표할 논문은 *Planning and Scheduling by Logic-Based Benders Decomposition*이다. 

이 논문은 2007년에 INFORMS지에 발표되었으며 저자는 카네기 멜론 대학의 J. N. Hooker이다.

## 논문의 주제

논문에서는 생산에서 makespan, tardiness를 최소화하는 planning and scheduling 문제를 다룬다.  

이때 mixed-integer linear programming(MILP), constraint programming(CP)를 사용한다.  

작업을 설비에 할당하는 문제는 MILP로 풀고, 스케줄링 문제는 CP로 푼 다음, 두 문제를 logic-based Benders decomposition로 연결지어 전체 문제를 해결하는 것이 이 논문의 핵심 아이디어다.

## Introduction

생산, 공급망에서 발생하는 스케줄링 문제에서 납기 내에 생산을 완료하도록 작업(Task)들이 설비에 할당이 되어야 한다.  

작업들은 자원 제약을 넘지 않는 선에서 병렬적으로 진행될 수도 있으며, 최종적인 목표는 비용, makespan, tardiness를 최소화 하는 것이다. 

그런데 이런 문제는 굉장히 어려운 문제이기에, 현실에선 대부분 상식적인 방식으로 문제를 푼다.  
중앙 관리자가 작업을 설비에 할당하면, 오퍼레이터가 디테일한 스케줄을 짜는 것이다. 이 과정에서 문제가 있으면 다시 중앙관리자가 작업을 할당하고, 다시 스케줄을 짜는 방식이다. 

그런데 이러한 방식은 시간이 굉장히 오래걸리고, 좋은 스케줄이라는 보장도 없다.  

이러한 방법에 Benders decomposition 기법을 적용하자면, Master 문제에서 설비를 할당하고, subproblem에서 독립적인 스케줄링 문제를 풀 수 있다. Master 문제에 추가되는 benders cut은 오퍼레이터의 피드백과 같은 것이다. 그리고 모든 할당과 스케줄링이 최적일 때 알고리즘을 끝내는 것이다.  

그런데 **이 문제에서 전통적인 benders decomposition(BD)은 적합하지 않다**.  
왜냐하면 전통적인 BD의 subproblem은 continuous한 문제여야 하는데, 스케줄링 문제는 조합 문제이기 때문이다.

하지만 이 논문에서는 BD의 subproblem을 logic-based한 형태로 확장해 스케줄링 문제에 적용하는 방법을 제시한다. 

Logic based BD의 다른 장점으로는 MILP와 CP의 장점을 살릴 수 있다는 것이다. MILP는 할당 문제, CP는 스케줄링 문제를 푸는 방식으로, 각자가 잘 풀 수 있는 문제를 풀게 할 수 있다는 것이다. 이 방법으로 상당히 문제를 빠르게 풀 수 있게 된다.  

게다가 언제든지 알고리즘을 종료하고, feasible solution을 얻을 수 있다는 장점도 있다.  

logic-based BD는 benders cut을 만드는 특정한 기준이 없고, 문제마다 달라질 수 있다. 

## The Problem

일반적인 생산계획 문제는 다음과 같이 정의할 수 있다.  

$$j \in \{1,...,n\}$$ : 작업  
$$i \in \{1,...,m\}$$ : 설비  
$$p_{ij}$$ : 소요시간  
$$c_{ij}$$ : 자원소모량  
$$r_j$$ : release time  
$$d_j$$ : deadline  
$$s_j$$ : start time  
$$C_i$$ : 최대 자원
$$J_{it}$$ : $$t$$시간에 $$i$$설비에서 작업하는 작업 $$j$$ 집합

![](/assets/img/logic_BD/1.png){:width="500px"}  

여기에 추가적인 제약을 넣을 수도 있다.  
예를 들어, 어떤 작업들은 같은 설비에 할당되어야 한다거나 어떤 작업은 어떤 작업보다 먼저 완료되어야 한다거나 하는 제약을 넣을 수 있다. 

그리고 이 논문에서는 다음과 같이 세가지 목적함수를 제안한다. 

![](/assets/img/logic_BD/obj.png){:width="500px"} 

## Constraint Programming Formulation

위와 같은 문제를 CP로도 만들 수 있는데, 여기서는 global constraints $$element$$와 $$cumulative$$가 사용된다. 

여기서 $$element$$는 equality제약, $$cumulative$$는 부등식 제약인 것 같다.

![](/assets/img/logic_BD/4.png){:width="500px"}

여기서 1,2번째 제약식은 시간과 관련된 제약이며 3번째 제약은 자원제약이다. 

## Mixed-Inter Programming Formulation

이를 MILP로 표현하면 다음과 같다.  

$$x_{ijt}$$ : $$j$$작업을 $$t$$시간에 $$i$$설비에서 작업한다면 1 아니면 0인 변수  

### minimum-cost formulation

![](/assets/img/logic_BD/5.png){:width="500px"}

(a) 제약은 각 작업이 한번은 해야한다는 제약이며, (b) 제약은 자원 제약, (c)는 time window 제약이다.  

### minimum-makespan formulation

![](/assets/img/logic_BD/6.png){:width="500px"}

### minimum total tardiness formulation

![](/assets/img/logic_BD/7.png){:width="500px"}

위 포뮬레이션들은 time-indexed한 변수들이기 때문에 확장이 가능하다.  

이산적인 이벤트를 가지고 연속된 시간을 사용하는 모델을 살펴보자.
$$n$$개의 작업이 있다면 $$2n$$개의 이벤트가 존재하는 것이다. 

모델은 각 이벤트에 대해서 각 작업이 끝나는 이벤트인지, 시작하는 이벤트인지 결정한다.
$$x_{ijk}$$ : 이벤트 $$k$$는 $$j$$작업이 $$i$$설비에서 시작하면 1아니면 0
$$y_{ijk}$$ : 이벤트 $$k$$는 $$j$$작업이 $$i$$설비에서 끝나면 1아니면 0
$$s_{ik}$$ : 이벤트 $$k$$가 설비$$i$$에서 시작하는 시간
$$f_{ij}$$ : 작업$$j$$가 설비$$i$$에 할당된 경우, 작업$$j$$가 설비$$i$$에서 끝나는 시간
$$R_{ik}$$ : 설비$$i$$에서 이벤트$$k$$가 발생할 때 작업들의 자원 총 사용량
$$R^s_{ik}$$
시작시간과 종료시간에 대한 변수를 나눴기 때문에 자원제약을 만들 수 있다. 

![](/assets/img/logic_BD/minimum_cost.png){:width="500px"}

(a)~(c)제약은 각 작업이 설비에 할당되고, 시작과 종료가 한번씩 이뤄져야 하는 것을 의미한다.  
(d)제약은 이벤트 1~2n이 순서대로 발생하도록 한다.
(e)제약은 time window 제약이다.  
(f),(g)제약은 종료 시간에 대한 변수를 정의한다.  
(h)~(j)제약은 자원제약이다.

다음과 같이 포뮬레이션을 만들어주면, 문제는 훨씬 더 어려워진다. 

## Logic-Based Benders Decomposition

$$C(x,y)$$가 변수 $$x, y$$를 가지는 제약이고, $$D_x, D_y$$가 $$x, y$$의 정의역(domain)이라고 할 때 다음과 같은 formulation에 Logic-based BD를 적용할 수 있다.  

![](/assets/img/logic_BD/8.png){:width="500px"}

여기서 $$x$$를 $$\bar{x}$$로 고정시키면 다음과 같은 subproblem을 얻을 수 있다. 

![](/assets/img/logic_BD/9.png){:width="500px"}

(9)번의 *inference dual*은 제약 $C(\bar{x}, y)$$을 만족하는 f(\bar{x}, y)에 대한 가장 타이트한 lower bound를 추정하는(infer) 문제다. 

![](/assets/img/logic_BD/10.png){:width="500px"}  

여기서 $$A \Longrightarrow^P B$$의 의미는 증명 $$P$$가 $$A$$에서 $$B$$를 추론한다는 뜻이다.  
그리고 $$\mathscr{P}$$는 증명들의 집합이다.  

만약 (9)가 선형 문제라면 그 *inference dual* 역시 선형 듀얼이 되고, $$\mathscr{P}$$에 속하는 증명들은 제약들에 있는 비음 선형 조합들에 해당한다. 

이 듀얼의 솔루션은 $$x = \bar{x}$$일 때 $$f(x,y)$$에 대한 가장 타이트한 bound라고 볼 수 있다.  

기본적으로 Benders Decomposition의 개념은, 다른 $$x$$값에 대한 바운드 $$B_\bar{x}(x)$$를 만드는데 이러한 proof schema를 사용한다. 

classical BD에서는 같은 선형조합이 사용되었다. 

일반적으로 bounding function $$B_\bar{x}(x)$$는 두개의 특성(property)을 가져야 한다.

![](/assets/img/logic_BD/property.png){:width="500px"}  

만약 (8)의 목적함수값이 $$z$$이고 $$z \geq B_\bar{x}(x)$$가 **Benders cut**이다. 

그러한 benders cut들을 넣은 마스터 문제를 여러번 반복해서 푸는데, 다음과 같은 식으로 표현될 수 있다.  
여기서 $$H$$는 반복횟수다. 

![](/assets/img/logic_BD/11.png){:width="500px"}

여기서 $$x^1,...,x^{H-1}$$은 이전의 $$H-1$$번의 마스터 문제를 통해 나온 해다.  
그렇다면 (11)의 $$\bar{x}$$는 다음 서브문제 (9)번에서 정해지게 된다.  

그렇다면 알고리즘은 언제 끝나는가?  
이전 $$H-1$$번의 서브문제에서 나온 optimal value들인 $$v^*_1, ..., v^*_{H-1}$$중 최소값인 v^*와 마스터 문제의 optimal value인 $$z^*_H$$가 같아질 때 끝난다. 

$$z^*_H$$는 최적해의 lower bound, $$v^*$$는 최적해의 upper bound이기 때문이다.

![](/assets/img/logic_BD/theorem.png){:width="500px"}

다시 (1)번의 생산 스케줄링 문제로 돌아오면, 변수 $$x,s$$는 각각 (8)번의 $$x,y$$에 부합하고 어떤 작업 $$\bar{x}$$를 설비에 할당하면 다음과 같은 서브문제가 만들어진다. 

![](/assets/img/logic_BD/12.png){:width="500px"}

즉, 각 설비 $$i$$에 대한 스케줄링 문제가 되고, 이를 CP solver로 풀어 Benders cut을 만들 수 있다.  
그렇게 만들어진 benders cut은 master문제의 제약이 되는 것이다. 

bounding function $$B_\bar{x}(x)$$는 $$x=\bar{x}$$에 대한 bound의 추론의 유형?(type of reasoning)을 통해 얻어지고 이 추론을 일반적인 $$x$$를 얻는것으로 확장한다.

## Minimizing Cost

cost의 경우 master문제의 변수로만으로도 목적함수 계산이 가능하기 때문에 가장 간단하다.  

(12)번 sub문제는 feasible할 때 $$\sum_j F_{x,j}$$값을 갖고, infeasible일 때 $$\infty$$를 갖는다.  

$$J_{hi} = \{j|x^j_j=i\}$$를 iteration $$h$$에서 설비 $$i$$에 할당된 작업들에 대한 집합이라고 하자.  

이때 설비 $$i$$에 대해서 feasible한 스케쥴이 없다면 가장 명확한 benders cut은 설비 $$i$$에 대해서 이 집합 $$J_{hi}$$를 할당하는 경우를 제외시키는 것이다.  

이 경우, bounding function은 다음과 같은 형태를 갖는다.  

![](/assets/img/logic_BD/13.png){:width="500px"}  

$$B_{x^h}$$는 cost function인 $$\sum_j F_{x_jj}$$와 같기 때문에 $$B1$$ property를 만족한다.  
$$B_{x^h}(x^h)$$가 서브문제의 optimal이기 때문에 $$B2$$역시 만족한다.