---
layout: post
title: "iTerm2 한글 깨짐 해결하기"
author: optboy
categories: [Programming]
---

MAC에서 멋진 터미널을 쓰고자 iTerm을 쓰시는 분들이 많을거라 생각한다.  

그런데 다음과 같이 한글 깨짐 현상이 일어나는 경우가 있는데, 해결방법은 생각보다 간단하다.  

![](/assets/img/iterm/error.png){:width="200px"}  

## 해결방법

1. iTerm을 실행하고, preferences > Profiles로 간다.

2. Text > Unicode normalization form을 NFC로 바꿔준다.

    ![](/assets/img/iterm/img1.png){:width="500px"}  

3. 다음과 같이 해결된 것을 볼 수 있다.

    ![](/assets/img/iterm/fixed.png){:width="200px"}  