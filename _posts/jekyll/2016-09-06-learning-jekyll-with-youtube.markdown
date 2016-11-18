---
layout: post
title:  "Youtube로 Jekyll을 배워보자 - 5 -"
date:   2016-09-06 02:11:00 +09:00
categories: Jekyll
tags : jekyll
---
[이전 글 보기][post_4]

이번 화 관련 영상들

[Jekyll: many CSS files][lecture_30]  
[Jekyll: unique titles for every page][lecture_31]

markdown 문법은 css 파일에도 적용되기 때문에, 여러 개의 의미 있는 조각으로 나뉘어진 css 파일을 include 문법을 통해 하나의 css 파일로 통합할 수 있다.  
이 방법은 css 관리는 쉽게 해 주면서 css 파일은 하나로 합쳐주므로 웹 브라우저가 css 파일 여러개를 다운받느라 네트워크 자원을 낭비하는 것을 막아준다.  

31강은 좀 갸웃 할 수 있는데 진작에 나왔어도 무방할 page.title 변수를 이용하여 if 문으로 페이지 제목을 바꿔주고 있다.

이미 28~29강에 걸쳐서 더 응용에 가까운 커스텀 class 할당까지 보여줬으므로 거기서부터 한 번 쭉 보면 좋을 것이다.

이제 Youtube 강의가 슬슬 마무리 단계인데 여기까지만 봐도 포스팅 하는데는 별 무리가 없는 수준이다.


[post_4]:{{ site.baseurl }}{% post_url 2016-08-30-learning-jekyll-with-youtube %}
[lecture_30]:https://www.youtube.com/watch?v=H4Fc2xL79nU&list=PLWjCJDeWfDdfVEcLGAfdJn_HXyM4Y7_k-
[lecture_31]:https://www.youtube.com/watch?v=ra9Td0DpK0s&list=PLWjCJDeWfDdfVEcLGAfdJn_HXyM4Y7_k-
