---
layout: post
title: "CPLEX 설치하기"
author: optboy
---

최적화 문제를 풀기 위한 상용 소프트웨어로는 google OR tools, IBM CPLEX 등이 있다. google OR tools의 경우에는 구글에서 무료로 사용할 수 있도록 오픈해두었기에 누구나 사용이 가능하다. 하지만 CPLEX는 사용하기 위해서는 돈이 꽤 든다.  

**하지만 학생이라면 CPLEX를 무료로 이용할 수 있다.**

## 준비물
- 인증가능한 교육기관 웹메일 

## 설치법
1. [IBM Academic Initiative][1]에 접속한다.  

2. 아래에서 ILOG CPLEX Optimization Studio를 찾는다.

    ![](/assets/img/cplex_download/cplex_page.png){:width="300px"}  

3. `Resister or Login ...` 을 눌러 IBM에 회원가입을 한다.

    ![](/assets/img/cplex_download/institution_submit.png){:width="300px"}  

    이때, 정상적으로 등록된 교육기관의 웹메일이 없을 경우 더이상 설치를 진행하기 어렵다. (google OR tools를 이용하기 바란다.)

4. 회원가입을 하고 이메일 인증까지 완료한다.

    ![](/assets/img/cplex_download/sign_up.png){:width="300px"}

5. 정상적으로 회원가입이 완료되었다면 ILOG CPLEX Optimization Studio에 download가 활성화된다.

    ![](/assets/img/cplex_download/changed_page.png){:width="300px"}

6. 다운로드를 눌러 자신의 OS에 맞는 설치파일을 다운로드해준다.

    ![](/assets/img/cplex_download/download_page.png){:width="500px"}  

    이때 Download Director을 설치해야하는데, Java가 설치되어 있어야 한다.

    ![](/assets/img/cplex_download/download_director_guide.png){:width="500px"}  

7. 다운로드한 파일의 압축을 풀고 CPLEX를 설치해준다.  

    ![](/assets/img/cplex_download/cplex_install.png){:width="300px"}

## python 모듈로 cplex를 사용하기
1. CPLEX가 설치된 경로로 이동한다.
    ```bash
    $ cd /Applications/CPLEX_Studio1210/cplex/python/3.7/x86-64_osx
    ```

2. 설치하고자하는 가상환경에서 cplex를 설치해준다.
    ```bash
    $ conda activate [가상환경 이름]
    $ python setup.py install
    ```

3. 설치가 잘 되었는지 확인한다.
    ```bash
    $ python
    >> import cplex
    ```
    에러가 안뜬다면 정상적으로 설치된 것이다.





[1]: https://my15.digitalexperience.ibm.com/b73a5759-c6a6-4033-ab6b-d9d4f9a6d65b/dxsites/151914d1-03d2-48fe-97d9-d21166848e65/technology/data-science