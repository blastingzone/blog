---
layout: post
title:  "로컬에서 멀쩡하던 Jekyll이 Travis CI에서 에러가 발생할 때"
date:   2016-11-18 20:35:00 +0900
categories: Jekyll
tags : jekyll
---
어제 포스트한 글이 뭐가 문제인지는 모르겠지만 Github에서는 Page Build Failed에러를 계속 뱉어내고 있는 중이다.

이 에러는 Github 설정이 잘못되었을 가능성도 있으므로 문제를 확실히 하기 위해서는 좀 더 조사가 필요한 상황이다.  

일단 문제 원인이 뭔지 알고 싶었으므로 테스트를 진행하였다.

## 내가 Jekyll을 잘못 사용하였나?

로컬에서 다음 명령어로 jekyll을 clean 빌드 하였다.

`bundle exec jekyll clean`

`bundle exec jekyll build`

그런데 문제가 없었다. 잘 빌드된다.

## 그럼 뭐가 문제일지 Travis CI에 물어보자

Jekyll 프로젝트 Root 폴더에 .travis.yml 파일을 추가하였다. 파일 내용은 다음과 같다.

~~~
language: ruby  
rvm:  
- 2.1  
script: "bundle exec jekyll build"  
branches:  
  only:  
    - gh-pages
~~~

자세한 travis-ci 설정 방법은 [이 Jekyll 공식 페이지][travis-jekyll-setting]를 보도록 하자. 에러 원인 파악이 우선이라 Github에 있는 대로 약식으로 설정하였지만 Jekyll 홈페이지에 설명하는 방법이 훨씬 자세하다.

그랬더니!

Github와 Travis 양쪽에서 빌드 에러가 나기 시작했다.

## 아니 그런데 Travis CI 빌드 에러는 좀 이상한데

있지도 않은 파일의 date format 형식이 잘못되었다는 에러를 내뱉는 게 아닌가.  

구글링을 해 보니 비슷한 이슈로 고통받는 사람들이 많았다.  

그리고 [여기][jekyll-invalid-issue]에 정답이 있었다.  

\_config.yml 파일에 **exclude: [vendor]** 문장을 하나 추가하면 끝난다.  

참고로 Gemfile 을 못 찾는다는 에러가 발생할 수 있는데 이때는 Jekyll 프로젝트의 Gemfile 파일이 대문자로 시작하고 있는지 확인해보자.


[travis-jekyll-setting]:https://jekyllrb.com/docs/continuous-integration/
[jekyll-invalid-issue]:https://github.com/jekyll/jekyll/issues/2938
