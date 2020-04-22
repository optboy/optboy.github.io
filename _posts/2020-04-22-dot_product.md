---
layout: post
title: "[선형대수] 점 곱 - dot product"
author: optboy
categories: [Linear algebra]
---

이번에는 dot product에 대해서 알아보자.  

## dot product(scalar product)란?

dot product는 두 벡터를 곱해서 하나의 스칼라값이 나오도록 하는 연산이다.

$$v_1 = (x_1, y_1), v_2 = (x_2, y_2)$$를 서로 다른 벡터라고 했을 때, 다음과 같다.

$$v_1 \cdot v_2 = x_1 \cdot x_2 + y_1 \cdot y_2$$

## dot product와 norm

벡터 $$v$$에 대해 자기 자신을 dot product하면 다음과 같다.  

$$v \cdot v = v_1 \cdot v_1 + v_2 \cdot v_2$$  

여기에 루트를 취하게 되면 다음과 같다.

$$
\eqalignno{
    \sqrt{v \cdot v} &= \sqrt{v_1 \cdot v_1 + v_2 \cdot v_2}\\
    &= \lVert v \rVert
}
$$  

즉, norm은 dot product에 루트를 취한 것과 같다.

## dot product의 기본성질

- 교환법칙이 성립한다.  

- 분배법칙이 성립한다. 

- 스칼라배가 가능하다. 

- 제곱하게 되면 0보다 크거나 같다. 

## dot product의 여러가지 성질 

추후 업데이트 예정.