---
layout: post
title: "Jekyll 사이트 변동사항을 실시간으로 체크하기"
author: optboy
---

Jekyll 테마를 사용해서 깃헙 블로그를 만들었다면, 작업을 하면서 생기는 변동사항을 사이트에서 직접 보기 위해서 매번 푸쉬를 해주기는 너무나도 귀찮을 것이다.  
그래서 이번에는 jekyll bundler을 이용해서 실시간으로 변동사항을 체크할 수 있는 방법을 소개한다.

## 준비물
- Ruby (`ruby --version`을 통해 확인하자.)

## 방법
1. jekyll bundler 설치하기
```bash
gem install jekyll bundler
```

2. 로컬 서버 실행하기
```bash
cd [내 블로그 작업환경 경로]
bundle exec jekyll serve
```
다음 명령어를 실행했을 때 `Server running ...`이라는 문구가 뜬다면 성공적으로 돌아가고 있는 것이다.  

3. 웹페이지에서 접속하기
이제 웹페이지를 통해서 정상적으로 페이지가 뜨는 지 확인해준다. 브라우저의 url에 `localhost:4000`을 입력하면 블로그가 뜰 것이다.

여기까지 완성됐다면 앞으로 블로그를 편집하고 웹페이지를 새로고침해보면서 블로그의 모습을 확인할 수 있다.
물론, 실제로 페이지를 수정하기 위해서는 `git push`를 해줘야 한다.





