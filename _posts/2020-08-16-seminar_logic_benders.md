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

`여기서 $$element$$는 equality제약, $$cumulative$$는 부등식 제약인 것 같다.`

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








