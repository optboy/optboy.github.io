---
layout: post
title: "Github blog 개설하기"
author: optboy
---

구글링을 하다보면 정말 많은 사람들이 자신들의 깃헙 블로그에 정보를 공유해놓은 것을 볼 수 있다.  
그럴 때마다 나도 이때까지 공부해온 것들을 멋지게 정리해서 사람들에게 공유하고 싶다는 생각이 들었다.  
그러다 우여곡절 끝에 깃헙 블로그를 개설하게 되었고, 첫 포스팅으로 깃헙 블로그를 개설하는 방법을 소개하고자 한다.  

## Github blog의 장점

1. **마크다운**을 이용해서 자유롭게 블로그를 꾸밀 수 있다.
2. **무료**로 .github.io url을 사용할 수 있다.
3. 다양한 **테마**(jekyll등을 사용)를 무료로 사용할 수 있다.


## Github blog 개설 방법

1. **Github 계정 만들기**  

    - Github blog이기 때문에 기본적으로 Github 계정이 필요하다.  
    - 계정 생성은 [Github][github]에 접속해서 간단하게 할 수 있다.

2. **새로운 Repository 만들기**  

    - 다음으로 Github page를 위한 repository를 생성해준다.
    - 단, 이때 repository이름은 `[username].github.io`로 설정한다. repository이름은 나중에 블로그의 도메인으로 쓰이게 된다. repository가 만들어지면 url을 통해 페이지를 확인할 수 있다.  

        ![make_repository](/assets/img/make_github_blog/make_repository.png){:width="500px"}  

    - 이제 본격적으로 작업을 하기 위해 컴퓨터로 파일을 들고 온다. repository안에 `Clone or download`를 눌러 주소를 복사해준다.  

        ![clone_link](/assets/img/make_github_blog/clone link.png){:width="500px"}  

        ```bash
        $ cd [저장할 폴더]
        $ git clone [복사한 주소]
        ```
        
3. **테마 적용하기**  

    - 앞서 언급했듯, Github blog는 다양한 테마를 사용할 수 있다.  
    - [jekyll][jekyll]에 접속해서 마음에 드는 테마를 선택한다.  

        ![jekyll_home](/assets/img/make_github_blog/jekyll home.png){:width="500px"}  

    - 적당한 테마를 고르고 테마를 다운로드 해준다. 이 블로그는 cayman테마를 이용해 만들었다.  

        ![cayman](/assets/img/make_github_blog/cayman.png){:width="500px"}

    - 다운로드받은 파일의 압축을 풀고 모든 파일을 블로그 repository로 옮겨준다.  

        ![paste](/assets/img/make_github_blog/paste.gif){:width="500px"}

    - _config.yml 파일에서 url을 내 블로그 주소와 동일하게 설정해준다.  

        ![yml](/assets/img/make_github_blog/yml_file.png){:width="500px"}

4. **완성**  

    - 이제 기본적인 단계는 끝이 났다. 깃헙에 변경된 파일을 올리고 제대로 테마가 적용되었는지 확인해준다. 
    ```bash
    $ cd [블로그 repository]
    $ git add .
    $ git commit -m '[이번 커밋에 대한 메모]'
    $ git push
    ```
    - 성공적으로 push되었다면 url에 블로그 주소를 치고 정상적으로 바뀌었는 지 확인한다.

* 참고: [줌코딩님의 블로그][reference]

[github]: https://github.com
[jekyll]: http://jekyllthemes.org
[reference]: https://zoomkoding.github.io/gitblog/2019/08/15/git-blog-1.html