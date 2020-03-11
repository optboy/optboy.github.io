---
layout: post
title: "Github 잔디가 안심어지는 현상 고치기"
author: optboy
categories: [Github]
---

1일 1커밋을 진행하고 있는 사람들에게 가장 민감한 것이 깃헙 잔디다. 하지만 어떤 경우 commit을 했는데도 잔디가 안심어지는 경우가 있다. 실제로 며칠 전 그런 현상을 겪고 정말 당황스러웠다. 하지만 검색해보니 아주 간단한 문제였다.

## 잔디가 안심어지는 이유    
- 로컬에서 git push하는 email과 github에 등록된 email이 다르기 때문이다.

## 해결법
1. 작업중인 git 폴더에서 local에 등록된 email을 확인한다.
    ```bash
    $ git config --list
    ```  

    위 명령어를 통해 email을 확인한다.

    ![](/assets/img/github_commit_error/config_list.png){:width="500px"}  

2. 깃헙에 등록된 email을 확인한다.  

    - 깃헙에 로그인 하고 setting에 들어간다.  

        ![](/assets/img/github_commit_error/setting.png){:width="200px"}  

    - setting에서 email로 들어가서 확인해준다.  

        ![](/assets/img/github_commit_error/email.png){:width="500px"}  

3. 만약 리스트의 이메일이 깃헙의 이메일과 다르다면, 아래 명령어를 통해 github 이메일과 같이 바꿔준다.  

    ```bash
    $ git config user.email "[github 이메일]"
    ```
    이때 모든 github 프로젝트에 대해서 이메일을 설정해주려면 git 다음에 `--global`을 붙여준다. 
    
#### 참고  
- [https://devkyu.tistory.com/872][1]
- [https://diordna.tistory.com/37][2]

[1]: https://devkyu.tistory.com/872
[2]: https://diordna.tistory.com/37
