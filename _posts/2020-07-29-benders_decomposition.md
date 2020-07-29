---
layout: post
title: "The Benders decomposition algorithm"
author: optboy
categories: [Optimization]
---

이번에는 까다로운 최적화 문제에 사용되는 기법인 Benders decomposition 방법에 대해 알아보겠다.

# Benders decomposition(BD)

BD는 benders가 1962년에 제안한 알고리즘으로, 사이즈가 큰 최적화 문제를 쉽게 풀기 위한 것이다.
이 방법은 문제의 구조를 잘 활용하여 전체적인 계산량을 분산시켜 exact하게 문제를 푸는데 주로 사용된다.

그러기 위해서 BD는 원래 문제를 Master Problem(MP)와 Sub Problem(SP) 두가지로 나눠서 푼다.  

## Example
예시를 통해 설명하자면, 이러한 문제가 있다고 하자.  

$$
\eqalignno{
    max \quad & 1.01x_1 + 1.02x_2 + ... + 1.1x_{10} + 1.045y\\
    st. \quad & x_1 + x_2 + ... + x_{10} + y \leq 1000 \\
    & x_1 \leq 100 \\
    & x_2 \leq 100 \\
    & ... \\
    & x_{10} \leq 100 \\
    & y \in \mathbb{Z} \\
    & x_1, x_2, ..., x_{10}, y \geq 0 
}
$$

이를 일반화하면 다음과 같은 식으로 표현할 수 있다.  

$$
\eqalignno{
    max \quad & c^Tx + f^Ty \\
    st. \quad & Ax + By \leq b \\
    \quad & y \in Y \\
    & x \geq 0 \\
}
$$

- $$c$$: 변수 $$x$$의 계수에 대한 벡터  
- $$x$$: 변수 $$x$$에 대한 벡터  
- $$f$$: 변수 $$y$$의 계수 스칼라
- $$y$$: 변수 $$y$$에 대한 스칼라
- $$Y$$: 양의 정수 집합
- $$A$$: 제약식에서의 변수 $$x$$의 계수 매트릭스
- $$B$$: 제약식에서 $$y$$의 계수 벡터
- $$b$$: 제약식의 RHS 벡터

### steps
BD의 단계는 다음과 같은데, 이를 통해 위 문제를 풀어보자.

- Initialize $$y^*$$, $$UB = +\infty$$, $$LB = -\infty$$
- while $$UB - LB > \epsilon$$
    - solve the dual of SP, $$u^*$$
    - If $$u^*$$ is unbounded
        - Add cut $$[b - By]^Tu^* \geq 0$$
    - else
        - LB $$:= max\{LB, f^Ty^* + [b - By^{*}]^Tu^{*} \}$$
        - Add cut $$z \leq f^Ty + [b - By]^Tu^*$$
    - End if
    - Solve MP $$max_y\{z \mid cuts, y \in Y\}$$
    - UB := $$z^*$$
- End While

먼저 BD를 시작하면서, master problem의 해를 초기화해줘야 한다. 여기서 $$y^*$$이 그것이다.  
위 문제의 master problem(MP)은 다음과 같다.  

$$
\eqalignno{
    MP & \\
    max \quad & z\\
    st. \quad & y \in Y \\
}
$$

새로운 변수 z를 최대화 하고, y는 양의 정수여야 한다는 제약식이 포함된 모델이다.  
따라서 현재 MP를 풀면, y는 어떤 양의 정수든 될 수 있고, z는 무한하게 증가할 수 있게 된다.  
여기서 우리는 $$y^*$$를 1500이라고 하자.

그리고 BD를 시작하면서 UB와 LB역시 초기화해줘야 하는데, 이때 각각을 양의 무한대, 음의 무한대로 초기화한다. 

초기화가 끝나면, iteration을 시작하는데, UB-LB가 $$\epsilon$$보다 작지 않다면, 계속해서 반복해준다.  
반복문 안에서는, 먼저 subproblem을 풀어서 optimal dual solution $$u^*$$을 구해준다.  

이때 subproblem은 원래 문제의 변수 $$y$$에 MP에서 구한 해 $$y^*$$를 대입하여 아래와 같이 만들어 줄 수 있다.

$$
\eqalignno{
    SP & \\
    max \quad & c^Tx\\
    st. \quad & Ax \leq b - By^* \\
    & x \geq 0 \\
}
$$

그리고 다음과 같이 위 SP의 dual을 구할 수 있다.

$$
\eqalignno{
    SP(dual) & \\
    min \quad & [b-By^*]^Tu\\
    st. \quad & A^Tu \leq c \\
    & u \geq 0 \\
}
$$

해당 dual 문제를 풀어서 $$u^*$$를 구할 수 있는 것이다.

다시 예시로 돌아와서, $$u^*$$를 구해보자.  
먼저 $$y^* = 1500$$이기 때문에, SP의 dual은 아래와 같이 만들어진다. 

$$
\eqalignno{
    min \quad & -500u_1 + 100u_2 + ... + 100u_{11}\\
    st. \quad & u_1 + u_2 \geq 1.01 \\
    & u_1 + u_3 \geq 1.02 \\
    & ... \\
    & u_1 + u_{10} \geq 1.1 \\
    & u_1 \geq 1.045 \\
    & u_1, ..., u_{11} \geq 0
}
$$

이 경우에 목적식을 보면, $$u_1$$이 $$\infty$$이고 나머지 $$u_2, ..., u_{11}$$이 0이라면 목적값은 $$-\infty$$이 되는 것을 알 수 있다.  
즉, 현재 dual solution, $$u^*$$는 unbounded임을 알 수 있다.  

dual이 unbounded일 경우 primal은 infeasible이기 때문에, $$[b - By]^Tu^* \geq 0$$를 만족하도록 cut을 추가해준다.  
이 경우에는, 제약식으로 $$1000 - y \geq 0$$을 추가해주면 된다. 그러면 $$u_1$$의 계수가 0보다 작아질 수 없고, 목적값이 음수가 될 수 없게 된다.  
즉, 솔루션이 더 이상 unbounded가 되지 않게 된다.

이제 MP에 $$1000-y \geq 0$$이라는 제약식이 추가되었고, 이를 다시 풀어준다.   

$$
\eqalignno{
    MP & \\
    max \quad & z\\
    st. & \quad 1000 - y \geq 0 \\
    & y \in Y \\
}
$$

그렇다면, $$y^* = 1000, z^* = +\infty$$라는 해를 구할 수 있게 된다.  
그리고 그렇게 구한 $$z^*$$를 $$UB$$로 설정해준다. 이 경우에는 양의 무한대로, 변하지 않는다. 

그렇기 때문에 여전히 $$UB - LB$$가 양의 무한대이기 때문에 반복문 안으로 다시 들어가서, $$u^*$$를 구해준다.  
이제 $$y^*$$이 1000이기 때문에 솔루션이 unbounded이 아니며, 우리는 $$u^*$$를 구할 수 있다.  

여기서, 만약 dual이 optimal solution을 갖는다면, dual과 primal의 optimal objective value는 같다는, **Strong Duality**를 이용해서 LB를 설정해준다.  
즉, optimal에서 primal 문제의 $$c^Tx^*$$는 결국 dual의 $$[b-By^*]^Tu^*$$와 같아지는데,  
이를 이용하면 원 문제의 목적식 $$c^Tx^* + f^Ty^*$$는 $$f^Ty^* + [b-By^*]^Tu^*$$로 표현할 수 있고, 이는 앞서 구한 솔루션을 토대로 만들어낼 수 있게 된다.  
현재까지의 $$f^Ty^* + [b-By^*]^Tu^*$$은 1045인데, 이를 Lower bound로 정해줄 수 있고, 동시에 dual solution $$u^*$$를 이용해서 새로운 cut을 만들 수 있다.  
목적식이 LB보다 작도록 하는 cut $$z \leq f^Ty + [b-By]^Tu^*$$에 dual solution $$u^*$$를 대입하면, $$z \leq 1100-0.055y$$라는 식을 얻을 수 있다.  

이제 MP에는 두가지 cut이 들어가서, 다음과 같은 식이 된다.  

$$
\eqalignno{
    MP & \\
    max \quad & z\\
    st. & \quad 1000 - y \geq 0 \\
    & z \leq 1100 - 0.055y \\
    & y \in Y \\
}
$$

이 MP를 이용해 다시 UB를 구해주고, 위에서 했던 과정을 반복해준다.  
결국에는 UB-LB가 $$\epsilon$$보다 작아지는 시점이 오게 되고, 해당 시점에서의 솔루션이 최종 솔루션이 되는 것이다. 

#### 참고
- [Benders Decomposition: An Easy Example](https://www.youtube.com/watch?v=vQzpydNOWDY)