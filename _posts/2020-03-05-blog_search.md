---
layout: post
title: "Github blog 구글에서 검색되도록 하기"
author: optboy
---

깃헙 블로그를 처음 만들고나서, 들뜬 마음으로 구글 검색창에 내 블로그를 검색해봤다. 하지만 내 블로그는 뜨지 않았고, 이런 저런 방법으로 검색을 해봤지만 끝까지 내 블로그를 볼 수 없었다.  
시간이 지나도 블로그를 찾을 수가 없어서 궁금한 마음에 왜 안뜨는지 검색을 해봤더니 Jekyll로 만든 블로그는 별도의 설정이 필요했다.  
그래서 이번에는 깃헙 블로그가 검색 포털에서 검색되도록 설정하는 법을 다뤄보겠다.

## Google Search Console에서 블로그 등록 & 인증하기
1. [Google Search Console][search_console_url]에 접속 한다.

2. 자신의 블로그 URL을 넣어 속성을 추가한다.

    ![](/assets/img/blog_search/google search.png){:width="350px"}  

3. 구글에서 제공하는 html 파일을 다운로드 한다.  

    ![](/assets/img/blog_search/html_download.png){:width="350px"}  

4. 다운받은 html 파일을 블로그 root폴더에 넣는다.  

    ![](/assets/img/blog_search/html_file_location.png){:width="250px"}  

5. git push 한 후, Google search console에서 확인 버튼을 눌려준다. 정상적으로 절차가 진행됐다면 다음 화면이 뜰 것이다.  

    ![](/assets/img/blog_search/success.png){:width="300px"}  

## sitemap.xml 파일 작성하기
1. 블로그의 root 폴더에 `sitemap.xml` 이라는 이름의 파일을 생성한다.  

2. `sitemap.xml`파일 안에 다음 [링크][my_site] 안의 코드를 넣는다.  

    - 첫번째, 두번째 줄의 `---`도 넣어줘야 한다.
    - 블로그의 _config.yml 파일의 url이 자신의 블로그 주소로 입력되어 있어야 한다.  
    
3. 

[search_console_url]: <https://search.google.com/search-console/>
[my_site]: <>