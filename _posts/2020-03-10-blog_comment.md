---
layout: post
title: "Jekyll 블로그 댓글 기능 추가하기"
author: optboy
categories: [Jekyll]
---

다른 사람들의 깃헙 블로그를 보면서 테마에 댓글 기능이 있는걸 보면서 부러워했다. 그런데 검색해보니 댓글 기능은 기본적으로 없고, 추가해야만 하는 것이었다. 그래서 나도 해보기로 했다.

## 댓글 기능 추가하는 법
1. **disque** 계정 생성하기  
    - [disque 홈페이지][disque]에서 `Get Started`를 눌러 계정을 생성한다.  

        ![](/assets/img/blog_comment/disque_homepage.png){:width="500px"}  

    - 간단하게 구글 계정을 연동해서 가입했다.

2. 가입하면 뜨는 페이지에서 `I want to install Disque on my site`를 눌러준다.

    ![](/assets/img/blog_comment/disque_select.png){:width="200px"} 

3. 필요한 정보들을 입력하고 `Create Site`해준다.  
  
    - Website Name : 자신의 블로그 이름 ex) optboy

        ![](/assets/img/blog_comment/disque_requirement.png){:width="400px"} 

4. 요금제를 선택해준다. 블로그의 경우 많은 댓글이 달리지 않으므로 `basic`으로도 충분하다.

    ![](/assets/img/blog_comment/choose_fee.png){:width="300px"} 

5. 사이트 종류를 선택해준다. 깃헙 블로그의 경우는 대개 Jekyll 일 것이다.

    ![](/assets/img/blog_comment/choose_site.png){:width="300px"} 

6. Install instruction 페이지에서 2번에 `Universal Embed Code`링크로 들어가서 전체 코드를 복사한다.

    ![](/assets/img/blog_comment/install_instructions.png){:width="300px"}
    ![](/assets/img/blog_comment/Universal.png){:width="300px"} 

     

7. 블로그 디렉토리 내에 `_site` 폴더 내부에 `disqus.html`파일을 만들고 코드를 붙여넣는다.  

    > 주의 : 7번부터는 테마에 따라 조금씩 다른 부분들이 있다. 이 블로그는 The Cayman Blog theme으로 만들어졌다.

    ![](/assets/img/blog_comment/include_direc.png){:width="300px"} 

8. 블로그 디렉토리의 `_config.yml` 파일에서 `disqus_url`과 `disqus_id`를 추가해준다.  

    ![](/assets/img/blog_comment/config_edit.png){:width="300px"} 

9. 블로그 디렉토리의 `_layouts` > `post.html`의 마지막 부분에 {% raw %}`{% include disqus.html %}`{% endraw %}을 넣어준다.

10. 완성!
잘 됐다면..이 블로그에도 댓글기능이 있을 것이다.

#### 참고
- [어떤 외국인 블로그](http://abstraction.blog/2017/10/02/creating-your-github-blog-from-scratch) 
- [MinJun님의 블로그](https://devmjun.github.io/archive/addComments) 

[disque]: https://disqus.com/