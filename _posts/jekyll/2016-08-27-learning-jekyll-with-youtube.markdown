---
layout: post
title:  "Youtube로 Jekyll을 배워보자 - 3 -"
date:   2016-08-27 06:12:00 +0900
categories: jekyll
---
[이전 글 보기][post_2]  
[다음 글 보기][post_4]

이번 화 관련 영상들

[Jekyll: nested layouts][lecture_17]

[Jekyll: nested layouts for a specific content type][lecture_19]

nested layout은 1편에서 봤던 layout 안에 layout을 집어넣는 방법으로, 좀 더 자세히 설명하자면 문서 상단의 YAML 부분에서 layout을 지정하는데, 이때 문서 A가 layout:default, 문서 B가 layout:A를 지정하게 되면 문서 A에는 우선 문서 B의 내용이 문서 A의 {{ "{{ content" }} }} 영역을 채우고, 다시 문서 B와 합쳐진 문서 A가 default 문서와 합쳐지면서 최종적으로 2번의 layout이 적용된 정적 페이지가 완성되는 것이다.

Jekyll 기본 테마를 보면 \_layouts 디렉토리 밑에 page.html 파일과 post.html 파일이 각각 이런 원리로 구성되어 있음을 알 수 있다.

[post_2]:{{ site.baseurl }}{% post_url 2016-08-25-learning-jekyll-with-youtube %}
[post_4]:{{ site.baseurl }}{% post_url 2016-08-30-learning-jekyll-with-youtube %}
[lecture_17]:https://www.youtube.com/watch?v=A6x1mFRmVX0&list=PLWjCJDeWfDdfVEcLGAfdJn_HXyM4Y7_k-
[lecture_19]:https://www.youtube.com/watch?v=rcRiJSaPwbc&index=19&list=PLWjCJDeWfDdfVEcLGAfdJn_HXyM4Y7_k-
